# Regras de Design — Carrossel (Estilo Conto)

> Cada slide parece uma página de um conto literário ou revista cultural.
> Tipografia séria, espaço respeitoso, texto que convida à leitura lenta.

---

## Conceito

O carrossel no estilo conto rejeita a urgência do feed. Em vez de chamar atenção com volume, chama com qualidade. Cada slide parece que pertence a uma publicação impressa — livro, revista literária, ensaio. A pessoa para porque sente que vai ler algo que vale a pena, não porque foi agredida visualmente.

**A regra central:** o texto é a peça de design. Tudo o que existe no slide existe pra servir a leitura.

---

## Dimensões

- **Instagram:** 1080x1350px (proporção 4:5)
- **TikTok:** 1080x1920px (proporção 9:16)
- **Safe area:** 72px nas laterais, 96px embaixo

---

## Paleta

Fundos sempre neutros. Nunca cores saturadas como fundo.

- **Fundo principal:** #F5F0E8 (creme, papel envelhecido) ou #FAFAF8 (branco levemente quente)
- **Fundo escuro (alternativa):** #1C1A17 (preto sépia) ou #0F0F0D (preto editorial)
- **Texto principal:** #1A1814 (quase preto, não preto puro)
- **Texto secundário:** #6B6560 (cinza sépia)
- **Destaque/acento:** usar a cor de destaque do design guide com moderação — só pra números de slide, ornamentos ou drop cap. Nunca como fundo de texto corrido

---

## Tipografia

A escolha da fonte define tudo nesse estilo.

### Fonte de corpo (obrigatório: serifada)
Usar uma das opções abaixo (em ordem de preferência), ou a fonte do design guide se for serifada:
- **Lora** (Google Fonts) — o padrão recomendado. Literária, legível, contemporânea
- **Playfair Display** — mais dramática. Para conteúdo com personalidade forte
- **Libre Baskerville** — clássica e confiável
- **DM Serif Display** — moderna com alma editorial

Se o design guide definir uma fonte serifada, usar ela. Se for sans-serif, usar Lora como override neste estilo.

### Fonte de suporte (opcional: sans-serif limpa)
Para número de slide, label de capítulo, byline. Usar a sans-serif do design guide ou Inter/DM Sans.

### Hierarquia
- **Título/headline:** 68-88px, peso 700 (bold) ou 400 (regular com itálico). Nunca condensado
- **Subtítulo/epígrafe:** 28-34px, itálico, peso 400
- **Corpo do texto:** 34-40px, peso 400, line-height 1.7-1.8
- **Número de slide/capítulo:** 18-22px, sans-serif, letter-spacing 4-6px, uppercase

---

## Estrutura de cada slide

### Elementos fixos (presentes em todos os slides)

