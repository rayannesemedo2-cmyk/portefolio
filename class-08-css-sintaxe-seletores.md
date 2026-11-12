# Guia Prático - UF 1.1 (Aula 8)

## Estilo com CSS I: Sintaxe, Formas de Inclusão e Seletores Fundamentais

- **Objetivo:** Compreender o papel revolucionário do CSS na web moderna e o princípio da separação entre conteúdo e apresentação, dominar as três formas de incluir estilos (com foco no CSS externo), aprender a anatomia de uma regra CSS (seletores, propriedades e valores), dominar os seletores essenciais (tipo, agrupamento, classe, identificador e descendentes), e inspecionar estilos com as ferramentas de programador do navegador (DevTools). No fim da aula, o portefólio pessoal ganha uma folha de estilos externa (`css/style.css`) limpa, elegante e partilhada por todas as páginas.

> **Como estudar com este guia:** este guia tem os mesmos passos que fizemos na aula, pela mesma ordem. Sigam as Partes e os Passos **por ordem**, no vosso computador, e escrevam o código e os comandos **à mão** (não copiem e colem). No fim de cada etapa há uma caixa **Confirmem antes de avançar**: só passem à frente quando o vosso resultado for igual ao que lá está. Se algo não funcionar, vejam a secção **Se Algo Correr Mal**, no fim do guia.

> **Mac:** sempre que aparecer a tecla **Ctrl**, usem a tecla **Cmd**.

> **Ponto de partida:** a pasta `portefolio` com as três páginas da aula 7 (`index.html`, `projetos.html`, `contactos.html`), equipadas com metadados SEO, meta viewport, ícone favicon SVG e formulário com validação nativa HTML5 (se faltaram, copiem a pasta [`projeto/sessao-07/`](../../projeto/sessao-07/)). O projeto já deve estar no vosso repositório no GitHub.

---

### Parte 1: O Que É o CSS e a Separação entre Conteúdo e Apresentação

Até à aula anterior, todas as páginas que construímos pareciam documentos de texto simples dos anos 90: texto preto sobre fundo branco, com links azuis sublinhados e fontes serifadas antiquadas. Isso acontece porque o HTML serve apenas para **dar significado e estrutura aos dados**, não para definir a sua aparência visual.

Hoje vamos entrar no universo do **CSS** (*Cascading Style Sheets*, ou Folhas de Estilo em Cascata), a tecnologia responsável por dar cor, forma, tipografia, espaçamento e vida aos documentos web.

#### Passo 1: A Metáfora da Construção

Para nunca mais esquecerem a diferença entre HTML e CSS, pensem na construção de uma casa:
- **HTML é a alvenaria e a estrutura:** os tijolos, os pilares de betão, as vigas, as canalizações e as portas. Define onde fica a sala, a cozinha ou o quarto. Sem uma boa estrutura, a casa rui.
- **CSS é o acabamento e a decoração:** a tinta nas paredes, a cor dos azulejos, a iluminação suave, os cortinados, a textura do chão e a disposição dos móveis. É o que transforma uma carcaça cinzenta num espaço agradável e acolhedor.

Nos primórdios da internet, nos anos 90, os programadores tentavam alterar cores misturando tags como `<font color="red">` ou atributos como `<body bgcolor="black">` diretamente dentro do HTML. O resultado era caótico: páginas gigantescas, código ilegível e uma manutenção infernal — para mudar uma cor em dez páginas era preciso editar centenas de linhas manualmente.

O CSS foi criado precisamente para resolver isso, introduzindo uma regra de ouro do desenvolvimento profissional: **separação absoluta de responsabilidades**. O HTML cuida do significado; o CSS cuida da estética.

#### Passo 2: A Anatomia de uma Regra CSS

Uma folha de estilos CSS é composta por uma sequência de **regras**. Cada regra diz ao navegador: *"Encontra estes elementos no documento e aplica-lhes estas características visuais"*.

Uma regra CSS divide-se sempre nas seguintes partes:

```css
seletor {
  propriedade: valor;
}
```

Vamos analisar cada componente:
- **Seletor:** Indica ao navegador quais os elementos HTML que vão receber o estilo (por exemplo, `h1`, `p`, ou `.destaque`).
- **Bloco de declarações:** Delimitado por chavetas `{ }`. Tudo o que estiver dentro destas chavetas aplica-se exclusivamente aos elementos capturados pelo seletor.
- **Propriedade:** O aspeto visual específico que queremos alterar (por exemplo, `color`, `font-size`, `background-color`).
- **Dois pontos (`:`):** Separa obrigatoriamente a propriedade do seu valor.
- **Valor:** A definição concreta que atribuímos à propriedade (por exemplo, `blue`, `16px`, `#ffffff`).
- **Ponto e vírgula (`;`):** Finaliza obrigatoriamente cada declaração. É o erro mais frequente de quem começa: se esquecerem um ponto e vírgula, o navegador não consegue interpretar a instrução seguinte e descarta-a silenciosamente!

Vejamos um exemplo real:

```css
h1 {
  color: #0284c7;
  font-size: 2rem;
}
```

Esta regra diz ao navegador: *"Procura todos os títulos `<h1>` da página e coloca o texto com a cor azul celeste `#0284c7` e o tamanho de letra `2rem`"*.

#### Passo 3: Comentários em CSS

Assim como no HTML usamos `<!-- comentário -->`, no CSS usamos uma sintaxe própria para deixar notas explicativas que o navegador ignora totalmente:

