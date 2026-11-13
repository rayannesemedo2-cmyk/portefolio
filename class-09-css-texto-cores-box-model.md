# Guia Prático - UF 1.1 (Aula 9)

## Estilo com CSS II: Texto, Fontes, Cores e o Box Model

- **Objetivo:** Escolher e escrever cores de quatro formas diferentes (nome, hexadecimal, `rgb()` e `hsl()`) e montar uma paleta legível; usar listas de fontes e uma fonte do Google Fonts; formatar texto com tamanhos em `rem` e `em`, peso, altura de linha, alinhamento e espaçamento; perceber o **box model** (conteúdo, `padding`, `border` e `margin`), vê-lo nas DevTools e controlar a largura das caixas com `box-sizing` e `max-width`. No fim da aula, o portefólio ganha uma identidade visual própria: uma paleta de cores, uma fonte para os títulos, conteúdo centrado e cartões, notas, botões e formulário desenhados com o box model.

> **Como estudar com este guia:** este guia tem os mesmos passos que fizemos na aula, pela mesma ordem. Sigam as Partes e os Passos **por ordem**, no vosso computador, e escrevam o código **à mão** (não copiem e colem). No fim de cada etapa há uma caixa **Confirmem antes de avançar:** só passem à frente quando o vosso resultado for igual ao que lá está. Se algo não funcionar, vejam a secção **Se Algo Correr Mal**, no fim do guia.

> **Mac:** sempre que aparecer a tecla **Ctrl**, usem a tecla **Cmd**.

> **Ponto de partida:** a pasta `portefolio` como ficou na aula 8: as três páginas (`index.html`, `projetos.html`, `contactos.html`) ligadas ao ficheiro `css/style.css`, que já tem as primeiras regras que escrevemos. Se faltaram, copiem a pasta [`projeto/sessao-08/`](../../projeto/sessao-08/). O projeto já deve estar no vosso repositório no GitHub.

---

### Parte 1: Ponto de Partida (Olhar com Atenção para o que Já Temos)

Na aula 8 ligámos o ficheiro `css/style.css` às três páginas e escrevemos as primeiras regras. Hoje vamos transformar esse primeiro rascunho numa folha de estilos a sério, com cores escolhidas, boas fontes e caixas bem desenhadas. Antes de escrever código novo, vamos olhar para o que já existe.

#### Passo 1: Ler as Regras da Aula 8

Abram a pasta `portefolio` no VS Code e abram o ficheiro `css/style.css`. Na aula 8 ficou mais ou menos assim (o vosso pode ter outros valores ou mais regras):

```css
body {
  font-family: sans-serif;
  background-color: rgb(209, 205, 205);
}
nav {
  color: blue;
}
h2 {
  color: red;
  font-size: 12pt;
  font-weight: bold;
}

h1 {
  color: black;
  font-family: "Franklin Gothic Medium";
}
```

Abram o `index.html` com o **Live Server** e deixem o browser aberto ao lado do VS Code durante toda a aula.

#### Passo 2: O Que Ainda Não Está Bem

Estas regras funcionam, mas têm quatro problemas que vamos resolver hoje:

1. **`font-family: "Franklin Gothic Medium"`** só tem uma fonte. Essa fonte existe no Windows, mas não existe no Mac nem no telemóvel. Quando a fonte não existe, o browser usa a fonte que lhe apetece (normalmente uma fonte com serifas, como a Times). Vamos aprender a escrever **listas de fontes** (Parte 3).
2. **`nav { color: blue; }`** não muda a cor dos links do menu. Os links (`<a>`) têm uma cor própria, dada pelo browser, e essa cor ganha à cor herdada do `nav`. Para mudar os links temos de escrever uma regra para os próprios links (Parte 4).
3. **`font-size: 12pt`** deixa o `h2` com o mesmo tamanho do texto normal, por isso deixa de parecer um título. Além disso, `pt` (pontos) é uma unidade das impressoras, não dos ecrãs. Vamos usar `rem` (Parte 4).
4. **As cores** (cinzento médio no fundo, vermelho puro, preto puro, azul puro) foram escolhidas ao acaso e cansam a vista. Vamos escolher uma **paleta** (Parte 2).

#### Passo 3: Arrumar o Ficheiro em Secções

Uma folha de estilos cresce depressa. Para encontrarmos as regras mais tarde, vamos dividi-la em secções com comentários.

Cada uma das regras da aula 8 vai voltar hoje, melhorada. Por isso, selecionem tudo no ficheiro `css/style.css` (**Ctrl + A**), apaguem e escrevam este esqueleto:

```css
/* ==========================================================================
   Portefólio Pessoal — Ana Martins
   Folha de Estilos Principal
   ========================================================================== */

/* --------------------------------------------------------------------------
   1. Base: caixas, corpo da página e largura do conteúdo
   -------------------------------------------------------------------------- */

/* --------------------------------------------------------------------------
   2. Texto e fontes
   -------------------------------------------------------------------------- */

/* --------------------------------------------------------------------------
   3. Cabeçalho, menu e rodapé
   -------------------------------------------------------------------------- */

/* --------------------------------------------------------------------------
   4. Tabelas e formulários
   -------------------------------------------------------------------------- */

/* --------------------------------------------------------------------------
   5. Componentes reutilizáveis (classes)
   -------------------------------------------------------------------------- */

/* --------------------------------------------------------------------------
   6. Elementos únicos (id)
   -------------------------------------------------------------------------- */
```

Escrevam o vosso nome no lugar de "Ana Martins". A partir de agora, cada regra nova vai para a secção certa: o guia diz sempre qual é.

**Resultado esperado:** ao guardarem, a página volta ao aspeto "sem estilo" (fundo branco, letra com serifas). É normal: o ficheiro só tem comentários, e o browser ignora os comentários.

> **Confirmem antes de avançar:**
>
> - Sabem explicar porque é que `nav { color: blue; }` não pintou os links do menu.
> - O ficheiro `css/style.css` tem o cabeçalho e as seis secções comentadas, e mais nada.
> - O `index.html` está aberto com o Live Server ao lado do VS Code.

---

### Parte 2: Cores (A Paleta do Portefólio)

Um pintor não usa todas as tintas da loja: escolhe meia dúzia de cores que combinam e usa sempre essas. Num site é igual. A esse conjunto de cores chamamos **paleta**.

#### Passo 1: Quatro Formas de Escrever uma Cor

Em CSS, a mesma cor pode ser escrita de várias formas. Estas quatro linhas dão todas o mesmo verde-azulado... exceto a primeira, que só se aproxima:

```css
color: teal; /* 1. pelo nome (só há cerca de 140 nomes) */
color: #0f766e; /* 2. hexadecimal */
color: rgb(15, 118, 110); /* 3. vermelho, verde e azul */
color: hsl(175, 77%, 26%); /* 4. tom, saturação e luminosidade */
```

1. **Nome:** `red`, `white`, `teal`, `orange`... É fácil, mas só há cerca de 140 nomes, e o `red` é um vermelho muito forte.
2. **Hexadecimal (`#0f766e`):** a forma mais usada. Depois do `#` vêm três pares de algarismos: vermelho (`0f`), verde (`76`) e azul (`6e`). Cada par vai de `00` (nada) a `ff` (o máximo). Usa os algarismos de 0 a 9 e as letras de `a` a `f`. Por isso `#000000` é preto e `#ffffff` é branco.
3. **`rgb(15, 118, 110)`:** a mesma ideia, com números normais de 0 a 255 para o vermelho (*red*), o verde (*green*) e o azul (*blue*). Foi a forma que usámos na aula 8: `rgb(209, 205, 205)`.
4. **`hsl(175, 77%, 26%)`:** a forma mais "humana":
   - **Tom** (*hue*): um ângulo no círculo das cores, de 0 a 360 (0 é vermelho, 120 é verde, 240 é azul).
   - **Saturação:** de `0%` (cinzento) a `100%` (cor viva).
   - **Luminosidade:** de `0%` (preto) a `100%` (branco). Para fazer a mesma cor mais clara, basta subir este último número.