**Número de slide:** canto superior direito ou inferior direito. Nunca intrusivo.
- Formato: `01`, `02`, `03` ou `I`, `II`, `III`
- Font-size: 18-20px, sans-serif, cor secundária (#6B6560 ou similar)
- Com ou sem total: `01` ou `01 / 08`

**Margem generosa:** padding horizontal de 80-96px. Texto nunca cola nas bordas.

**Linha decorativa (opcional):** linha fina horizontal (1px, cor sépia 20%) separando número do conteúdo. Mais fina que borda, mais leve que separador.

### Slide 1 — Capa

A capa do estilo conto não grita. Seduz.

- **Título:** centralizado ou alinhado à esquerda, 72-88px. Pode ser itálico
- **Subtítulo/gancho:** abaixo do título, 28-34px, itálico. Uma frase que cria desejo de ler
- **Autoria (opcional):** nome do perfil em pequeno abaixo do subtítulo, sans-serif, letter-spacing
- **Ornamento (opcional):** um símbolo tipográfico simples (❧ ✦ · — ) entre título e subtítulo, na cor de destaque. Só um, nunca amontoado
- **Fundo:** creme (#F5F0E8) ou escuro, sem textura agressiva

### Slides de conteúdo

Cada slide é uma "página" do conto. Layout limpo, mas não estéril.

**Opção A — Drop cap + parágrafo**
A primeira letra do slide é um drop cap: 3-4 linhas de altura, na cor de destaque ou no peso bold da fonte serifada. O resto do texto flui normalmente ao lado. Usar no segundo slide e quando começar um novo "capítulo".

```css
.drop-cap::first-letter {
  font-size: 5.5em;
  font-weight: 700;
  float: left;
  line-height: 0.85;
  margin: 0.05em 0.12em 0 0;
  color: var(--destaque);
}
```

**Opção B — Epígrafe**
Slide com aspas literárias grandes e uma frase de impacto. Para insights ou viradas.
- Aspas tipográficas (`"`) em 200-280px, weight 700, opacity 0.06, cor do texto. Posicionadas como elemento decorativo de fundo
- Texto em itálico, 36-42px, centralizado ou alinhado à esquerda
- Atribuição (opcional) embaixo: "— nome" em sans-serif pequena

**Opção C — Texto corrido**
Parágrafo limpo. Sem drop cap, sem aspas. Só o texto e o espaço.
- Alinhamento: **justificado** com `text-align: justify; hyphens: auto; -webkit-hyphens: auto` (dá o look de livro). Alternativa: alinhado à esquerda se o texto for muito curto e justificado ficar feio
- Line-height 1.75-1.85
- No máximo 3-4 frases por slide (densidade de livro, não de post)

**Opção D — Título de capítulo**
Slide de transição entre seções. Só um número romano ou título de seção, centralizado, tamanho grande. Respiro puro antes de uma virada.

### Slide final — CTA

Diferente da maioria dos carrosséis, o CTA do estilo conto não é comercial. É uma continuação da voz.

- Texto em 2-3 frases que fecham o arco, como o parágrafo final de um conto
- A chamada pra ação está embutida no texto, não separada como botão
- Sem "segue pra mais", sem emoji, sem urgência artificial
- Pode ter o nome ou @ do perfil discreto no rodapé, em sans-serif pequena

---

## Ritmo visual

O carrossel conto alterna entre densidade e respiro.

- **Slides densos** (texto corrido): 2-3 parágrafos curtos, ocupam 60-70% do slide
- **Slides leves** (epígrafe ou capítulo): uma frase ou número, muito respiro
- **Nunca** 3 slides densos seguidos sem um respiro
- A variação de peso visual (denso → leve → denso) cria ritmo de leitura, como capítulos curtos

---

## Imagens

No estilo conto, imagens são raras e intencionais.

**Capa com imagem:** se o usuário tiver uma foto/ilustração, usar como fundo com overlay forte:
```css
.capa-bg { position: absolute; inset: 0; width: 100%; height: 100%; object-fit: cover; object-position: center; }
.capa-overlay { position: absolute; inset: 0; background: linear-gradient(180deg, rgba(28,26,23,0.3) 0%, rgba(28,26,23,0.75) 100%); }
```
Texto em branco sobre o overlay. Imagem serve de atmosfera, não de informação.

**Slides internos com imagem:** colocar a imagem em um bloco contido, como gravura de livro:
```css
.gravura {
  width: 100%;
  max-height: 480px;
  object-fit: contain;
  border-radius: 4px;
  margin: 32px 0;
  filter: sepia(15%) contrast(95%); /* toque editorial sutil */
}
```

**Sem imagem:** o design funciona completamente sem foto. Não inventar elemento visual pra preencher espaço. O respiro É o design.

---

## Elementos decorativos (com parcimônia)

- **Ornamento tipográfico:** ❧ ✦ ◆ · — um por slide, máximo. Na cor de destaque ou sépia
- **Linha fina horizontal:** 1px, largura parcial (30-50% do slide), centralizada. Separa seções sem brutalidade
- **Aspas decorativas de fundo:** opacity 0.04-0.07. Deve ser quase invisível, só sentido
- **Número de página:** sempre. É o único elemento fixo obrigatório

**NUNCA usar:**
- Gradientes coloridos
- Noise/grain (não combina com o look literário)
- Blocos de cor parciais como decoração
- Stripes, glow, neon
- Emojis no corpo do texto (o CTA pode ter no máximo um, se o tom pedir)

---

## HTML técnico

- 1080x1350px, inline CSS, Google Fonts via `<link>`
- `hyphens: auto` no container de texto (essencial pro justificado funcionar)
- `font-feature-settings: "liga" 1, "kern" 1` pra ligaturas tipográficas
- Drop cap via `::first-letter` no CSS
- Aspas tipográficas reais (`"` e `"`) em vez de aspas retas (`"`)
- Fundo creme é `#F5F0E8` — nunca branco puro neste estilo

---

## O que ajustar

- **Quer fundo escuro:** trocar pra #1C1A17 e texto pra #EDE9E0. Todo o resto permanece
- **Sem justificado:** mudar pra `text-align: left` em todo o corpo
- **Fonte diferente:** trocar na seção Tipografia. Deve ser serifada
- **Mais solto (menos livro, mais ensaio):** aumentar line-height pra 2.0, diminuir font-size pra 30px, adicionar mais respiro entre parágrafos
- **Com foto em todos os slides:** adicionar imagem como gravura nos slides internos

Pede pro Claude: "muda a regra X no design do carrossel" e ele edita este arquivo.