```css
/* Isto é um comentário em CSS */
/* Serve para organizar secções da folha de estilos */
```

> **Atenção:** Em CSS não funcionam os comentários de barra dupla `//` como no JavaScript, nem os comentários de HTML `<!-- -->`. Usem sempre a barra com asterisco `/* ... */`.

> **Confirmem antes de avançar:**
>
> - Compreendem a separação de responsabilidades entre HTML (conteúdo/semântica) e CSS (apresentação visual).
> - Conseguem identificar num bloco CSS o seletor, o bloco de chavetas, as propriedades, os valores e os pontos e vírgula.
> - Sabem como se escreve um comentário em CSS.

---

### Parte 2: Onde Colocar o CSS? As Três Formas de Inclusão

O navegador pode ler instruções de CSS de três formas distintas. Vamos conhecê-las para perceber qual delas devemos usar.

#### Passo 1: CSS Inline (No Próprio Elemento)

Podemos aplicar regras diretamente num elemento HTML através do atributo `style=""`:

```html
<p style="color: red; font-size: 18px;">
  Este parágrafo tem estilos diretamente na tag.
</p>
```

- **Vantagem:** Efeito imediato, útil para testes relâmpago de poucos segundos.
- **Desvantagem fatal:** Viola o princípio da separação de responsabilidades. Se tivermos 50 parágrafos, temos de colar o estilo 50 vezes. Mistura código de apresentação com marcação semântica e torna qualquer alteração futura um pesadelo. **É considerada uma má prática na indústria e não deve ser utilizada em projetos normais.**

#### Passo 2: CSS Interno (No `<head>` com a Tag `<style>`)

Podemos escrever regras CSS dentro do próprio ficheiro HTML, agrupadas num bloco `<style>` inserido no elemento `<head>`:

```html
<head>
  <style>
    p {
      color: #334155;
      line-height: 1.6;
    }
  </style>
</head>
```

- **Vantagem:** Concentra as regras no topo do documento sem poluir o corpo (`<body>`).
- **Desvantagem:** Os estilos só funcionam dentro daquele ficheiro HTML específico. Se o nosso site tiver três páginas (`index.html`, `projetos.html`, `contactos.html`), teríamos de copiar e colar o bloco `<style>` nas três. Se quiséssemos mudar a cor de fundo do site, tínhamos de editar três ficheiros separados.

#### Passo 3: CSS Externo (Ficheiro `.css` Separado com `<link>`) — A Boa Prática da Indústria

A forma profissional, elegante e escalável de estilizar um site é criar um ficheiro de texto dedicado com a extensão `.css` e ligá-lo a todas as páginas HTML através do elemento `<link rel="stylesheet">`.

As vantagens são avassaladoras:
- **Reutilização absoluta:** Uma única folha de estilos pode controlar a aparência de centenas de páginas em simultâneo.
- **Manutenção centralizada:** Para mudar a cor principal ou o tipo de letra de todo o site, editamos apenas uma linha num único ficheiro.
- **Velocidade de carregamento:** O navegador descarrega o ficheiro CSS uma única vez e guarda-o em cache, tornando a navegação entre as páginas do site quase instantânea.

#### Passo 4: Criar a Pasta `css` e o Ficheiro `style.css`

Vamos colocar em prática no nosso portefólio:

1. Abram a pasta `portefolio` no VS Code.
2. Na raiz da pasta, criem uma nova pasta chamada `css`.
3. Dentro da pasta `css/`, criem um novo ficheiro chamado `style.css`.
4. Abram o ficheiro `css/style.css` e escrevam o seguinte cabeçalho com comentários:

```css
/* ==========================================================================
   Portefólio Pessoal — Ana Martins
   Folha de Estilos Principal
   ========================================================================== */
```

Guardem o ficheiro.

#### Passo 5: Ligar a Folha de Estilos no `<head>` das Três Páginas

Agora vamos avisar as três páginas HTML de que devem carregar esta folha de estilos externa.

No ficheiro `index.html`, dentro do elemento `<head>`, adicionem o elemento `<link>` logo a seguir ao favicon:

```html
<link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
<link rel="stylesheet" href="css/style.css" />
```

Vamos analisar os atributos desta tag:
- **`<link>`:** Elemento vazio (sem tag de fecho) que cria uma relação entre o documento atual e um recurso externo.
- **`rel="stylesheet"`:** Indica ao navegador a natureza da ligação — neste caso, uma folha de estilos (*style sheet*).
- **`href="css/style.css"`:** O caminho relativo até ao ficheiro CSS a partir da localização do documento HTML.

Repitam este mesmo passo no `<head>` de `projetos.html` e de `contactos.html`.

> **Dica:** No VS Code, se escreverem `link:css` e carregarem na tecla **Tab**, o editor gera automaticamente a tag `<link rel="stylesheet" href="style.css">`. Basta apenas ajustar o caminho para `css/style.css`.

> **Confirmem antes de avançar:**
>
> - A pasta `portefolio/css/` existe e contém o ficheiro `style.css`.
> - Os ficheiros `index.html`, `projetos.html` e `contactos.html` possuem a tag `<link rel="stylesheet" href="css/style.css" />` dentro do `<head>`.
> - Ao abrirem o `index.html` com o Live Server no navegador, não surgem erros de ficheiro em falta na consola.

---

### Parte 3: Seletores Fundamentais — Tipo, Agrupamento e Herança

Agora que a nossa folha de estilos está ligada às páginas, vamos começar a escrever as nossas primeiras regras reais de CSS.

#### Passo 1: O Seletor de Tipo (Elemento)

