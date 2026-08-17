# CLAUDE.md — Guia para AI Assistants

Este repositório é a skill `/carrossel` para Claude Code. Ela cria carrosséis completos para Instagram e TikTok: gera texto editorial, HTMLs estilizados e renderiza em PNG via Playwright.

---

## Estrutura do repositório

```
carrossel-ratos/
├── SKILL.md                        ← fluxo principal da skill (leia isto primeiro)
├── CLAUDE.md                       ← este arquivo
├── README.md                       ← documentação pública de instalação
└── references/
    ├── design-carrossel.md         ← estilo ativo (substituído no setup do usuário)
    ├── design-minimalista.md       ← template estilo minimalista
    ├── design-elaborado.md         ← template estilo elaborado (texturas, noise, split)
    ├── design-tweet.md             ← template estilo tweet (simula post do Twitter/X)
    └── badge-verificado.svg        ← badge azul de verificado pro estilo tweet
```

### Onde vive o conteúdo do usuário (fora deste repo)

Quando instalada, a skill espera encontrar estes arquivos no projeto do usuário:

```
[projeto do usuário]/
├── marca/
│   ├── design-guide.md             ← cores, fontes, logo, perfil do autor
│   └── foto-perfil.jpg             ← foto de perfil (opcional, estilo tweet)
├── _contexto/
│   ├── empresa.md                  ← contexto do negócio e público-alvo
│   └── preferencias.md             ← tom de voz e preferências de escrita
└── conteudo/
    └── carrosseis/
        └── [tema]/
            ├── carousel-text.md    ← texto aprovado + legenda
            ├── imagens/            ← fotos do usuário ou geradas por IA
            ├── instagram/          ← HTMLs + PNGs 1080x1350
            └── tiktok/             ← HTMLs + PNGs 1080x1920 (opcional)
```

---

## Como a skill funciona

### Instalação pelo usuário

```bash
git clone https://github.com/roselmavilanova-hash/carrossel-ratos ~/.claude/skills/carrossel
```

Depois de instalada, o usuário ativa a skill com qualquer variação de:
- `faz um carrossel sobre [tema]`
- `carrossel`, `carousel`, `slides instagram`, `slides tiktok`

### Setup guiado (primeira vez)

Antes de criar qualquer carrossel, a skill checa 5 condições:

1. **Design guide** (`marca/design-guide.md`) — cores, fontes, estilo geral, logo
2. **Estilo de design dos slides** (`references/design-carrossel.md`) — minimalista, elaborado ou tweet
3. **Tom de voz** (`_contexto/preferencias.md`) — informal, profissional, técnico; o que evitar
4. **Contexto do negócio** (`_contexto/empresa.md`) — o que o usuário faz e pra quem
5. **Playwright** — verifica se está instalado; instala `chromium` se necessário

Se tudo já estiver configurado, vai direto para o workflow. Não repetir perguntas já respondidas.

### Workflow em 3 fases

#### Fase 1 — Texto
1. Ler contexto e preferências do usuário
2. Se input for link: WebFetch normal, Jina Reader como fallback (`https://r.jina.ai/[url]`), `api.fxtwitter.com` para links do X/Twitter
3. Pesquisar termos desconhecidos antes de escrever — nunca chutar
4. Briefing rápido: número de slides, imagens, CTA, tipo de conteúdo
5. **CHECKPOINT 1:** Mostrar espinha dorsal + 5 opções de capa → aguardar aprovação
6. Escrever slides seguindo o arco narrativo (capa → hook → mecanismo → provas → virada → CTA)
7. Gerar legenda do Instagram
8. **CHECKPOINT 2:** Mostrar texto completo + legenda → aguardar aprovação

#### Fase 2 — Visual (HTMLs + PNGs)
1. Ler `marca/design-guide.md` e `references/design-carrossel.md`
2. Criar HTMLs 1080x1350px com inline CSS + Google Fonts
3. Renderizar slide 1 via Playwright CLI
4. **CHECKPOINT:** Mostrar slide 1 → se aprovado, renderizar os demais
5. Salvar em `conteudo/carrosseis/[tema]/instagram/`

```bash
# Comando de renderização
npx playwright screenshot --viewport-size=1080,1350 --full-page \
  "file:///caminho/absoluto/slide-01.html" "slide-01.png"
```