**Transparência:** se acrescentarmos um quarto valor ao `rgb()`, de `0` (invisível) a `1` (opaco), a cor fica transparente. Vamos usar isto para as sombras na Parte 5:

```css
color: rgba(15, 23, 42, 0.08); /* azul quase preto, com 8% de opacidade */
```

> **Dica:** não precisam de decorar códigos de cores. No VS Code, passem o rato por cima de uma cor no CSS: aparece um quadrado com a cor e um seletor de cores (*color picker*). Cliquem no topo desse seletor para trocar entre hexadecimal, `rgb()` e `hsl()`.

#### Passo 2: Escolher a Paleta e Guardá-la num Comentário

A paleta da Ana tem uma cor principal (verde-azulado), uma cor de realce (laranja) e os tons neutros para o texto, as bordas e os fundos. Escrevam-na num comentário, **logo a seguir ao cabeçalho do ficheiro**, antes da secção 1:

```css
/* Paleta de cores
   - Principal (verde-azulado): #0f766e
   - Títulos:                   #134e4a
   - Texto:                     #1f2937
   - Texto secundário:          #6b7280
   - Linhas e bordas:           #e5e7eb
   - Fundo da página:           #f8fafc
   - Fundo dos cartões:         #ffffff
   - Realce (laranja):          #ea580c
*/
```

Este comentário não faz nada no ecrã: serve para nós. Sempre que precisarmos de uma cor, vamos buscá-la aqui, e o site fica coerente.