O seletor de tipo é a forma mais direta de estilizar: seleciona todos os elementos HTML de determinada tag.

Abram o ficheiro `css/style.css` e adicionem a nossa primeira regra global no elemento `body`:

```css
/* --------------------------------------------------------------------------
   1. Estilos Globais e Tipografia
   -------------------------------------------------------------------------- */

body {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  line-height: 1.6;
  color: #334155;
  background-color: #f8fafc;
  margin: 0;
  padding: 24px 16px;
}
```

O que acabámos de definir nesta regra?
- **`font-family`:** Define uma lista de fontes de substituição (*font stack*). O navegador tenta usar `system-ui` (a fonte moderna do sistema operativo: San Francisco no Mac, Segoe UI no Windows, Roboto no Android). Se não estiver disponível, recua para uma fonte sem serifa genérica (`sans-serif`).
- **`line-height: 1.6`:** Define o espaçamento entre linhas (altura de linha). O valor padrão do navegador é demasiado apertado (cerca de 1.15 ou 1.2). Um valor de 1.5 a 1.6 torna a leitura incrivelmente confortável para a vista.
- **`color: #334155`:** A cor do texto. Em design web raramente usamos preto puro (`#000000`), pois causa um contraste demasiado agressivo sobre o fundo branco. Um cinzento ardósia escuro como `#334155` é muito mais suave e profissional.
- **`background-color: #f8fafc`:** Uma cor de fundo suave e moderna, ligeiramente acinzentada em vez do branco ofuscante.
- **`padding: 24px 16px`:** Um espaçamento interno para afastar o conteúdo das margens da janela do navegador.

**Resultado esperado:**
Guardem o ficheiro `style.css` e olhem para o navegador: num piscar de olhos, todo o texto do site mudou para uma tipografia moderna e elegante, o fundo ficou suave e o espaçamento ficou limpo!

#### Passo 2: O Poder da Herança

Reparem num pormenor fascinante: nós não escrevemos nenhuma regra para os parágrafos `<p>`, para as listas `<ul>`, nem para os títulos `<h2>`. Então porque é que eles estão a usar a nova fonte e a cor cinzenta?

Isto acontece graças a um conceito fundamental do CSS chamado **Herança**:
- Certas propriedades CSS (especialmente as ligadas ao texto e tipografia, como `color`, `font-family`, `font-size` e `line-height`) são automaticamente herdadas pelos elementos filhos a partir dos seus elementos pais.
- Como o elemento `<body>` é o pai de todo o conteúdo visível da página, qualquer estilo tipográfico aplicado ao `body` transmite-se em cascata para todos os parágrafos, listas e secções interiores.

> **Dica:** Nem todas as propriedades são herdadas! Por exemplo, bordas (`border`), margens (`margin`), preenchimento (`padding`) e cores de fundo (`background-color`) não são herdadas pelos filhos, o que faz todo o sentido: se colocássemos uma borda no `body`, não quereríamos que cada palavra ou parágrafo dentro dele ficasse também envolvido numa caixa com borda!

#### Passo 3: Agrupamento de Seletores com Vírgula

Muitas vezes queremos aplicar o mesmo conjunto de regras a vários elementos diferentes. Em vez de escrevermos código repetido:

```css
/* Mau: código repetido */
h1 {
  color: #0f172a;
  line-height: 1.25;
}
h2 {
  color: #0f172a;
  line-height: 1.25;
}
h3 {
  color: #0f172a;
  line-height: 1.25;
}
```

Podemos **agrupar os seletores separando-os por vírgula**:

```css
/* Bom: agrupamento limpo e sustentável */
h1,
h2,
h3 {
  color: #0f172a;
  line-height: 1.25;
}
```

A vírgula significa literalmente "E". A regra aplica-se a `h1` E `h2` E `h3`.

Abaixo do agrupamento, podemos especificar as particularidades de tamanho e margens de cada título:

```css
h1 {
  font-size: 2rem;
  margin-top: 12px;
  margin-bottom: 8px;
}

h2 {
  font-size: 1.4rem;
  margin-top: 28px;
  margin-bottom: 12px;
  border-bottom: 2px solid #e2e8f0;
  padding-bottom: 6px;
}

h3 {
  font-size: 1.15rem;
  margin-top: 20px;
  margin-bottom: 8px;
}
```

Reparem como adicionámos uma linha subtil de separação sob todos os títulos `<h2>` com `border-bottom: 2px solid #e2e8f0;`. Isso cria uma hierarquia visual imediata entre secções!

#### Passo 4: Estilizar Parágrafos, Imagens, Cabeçalho e Rodapé

Acrescentem as seguintes regras em `css/style.css`:

```css
p {
  margin-top: 0;
  margin-bottom: 16px;
}

a {
  color: #0284c7;
  text-decoration: underline;
}

img {
  max-width: 100%;
  height: auto;
}

header {
  text-align: center;
  margin-bottom: 32px;
}

footer {
  text-align: center;
  margin-top: 48px;
  padding-top: 16px;
  border-top: 1px solid #cbd5e1;
  color: #64748b;
  font-size: 0.9rem;
}
```

- **`text-align: center`** no `header` e no `footer`: centra a fotografia, o título principal da Ana e a mensagem de copyright.
- **`img { max-width: 100%; height: auto; }`**: uma regra de ouro para garantir que nenhuma imagem ultrapassa a largura do ecrã.

#### Passo 5: Estilizar Tabelas com Seletores de Tipo

Vamos dar um acabamento profissional às tabelas de percurso e de disponibilidade:

```css
/* Tabelas */
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 16px;
  margin-bottom: 24px;
}

th,
td {
  border: 1px solid #cbd5e1;
  padding: 10px 12px;
  text-align: left;
}

th {
  background-color: #f1f5f9;
  color: #0f172a;
}
```

- **`border-collapse: collapse`:** Junta as bordas duplas padrão das tabelas numa única linha fina e nítida.
- **`padding: 10px 12px`:** Dá espaço para o texto respirar dentro de cada célula.

> **Confirmem antes de avançar:**
>
> - Ao guardarem `css/style.css`, tanto `index.html` como `projetos.html` e `contactos.html` mostram a mesma tipografia e cores no navegador.
> - Os títulos `<h2>` têm uma linha cinzenta suave por baixo.
> - As tabelas têm linhas limpas e cabeçalhos com fundo cinzento claro.
> - O cabeçalho e o rodapé estão centrados horizontalmente.

---

### Parte 4: Seletores de Classe e Reutilização

Os seletores de tipo afetam **todos** os elementos daquela tag na página inteira. Mas e se quisermos que um parágrafo específico tenha um destaque especial, ou que um determinado artigo se pareça com um cartão elevado?

É aqui que entram as **Classes**.

#### Passo 1: O Que É uma Classe?

Uma classe é um rótulo que atribuímos a um ou mais elementos no HTML através do atributo `class="..."`.

- No **HTML**, escrevemos o atributo `class="nome-da-classe"` (sem ponto).
- No **CSS**, referenciamos essa classe com um ponto no início: `.nome-da-classe`.

A grande virtude das classes é a sua **reutilização**: podemos aplicar a mesma classe a 5, 20 ou 100 elementos diferentes, em várias páginas, garantindo que todos partilham exatamente a mesma identidade visual.

#### Passo 2: Criar a Classe `.cartao`

Vamos criar um estilo de cartão para envolver os nossos testemunhos e projetos:

No ficheiro `css/style.css`, adicionem:

```css
/* --------------------------------------------------------------------------
   3. Seletores de Classe (Componentes Reutilizáveis)
   -------------------------------------------------------------------------- */

/* Cartões destacados (projetos e testemunhos) */
.cartao {
  background-color: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 16px 20px;
  margin-bottom: 20px;
}
```

- **`background-color: #ffffff`:** Fundo branco puro, que se destaca suavemente do fundo `#f8fafc` do corpo da página.
- **`border: 1px solid #e2e8f0`:** Uma moldura subtil.
- **`border-radius: 8px`:** Cantos suavemente arredondados, dando um ar moderno e polido.
- **`padding: 16px 20px`:** Espaçamento interior para o texto não colar às bordas.

Agora abram `index.html` e adicionem a classe ao `<article>` do testemunho:

```html
<section>
  <!-- Testemunhos -->
  <h2>O que dizem de mim</h2>
  <article class="cartao">
    <blockquote>
      <p>A Ana resolve qualquer problema com calma e com um sorriso.</p>
    </blockquote>
    <p>— Carla Sousa, gerente da loja onde a Ana trabalhou</p>
  </article>
</section>
```

Vejam no navegador: o testemunho aparece agora dentro de um cartão elegante!

Em `projetos.html`, podemos aplicar a mesma classe `.cartao` a cada um dos projetos da lista, transformando simples itens de texto em cartões estruturados de portefólio!

#### Passo 3: Criar a Classe `.curiosidade`

Lembram-se da caixa `<aside>` onde colocámos a curiosidade sobre Tim Berners-Lee e o CERN? Vamos dar-lhe um destaque acolhedor com uma borda lateral colorida:

No ficheiro `css/style.css`:

```css
/* Caixas de curiosidade e notas informativas */
.curiosidade {
  background-color: #f0fdf4;
  border-left: 4px solid #16a34a;
  padding: 12px 16px;
  margin: 20px 0;
}
```

- **`background-color: #f0fdf4`:** Fundo verde muito suave.
- **`border-left: 4px solid #16a34a`:** Uma barra verde viva na lateral esquerda, que guia imediatamente o olhar do leitor.

No ficheiro `index.html`, atualizem a tag `<aside>`:

```html
<aside class="curiosidade">
  <p>
    <strong>Sabiam que…</strong> o primeiro site da história foi publicado em
    1991, no CERN, por Tim Berners-Lee.
  </p>
</aside>
```

#### Passo 4: Criar a Classe `.botao`

Os botões de formulário padrão do navegador parecem relíquias do Windows 95. Vamos criar uma classe utilitária `.botao` que pode ser aplicada tanto a elementos `<button>` como a links `<a>`:

No ficheiro `css/style.css`:

```css
/* Botões de ação */
.botao {
  display: inline-block;
  background-color: #0284c7;
  color: #ffffff;
  padding: 8px 16px;
  border: 1px solid #0284c7;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 600;
  cursor: pointer;
}

.botao-secundario {
  background-color: #64748b;
  border-color: #64748b;
  color: #ffffff;
}

.destaque {
  font-weight: 600;
  color: #0369a1;
}
```

No ficheiro `contactos.html`, apliquem estas classes aos botões do formulário:

```html
<p>
  <button type="submit" class="botao">Enviar mensagem</button>
  <button type="reset" class="botao botao-secundario">
    Limpar formulário
  </button>
</p>
```

E no `index.html`, na secção de contacto rápido, transformem a ligação à página de contactos num botão convidativo:

```html
<p>
  Enviem-me um e-mail para
  <a href="mailto:ana.martins@exemplo.pt" class="destaque"
    >ana.martins@exemplo.pt</a
  >
  ou enviem uma mensagem através da
  <a href="contactos.html#formulario-contacto" class="botao"
    >Página de Contactos</a
  >.
</p>
```

> **Atenção:** Reparem na regra `.botao botao-secundario`: um elemento HTML pode ter **várias classes em simultâneo**, bastando separá-las por espaço no atributo `class="botao botao-secundario"`. O botão de limpar herda a forma do `.botao` e substitui apenas a cor com a do `.botao-secundario`.

> **Confirmem antes de avançar:**
>
> - O testemunho em `index.html` e os projetos em `projetos.html` estão inseridos em cartões brancos com cantos arredondados (`.cartao`).
> - A nota informativa tem fundo verde claro e barra lateral verde (`.curiosidade`).
> - Os botões de submissão do formulário exibem fundo azul moderno e o botão de limpar exibe fundo cinzento.

---

### Parte 5: Seletores de Identificador (ID) e Seletores Descendentes

Já dominamos tipos e classes. Vamos agora aprender os dois seletores que nos dão precisão cirúrgica no código.

#### Passo 1: O Seletor de Identificador (`#id`)

O identificador corresponde ao atributo `id="..."` do HTML.

- No **HTML**, escrevemos `id="nome-do-id"`.
- No **CSS**, referenciamos esse identificador com o cardinal `#`: `#nome-do-id`.

Ao contrário das classes, que podem e devem ser repetidas em múltiplos elementos, **um ID tem de ser rigorosamente único na página inteira**.

Quando devemos usar um seletor de ID no CSS? Apenas quando queremos estilizar uma secção ou bloco verdadeiramente único da página, como o bloco do formulário de contacto:

No ficheiro `css/style.css`:

```css
/* --------------------------------------------------------------------------
   4. Seletores de Identificador (Elementos Únicos)
   -------------------------------------------------------------------------- */

#formulario-contacto {
  background-color: #ffffff;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  padding: 24px;
  margin-top: 24px;
}
```

No ficheiro `contactos.html`, a secção já possui `<section id="formulario-contacto">`. Ao guardarem o CSS, o formulário inteiro fica emoldurado num bloco elegante e limpo!

#### Passo 2: Seletores Descendentes (Contexto)

E se quisermos estilizar os links que estão dentro do menu de navegação, sem alterar os outros links do meio dos textos?

Não precisamos de encher cada link do menu de classes! Usamos um **Seletor Descendente**, separando os elementos por um **espaço**:

```css
nav a {
  text-decoration: none;
  color: #0284c7;
  font-weight: 600;
  padding: 6px 12px;
}
```

O que significa `nav a` com espaço?
- Significa: *"Procura qualquer elemento `<a>` que esteja **dentro** de um elemento `<nav>`"*.
- Todos os outros links fora da barra de navegação continuam normais, com o sublinhado habitual.

Vamos também transformar a lista do menu numa barra de navegação horizontal moderna:

```css
/* --------------------------------------------------------------------------
   2. Seletores Descendentes (Contexto)
   -------------------------------------------------------------------------- */

/* Menu de navegação */
nav ul {
  list-style: none;
  padding: 0;
  margin: 16px 0 0 0;
}

nav li {
  display: inline-block;
  margin: 0 8px;
}

nav a {
  text-decoration: none;
  color: #0284c7;
  font-weight: 600;
  padding: 6px 12px;
}
```

- **`nav ul { list-style: none; }`**: Remove os pontos pretos circulares da lista não ordenada.
- **`nav li { display: inline-block; }`**: Faz com que cada item da lista se posicione lado a lado na mesma linha horizontal, em vez de empilhado verticalmente.

Vejam também a citação dentro dos artigos:

```css
article blockquote {
  margin: 0 0 8px 0;
  font-style: italic;
  color: #334155;
}
```

> **Atenção — A diferença crucial entre vírgula e espaço:**
> - `nav, a` (com vírgula) seleciona o elemento `<nav>` **E** todos os elementos `<a>` da página inteira.
> - `nav a` (com espaço) seleciona apenas os elementos `<a>` que sejam **filhos ou descendentes** do `<nav>`.

> **Confirmem antes de avançar:**
>
> - O menu de navegação no topo de todas as páginas apresenta os links dispostos horizontalmente, sem marcas de lista e sem sublinhados azuis primitivos.
> - O formulário de contactos na página `contactos.html` está enquadrado num bloco branco delimitado com borda e espaçamento interior (`#formulario-contacto`).
> - Os links normais do corpo do texto (como o link de e-mail) mantêm a sua formatação adequada.

---

### Parte 6: Inspecionar e Depurar CSS nas DevTools

Como programadores web, passamos metade do nosso tempo no editor de código e a outra metade nas **Ferramentas de Programador** (*DevTools*) do navegador. As DevTools permitem ver exatamente o que o navegador está a pensar quando desenha a página.

#### Passo 1: Abrir o Painel "Elements" e a Aba "Styles"

1. Abram `index.html` no navegador através do Live Server.
2. Cliquem com o botão direito do rato em cima do título principal "Ana Martins" e escolham **Inspecionar** (ou carreguem em **F12** ou **Ctrl + Shift + I** / **Cmd + Option + I** no Mac).
3. Na janela das DevTools:
   - No lado esquerdo ou superior vêem a árvore HTML (o DOM).
   - No lado direito ou inferior encontram o separador **Styles** (Estilos).