#### Fase 3 — Versão TikTok (opcional)
- Mesmos HTMLs adaptados para 1080x1920px
- Safe zone inferior de 230px (UI do TikTok sobrepõe)
- Salvar em `conteudo/carrosseis/[tema]/tiktok/`

---

## Estilos de design disponíveis

| Estilo | Arquivo de origem | Características |
|--------|-------------------|-----------------|
| **Minimalista** | `references/design-minimalista.md` | Clean, espaço em branco, layouts simples |
| **Elaborado** | `references/design-elaborado.md` | Texturas, noise SVG, split layouts, composições ousadas |
| **Tweet** | `references/design-tweet.md` | Simula tweet do Twitter, fundo branco, avatar + @handle |

Quando o usuário escolhe um estilo, o conteúdo do arquivo de origem é copiado integralmente para `references/design-carrossel.md`. Para trocar: `"muda o estilo do carrossel pra tweet"`.

---

## Convenções de código

### HTML dos slides
- Arquivo por slide: `slide-01.html`, `slide-02.html`, etc.
- Inline CSS only — sem folhas de estilo externas (exceto Google Fonts via `<link>`)
- Dimensões fixas no elemento raiz: `width: 1080px; height: 1350px` (Instagram)
- Safe area: 56px laterais, 80px embaixo
- Noise/grain com SVG filter inline (ver `design-elaborado.md` para o snippet)
- Referências a imagens: caminhos relativos a partir do HTML

### Regras de texto (anti-AI slop)

**Proibido:**
- Estruturas binárias: "não é X, é Y"
- Cacoetes: "e isso muda tudo", "no fim das contas", "simplesmente", "basicamente"
- Jargão corporativo: "ecossistema", "mindset", "sinergia", "disruptivo"
- Aberturas genéricas: "hoje vamos falar sobre", "neste carrossel tu vai"
- Travessões (—) — a menos que `preferencias.md` diga o contrário
- Dados inventados — se não tiver dado verificável, usar opinião forte e honesta

**Obrigatório:**
- Artigos sempre presentes: "um mercado", "a marca" (nunca cortar)
- Especificidade: dado + fonte + ano ("cresceu 34% em 2024, Statista")
- Cada slide é um parágrafo fluido com conectivos naturais, não lista disfarçada
- Curiosity gap entre slides — a passagem deve ser inevitável pela narrativa

### Checkpoints obrigatórios

Há 3 checkpoints onde a skill **deve pausar e aguardar aprovação**:
1. Espinha dorsal + escolha de capa (Fase 1)
2. Texto completo + legenda (Fase 1)
3. Slide 1 renderizado (Fase 2)

Nunca pular checkpoints. Não renderizar todos os slides antes de mostrar o slide 1.

---

## Geração de imagens por IA

Se o usuário quiser imagens mas não tiver nenhuma:

1. Verificar se `~/.claude/skills/nanobanana-ratos/` existe e tem `.env`
2. Se sim: usar a skill `nanobanana-ratos` para gerar
3. Se não: sugerir instalação ou orientar a usar Canva/ChatGPT/Midjourney

---

## Como editar a skill

### Alterar regras de design
Editar `references/design-minimalista.md`, `design-elaborado.md` ou `design-tweet.md`.
O arquivo `references/design-carrossel.md` neste repo contém apenas um placeholder — o conteúdo real é copiado para o projeto do usuário no setup.

### Alterar o fluxo de criação
Editar `SKILL.md`. É o arquivo central que controla todo o comportamento da skill.

### Adicionar novo estilo de design
1. Criar `references/design-[nome].md` seguindo a estrutura dos arquivos existentes
2. Adicionar a opção na seção "Estilo de design dos slides" do `SKILL.md`

---

## Dependências

- **Playwright** (`npx playwright screenshot`) — renderização de HTMLs em PNG
- **Google Fonts** — carregadas via `<link>` no HTML (Playwright precisa de internet)
- **WebFetch / Jina Reader** — para buscar conteúdo de links fornecidos pelo usuário
- **Skill `nanobanana-ratos`** (opcional) — geração de imagens por IA

---

## Licença

CC BY 4.0