> **Os vossos dados:** escolham a **vossa** cor principal e a vossa cor de realce. Mantenham os tons neutros (texto escuro, fundos claros) se não tiverem a certeza. Sites com paletas prontas a usar: [coolors.co](https://coolors.co) e [tailwindcss.com/docs/colors](https://tailwindcss.com/docs/colors) (em inglês).

#### Passo 3: Contraste (o Texto Tem de Se Ler)

Uma cor bonita não serve de nada se o texto não se ler. O que conta é o **contraste**: a diferença de luz entre a cor do texto e a cor do fundo.

- Texto escuro em fundo claro (ou o contrário) lê-se bem.
- Cinzento claro em branco, ou amarelo em branco, lê-se mal, sobretudo ao sol ou para quem vê mal.
- A regra internacional de acessibilidade (WCAG) pede um contraste de pelo menos **4.5 para 1** no texto normal.

Também por isso não usamos preto puro (`#000000`) sobre branco puro: o contraste é tão forte que cansa. Um cinzento muito escuro, como `#1f2937`, lê-se melhor.

> **Dica:** nas DevTools (Parte 5) há um medidor de contraste. Cliquem no quadrado de uma cor de texto no separador **Styles**: o seletor de cores mostra "Contrast ratio" e um visto verde quando o contraste é suficiente.

#### Passo 4: As Primeiras Cores no Site

Agora sim, as primeiras regras. Na **secção 1**, escrevam a regra do `body`:

```css
body {
  color: #1f2937;
  background-color: #f8fafc;
}
```

Na **secção 2**, escrevam a cor dos títulos e dos links:

```css
h1,
h2,
h3 {
  color: #134e4a;
}

a {
  color: #0f766e;
}
```

- **`color`** muda a cor do **texto**.
- **`background-color`** muda a cor do **fundo** da caixa.
- **`h1, h2, h3`** com vírgulas aplica a mesma regra aos três títulos (agrupamento, aula 8).
- **`a`** escolhe os links diretamente, por isso agora os links do menu mudam de cor (era o problema 2 da Parte 1).

**Resultado esperado:** o fundo fica cinzento muito claro, o texto cinzento-escuro, os títulos verde-escuro e todos os links (os do menu também) verde-azulado.

> **Desafio rápido:** no `body`, troquem `#f8fafc` por `hsl(210, 40%, 98%)`. A página fica igual? Agora mudem o último número para `90%` e depois para `20%`. Voltem a pôr `#f8fafc` no fim.

> **Confirmem antes de avançar:**
>
> - Sabem ler um código hexadecimal: `#ffffff` é branco, `#000000` é preto.
> - O comentário com a vossa paleta está no topo do `style.css`.
> - Os links do menu estão com a vossa cor principal.

---

### Parte 3: Fontes (A Letra do Site)

A letra é a "voz" do site: a mesma frase escrita numa letra redonda ou numa letra antiga de jornal transmite uma ideia diferente.

#### Passo 1: Listas de Fontes (*Font Stack*)

O browser só consegue mostrar fontes que **existem no computador de quem visita o site**. Como não sabemos que computador é, damos uma **lista de fontes**, separadas por vírgulas. O browser tenta a primeira; se não existir, tenta a segunda; e assim por diante.

Na **secção 1**, acrescentem duas linhas à regra do `body`:

```css
body {
  font-family:
    system-ui,
    -apple-system,
    "Segoe UI",
    Roboto,
    sans-serif;
  line-height: 1.6;
  color: #1f2937;
  background-color: #f8fafc;
}
```

Ao guardarem, o Prettier parte a lista em várias linhas, uma fonte por linha. Para o browser é igual a escrevê-la numa linha só.

Vamos ler a lista de cima para baixo:

1. **`system-ui`:** a fonte do sistema operativo (a mesma dos menus do Windows, do Mac ou do Android).
2. **`-apple-system`:** o mesmo, para versões antigas do Safari.
3. **`"Segoe UI"`:** a fonte do Windows. Leva aspas porque o nome tem um espaço.
4. **`Roboto`:** a fonte do Android.
5. **`sans-serif`:** a última hipótese, que existe sempre. É uma **família genérica**: o browser escolhe uma fonte qualquer **sem serifas**.

As famílias genéricas mais usadas são:

- **`serif`:** letras com serifas (os pequenos "pés" nas pontas), como a Times ou a Georgia. Lembram livros e jornais.
- **`sans-serif`:** letras sem serifas, como a Arial ou a Helvetica. Mais limpas no ecrã.
- **`monospace`:** todas as letras com a mesma largura, como no editor de código.

A linha **`line-height: 1.6`** (altura de linha) afasta as linhas umas das outras: cada linha passa a ter 1,6 vezes a altura da letra. O valor do browser (cerca de 1.2) é apertado demais para ler parágrafos longos. Escrevemos o número **sem unidade**, para que cada elemento faça a conta com o seu próprio tamanho de letra.

**Resultado esperado:** todo o texto passa a ter uma letra moderna, sem serifas, e os parágrafos ficam mais arejados. Ninguém escreveu regras para os parágrafos nem para as listas: eles **herdam** a fonte e a cor do `body`.

> **Atenção:** a última fonte da lista é sempre uma família genérica (`sans-serif`, `serif` ou `monospace`), **sem aspas**. Era isto que faltava no `"Franklin Gothic Medium"` da aula 8.

#### Passo 2: Uma Fonte da Web com o Google Fonts

E se quisermos uma fonte que não está no computador de ninguém? Podemos pedir ao browser que a **descarregue** da internet, tal como descarrega as imagens. O serviço gratuito mais usado é o **Google Fonts**.

Para os títulos da Ana escolhemos a fonte **Poppins**:

1. Abram [fonts.google.com](https://fonts.google.com) e pesquisem "Poppins".
2. Cliquem na fonte e depois em **Get font** e em **Get embed code**.
3. Do lado esquerdo, escolham só os pesos de que precisamos: **SemiBold 600** e **Bold 700**. Cada peso é um ficheiro a descarregar, por isso não escolham pesos que não vão usar.
4. Do lado direito, no separador **Web** e com a opção `<link>` escolhida, aparece o código a copiar.

No `<head>` do `index.html`, colem esse código **antes** da linha do `style.css` (a ordem conta: primeiro a fonte, depois as regras que a usam):

```html
<link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;700&display=swap"
  rel="stylesheet"
/>
<link rel="stylesheet" href="css/style.css" />
```

- **`rel="preconnect"`:** as duas primeiras linhas pedem ao browser que comece já a ligar-se aos servidores do Google. A fonte chega uns milissegundos mais cedo. Não são obrigatórias, mas o Google recomenda-as.
- **`<link href="...css2?family=Poppins..." rel="stylesheet" />`:** é uma folha de estilos, como a nossa, mas escrita pelo Google. Lá dentro está a "morada" dos ficheiros da fonte.
- **`wght@600;700`:** os pesos que escolhemos.
- **`display=swap`:** enquanto a fonte não chega, o browser mostra o texto com a fonte seguinte da lista, em vez de o esconder.

Repitam exatamente o mesmo no `<head>` de `projetos.html` e de `contactos.html`.

Agora, na **secção 2**, digam aos títulos para usarem a Poppins:

```css
h1,
h2,
h3 {
  font-family: "Poppins", system-ui, sans-serif;
  color: #134e4a;
  line-height: 1.25;
}
```

Os títulos são curtos e a letra é grande, por isso usamos uma altura de linha mais pequena (`1.25`) do que nos parágrafos.

**Resultado esperado:** o nome no topo e os títulos das secções mudam para uma letra redonda e geométrica (a Poppins), diferente da letra dos parágrafos.

> **Atenção:** o Google Fonts precisa de internet. Sem internet, os títulos aparecem com `system-ui` (a fonte seguinte da lista) e o site continua legível. É para isto que serve a lista de fontes.

> **Os vossos dados:** podem escolher outra fonte para os vossos títulos. Boas opções para começar: Poppins, Montserrat, Nunito, Merriweather (com serifas) ou Playfair Display (com serifas, mais elegante). Usem no máximo **duas** fontes no site: uma para os títulos e outra para o texto.

> **Confirmem antes de avançar:**
>
> - Os parágrafos estão numa letra sem serifas e mais arejados.
> - As três páginas têm as três linhas do Google Fonts no `<head>`, antes do `style.css`.
> - Os títulos das três páginas aparecem com a fonte que escolheram.

---

### Parte 4: Texto (Tamanhos, Pesos e Espaçamento)

#### Passo 1: As Unidades de Medida

Para dizer "quão grande", o CSS precisa de um número **e** de uma unidade, escritos juntos, sem espaço (`16px`, e não `16 px`). Estas são as unidades que vamos usar:

1. **`px` (píxeis):** uma medida fixa. Boa para coisas que não devem crescer, como bordas (`1px`) e espaços pequenos.
2. **`rem`:** relativa ao tamanho de letra da página, que por omissão é 16px. Então `1rem` = 16px, `2rem` = 32px e `0.875rem` = 14px. Se a pessoa aumentar o tamanho de letra nas definições do browser (por ver mal, por exemplo), tudo o que está em `rem` cresce com ela. **Usamos `rem` para tamanhos de letra.**
3. **`em`:** relativa ao tamanho de letra **do próprio elemento**. Num botão com letra de 20px, `1em` = 20px. Útil para espaços que devem crescer com a letra, como o interior de um botão (Parte 7).
4. **`%`:** relativa ao elemento que está à volta (o pai). `width: 100%` ocupa a largura toda do pai.

E a unidade `pt` da aula 8? Os pontos vêm da tipografia em papel. Funcionam, mas no ecrã não há razão para os usar.

#### Passo 2: Tamanho e Peso dos Títulos

Na **secção 2**, por baixo da regra agrupada dos títulos, escrevam uma regra para cada título:

```css
h1 {
  font-size: 2.5rem;
  font-weight: 700;
}

h2 {
  font-size: 1.6rem;
  font-weight: 600;
}

h3 {
  font-size: 1.2rem;
  font-weight: 600;
}
```

- **`font-size`:** o tamanho da letra. O `h1` fica com 2,5 × 16 = 40px.
- **`font-weight`:** a grossura (o peso) da letra, de `100` (muito fina) a `900` (muito grossa). `400` é o normal (igual a `normal`) e `700` é o negrito (igual a `bold`). O `600` fica entre os dois. Os pesos que usamos aqui são os que pedimos ao Google Fonts.

**Resultado esperado:** há uma diferença clara de tamanho entre o nome (`h1`), os títulos das secções (`h2`) e os subtítulos (`h3`), e os três são maiores do que o texto normal.

> **Atenção:** se pedirem um peso que não descarregaram (por exemplo `font-weight: 300` com a Poppins que só tem 600 e 700), o browser "inventa" esse peso a partir de outro, e o resultado fica feio. Peçam ao Google Fonts os pesos que vão usar.

#### Passo 3: O Cabeçalho e o Menu

Nas próximas regras usamos seletores descendentes (aula 8): `header p` quer dizer "os parágrafos que estão **dentro** do `header`".

Na **secção 3**, escrevam:

```css
header {
  text-align: center;
}

header p {
  font-size: 1.125rem;
  color: #6b7280;
}

nav ul {
  list-style: none;
  padding: 0;
}

nav li {
  display: inline-block;
}

nav a {
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  text-decoration: none;
  color: #134e4a;
}
```

- **`text-align: center`:** centra o texto (e a fotografia) do cabeçalho. Outros valores: `left` (esquerda), `right` (direita) e `justify` (justificado).
- **`header p`:** a frase de apresentação fica um pouco maior e cinzenta, para ficar claro que é secundária em relação ao nome.
- **`nav ul` e `nav li`:** tiram as marcas da lista e põem os itens do menu lado a lado (aula 8).
- **`text-transform: uppercase`:** mostra o texto em maiúsculas sem mudar o HTML. No HTML continua a estar "Início"; só o ecrã mostra "INÍCIO". Também existem `lowercase` (minúsculas) e `capitalize` (Primeira Letra Maiúscula).
- **`letter-spacing: 0.08em`:** afasta as letras umas das outras. Texto em maiúsculas pequeno lê-se melhor com as letras um pouco afastadas.
- **`text-decoration: none`:** tira o sublinhado dos links do menu. Os links no meio do texto continuam sublinhados, para se perceber que são clicáveis.

**Resultado esperado:** o cabeçalho está centrado e o menu é uma linha de três palavras em maiúsculas pequenas, espaçadas e sem sublinhado.

#### Passo 4: Rodapé, Links e Texto Inclinado

Ainda na **secção 3**, escrevam a regra do rodapé:

```css
footer {
  text-align: center;
  font-size: 0.875rem;
  color: #6b7280;
}
```

Na **secção 2**, acrescentem o peso à regra dos links:

```css
a {
  color: #0f766e;
  font-weight: 600;
}
```

Na **secção 4**, a legenda das tabelas fica em itálico, alinhada à esquerda e cinzenta:

```css
caption {
  font-style: italic;
  text-align: left;
  color: #6b7280;
}
```

**`font-style: italic`** inclina a letra. O contrário é `font-style: normal`.

> **Desafio rápido:** nas DevTools ou no VS Code, mudem o `font-size` do `h1` para `5rem` e vejam o nome crescer. Experimentem `text-transform: uppercase` no `h1`. Voltem aos valores do guia no fim.

> **Confirmem antes de avançar:**
>
> - Sabem quanto é `2rem` em píxeis (32px) e porque é que usamos `rem` para os tamanhos de letra.
> - O menu está em maiúsculas, espaçado e sem sublinhado.
> - O rodapé tem letra mais pequena e cinzenta.
> - A legenda (`caption`) das tabelas está em itálico.

---

### Parte 5: O Box Model (Todos os Elementos São Caixas)

Esta é a ideia mais importante da aula: **para o browser, cada elemento da página é uma caixa retangular**. Um título, um parágrafo, uma imagem, um link: tudo são caixas. O **box model** (modelo de caixa) descreve as camadas de cada caixa.

#### Passo 1: As Quatro Camadas de uma Caixa

Pensem num quadro pendurado numa parede:

1. **Conteúdo (*content*):** a pintura. No HTML, é o texto ou a imagem.
2. **`padding` (preenchimento):** o passe-partout, o cartão à volta da pintura. É espaço **dentro** da moldura e tem a cor de fundo da caixa.
3. **`border` (borda):** a moldura.
4. **`margin` (margem):** a parede livre entre este quadro e o quadro seguinte. É espaço **fora** da moldura, sempre transparente.

```
┌─────────────────────────────── margin ───────────────────────────────┐
│                                                                      │
│   ┌──────────────────────────── border ────────────────────────────┐ │
│   │                                                                │ │
│   │   ┌───────────────────────── padding ────────────────────────┐ │ │
│   │   │                                                          │ │ │
│   │   │                     conteúdo (texto)                     │ │ │
│   │   │                                                          │ │ │
│   │   └──────────────────────────────────────────────────────────┘ │ │
│   │                                                                │ │
│   └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

#### Passo 2: Ver as Caixas nas DevTools

1. No `index.html` aberto no browser, cliquem com o botão direito no testemunho ("A Ana resolve qualquer problema...") e escolham **Inspecionar**.
2. No painel **Elements**, cliquem na linha `<article class="cartao">`.
3. Passem o rato por cima dessa linha: no ecrã, a caixa fica pintada. O azul é o conteúdo, o verde é o `padding` e o laranja é a `margin`.
4. Do lado direito, abram o separador **Computed** (Calculado). No topo aparece o desenho do box model, com um número em cada camada. Por agora o `padding` e a `border` mostram `-` (zero).

Vamos usar este desenho durante toda a Parte 5 para confirmar cada valor.

#### Passo 3: `padding` (O Espaço Dentro da Caixa)

O testemunho já tem a classe `cartao` desde a aula 8. Confirmem no `index.html`:

```html
<article class="cartao">
  <blockquote>
    <p>A Ana resolve qualquer problema com calma e com um sorriso.</p>
  </blockquote>
  <p>— Carla Sousa, gerente da loja onde a Ana trabalhou</p>
</article>
```

Se não tiverem o `class="cartao"`, acrescentem-no. Na **secção 5** do CSS, escrevam:

```css
.cartao {
  background-color: #ffffff;
  padding: 20px 24px;
}
```

**Resultado esperado:** o testemunho fica numa caixa branca, e o texto já não está encostado às bordas da caixa: há 20px de branco em cima e em baixo e 24px de cada lado.

A propriedade `padding` aceita 1, 2 ou 4 valores (é uma **propriedade de atalho**, *shorthand*):

1. **`padding: 20px;`** os quatro lados com 20px.
2. **`padding: 20px 24px;`** em cima e em baixo 20px; direita e esquerda 24px.
3. **`padding: 10px 20px 30px 40px;`** cada lado o seu valor, pela ordem dos ponteiros do relógio, a começar ao meio-dia: **cima, direita, baixo, esquerda**.

Também podem escrever um lado de cada vez: `padding-top`, `padding-right`, `padding-bottom` e `padding-left`.

> **Desafio rápido:** nas DevTools, no separador **Computed**, confirmem os números do `padding` no desenho (20 em cima e em baixo, 24 dos lados). Depois mudem a regra para `padding: 10px 20px 30px 40px;`, vejam qual lado mudou e voltem a `20px 24px`.

#### Passo 4: `border` (A Moldura)

Acrescentem uma borda à regra `.cartao`:

```css
.cartao {
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 20px 24px;
}
```

A propriedade `border` junta três valores, por qualquer ordem:

1. **Espessura:** `1px`.
2. **Estilo:** `solid` (contínua). Outros estilos: `dashed` (tracejada), `dotted` (pontilhada) e `double` (dupla).
3. **Cor:** `#e5e7eb`.

**`border-radius: 12px`** arredonda os cantos da caixa. Quanto maior o número, mais redondo o canto.

Também podemos pôr a borda só num lado: `border-top`, `border-right`, `border-bottom` ou `border-left`. Vamos usar isso nos títulos. Na **secção 2**, acrescentem à regra do `h2`:

```css
h2 {
  font-size: 1.6rem;
  font-weight: 600;
  padding-bottom: 8px;
  border-bottom: 2px solid #e5e7eb;
}
```

O `padding-bottom` afasta a linha do texto do título.

E a fotografia do cabeçalho? Uma imagem também é uma caixa, por isso também aceita borda. Com `border-radius: 50%`, os cantos arredondam até metade da largura e a caixa quadrada fica um círculo. Na **secção 3**:

```css
header img {
  border: 4px solid #ffffff;
  border-radius: 50%;
}
```

**Resultado esperado:** o testemunho tem uma moldura cinzenta fina e cantos redondos; cada `h2` tem uma linha por baixo; a fotografia é um círculo com um aro branco.

> **Desafio rápido:** na regra `.cartao`, troquem `solid` por `dashed`, depois por `dotted`, e mudem a espessura para `4px`. Voltem a `1px solid` no fim.

#### Passo 5: `margin` (O Espaço Fora da Caixa)

O `padding` afasta o conteúdo da moldura; a `margin` afasta a caixa das **outras caixas**. Acrescentem à regra `.cartao`:

```css
.cartao {
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 20px 24px;
  margin-bottom: 24px;
}
```

Abram o `projetos.html`: os três projetos (também com `class="cartao"`) estão separados por 24px de espaço. Reparem que esse espaço **não é branco**: a margem é sempre transparente e deixa ver o fundo da página.

A `margin` funciona como o `padding`: aceita 1, 2 ou 4 valores e tem as versões `margin-top`, `margin-right`, `margin-bottom` e `margin-left`.

Agora as margens dos títulos e dos parágrafos. Na **secção 2**, juntem as margens às regras dos títulos e escrevam a regra do `p`:

```css
h1 {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 16px 0 4px;
}

h2 {
  font-size: 1.6rem;
  font-weight: 600;
  margin: 48px 0 16px;
  padding-bottom: 8px;
  border-bottom: 2px solid #e5e7eb;
}

h3 {
  font-size: 1.2rem;
  font-weight: 600;
  margin: 0 0 8px;
}

p {
  margin: 0 0 16px;
}
```

Com **3 valores** (`margin: 48px 0 16px`) a ordem é: cima, direita **e** esquerda, baixo. Cada `h2` fica com muito espaço por cima (separa as secções) e pouco por baixo (fica "colado" ao texto que apresenta).

> **Atenção:** quando duas margens verticais se tocam (a margem de baixo de um parágrafo e a margem de cima do título seguinte), o browser **não as soma**: fica só a maior. Chama-se **fusão de margens** (*margin collapse*). Se o espaço entre dois elementos vos parecer mais pequeno do que a soma, é por isto.

#### Passo 6: Uma Sombra à Volta da Caixa

A sombra não é uma camada do box model, mas desenha-se à volta da caixa e dá a ideia de que o cartão está "levantado" da página. Acrescentem à regra `.cartao`:

```css
box-shadow: 0 2px 8px rgba(15, 23, 42, 0.08);
```

Os valores são, por ordem:

1. **`0`:** deslocamento para a direita (aqui, nenhum).
2. **`2px`:** deslocamento para baixo (como se a luz viesse de cima).
3. **`8px`:** desfoque (quanto maior, mais suave).
4. **`rgba(15, 23, 42, 0.08)`:** a cor, quase transparente (8%). Sombras pretas e opacas parecem sujidade; sombras quase transparentes parecem naturais.

Façam o mesmo na fotografia do cabeçalho (**secção 3**), com a cor principal transparente:

```css
header img {
  border: 4px solid #ffffff;
  border-radius: 50%;
  box-shadow: 0 4px 12px rgba(15, 118, 110, 0.25);
}
```

> **Confirmem antes de avançar:**
>
> - Sabem dizer, por ordem de dentro para fora, as quatro camadas de uma caixa: conteúdo, `padding`, `border`, `margin`.
> - Sabem a diferença entre `padding` (dentro, com a cor de fundo) e `margin` (fora, transparente).
> - No separador **Computed** das DevTools, o desenho do `.cartao` mostra padding 20/24, border 1 e margin-bottom 24.
> - Os projetos em `projetos.html` estão em cartões brancos, com moldura, cantos redondos, sombra suave e espaço entre eles.

---

### Parte 6: A Largura das Caixas (`box-sizing` e Conteúdo Centrado)

#### Passo 1: O Problema dos 100%

Vamos dar ao campo da mensagem do formulário a largura toda. Na **secção 4**, escrevam:

```css
input,
select,
textarea {
  padding: 8px 10px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-family: inherit;
  font-size: 1rem;
}

textarea {
  width: 100%;
}
```

- Os campos ganham espaço interior, uma moldura cinzenta e cantos redondos.
- **`font-family: inherit`:** por omissão, os campos de formulário **não** herdam a fonte da página. O valor `inherit` obriga-os a herdar.
- **`width: 100%`:** o `textarea` ocupa a largura toda do elemento onde está.

Abram o `contactos.html` e olhem com atenção para o lado direito da caixa da mensagem: **ela sai uns píxeis para fora** do quadro do formulário. Porquê?

Por omissão, o `width` mede **só o conteúdo**. O browser faz esta conta:

- 100% do conteúdo + 10px + 10px de `padding` + 1px + 1px de `border` = **100% + 22px**.

#### Passo 2: A Solução: `box-sizing: border-box`

A propriedade `box-sizing` muda a forma de medir:

1. **`content-box`** (o valor por omissão): o `width` é só o conteúdo; o `padding` e a `border` somam-se por fora.
2. **`border-box`:** o `width` é a caixa toda, **incluindo** o `padding` e a `border`. O browser encolhe o conteúdo para tudo caber.

Com `border-box`, `width: 100%` quer dizer mesmo 100%. É tão mais fácil que quase todos os sites o aplicam a **todos** os elementos. Para isso usamos um seletor novo, o **seletor universal** `*` (asterisco), que escolhe todos os elementos da página.

No início da **secção 1**, antes do `body`, escrevam:

```css
/* A largura de cada caixa passa a incluir o padding e a borda */
* {
  box-sizing: border-box;
}
```

E, por cima do `textarea` (**secção 4**), deixem um comentário para se lembrarem:

```css
/* Sem border-box, os 100% + padding + borda sairiam do fieldset */
textarea {
  width: 100%;
}
```

**Resultado esperado:** a caixa da mensagem cabe exatamente dentro do formulário.

> **Desafio rápido:** nas DevTools, encontrem a regra `*` no separador **Styles** e desliguem a caixa ao lado de `box-sizing`. A caixa da mensagem volta a sair. Voltem a ligá-la.

#### Passo 3: Centrar o Conteúdo com `max-width` e `margin: auto`

Num ecrã largo, as linhas de texto ficam compridas demais: os olhos perdem-se a passar para a linha seguinte. Uma boa linha de texto tem entre 60 e 80 letras. Vamos limitar a largura do `<main>` e centrá-lo.

Na **secção 1**, acrescentem `margin: 0` ao `body` e escrevam a regra do `main`:

```css
body {
  font-family:
    system-ui,
    -apple-system,
    "Segoe UI",
    Roboto,
    sans-serif;
  line-height: 1.6;
  color: #1f2937;
  background-color: #f8fafc;
  margin: 0;
}

/* Conteúdo centrado, com uma largura máxima confortável para ler */
main {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 16px;
}
```

- **`margin: 0`** no `body`: o browser põe 8px de margem à volta da página. Tiramo-la para o cabeçalho poder ir de uma ponta à outra do ecrã.
- **`max-width: 800px`:** o `main` nunca fica mais largo do que 800px. Num ecrã estreito (um telemóvel) fica mais pequeno, sem problema. Se escrevêssemos `width: 800px`, num telemóvel com 400px de largura o texto saía do ecrã.
- **`margin: 0 auto`:** zero em cima e em baixo; `auto` à direita e à esquerda. Com `auto`, o browser divide o espaço que sobra em duas partes iguais, uma de cada lado, e a caixa fica **centrada**.
- **`padding: 0 16px`:** num ecrã estreito, o texto não fica encostado às bordas do ecrã.

Agora o cabeçalho e o rodapé. Na **secção 3**, completem as regras:

```css
header {
  background-color: #ffffff;
  border-bottom: 1px solid #e5e7eb;
  padding: 40px 16px 16px;
  text-align: center;
}

header p {
  font-size: 1.125rem;
  color: #6b7280;
  margin-bottom: 0;
}

footer {
  max-width: 800px;
  margin: 64px auto 0;
  padding: 24px 16px;
  border-top: 1px solid #e5e7eb;
  text-align: center;
  font-size: 0.875rem;
  color: #6b7280;
}

footer p {
  margin: 0;
}
```

O cabeçalho é uma faixa branca de uma ponta à outra do ecrã; o rodapé fica centrado, com a mesma largura máxima do conteúdo e uma linha por cima.

**Resultado esperado:** num ecrã largo, o conteúdo está numa coluna centrada, com espaço livre dos dois lados. Se estreitarem a janela do browser, a coluna encolhe e o texto continua dentro do ecrã.

#### Passo 4: Caixas em Linha e `inline-block`

Na aula 3 vimos que há elementos **de bloco** (começam numa linha nova e ocupam a largura toda: `p`, `h2`, `section`) e elementos **em linha** (ficam dentro da linha de texto: `a`, `strong`, `span`). No box model, há uma diferença importante:

- Num elemento **em linha**, o `padding` de cima e de baixo é desenhado, mas **não empurra** as linhas vizinhas, e a `margin` de cima e de baixo é ignorada.
- Com **`display: inline-block`**, o elemento continua na linha, mas passa a respeitar o `padding` e a `margin` em todos os lados.

Os links do menu são elementos em linha. Para lhes darmos uma "zona de clique" maior, completem as regras do menu na **secção 3**:

```css
nav ul {
  list-style: none;
  margin: 24px 0 0;
  padding: 0;
}

nav li {
  display: inline-block;
  margin: 0 4px;
}

nav a {
  display: inline-block;
  padding: 8px 16px;
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  text-decoration: none;
  color: #134e4a;
}
```

**Resultado esperado:** os itens do menu ficam mais afastados uns dos outros. Nas DevTools, ao passarem o rato por cima de um link do menu, a zona pintada (conteúdo + `padding`) é maior do que a palavra: é a área onde se pode clicar.

> **Confirmem antes de avançar:**
>
> - Sabem explicar a diferença entre `box-sizing: content-box` e `border-box`.
> - A caixa da mensagem em `contactos.html` não sai do formulário.
> - O conteúdo das três páginas está numa coluna centrada, com no máximo 800px.
> - O cabeçalho é uma faixa branca de uma ponta à outra do ecrã.

---

### Parte 7: Os Componentes do Portefólio (Notas, Botões, Tabelas e Formulário)

Com as cores, as fontes e o box model, já sabemos desenhar qualquer caixa. Vamos acabar os restantes componentes do portefólio.

#### Passo 1: Confirmar as Classes no HTML

As regras desta parte usam as classes que já estão no HTML desde a aula 8. Confirmem que as têm (e, se faltar alguma, acrescentem-na):

1. Em `index.html` e `contactos.html`, a caixa `<aside>` tem `class="curiosidade"`.
2. Em `index.html` e `contactos.html`, o link do e-mail tem `class="destaque"`.
3. Em `index.html`, o link para a página de contactos tem `class="botao"`.
4. Em `contactos.html`, o botão de enviar tem `class="botao"` e o de limpar tem `class="botao botao-secundario"`.
5. Em `projetos.html`, cada projeto é um `<article class="cartao">`.
6. Em `contactos.html`, a secção do formulário tem `id="formulario-contacto"`.

#### Passo 2: A Citação do Cartão e a Caixa de Curiosidade

Na **secção 5**, por baixo de `.cartao`, escrevam:

```css
.cartao blockquote {
  margin: 0 0 12px;
  font-size: 1.125rem;
  font-style: italic;
  color: #134e4a;
}

.curiosidade {
  background-color: #fff7ed;
  border-left: 4px solid #ea580c;
  border-radius: 0 8px 8px 0;
  padding: 16px 20px;
  margin: 24px 0;
}

.curiosidade p {
  margin: 0;
}

.destaque {
  font-weight: 700;
  color: #0f766e;
}
```

- **`.cartao blockquote`:** o `blockquote` tem margens grandes do browser (cerca de 40px dos lados). Tiramo-las, e a citação fica maior e em itálico.
- **`.curiosidade`:** fundo laranja muito claro, com uma barra laranja à esquerda. `border-radius: 0 8px 8px 0` usa quatro valores, um por canto (cima-esquerda, cima-direita, baixo-direita, baixo-esquerda): só os cantos da direita ficam redondos, para a barra continuar direita.
- **`.curiosidade p { margin: 0; }`:** o parágrafo dentro da caixa já não precisa da margem de baixo; o `padding` da caixa trata do espaço.

#### Passo 3: Os Botões

Ainda na **secção 5**:

```css
/* Padding em em: cresce e encolhe com o tamanho da letra do botão */
.botao {
  display: inline-block;
  padding: 0.6em 1.4em;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 600;
  color: #ffffff;
  background-color: #0f766e;
  border: 2px solid #0f766e;
  border-radius: 8px;
  text-decoration: none;
  cursor: pointer;
}

.botao-secundario {
  color: #0f766e;
  background-color: #ffffff;
}
```

- **`display: inline-block`:** a classe serve para links (`<a>`, em linha) e para botões (`<button>`). Assim o `padding` funciona nos dois.
- **`padding: 0.6em 1.4em`:** em `em`, o espaço interior acompanha o tamanho da letra. Se um dia fizerem um botão grande com `font-size: 1.5rem`, o espaço cresce na mesma proporção, sem mais contas.
- **`border: 2px solid #0f766e`:** a borda tem a mesma cor do fundo, por isso não se vê. Serve para o botão secundário, que tem fundo branco e mostra essa borda.
- **`cursor: pointer`:** o rato passa a ser uma "mãozinha" por cima do botão.
- **`.botao-secundario`:** muda só as cores. Como tem as duas classes (`class="botao botao-secundario"`), o botão de limpar fica com a forma do `.botao` e com as cores do `.botao-secundario`: fundo branco, texto e borda verde-azulados.

**Resultado esperado:** em `contactos.html`, "Enviar mensagem" é um botão verde-azulado com letra branca, e "Limpar formulário" é um botão branco com borda e letra verde-azuladas, com o mesmo tamanho.

#### Passo 4: As Tabelas

Na **secção 4**, juntem às regras que já lá estão:

```css
table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0 24px;
  background-color: #ffffff;
}

caption {
  margin-bottom: 8px;
  font-style: italic;
  text-align: left;
  color: #6b7280;
}

th,
td {
  padding: 10px 12px;
  border: 1px solid #e5e7eb;
  text-align: left;
}

thead th {
  background-color: #0f766e;
  color: #ffffff;
}
```

- **`border-collapse: collapse`:** cada célula tem a sua borda; sem isto, aparecem bordas duplas entre as células. Com `collapse`, as bordas vizinhas juntam-se numa só.
- **`padding` em `th, td`:** as células são caixas, por isso o texto ganha espaço para respirar.
- **`thead th`:** só os cabeçalhos das colunas (que estão dentro do `thead`) ficam com fundo verde-azulado e letra branca. Os cabeçalhos das linhas (no `tbody`) ficam com o fundo branco.

#### Passo 5: O Formulário

Na **secção 4**, escrevam as regras dos grupos do formulário e dos rótulos:

```css
fieldset {
  margin: 0 0 24px;
  padding: 16px 20px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
}

legend {
  padding: 0 8px;
  font-family: "Poppins", system-ui, sans-serif;
  font-weight: 600;
  color: #134e4a;
}

label {
  font-weight: 600;
}
```

O `<legend>` fica por cima da borda do `fieldset`; o `padding: 0 8px` afasta a borda das letras da legenda.

Por fim, a secção do formulário é única no site, por isso usamos o seu `id`. Na **secção 6**:

```css
#formulario-contacto {
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 8px 24px 24px;
  margin-top: 48px;
}

#formulario-contacto h2 {
  margin-top: 24px;
}
```

O `h2` tem `margin-top: 48px` para separar as secções, mas dentro do quadro branco isso seria espaço a mais. A regra `#formulario-contacto h2` reduz essa margem só para o título que está dentro do formulário.

**Resultado esperado:** o formulário de `contactos.html` está num quadro branco com cantos redondos; cada grupo (`fieldset`) tem a sua moldura cinzenta e a legenda com a fonte dos títulos; os campos têm moldura cinzenta e cantos redondos.

> **Confirmem antes de avançar:**
>
> - A curiosidade em `index.html` e a nota em `contactos.html` têm fundo laranja-claro e barra laranja à esquerda.
> - O link "Página de Contactos" no `index.html` parece um botão.
> - As tabelas têm os cabeçalhos das colunas com fundo da cor principal e letra branca.
> - O vosso `style.css` está igual ao código completo no fim deste guia (com as vossas cores e fontes).

---

### Parte 8: Guardar a Evolução no Git e no GitHub

1. Abram o terminal do VS Code (**Ctrl + `**).
2. Escrevam `git status`: devem aparecer como modificados os três ficheiros HTML (por causa do Google Fonts) e o `css/style.css`.
3. Adicionem tudo à área de preparação:

```bash
git add .
```

4. Criem o commit:

```bash
git commit -m "Adiciona paleta de cores, fontes e box model ao portefolio"
```

5. Enviem para o GitHub:

```bash
git push
```

6. Abram o vosso repositório no GitHub e confirmem que o último commit aparece com a vossa mensagem.

> **Confirmem antes de avançar:**
>
> - O `git status` mostra *nothing to commit, working tree clean*.
> - No GitHub, o ficheiro `css/style.css` mostra o código novo.

---

**O projeto no fim da aula:**

```
portefolio/
├── css/
│   └── style.css
├── imagens/
│   ├── favicon.svg
│   └── foto.svg
├── contactos.html
├── index.html
└── projetos.html
```

O HTML só mudou no `<head>` das três páginas (as três linhas do Google Fonts). No `index.html` fica assim:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="Portefólio pessoal de Ana Martins, futura programadora web em Setúbal. Apresentação, percurso de formação e projetos práticos."
  />
  <meta name="author" content="Ana Martins" />
  <title>Ana Martins | Portefólio</title>
  <link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;700&display=swap"
    rel="stylesheet"
  />
  <link rel="stylesheet" href="css/style.css" />
</head>
```

#### Código completo de `css/style.css`

```css
/* ==========================================================================
   Portefólio Pessoal — Ana Martins
   Folha de Estilos Principal
   ========================================================================== */

/* Paleta de cores
   - Principal (verde-azulado): #0f766e
   - Títulos:                   #134e4a
   - Texto:                     #1f2937
   - Texto secundário:          #6b7280
   - Linhas e bordas:           #e5e7eb
   - Fundo da página:           #f8fafc
   - Fundo dos cartões:         #ffffff
   - Realce (laranja):          #ea580c
*/

/* --------------------------------------------------------------------------
   1. Base: caixas, corpo da página e largura do conteúdo
   -------------------------------------------------------------------------- */

/* A largura de cada caixa passa a incluir o padding e a borda */
* {
  box-sizing: border-box;
}

body {
  font-family:
    system-ui,
    -apple-system,
    "Segoe UI",
    Roboto,
    sans-serif;
  line-height: 1.6;
  color: #1f2937;
  background-color: #f8fafc;
  margin: 0;
}

/* Conteúdo centrado, com uma largura máxima confortável para ler */
main {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 16px;
}

/* --------------------------------------------------------------------------
   2. Texto e fontes
   -------------------------------------------------------------------------- */

h1,
h2,
h3 {
  font-family: "Poppins", system-ui, sans-serif;
  color: #134e4a;
  line-height: 1.25;
}

h1 {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 16px 0 4px;
}

h2 {
  font-size: 1.6rem;
  font-weight: 600;
  margin: 48px 0 16px;
  padding-bottom: 8px;
  border-bottom: 2px solid #e5e7eb;
}

h3 {
  font-size: 1.2rem;
  font-weight: 600;
  margin: 0 0 8px;
}

p {
  margin: 0 0 16px;
}

a {
  color: #0f766e;
  font-weight: 600;
}

img {
  max-width: 100%;
  height: auto;
}

/* --------------------------------------------------------------------------
   3. Cabeçalho, menu e rodapé
   -------------------------------------------------------------------------- */

header {
  background-color: #ffffff;
  border-bottom: 1px solid #e5e7eb;
  padding: 40px 16px 16px;
  text-align: center;
}

header img {
  border: 4px solid #ffffff;
  border-radius: 50%;
  box-shadow: 0 4px 12px rgba(15, 118, 110, 0.25);
}

header p {
  font-size: 1.125rem;
  color: #6b7280;
  margin-bottom: 0;
}

nav ul {
  list-style: none;
  margin: 24px 0 0;
  padding: 0;
}

nav li {
  display: inline-block;
  margin: 0 4px;
}

nav a {
  display: inline-block;
  padding: 8px 16px;
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  text-decoration: none;
  color: #134e4a;
}

footer {
  max-width: 800px;
  margin: 64px auto 0;
  padding: 24px 16px;
  border-top: 1px solid #e5e7eb;
  text-align: center;
  font-size: 0.875rem;
  color: #6b7280;
}

footer p {
  margin: 0;
}

/* --------------------------------------------------------------------------
   4. Tabelas e formulários
   -------------------------------------------------------------------------- */

table {
  width: 100%;
  border-collapse: collapse;
  margin: 16px 0 24px;
  background-color: #ffffff;
}

caption {
  margin-bottom: 8px;
  font-style: italic;
  text-align: left;
  color: #6b7280;
}

th,
td {
  padding: 10px 12px;
  border: 1px solid #e5e7eb;
  text-align: left;
}

thead th {
  background-color: #0f766e;
  color: #ffffff;
}

fieldset {
  margin: 0 0 24px;
  padding: 16px 20px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
}

legend {
  padding: 0 8px;
  font-family: "Poppins", system-ui, sans-serif;
  font-weight: 600;
  color: #134e4a;
}

label {
  font-weight: 600;
}

input,
select,
textarea {
  padding: 8px 10px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-family: inherit;
  font-size: 1rem;
}

/* Sem border-box, os 100% + padding + borda sairiam do fieldset */
textarea {
  width: 100%;
}

/* --------------------------------------------------------------------------
   5. Componentes reutilizáveis (classes)
   -------------------------------------------------------------------------- */

.cartao {
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 20px 24px;
  margin-bottom: 24px;
  box-shadow: 0 2px 8px rgba(15, 23, 42, 0.08);
}

.cartao blockquote {
  margin: 0 0 12px;
  font-size: 1.125rem;
  font-style: italic;
  color: #134e4a;
}

.curiosidade {
  background-color: #fff7ed;
  border-left: 4px solid #ea580c;
  border-radius: 0 8px 8px 0;
  padding: 16px 20px;
  margin: 24px 0;
}

.curiosidade p {
  margin: 0;
}

.destaque {
  font-weight: 700;
  color: #0f766e;
}

/* Padding em em: cresce e encolhe com o tamanho da letra do botão */
.botao {
  display: inline-block;
  padding: 0.6em 1.4em;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 600;
  color: #ffffff;
  background-color: #0f766e;
  border: 2px solid #0f766e;
  border-radius: 8px;
  text-decoration: none;
  cursor: pointer;
}

.botao-secundario {
  color: #0f766e;
  background-color: #ffffff;
}

/* --------------------------------------------------------------------------
   6. Elementos únicos (id)
   -------------------------------------------------------------------------- */

#formulario-contacto {
  background-color: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 8px 24px 24px;
  margin-top: 48px;
}

#formulario-contacto h2 {
  margin-top: 24px;
}
```

---

### Se Algo Correr Mal

1. **Os títulos não mudam para a fonte do Google Fonts.**
   - Confirmem que as linhas do Google Fonts estão no `<head>` **das três páginas** e **antes** do `style.css`.
   - Confirmem que o nome no CSS está igual ao do Google, com aspas e maiúscula: `"Poppins"`.
   - Confirmem que têm internet. Sem internet, os títulos aparecem com a fonte seguinte da lista, e isso é normal.
2. **Escrevi um tamanho e não acontece nada.**
   - Falta a unidade (`font-size: 2;` não funciona; tem de ser `2rem`), ou há um espaço entre o número e a unidade (`2 rem`).
   - As únicas exceções são o `line-height` (que funciona sem unidade) e o valor `0`, que não precisa de unidade.
3. **Uma cor não funciona.**
   - Falta o `#` antes do código hexadecimal (`0f766e` em vez de `#0f766e`), ou o código tem uma letra que não existe em hexadecimal (só se usam 0 a 9 e `a` a `f`).
   - Num `rgb()`, falta uma vírgula ou um parêntese.
4. **A caixa da mensagem (`textarea`) sai para fora do formulário.**
   - Falta a regra `* { box-sizing: border-box; }` no topo da secção 1, ou falta o asterisco.
5. **O conteúdo não fica centrado.**
   - Confirmem que escreveram `max-width` (e não só `width`) e `margin: 0 auto` na regra do `main`. Sem largura máxima, a caixa ocupa a largura toda e não há espaço para dividir pelos lados.
6. **O espaço à volta de um link do menu não muda.**
   - Os links são elementos em linha: falta `display: inline-block;` na regra `nav a`.
7. **Há um espaço que não sei de onde vem.**
   - Inspecionem o elemento nas DevTools e vejam o desenho do box model no separador **Computed**. Passem o rato pelos elementos vizinhos: o laranja (margem) mostra quem está a criar o espaço. Muitas vezes são as margens do browser em `h2`, `p`, `ul` ou `blockquote`.

---

### O Que Aprendemos Hoje

Antes de passarem ao exercício, confirmem que conseguem explicar:

- [ ] As quatro formas de escrever uma cor (nome, hexadecimal, `rgb()` e `hsl()`) e como fazer uma cor transparente com `rgba()`.
- [ ] O que é uma paleta e porque é que o contraste entre o texto e o fundo é importante.
- [ ] Porque é que `font-family` tem uma lista de fontes e acaba sempre numa família genérica.
- [ ] Como usar uma fonte do Google Fonts (o `<link>` no `<head>` e o nome no `font-family`).
- [ ] A diferença entre `px`, `rem`, `em` e `%`, e porque usamos `rem` nos tamanhos de letra.
- [ ] O que fazem `font-weight`, `line-height`, `text-align`, `text-transform`, `letter-spacing`, `text-decoration` e `font-style`.
- [ ] As quatro camadas do box model (conteúdo, `padding`, `border`, `margin`) e onde as ver nas DevTools.
- [ ] Como escrever `padding` e `margin` com 1, 2, 3 ou 4 valores.
- [ ] O que faz `box-sizing: border-box` e porque o aplicamos a todos os elementos com `*`.
- [ ] Como centrar uma caixa com `max-width` e `margin: 0 auto`.
- [ ] Porque é que um link precisa de `display: inline-block` para o `padding` funcionar em todos os lados.

---

### Palavras Novas

- **Paleta de cores:** o conjunto pequeno de cores escolhidas para um site e usadas sempre.
- **Hexadecimal (`#rrggbb`):** forma de escrever uma cor com três pares de algarismos (0 a 9 e `a` a `f`) para o vermelho, o verde e o azul.
- **`rgb()` / `rgba()`:** forma de escrever uma cor com três números de 0 a 255 (vermelho, verde, azul); o `rgba()` acrescenta a opacidade, de 0 a 1.
- **`hsl()`:** forma de escrever uma cor com o tom (0 a 360), a saturação (%) e a luminosidade (%).
- **Contraste:** a diferença de luz entre a cor do texto e a do fundo; quanto maior, mais fácil de ler.
- **Lista de fontes (*font stack*):** lista de fontes no `font-family`; o browser usa a primeira que existir.
- **Família genérica:** a última fonte da lista (`serif`, `sans-serif`, `monospace`), que existe sempre.
- **Serifa:** o pequeno traço nas pontas das letras de fontes como a Times ou a Georgia.
- **Google Fonts:** serviço gratuito do Google com fontes que o browser descarrega ao abrir a página.
- **Peso da fonte (`font-weight`):** a grossura da letra, de 100 a 900 (400 normal, 700 negrito).
- **`rem`:** unidade relativa ao tamanho de letra da página (por omissão, 1rem = 16px).
- **`em`:** unidade relativa ao tamanho de letra do próprio elemento.
- **Box model (modelo de caixa):** a forma como o browser desenha cada elemento: conteúdo, `padding`, `border` e `margin`.
- **`padding` (preenchimento):** espaço entre o conteúdo e a borda, dentro da caixa, com a cor de fundo.
- **`border` (borda):** a linha à volta da caixa, com espessura, estilo e cor.
- **`margin` (margem):** espaço transparente fora da borda, que afasta a caixa das outras.
- **Propriedade de atalho (*shorthand*):** propriedade que junta várias numa só, como `padding: 20px 24px` ou `border: 1px solid #e5e7eb`.
- **Fusão de margens (*margin collapse*):** quando duas margens verticais se tocam, fica só a maior.
- **`box-sizing`:** define se o `width` inclui só o conteúdo (`content-box`) ou também o `padding` e a borda (`border-box`).
- **Seletor universal (`*`):** seletor que escolhe todos os elementos da página.
- **`max-width`:** largura máxima de uma caixa; num ecrã mais estreito, a caixa encolhe.
- **`inline-block`:** valor de `display` que mantém o elemento na linha, mas respeita `padding` e `margin` em todos os lados.

---

### Para Saber Mais

Os recursos abaixo estão em inglês. Usem a tradução automática do browser (botão direito → **Traduzir para português**) se precisarem.

- [Cores em CSS (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)
- [Formatar texto e fontes (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Fundamentals)
- [Fontes da web (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)
- [O box model (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
- [O box model (web.dev)](https://web.dev/learn/css/box-model)
- [Google Fonts](https://fonts.google.com)

---

# Exercício Final: Os Elétricos de Lisboa

Agora é a vossa vez de praticar sozinhos. O enunciado completo está também na ficha [`ex-009.md`](../../exercicios/ex-009.md) e os ficheiros de apoio estão na pasta [`exercicios/ex-009/`](../../exercicios/ex-009/).

### Missão 1: A Minha Cidade com Identidade Visual

1. Criem a pasta `sessao-09` dentro de `exercicios-uf1.1` e copiem para lá todo o conteúdo da pasta `sessao-08`.
2. No `css/estilo.css`, escrevam um comentário com a paleta das páginas da cidade e dos Passadiços (uma cor principal, uma cor de realce e os neutros).
3. Escolham uma fonte no Google Fonts para os títulos e liguem-na no `<head>` de `cidade.html` e `passadicos-paiva.html`.
4. Reorganizem o `estilo.css` com `* { box-sizing: border-box; }`, um `main` centrado com `max-width` e `margin: 0 auto`, tamanhos de letra em `rem` e cartões com `padding`, `border`, `border-radius`, `margin` e `box-shadow`.
5. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Adiciona paleta, fontes e box model a cidade e passadicos"`, `git push`.

### Missão 2: A Página dos Elétricos de Lisboa

1. Copiem os ficheiros [`eletricos-lisboa.txt`](../../exercicios/ex-009/eletricos-lisboa.txt) e [`eletrico.svg`](../../exercicios/ex-009/eletrico.svg) para a vossa pasta `sessao-09` (a imagem vai para `imagens/`).
2. Criem a página `eletricos-lisboa.html` com o texto do ficheiro `.txt`: cabeçalho com imagem e menu, cinco cartões com as linhas, uma caixa de curiosidade, uma tabela de resumo e uma caixa de avisos.
3. Criem `css/eletricos.css` com uma paleta amarela e escura, uma fonte do Google Fonts e o box model aplicado a todos os componentes.
4. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Cria pagina dos Eletricos de Lisboa"`, `git push`.

### Missão 3: Detetives do Box Model

1. Abram `eletricos-lisboa.html` com o Live Server e inspecionem o primeiro cartão nas DevTools.
2. No separador **Computed**, leiam e anotem os valores do conteúdo, do `padding`, da `border` e da `margin`.
3. Calculem a largura total do cartão com `border-box` e com `content-box` (desligando o `box-sizing` nas DevTools) e comparem.

**Critérios de sucesso:**

- [ ] A pasta `sessao-09` tem `css/estilo.css` e `css/eletricos.css`, cada uma com a sua paleta num comentário.
- [ ] As três páginas usam uma fonte do Google Fonts nos títulos, com uma lista de fontes que acaba numa família genérica.
- [ ] Os tamanhos de letra estão em `rem`.
- [ ] O conteúdo das páginas está centrado, com uma largura máxima.
- [ ] Os cartões, as caixas de nota e os botões usam `padding`, `border`, `border-radius` e `margin`.
- [ ] Os campos de formulário com `width: 100%` não saem do formulário.
- [ ] O validador do W3C não mostra erros de HTML.
- [ ] O repositório no GitHub tem os commits das Missões 1 e 2.

### Missão 4: O Relatório

Respondam às perguntas por palavras vossas:

1. Cores:
   Escrevam a cor branca de três formas diferentes. Para que serve o quarto número em `rgba(0, 0, 0, 0.5)`?
   Resposta: [Preencher]

2. Fontes:
   Porque é que escrevemos `font-family: "Poppins", system-ui, sans-serif;` em vez de só `font-family: "Poppins";`?
   Resposta: [Preencher]

3. Unidades:
   Qual é a diferença entre `rem` e `em`? Quantos píxeis tem um título com `font-size: 1.5rem`?
   Resposta: [Preencher]

4. Box model:
   Expliquem, com as vossas palavras, a diferença entre `padding` e `margin`. Qual dos dois mostra a cor de fundo da caixa?
   Resposta: [Preencher]

5. box-sizing:
   Uma caixa tem `width: 300px`, `padding: 20px` e `border: 5px solid`. Que largura ocupa no ecrã com `content-box`? E com `border-box`?
   Resposta: [Preencher]

---

### Desafio Bónus (Para os mais rápidos)

1. Usem o medidor de contraste das DevTools em todas as cores de texto da página dos Elétricos e corrijam as que não têm o visto verde.
2. Criem uma classe `.botao-grande` que só muda o `font-size` para `1.25rem` e apliquem-na a um botão juntamente com `.botao`. Confirmem que o `padding` (em `em`) cresceu sozinho.
3. Escrevam a cor de fundo da caixa de avisos em `hsl()` e criem uma versão mais clara e outra mais escura só mudando a luminosidade.