#### Passo 2: O Que Vemos no Separador "Styles"?

Ao selecionarem o `<h1>`:
- O painel mostra todas as regras CSS que afetam aquele elemento, ordenadas por ordem de prioridade.
- À direita de cada regra, o navegador indica o ficheiro e a linha exata de onde ela vem (por exemplo, `style.css:25`). Se clicarem nessa ligação, o navegador mostra a linha de código diretamente!
- Se uma propriedade aparecer com uma linha horizontal a riscá-la (rasurada), significa que foi **sobreposta** por outra regra de maior prioridade na cascata.

#### Passo 3: Experimentar Alterações em Tempo Real

Podem editar qualquer valor diretamente no navegador:
1. No painel Styles, encontrem a regra `body` e desmarquem a caixa ao lado de `background-color`. O fundo volta imediatamente ao branco padrão!
2. Marquem novamente a caixa para reativar.
3. Cliquem na caixa de cor de `#0284c7` na regra do link: abre-se um seletor visual de cores (*color picker*). Podem escolher qualquer tom e ver o site mudar instantaneamente no ecrã.

> **Dica:** As alterações feitas nas DevTools são temporárias: servem para testar e experimentar. Assim que recarregarem a página (**F5**), o site volta a ler o ficheiro `css/style.css`. Quando encontrarem o valor de cor ou espaçamento perfeito nas DevTools, copiem-no para o vosso ficheiro no VS Code e guardem.

> **Confirmem antes de avançar:**
>
> - Conseguem abrir o painel Styles nas DevTools e inspecionar os estilos aplicados ao `body`, ao `h1` e aos links de navegação.
> - Compreendem como as DevTools indicam o ficheiro e o número da linha de cada regra.

---

### Parte 7: Guardar a Evolução no Git e GitHub

Com a nossa primeira folha de estilos profissional ligada a todas as páginas e o HTML limpo com classes e identificadores, vamos registar o nosso progresso no Git.

1. Abram o terminal do VS Code (**Ctrl + `** ou **Cmd + `**).
2. Escrevam `git status`: verão a nova pasta `css/style.css` e os ficheiros HTML modificados.
3. Adicionem tudo à área de preparação:

```bash
git add .
```

4. Criem o commit com uma mensagem descritiva em português:

```bash
git commit -m "Adiciona folha de estilos externa css/style.css com seletores de tipo classe e id"
```

5. Enviem para o repositório remoto no GitHub:

```bash
git push
```

6. Abram o vosso repositório no GitHub no navegador e confirmem que a pasta `css/` e as alterações aos ficheiros HTML estão guardadas na nuvem.

> **Confirmem antes de avançar:**
>
> - O comando `git status` reporta a árvore de trabalho limpa (*working tree clean*).
> - O vosso repositório no GitHub exibe o commit com a pasta `css/`.

---

**O projeto no fim da aula:**

A estrutura de pastas da vossa pasta `portefolio/` deve ficar rigorosamente assim:

```
portefolio/
├── css/
│   └── style.css
├── imagens/
│   ├── foto.svg
│   └── favicon.svg
├── index.html
├── projetos.html
└── contactos.html
```

#### Código Completo de `css/style.css`:

```css
/* ==========================================================================
   Portefólio Pessoal — Ana Martins
   Folha de Estilos Principal (CSS I: Sintaxe e Seletores)
   ========================================================================== */

/* --------------------------------------------------------------------------
   1. Seletores de Tipo (Estilos Globais e Tipografia)
   -------------------------------------------------------------------------- */

body {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  line-height: 1.6;
  color: #334155;
  background-color: #f8fafc;
  margin: 0;
  padding: 24px 16px;
}

/* Agrupamento de títulos */
h1,
h2,
h3 {
  color: #0f172a;
  line-height: 1.25;
}

h1 {
  font-size: 2rem;
  margin-top: 12px;
  margin-bottom: 8px;
}

h2 {
  font-size: 1.4rem;
  margin-top: 28px;
  margin-bottom: 12px;
  border-bottom: 2px solid #e2e8f0;
  padding-bottom: 6px;
}

h3 {
  font-size: 1.15rem;
  margin-top: 20px;
  margin-bottom: 8px;
}

p {
  margin-top: 0;
  margin-bottom: 16px;
}

a {
  color: #0284c7;
  text-decoration: underline;
}

img {
  max-width: 100%;
  height: auto;
}

header {
  text-align: center;
  margin-bottom: 32px;
}

footer {
  text-align: center;
  margin-top: 48px;
  padding-top: 16px;
  border-top: 1px solid #cbd5e1;
  color: #64748b;
  font-size: 0.9rem;
}

/* Tabelas */
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 16px;
  margin-bottom: 24px;
}

th,
td {
  border: 1px solid #cbd5e1;
  padding: 10px 12px;
  text-align: left;
}

th {
  background-color: #f1f5f9;
  color: #0f172a;
}

/* Formulários */
label {
  display: block;
  font-weight: 600;
  margin-top: 12px;
  margin-bottom: 4px;
}

input,
select,
textarea {
  font-family: inherit;
  font-size: 1rem;
}

/* --------------------------------------------------------------------------
   2. Seletores Descendentes (Contexto)
   -------------------------------------------------------------------------- */

/* Menu de navegação */
nav ul {
  list-style: none;
  padding: 0;
  margin: 16px 0 0 0;
}

nav li {
  display: inline-block;
  margin: 0 8px;
}

nav a {
  text-decoration: none;
  color: #0284c7;
  font-weight: 600;
  padding: 6px 12px;
}

/* Citações em artigos */
article blockquote {
  margin: 0 0 8px 0;
  font-style: italic;
  color: #334155;
}

/* --------------------------------------------------------------------------
   3. Seletores de Classe (Componentes Reutilizáveis)
   -------------------------------------------------------------------------- */

/* Cartões destacados (projetos e testemunhos) */
.cartao {
  background-color: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 16px 20px;
  margin-bottom: 20px;
}

/* Caixas de curiosidade e notas informativas */
.curiosidade {
  background-color: #f0fdf4;
  border-left: 4px solid #16a34a;
  padding: 12px 16px;
  margin: 20px 0;
}

/* Texto destacado */
.destaque {
  font-weight: 600;
  color: #0369a1;
}

/* Botões de ação */
.botao {
  display: inline-block;
  background-color: #0284c7;
  color: #ffffff;
  padding: 8px 16px;
  border: 1px solid #0284c7;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 600;
  cursor: pointer;
}

.botao-secundario {
  background-color: #64748b;
  border-color: #64748b;
  color: #ffffff;
}

/* --------------------------------------------------------------------------
   4. Seletores de Identificador (Elementos Únicos)
   -------------------------------------------------------------------------- */

#formulario-contacto {
  background-color: #ffffff;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  padding: 24px;
  margin-top: 24px;
}

#percurso {
  margin-top: 32px;
}
```

---

### Se Algo Correr Mal

1. **O CSS não faz qualquer efeito na página e tudo continua preto e branco.**
   - O caminho no `<link>` está quase certamente errado. Verifiquem se escreveram `href="css/style.css"`. Se escreverem apenas `href="style.css"`, o navegador procura o ficheiro na raiz da pasta e não o encontra. Verifiquem também se guardaram o ficheiro `style.css` no VS Code (bolinha branca no separador).
2. **Uma regra específica não funciona e todas as que estão abaixo dela deixaram de funcionar.**
   - Esqueceram-se de um ponto e vírgula `;` no fim de uma declaração ou esqueceram-se de fechar uma chaveta `}`. Abram o ficheiro CSS e procurem linhas assinaladas a vermelho pelo VS Code.
3. **A classe não faz efeito no HTML.**
   - Confirmem se escreveram com ponto no CSS (`.cartao`) e **sem ponto** no HTML (`class="cartao"`). Se escreverem `class=".cartao"` no HTML, o estilo nunca funcionará.
4. **O menu não fica horizontal.**
   - Certifiquem-se de que aplicaram `display: inline-block;` nos elementos `nav li`, e que o seletor tem o espaço (`nav li`).
5. **O navegador não mostra as minhas alterações mesmo depois de guardar.**
   - O navegador pode ter guardado a folha de estilo em cache. Forcem uma atualização limpa carregando em **Ctrl + F5** (no Windows) ou **Cmd + Shift + R** (no Mac).

---

### O Que Aprendemos Hoje

Antes de passarem ao exercício prático individual, confirmem que compreendem e conseguem explicar:

- [ ] A separação entre o conteúdo/estrutura (HTML) e a apresentação visual (CSS).
- [ ] Porque é que o CSS externo com `<link rel="stylesheet">` é a única forma profissional e sustentável de estilizar um site.
- [ ] A anatomia de uma regra CSS: seletor, chavetas, propriedade, dois pontos, valor e ponto e vírgula.
- [ ] Como funciona o conceito de herança tipográfica a partir do elemento `body`.
- [ ] Como agrupar seletores com vírgula (`h1, h2, h3`) para partilhar regras sem duplicação de código.
- [ ] A diferença prática entre um seletor de tipo (`p`), um seletor de classe (`.cartao`), um seletor de ID (`#formulario-contacto`) e um seletor descendente (`nav a`).
- [ ] A regra de unicidade do identificador (`id`): apenas um elemento com determinado ID por página.
- [ ] Como usar o separador "Styles" nas DevTools para testar cores, inspecionar regras e detetar erros em tempo real.

---

### Palavras Novas

- **CSS (*Cascading Style Sheets*):** Linguagem de folhas de estilo usada para descrever a apresentação, layout e estilo de documentos HTML.
- **Regra CSS:** Bloco completo composto por um seletor e uma lista de declarações envolta em chavetas.
- **Seletor:** Expressão que define a quais elementos da página as regras CSS serão aplicadas.
- **Propriedade:** Característica visual ou de layout que pretendemos alterar (ex.: `color`, `background-color`, `font-size`).
- **Valor:** Configuração específica atribuída a uma propriedade (ex.: `#0284c7`, `1.6`, `none`).
- **Seletor de Tipo:** Seletor que tem como alvo todas as ocorrências de uma tag HTML específica (ex.: `body`, `p`, `table`).
- **Seletor de Classe:** Seletor iniciado por um ponto (`.`) que tem como alvo qualquer elemento HTML que possua o atributo `class` correspondente.
- **Seletor de Identificador (ID):** Seletor iniciado por um cardinal (`#`) que tem como alvo o único elemento HTML com o atributo `id` correspondente.
- **Seletor Descendente:** Seletor composto por dois ou mais elementos separados por espaço (ex.: `nav a`), que seleciona apenas os elementos que estão inseridos dentro do contentor especificado.
- **Herança:** Mecanismo pelo qual certas propriedades de estilo aplicadas a um elemento pai são automaticamente transferidas para os seus descendentes.
- **DevTools (Painel Styles):** Ferramentas de desenvolvimento integradas no navegador que permitem inspecionar e alterar as regras CSS aplicadas a cada elemento em tempo real.

---

### Para Saber Mais

Os recursos abaixo encontram-se em inglês. Usem a tradução automática do navegador (botão direito → **Traduzir para português**) se necessário.

- [Introdução ao CSS e Primeiros Passos (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps)
- [Como o CSS é estruturado: Seletores e Sintaxe (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)
- [Guia completo de Seletores CSS (web.dev)](https://web.dev/learn/css/selectors)
- [Inspecionar e depurar estilos CSS com o Chrome DevTools](https://developer.chrome.com/docs/devtools/css/)

---

# Exercício Final: Faróis de Portugal

Agora é a vossa vez de praticar sozinhos. O enunciado completo encontra-se também na ficha [`ex-008.md`](../../exercicios/ex-008.md) e os ficheiros de apoio estão na pasta [`exercicios/ex-008/`](../../exercicios/ex-008/).

### Missão 1: A Minha Cidade com Estilo

1. Criem a pasta `sessao-08` dentro de `exercicios-uf1.1` e copiem para lá todo o conteúdo da pasta `sessao-07`.
2. Criem uma pasta `css` e o ficheiro `css/estilo.css`.
3. Liguem `cidade.html` e `passadicos-paiva.html` a `css/estilo.css` através de `<link rel="stylesheet" href="css/estilo.css" />`.
4. Definam no ficheiro CSS regras completas com:
   - Seletores de tipo (`body`, `h1, h2, h3`, `p`, `table`, `th`, `td`).
   - Seletores descendentes para o menu (`nav ul`, `nav li`, `nav a`).
   - Seletores de classe para cartões (`.cartao`), caixas de nota (`.curiosidade` ou `.aviso`) e botões (`.botao`, `.botao-secundario`).
   - Seletor de identificador para os formulários (`#formulario-sugestoes`, `#formulario-reserva`).
5. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Adiciona folha de estilos CSS externa a cidade e passadicos"`, `git push`.

### Missão 2: A Página dos Faróis de Portugal

1. Copiem os ficheiros [`farois-portugal.txt`](../../exercicios/ex-008/farois-portugal.txt) e [`farol.svg`](../../exercicios/ex-008/farol.svg) para a vossa pasta `sessao-08`.
2. Criem o ficheiro `farois-portugal.html` com estrutura semântica completa:
   - `<head>` com metadados SEO, meta viewport, favicon e ligação a `css/farois.css`.
   - `<header>` com imagem do farol, título principal e menu com âncoras para as secções da página.
   - `<main>` dividido em 5 secções temáticas: destaques com 3 artigos (`.cartao`), normas de segurança com caixa de aviso (`.aviso`), tabela comparativa estilizada, formulário validado de agendamento de visita à lanterna, e contactos institucionais.
   - `<footer>` com os direitos de autor da Direção de Faróis.
3. Criem o ficheiro `css/farois.css` com paleta de inspiração marítima (azul-escuro, branco e realces náuticos).
4. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Cria pagina dos Farois de Portugal com estilos CSS dedicados"`, `git push`.

**Critérios de sucesso:**

- [ ] A pasta `sessao-08` contém a pasta `css/` com `estilo.css` e `farois.css`.
- [ ] Todas as páginas carregam a respetiva folha de estilos externa via `<link rel="stylesheet">`.
- [ ] O menu de navegação em todas as páginas tem os links dispostos horizontalmente sem marcas de lista.
- [ ] Os artigos dos faróis e testemunhos estão estruturados com o formato de cartão (`.cartao`).
- [ ] Os formulários e botões possuem acabamento visual atraente e profissional.
- [ ] O validador do W3C confirma que o HTML está limpo e sem erros.
- [ ] O repositório no GitHub reflete todos os novos ficheiros e mensagens de commit.

### Missão 3: O Relatório

Respondam às seguintes questões por palavras vossas:

1. As Três Formas de Inclusão de CSS:
   Quais são as três formas de aplicar CSS a um documento HTML (inline, interno e externo) e por que razão o CSS externo é considerado a melhor prática da indústria?
   Resposta: [Preencher]

2. Seletores de Tipo vs Classe vs ID:
   Expliquem a diferença prática entre um seletor de tipo (`p`), um seletor de classe (`.destaque`) e um seletor de identificador (`#formulario`), dando um exemplo de quando se deve usar cada um.
   Resposta: [Preencher]

3. Seletores Descendentes:
   Qual é a diferença entre a regra `nav, a { ... }` (com vírgula) e a regra `nav a { ... }` (com espaço)?
   Resposta: [Preencher]

4. Depuração com DevTools:
   Como é que o separador "Styles" das Ferramentas de Programador (DevTools) ajuda um programador a identificar problemas quando uma regra de estilo não está a funcionar?
   Resposta: [Preencher]

---

### Desafio Bónus (Para os mais rápidos)

1. Adicionem a pseudo-classe `:hover` aos botões e links da página (`.botao:hover`, `nav a:hover`) para que mudem suavemente de cor quando o utilizador passa o cursor do rato por cima.
2. Adicionem a propriedade `cursor: pointer;` nos botões `<button>` para que o ponteiro do rato se transforme numa mãozinha indicadora de clique.
3. Utilizem a pseudo-classe `:focus` nos campos de texto do formulário (`input:focus`, `select:focus`, `textarea:focus`) com uma borda azul viva (`outline: none; border-color: #0284c7;`) para indicar claramente ao utilizador qual o campo que tem o cursor ativo.

