# Guia Prático - UF 1.1 (Aula 7)

## Validação de Formulários + Metadados: Blindar Dados e Otimizar para a Web

- **Objetivo:** Compreender a importância dos metadados e do SEO técnico (`<meta>`, `<link>`), preparar o site para ecrãs móveis com a meta `viewport`, criar e associar um favicon em SVG, e blindar os formulários com validação nativa de HTML5 (`required`, `minlength`, `maxlength`, `pattern`, `title`) sem escrever uma única linha de JavaScript.

> **Como estudar com este guia:** este guia tem os mesmos passos que fizemos na aula, pela mesma ordem. Sigam as Partes e os Passos **por ordem**, no vosso computador, e escrevam o código e os comandos **à mão** (não copiem e colem). No fim de cada etapa há uma caixa **Confirmem antes de avançar**: só passem à frente quando o vosso resultado for igual ao que lá está. Se algo não funcionar, vejam a secção **Se Algo Correr Mal**, no fim do guia.

> **Mac:** sempre que aparecer a tecla **Ctrl**, usem a tecla **Cmd**.

> **Ponto de partida:** a pasta `portefolio` com as três páginas da aula 6 (`index.html`, `projetos.html`, `contactos.html`) com o formulário de contacto básico já estruturado (se faltaram, copiem a pasta [`projeto/sessao-06/`](../../projeto/sessao-06/)). O projeto já deve estar no GitHub.

---

### Parte 1: Metadados e SEO — A Montra para os Motores de Busca

Até aqui concentrámo-nos no corpo da página (`<body>`), que é o que os humanos vêem quando visitam o nosso site. Agora vamos olhar com olhos de programador para a cabeça do documento (`<head>`).

#### Passo 1: O Que São Metadados?

A palavra **metadados** significa literalmente "dados sobre outros dados". São instruções, informações e descrições técnicas invisíveis aos olhos do visitante comum, mas que são lidas e processadas por:

- **Motores de busca** (Google, Bing, DuckDuckGo) para indexar e catalogar a página.
- **Redes sociais e aplicações de mensagens** (WhatsApp, LinkedIn, Slack) para gerar pré-visualizações quando partilhamos uma ligação.
- **Navegadores web** para saberem como desenhar o ecrã e que ícone colocar no separador.

#### Passo 2: O Que É SEO?

**SEO** (_Search Engine Optimization_ ou Otimização para Motores de Busca) é o conjunto de técnicas e boas práticas que tornam um site facilmente compreensível para os motores de busca, melhorando a probabilidade de aparecer nos primeiros lugares dos resultados orgânicos (gratuitos).

Quando pesquisam algo no Google, cada resultado apresenta três elementos principais:

1. O **Título** da página (retirado da tag `<title>`).
2. O **Endereço web** (URL).
3. O **Excerto / Resumo** do conteúdo (conhecido em inglês como _snippet_).

De onde retira o Google esse resumo descritivo? Da tag `<meta name="description" content="">`!

#### Passo 3: A Tag `<meta name="description">`

A meta description é o vosso "cartão de visita" nos resultados de pesquisa.

```html
<meta
  name="description"
  content="Portefólio pessoal de Ana Martins, futura programadora web em Setúbal. Apresentação, percurso de formação e projetos práticos."
/>
```

Boas práticas para escrever meta descriptions:

- **Tamanho ideal:** Entre 120 e 160 caracteres. Se for mais curta, desperdiçam espaço precioso de comunicação; se for mais comprida, o Google corta o texto com reticências (...).
- **Conteúdo único por página:** Cada página do vosso site deve ter uma descrição diferente, refletindo o seu conteúdo específico.
- **Linguagem humana e apelativa:** Deve funcionar como um convite convincente que leve a pessoa a clicar.

#### Passo 4: Outros Metadados Úteis (`author`)

Também podemos indicar a autoria do projeto com `<meta name="author">`:

```html
<meta name="author" content="Ana Martins" />
```

> **Nota histórica sobre as "keywords":** Nos anos 90 usava-se `<meta name="keywords" content="web, programador, html">`. No entanto, como muitos sites abusavam repetindo palavras centenas de vezes para tentar enganar as pesquisas, os motores de busca modernos (incluindo o Google) ignoram totalmente esta tag há mais de quinze anos. Não percam tempo a colocá-la.

> **Confirmem antes de avançar:**
>
> - Compreendem o conceito de metadados e o papel do `<head>`.
> - Sabem que o texto da `<meta name="description">` é o resumo que surge nos resultados do Google.

---

### Parte 2: A Meta Viewport e a Preparação para Telemóveis

Hoje em dia, mais de metade de todo o tráfego da internet mundial é feito através de telemóveis e tablets. No entanto, os computadores e os telemóveis têm ecrãs com dimensões e densidades de píxeis completamente diferentes.

#### Passo 1: O Problema dos Sites Antigos em Ecrãs Pequenos

Quando os primeiros smartphones surgiram, os sites eram desenhados exclusivamente para monitores de computadores de secretária (com larguras padrão de 980 píxeis ou mais). Para conseguir mostrar esses sites num ecrã de telemóvel de apenas 360 ou 400 píxeis de largura, os navegadores móveis adotaram uma solução de recurso:

- Fingiam que o ecrã do telemóvel tinha 980 píxeis de largura.
- Encolhiam a página inteira num zoom-out minúsculo, obrigando o utilizador a fazer o gesto de pinça (_pinch-to-zoom_) e a arrastar o ecrã para os lados para conseguir ler qualquer palavra.

#### Passo 2: A Tag `<meta name="viewport">`

Para avisar o navegador do telemóvel de que a nossa página foi planeada de forma moderna e não precisa de simular um monitor gigante, usamos uma tag obrigatória em qualquer site atual:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Vamos dissecar o que cada parte significa:

- **`name="viewport"`:** Indica que a instrução se aplica à área visível do navegador (a "janela de visualização").
- **`width=device-width`:** Ordena ao navegador: _"Usa a largura real do ecrã físico deste dispositivo (seja 390px num smartphone, 768px num tablet ou 1920px num monitor), em vez dos 980px fictícios"_.
- **`initial-scale=1.0`:** Define o nível de zoom inicial a 100% (escala real 1:1), sem encolher nem ampliar o texto ao carregar a página.

> **Atenção:** Sem esta tag, nenhuma regra de responsividade que aprendermos nas aulas de CSS funcionará em telemóveis reais! É uma das linhas mais importantes de todo o documento HTML.

#### Passo 3: Adicionar a Viewport e Descrições às Três Páginas

Abram a pasta `portefolio` no VS Code e atualizem o `<head>` de cada um dos três ficheiros.

No ficheiro `index.html`:

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
</head>
```

No ficheiro `projetos.html`:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="Projetos desenvolvidos por Ana Martins: portefólio pessoal, páginas semânticas, dados acessíveis e código versionado no GitHub."
  />
  <meta name="author" content="Ana Martins" />
  <title>Projetos | Ana Martins</title>
</head>
```

No ficheiro `contactos.html`:

```html
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="Entre em contacto com Ana Martins para propostas de estágio, projetos de desenvolvimento web ou esclarecimento de dúvidas."
  />
  <meta name="author" content="Ana Martins" />
  <title>Contactos | Ana Martins</title>
</head>
```

> **Confirmem antes de avançar:**
>
> - As três páginas possuem a tag `<meta name="viewport">` exatamente igual.
> - Cada página tem uma `<meta name="description">` exclusiva e adequada ao seu conteúdo.

---

### Parte 3: O Ícone do Site (Favicon SVG)

Já repararam no pequeno ícone que aparece ao lado do título da página em cada separador do vosso navegador, na lista de favoritos e no histórico de navegação? Esse ícone chama-se **favicon** (_favorite icon_).

#### Passo 1: O Que É um Favicon Moderno?

No passado, os favicons eram obrigatoriamente ficheiros com o formato proprietário `.ico` e com uma resolução muito baixa (16×16 píxeis).

Hoje, todos os navegadores modernos suportam **favicons em formato SVG** (`image/svg+xml`). As vantagens são fantásticas:

- É desenhado com código puro em texto simples.
- Pesa menos de 1 kilobyte.
- Fica perfeitamente nítido em qualquer ecrã, desde telemóveis normais até aos ecrãs Retina mais avançados.

#### Passo 2: Criar o Ficheiro `favicon.svg`

1. Na pasta `portefolio/imagens/`, cliquem com o botão direito e escolham **New File**.
2. Criem o ficheiro com o nome `favicon.svg`.
3. Escrevam o seguinte código SVG (um quadrado arredondado com as marcas de código `</>`):

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32" width="32" height="32">
  <rect width="32" height="32" rx="8" fill="#264653"/>
  <path d="M10 11 L5 16 L10 21" stroke="#2a9d8f" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
  <path d="M22 11 L27 16 L22 21" stroke="#2a9d8f" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
  <line x1="18" y1="10" x2="14" y2="22" stroke="#e76f51" stroke-width="2.5" stroke-linecap="round"/>
</svg>
```

Guardem o ficheiro.

#### Passo 3: Ligar o Favicon no `<head>` das Três Páginas

Para dizer ao navegador qual é o ficheiro a usar como ícone, usamos o elemento `<link>` dentro do `<head>`:

```html
<link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
```

- **`rel="icon"`:** Informa o navegador de que este link aponta para o ícone do documento.
- **`type="image/svg+xml"`:** Especifica o tipo MIME do ficheiro (imagem vetorial SVG).
- **`href="imagens/favicon.svg"`:** O caminho relativo para onde guardámos o ficheiro.

Acrescentem esta linha logo abaixo do `<title>` em `index.html`, `projetos.html` e `contactos.html`.

Guardem e olhem para o separador do browser: o separador cinzento genérico agora exibe orgulhosamente o vosso ícone personalizado!

> **Dica:** Se o ícone não atualizar imediatamente no navegador, façam uma atualização forçada da cache: **Ctrl + F5** (no Windows) ou **Cmd + Shift + R** (no Mac).

> **Confirmem antes de avançar:**
>
> - O ficheiro `imagens/favicon.svg` existe na pasta de imagens.
> - Os três ficheiros HTML têm a tag `<link rel="icon">`.
> - O separador do navegador mostra o ícone de código.

---

### Parte 4: Porquê Validar no Cliente? A Primeira Linha de Defesa

Na aula anterior criámos um formulário funcional em `contactos.html`. Mas experimentem fazer isto no vosso navegador:

1. Abram `contactos.html`.
2. Não escrevam nada em nenhum campo.
3. Cliquem diretamente no botão **Enviar mensagem**.

O formulário é enviado em branco! Se isto fosse um site em produção, a caixa de entrada da Ana iria encher-se de mensagens sem nome, sem e-mail e sem texto, ou o servidor iria registar erros desnecessários.

#### Passo 1: A Analogia do Revisor de Bilhetes

Pensem num comboio de alta velocidade:

- Em vez de deixar toda a gente entrar e só descobrir que metade dos passageiros não tem bilhete quando o comboio já vai a 200 km/h, o revisor verifica o bilhete **na porta de embarque**, antes de qualquer pessoa entrar na carruagem.

Em aplicações web:

- A **validação no cliente (no browser)** é o revisor na porta de embarque: confere se os campos estão preenchidos, se o e-mail tem arroba e se os números têm os dígitos certos. Dá **feedback visual instantâneo** à pessoa, sem gastar tráfego de rede nem esperar pelo servidor.
- A **validação no servidor** continua a ser indispensável por questões de segurança (pois um utilizador mal-intencionado pode desativar o navegador ou enviar pedidos diretos via terminal). Mas a validação no cliente poupa 99% das dores de cabeça e oferece uma experiência de utilização muito mais agradável.

#### Passo 2: O Atributo `required`

O atributo booleano `required` é a regra mais básica e poderosa da validação HTML5. Diz simplesmente: _"Este campo tem de ser preenchido antes de submeter o formulário"_.

```html
<input type="text" id="nome" name="nome" required />
```

Se o utilizador tentar submeter o formulário com o campo vazio, o navegador interrompe o envio de imediato, coloca o foco no campo em falta e exibe uma caixa flutuante nativa (em português: _"Preencha este campo"_).

#### Passo 3: Validação Automática de E-mail

Ao usarmos `<input type="email" id="email" name="email" required />`, o navegador não se limita a verificar se o campo tem texto:

- Verifica ativamente se o texto introduzido contém o símbolo `@` e um domínio após ele (ex.: `nome@dominio.pt`).
- Se escreverem apenas `joao`, o navegador avisa: _"Inclua um «@» no endereço de e-mail"_.

#### Passo 4: O Truque do `<select required>`

Como obrigar um utilizador a escolher uma opção válida num menu suspenso `<select>`?

```html
<select id="assunto" name="assunto" required>
  <option value="">-- Escolha um assunto --</option>
  <option value="estagio">Proposta de estágio</option>
  <option value="projeto">Projeto ou colaboração</option>
</select>
```

O segredo está no valor `value=""` da primeira opção!

- Para o navegador, um valor vazio (`""`) conta como "não preenchido".
- Se o utilizador deixar o menu no convite inicial e tentar submeter, o `required` aciona o alarme: _"Selecione um item da lista"_.

> **Confirmem antes de avançar:**
>
> - Ao colocarem `required` no nome, e-mail e assunto, o navegador recusa envios em branco.
> - O navegador exibe balões de aviso nativos no vosso idioma do sistema.

---

### Parte 5: Restrições de Comprimento e Padrões Numéricos (`minlength`, `maxlength`, `pattern`, `title`)

Validar se um campo está preenchido é apenas metade da batalha. Muitas vezes precisamos de garantir que o que foi escrito cumpre critérios de qualidade mínimos.

#### Passo 1: Limitar o Número de Caracteres (`minlength` e `maxlength`)

Imaginem que alguém escreve apenas "A" no nome ou "ok" na mensagem. Não é útil para quem vai responder.

- **`minlength="3"`:** Exige um número mínimo de caracteres para que o campo seja considerado válido.
- **`maxlength="80"`:** Impede fisicamente o utilizador de digitar mais caracteres do que o limite permitido.

Vejam o campo de nome no nosso formulário:

```html
<input
  type="text"
  id="nome"
  name="nome"
  placeholder="Ex.: Maria Santos"
  required
  minlength="3"
  maxlength="80"
/>
```

Se tentarem escrever apenas duas letras ("Zé") e submeterem, o navegador alerta: _"Aumente o texto para 3 caracteres ou mais (está a utilizar 2 caracteres)"_.

E na área de texto da mensagem:

```html
<textarea
  id="mensagem"
  name="mensagem"
  rows="6"
  cols="40"
  placeholder="Escreva aqui a sua mensagem..."
  required
  minlength="10"
  maxlength="1000"
></textarea>
```

#### Passo 2: Padrões com Expressões Regulares (`pattern` e `title`)

E se quisermos validar um formato específico, como um contacto telefónico nacional com exatamente 9 algarismos numéricos?

Usamos o atributo `pattern` com uma **Expressão Regular** (_regex_):

```html
<input
  type="tel"
  id="telefone"
  name="telefone"
  placeholder="912345678"
  pattern="[0-9]{9}"
  title="Indique um contacto telefónico válido com 9 algarismos"
/>
```

O que significa `pattern="[0-9]{9}"`?

- **`[0-9]`:** Aceita apenas algarismos de 0 a 9 (rejeita letras, espaços e símbolos).
- **`{9}`:** Exige que sejam rigorosamente 9 algarismos seguidos.

E o atributo `title`?

- Se o utilizador escrever `1234` ou letras, o navegador avisa que o formato não cumpre o pedido e **mostra o texto do `title`** como mensagem de ajuda ao utilizador!

> **Atenção:** Como o campo de telefone é opcional, se estiver totalmente vazio o navegador permite o envio. Mas se a pessoa começar a escrever um número, terá obrigatoriamente de ter os 9 algarismos válidos!

#### Passo 3: Caixa de Autorização Obrigatória

Na era do RGPD (Regulamento Geral sobre a Proteção de Dados), não se devem recolher dados de contacto sem consentimento explícito. Colocar `required` numa caixa de seleção (`checkbox`) significa que o formulário só pode ser submetido se a caixa estiver marcada:

```html
<p>
  <input
    type="checkbox"
    id="autorizacao"
    name="autorizacao"
    value="sim"
    required
  />
  <label for="autorizacao"
    >Autorizo o tratamento destes dados para resposta a este contacto</label
  >
</p>
```

Se tentarem enviar sem marcar o visto, o navegador não deixa avançar: _"Marque esta caixa se pretende continuar"_.

#### Passo 4: O Formulário Blindado em `contactos.html`

Vejam como fica a secção `#formulario-contacto` completa em `contactos.html`:

```html
<section id="formulario-contacto">
  <!-- Formulário de Contacto com Validação HTML5 -->
  <h2>Envie uma mensagem</h2>
  <p>
    Se preferir, pode enviar uma mensagem diretamente através do formulário
    abaixo:
  </p>

  <form action="#" method="post">
    <fieldset>
      <legend>Os seus dados</legend>

      <p>
        <label for="nome">Nome completo:</label><br />
        <input
          type="text"
          id="nome"
          name="nome"
          placeholder="Ex.: Maria Santos"
          required
          minlength="3"
          maxlength="80"
        />
      </p>

      <p>
        <label for="email">Correio eletrónico:</label><br />
        <input
          type="email"
          id="email"
          name="email"
          placeholder="maria@exemplo.pt"
          required
        />
      </p>

      <p>
        <label for="telefone">Telefone / Telemóvel (opcional):</label><br />
        <input
          type="tel"
          id="telefone"
          name="telefone"
          placeholder="912345678"
          pattern="[0-9]{9}"
          title="Indique um contacto telefónico válido com 9 algarismos"
        />
      </p>
    </fieldset>

    <fieldset>
      <legend>Motivo e Mensagem</legend>

      <p>
        <label for="assunto">Assunto:</label><br />
        <select id="assunto" name="assunto" required>
          <option value="">-- Escolha um assunto --</option>
          <option value="estagio">Proposta de estágio</option>
          <option value="projeto">Projeto ou colaboração</option>
          <option value="duvida">Dúvida / Troca de ideias</option>
          <option value="outro">Outro assunto</option>
        </select>
      </p>

      <p>Como prefere receber a resposta?</p>
      <p>
        <input
          type="radio"
          id="pref-email"
          name="preferencia"
          value="email"
          checked
        />
        <label for="pref-email">Por e-mail</label><br />
        <input
          type="radio"
          id="pref-telefone"
          name="preferencia"
          value="telefone"
        />
        <label for="pref-telefone">Por telefone</label>
      </p>

      <p>
        <label for="mensagem">Mensagem:</label><br />
        <textarea
          id="mensagem"
          name="mensagem"
          rows="6"
          cols="40"
          placeholder="Escreva aqui a sua mensagem..."
          required
          minlength="10"
          maxlength="1000"
        ></textarea>
      </p>

      <p>
        <input
          type="checkbox"
          id="autorizacao"
          name="autorizacao"
          value="sim"
          required
        />
        <label for="autorizacao"
          >Autorizo o tratamento destes dados para resposta a este
          contacto</label
        >
      </p>
    </fieldset>

    <p>
      <button type="submit">Enviar mensagem</button>
      <button type="reset">Limpar formulário</button>
    </p>
  </form>
</section>
```

> **Confirmem antes de avançar:**
>
> - Ao clicar em "Enviar" com o formulário limpo, o foco vai para o nome.
> - Com o nome preenchido, vai para o e-mail.
> - Se o e-mail não tiver `@`, o envio é travado.
> - Se o assunto estiver na primeira opção neutra, o envio é travado.
> - Se a mensagem tiver menos de 10 caracteres, o envio é travado.
> - Se a caixa de autorização estiver desmarcada, o envio é travado.

---

### Parte 6: Guardar a Evolução no Git e GitHub

Com todas as páginas equipadas com metadados e o formulário totalmente validado, vamos registar o nosso progresso no Git.

1. Abram o terminal do VS Code (**Ctrl + `** ou **Cmd + `**).
2. Escrevam `git status`: verão as três páginas modificadas e o novo `imagens/favicon.svg`.
3. Adicionem tudo à área de preparação:

```bash
git add .
```

4. Criem o commit com uma mensagem descritiva:

```bash
git commit -m "Adiciona metadados SEO viewport favicon e validacao HTML5"
```

5. Enviem para o GitHub:

```bash
git push
```

6. Confirmem no vosso repositório no GitHub que os três ficheiros e a imagem do favicon estão atualizados.

> **Confirmem antes de avançar:**
>
> - O `git status` mostra a árvore de trabalho limpa.
> - O `git log --oneline -n 1` mostra o vosso novo commit.

---

**O projeto no fim da aula:**

```
portefolio/
├── imagens/
│   ├── foto.svg
│   └── favicon.svg
├── index.html
├── projetos.html
└── contactos.html
```

#### Código completo de `index.html`:

```html
<!doctype html>
<html lang="pt-PT">
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
  </head>
  <body>
    <header>
      <!-- Apresentação -->
      <img
        src="imagens/foto.svg"
        alt="Ilustração do rosto de Ana Martins, a sorrir"
        width="160"
        height="160"
      />
      <h1>Ana Martins</h1>
      <p>
        Futura <strong>programadora web</strong>, a aprender a construir sites
        de raiz.
      </p>

      <nav>
        <ul>
          <li><a href="index.html">Início</a></li>
          <li><a href="projetos.html">Projetos</a></li>
          <li><a href="contactos.html">Contactos</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <section>
        <!-- Sobre mim -->
        <h2>Sobre mim</h2>
        <p>
          Sou de Setúbal e trabalhei dez anos no comércio, sempre ao balcão.
        </p>
        <p>
          Em 2026 decidi mudar de vida e aprender a programar: quero ser
          programadora <span lang="en">full-stack</span>.
        </p>

        <h3>Competências em desenvolvimento</h3>
        <ul>
          <li>HTML5 semântico e estruturação acessível</li>
          <li>Controlo de versões com Git e GitHub</li>
          <li>Atenção ao detalhe e organização de código</li>
          <li>Comunicação e trabalho em equipa</li>
        </ul>

        <aside>
          <p>
            <strong>Sabiam que…</strong> o primeiro site da história foi
            publicado em 1991, no CERN, por Tim Berners-Lee.
          </p>
        </aside>
      </section>

      <section>
        <!-- Percurso -->
        <h2>O meu percurso</h2>
        <p>
          O meu caminho profissional e as etapas de formação que me trouxeram
          até aqui:
        </p>

        <table>
          <caption>
            Percurso formativo e profissional de Ana Martins
          </caption>
          <thead>
            <tr>
              <th scope="col">Período</th>
              <th scope="col">Área / Função</th>
              <th scope="col">Entidade</th>
              <th scope="col">Local</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">2026 – Presente</th>
              <td>Curso de Desenvolvimento Web Full-Stack</td>
              <td>Formação Profissional</td>
              <td>Setúbal</td>
            </tr>
            <tr>
              <th scope="row">2016 – 2026</th>
              <td>Comércio e atendimento ao público</td>
              <td>Loja Central</td>
              <td>Setúbal</td>
            </tr>
            <tr>
              <th scope="row">2013 – 2016</th>
              <td>Ensino Secundário</td>
              <td>Escola Secundária de Bocage</td>
              <td>Setúbal</td>
            </tr>
          </tbody>
        </table>
      </section>

      <section>
        <!-- Testemunhos -->
        <h2>O que dizem de mim</h2>
        <article>
          <blockquote>
            <p>A Ana resolve qualquer problema com calma e com um sorriso.</p>
          </blockquote>
          <p>— Carla Sousa, gerente da loja onde a Ana trabalhou</p>
        </article>
      </section>

      <section>
        <!-- Contactos Rápidos -->
        <h2>Contacto rápido</h2>
        <p>
          Estou sempre disponível para trocar ideias ou conversar sobre novas
          oportunidades.
        </p>
        <p>
          Enviem-me um e-mail para
          <a href="mailto:ana.martins@exemplo.pt">ana.martins@exemplo.pt</a>
          ou enviem uma mensagem através do formulário na página de
          <a href="contactos.html#formulario-contacto">contactos</a>.
        </p>
      </section>
    </main>

    <footer>
      <p>&copy; 2026 Ana Martins</p>
    </footer>
  </body>
</html>
```

#### Código completo de `projetos.html`:

```html
<!doctype html>
<html lang="pt-PT">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta
      name="description"
      content="Projetos desenvolvidos por Ana Martins: portefólio pessoal, páginas semânticas, dados acessíveis e código versionado no GitHub."
    />
    <meta name="author" content="Ana Martins" />
    <title>Projetos | Ana Martins</title>
    <link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
  </head>
  <body>
    <header>
      <!-- Apresentação -->
      <img
        src="imagens/foto.svg"
        alt="Ilustração do rosto de Ana Martins, a sorrir"
        width="160"
        height="160"
      />
      <h1>Ana Martins</h1>
      <p>
        Futura <strong>programadora web</strong>, a aprender a construir sites
        de raiz.
      </p>

      <nav>
        <ul>
          <li><a href="index.html">Início</a></li>
          <li><a href="projetos.html">Projetos</a></li>
          <li><a href="contactos.html">Contactos</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <section>
        <!-- Projetos Realizados -->
        <h2>Os meus projetos</h2>
        <p>
          Aqui partilho os projetos que construí até ao momento durante a minha
          formação de desenvolvimento web:
        </p>

        <ol>
          <li>
            <strong>Portefólio Pessoal:</strong> Este mesmo site, construído de
            raiz com HTML5 semântico, estruturação multi-páginas e versionado no
            GitHub.
          </li>
          <li>
            <strong>A Minha Cidade:</strong> Uma página dedicada a Braga, com
            ilustrações SVG, dados históricos e curiosidades regionais.
          </li>
          <li>
            <strong>Receita Tradicional:</strong> Estruturação semântica de uma
            receita de arroz doce, com lista de ingredientes e modo de preparo.
          </li>
          <li>
            <strong>Festival Gastronómico:</strong> Página informativa sobre o
            Festival da Sardinha de Portimão, com secções temáticas e
            testemunhos.
          </li>
        </ol>
      </section>

      <section>
        <!-- Tabela Resumo dos Projetos -->
        <h2>Resumo técnico dos projetos</h2>
        <p>
          Uma visão geral das tecnologias e do estado atual de cada trabalho:
        </p>

        <table>
          <caption>
            Resumo dos projetos desenvolvidos e tecnologias aplicadas
          </caption>
          <thead>
            <tr>
              <th scope="col">Projeto</th>
              <th scope="col">Tecnologias</th>
              <th scope="col">Ano</th>
              <th scope="col">Estado</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Portefólio Pessoal</th>
              <td>HTML5, Git, GitHub</td>
              <td>2026</td>
              <td>Em desenvolvimento</td>
            </tr>
            <tr>
              <th scope="row">A Minha Cidade</th>
              <td>HTML5, SVG</td>
              <td>2026</td>
              <td>Concluído</td>
            </tr>
            <tr>
              <th scope="row">Receita Tradicional</th>
              <td>HTML5</td>
              <td>2026</td>
              <td>Concluído</td>
            </tr>
            <tr>
              <th scope="row">Festival Gastronómico</th>
              <td>HTML5 semântico</td>
              <td>2026</td>
              <td>Concluído</td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>

    <footer>
      <p>&copy; 2026 Ana Martins</p>
    </footer>
  </body>
</html>
```

#### Código completo de `contactos.html`:

```html
<!doctype html>
<html lang="pt-PT">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta
      name="description"
      content="Entre em contacto com Ana Martins para propostas de estágio, projetos de desenvolvimento web ou esclarecimento de dúvidas."
    />
    <meta name="author" content="Ana Martins" />
    <title>Contactos | Ana Martins</title>
    <link rel="icon" type="image/svg+xml" href="imagens/favicon.svg" />
  </head>
  <body>
    <header>
      <!-- Apresentação -->
      <img
        src="imagens/foto.svg"
        alt="Ilustração do rosto de Ana Martins, a sorrir"
        width="160"
        height="160"
      />
      <h1>Ana Martins</h1>
      <p>
        Futura <strong>programadora web</strong>, a aprender a construir sites
        de raiz.
      </p>

      <nav>
        <ul>
          <li><a href="index.html">Início</a></li>
          <li><a href="projetos.html">Projetos</a></li>
          <li><a href="contactos.html">Contactos</a></li>
        </ul>
      </nav>
    </header>

    <main>
      <section>
        <!-- Contactos Principais -->
        <h2>Vamos conversar?</h2>
        <p>
          Estou disponível para novas oportunidades de estágio e colaboração a
          partir de 2027. Podem entrar em contacto comigo através dos seguintes
          canais:
        </p>

        <ul>
          <li>
            <strong>E-mail:</strong>
            <a href="mailto:ana.martins@exemplo.pt">ana.martins@exemplo.pt</a>
          </li>
          <li>
            <strong>GitHub:</strong>
            <a
              href="https://github.com/ana-martins-dev"
              target="_blank"
              rel="noreferrer noopener"
              >github.com/ana-martins-dev</a
            >
          </li>
          <li>
            <strong>Localização:</strong> Setúbal, Portugal (disponível para
            trabalho presencial ou remoto)
          </li>
        </ul>

        <aside>
          <p>
            <strong>Nota:</strong> Costumo responder a todas as mensagens no
            prazo máximo de 24 horas úteis.
          </p>
        </aside>
      </section>

      <section id="formulario-contacto">
        <!-- Formulário de Contacto com Validação HTML5 -->
        <h2>Envie uma mensagem</h2>
        <p>
          Se preferir, pode enviar uma mensagem diretamente através do
          formulário abaixo:
        </p>

        <form action="#" method="post">
          <fieldset>
            <legend>Os seus dados</legend>

            <p>
              <label for="nome">Nome completo:</label><br />
              <input
                type="text"
                id="nome"
                name="nome"
                placeholder="Ex.: Maria Santos"
                required
                minlength="3"
                maxlength="80"
              />
            </p>

            <p>
              <label for="email">Correio eletrónico:</label><br />
              <input
                type="email"
                id="email"
                name="email"
                placeholder="maria@exemplo.pt"
                required
              />
            </p>

            <p>
              <label for="telefone">Telefone / Telemóvel (opcional):</label
              ><br />
              <input
                type="tel"
                id="telefone"
                name="telefone"
                placeholder="912345678"
                pattern="[0-9]{9}"
                title="Indique um contacto telefónico válido com 9 algarismos"
              />
            </p>
          </fieldset>

          <fieldset>
            <legend>Motivo e Mensagem</legend>

            <p>
              <label for="assunto">Assunto:</label><br />
              <select id="assunto" name="assunto" required>
                <option value="">-- Escolha um assunto --</option>
                <option value="estagio">Proposta de estágio</option>
                <option value="projeto">Projeto ou colaboração</option>
                <option value="duvida">Dúvida / Troca de ideias</option>
                <option value="outro">Outro assunto</option>
              </select>
            </p>

            <p>Como prefere receber a resposta?</p>
            <p>
              <input
                type="radio"
                id="pref-email"
                name="preferencia"
                value="email"
                checked
              />
              <label for="pref-email">Por e-mail</label><br />
              <input
                type="radio"
                id="pref-telefone"
                name="preferencia"
                value="telefone"
              />
              <label for="pref-telefone">Por telefone</label>
            </p>

            <p>
              <label for="mensagem">Mensagem:</label><br />
              <textarea
                id="mensagem"
                name="mensagem"
                rows="6"
                cols="40"
                placeholder="Escreva aqui a sua mensagem..."
                required
                minlength="10"
                maxlength="1000"
              ></textarea>
            </p>

            <p>
              <input
                type="checkbox"
                id="autorizacao"
                name="autorizacao"
                value="sim"
                required
              />
              <label for="autorizacao"
                >Autorizo o tratamento destes dados para resposta a este
                contacto</label
              >
            </p>
          </fieldset>

          <p>
            <button type="submit">Enviar mensagem</button>
            <button type="reset">Limpar formulário</button>
          </p>
        </form>
      </section>

      <section>
        <!-- Disponibilidade -->
        <h2>Horário de disponibilidade</h2>
        <p>
          Os períodos em que estou mais facilmente contactável para reuniões ou
          conversas informais:
        </p>

        <table>
          <caption>
            Disponibilidade semanal para contacto e reuniões
          </caption>
          <thead>
            <tr>
              <th scope="col">Dias da semana</th>
              <th scope="col">Horário</th>
              <th scope="col">Formato preferencial</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Segunda a Sexta</th>
              <td>09:00 – 18:00</td>
              <td>E-mail ou videoconferência</td>
            </tr>
            <tr>
              <th scope="row">Sábado</th>
              <td>10:00 – 13:00</td>
              <td>E-mail</td>
            </tr>
            <tr>
              <th scope="row">Domingo</th>
              <td>Indisponível</td>
              <td>Descanso semanal</td>
            </tr>
          </tbody>
        </table>
      </section>
    </main>

    <footer>
      <p>&copy; 2026 Ana Martins</p>
    </footer>
  </body>
</html>
```

---

### Se Algo Correr Mal

1. **O favicon não aparece no separador do navegador.**
   - O browser costuma guardar favicons em cache agressiva. Carreguem com força em **Ctrl + F5** (Windows) ou **Cmd + Shift + R** (Mac). Confirmem também que o caminho `href="imagens/favicon.svg"` está correto e que o ficheiro se chama exatamente `favicon.svg`.
2. **O formulário é enviado mesmo com o `<select>` na opção inicial.**
   - A primeira opção tem de ter explicitamente o atributo `value=""` (vazio). Se escreverem apenas `<option>-- Escolha --</option>` sem `value=""`, o navegador assume que o texto da opção é o próprio valor e considera o campo preenchido!
3. **O campo de telefone acusa sempre erro, mesmo quando escrevo 9 números.**
   - Certifiquem-se de que não introduziram espaços ou traços. A regex `[0-9]{9}` exige rigorosamente 9 números seguidos (ex.: `912345678`).
4. **O validador W3C avisa sobre caracteres especiais na meta description.**
   - Não usem aspas duplas (`"`) soltas dentro do atributo `content="..."` da descrição, pois isso fecha o atributo antes do tempo. Usem aspas simples ou entidades (`&quot;`).
5. **A caixa de autorização não bloqueia o envio.**
   - Confirmem se colocaram a palavra `required` no elemento `<input type="checkbox" ... required />`.
6. **O navegador não mostra as mensagens em português.**
   - As mensagens de erro dos balões nativos dependem da língua configurada no vosso navegador e da tag `<html lang="pt-PT">` no topo do documento.

---

### O Que Aprendemos Hoje

Antes de passarem ao exercício prático individual, confirmem que compreendem e conseguem explicar:

- [ ] O conceito de metadados e porque vivem dentro de `<head>`.
- [ ] O que é SEO e onde é que o Google apresenta o texto da `<meta name="description">`.
- [ ] A regra de ouro da meta description (tamanho ideal de 120-160 caracteres e unicidade por página).
- [ ] A importância vital da `<meta name="viewport">` para renderização em ecrãs móveis.
- [ ] O que é um favicon e as vantagens do formato SVG.
- [ ] Porque é fundamental validar no cliente (experiência do utilizador) e manter validação no servidor (segurança).
- [ ] Como funciona o atributo `required` em caixas de texto, seletores e checkboxes.
- [ ] O uso de `minlength` e `maxlength` para garantir mensagens com substância.
- [ ] Como validar padrões específicos com `pattern` e como criar mensagens de ajuda com `title`.

---

### Palavras Novas

- **Metadados:** Informação técnica descritiva sobre o documento web que não é exibida na área visível da página.
- **`<meta>`:** Elemento HTML no `<head>` que transporta metadados estruturados.
- **SEO (_Search Engine Optimization_):** Técnicas de otimização de páginas para obtenção de melhores posições nos resultados de motores de busca.
- **Snippet:** Excerto ou resumo de uma página apresentado nos resultados de pesquisa do Google.
- **Viewport:** A janela de visualização do navegador onde o conteúdo da página é desenhado.
- **`width=device-width`:** Instrução que ajusta a largura da janela de visualização à largura física do ecrã do dispositivo.
- **`initial-scale=1.0`:** Nível de escala e zoom inicial da página ao ser carregada.
- **Favicon:** Ícone representativo do site apresentado no separador do navegador, favoritos e histórico.
- **`<link rel="icon">`:** Elemento do `<head>` que estabelece a ligação ao ficheiro do favicon.
- **Validação no cliente:** Verificação imediata das regras de preenchimento dos campos efetuada pelo próprio navegador antes do envio.
- **`required`:** Atributo booleano que impede a submissão de um formulário se o campo estiver vazio.
- **`minlength` e `maxlength`:** Atributos que estabelecem o número mínimo e máximo de caracteres aceites num campo de texto.
- **`pattern`:** Atributo que valida os dados introduzidos contra uma expressão regular.
- **Expressão Regular (_Regex_):** Sequência de símbolos que define um padrão de pesquisa ou validação formal de texto (ex.: `[0-9]{9}`).
- **`title`:** Atributo que serve de texto explicativo em balões de ajuda de campos validados por `pattern`.

---

### Para Saber Mais

Os recursos abaixo encontram-se em inglês. Usem a tradução automática do navegador (botão direito → **Traduzir para português**) se necessário.

- [O que há na cabeça? Metadados em HTML (MDN)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
- [Validação de dados em formulários (MDN)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)
- [Tudo o que precisas de saber sobre favicons modernos (web.dev)](https://web.dev/articles/building-a-favicon)
- [Guia básico de SEO para iniciantes (Google Search Central)](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)
- [A meta tag Viewport e o design responsivo (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag)

---

# Exercício Final: Os Passadiços do Paiva

Agora é a vossa vez de praticar sozinhos. O enunciado completo encontra-se também na ficha [`ex-007.md`](../../exercicios/ex-007.md) e os ficheiros de apoio estão na pasta [`exercicios/ex-007/`](../../exercicios/ex-007/).

### Missão 1: A Minha Cidade, Versão 7

1. Criem a pasta `sessao-07` dentro de `exercicios-uf1.1` e copiem para lá todo o conteúdo da pasta `sessao-06`.
2. Desenhem um favicon em SVG chamado `favicon.svg` dentro da pasta `imagens/`.
3. No ficheiro `cidade.html`, configurem os metadados no `<head>`: `<meta name="viewport">`, `<meta name="description">` personalizada, `<meta name="author">` e `<link rel="icon">`.
4. No formulário da secção `#sugestoes`, apliquem validação rigorosa:
   - Nome obrigatório (`required`), com 3 a 60 caracteres (`minlength` e `maxlength`).
   - E-mail e categoria obrigatórios (`required`).
   - Descrição obrigatória com 20 a 800 caracteres.
   - Caixa de autorização com preenchimento obrigatório (`required`).
5. Validem no [validador do W3C](https://validator.w3.org/#validate_by_input).
6. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Cidade com metadados e validacao de formulario"`, `git push`.

### Missão 2: A Página dos Passadiços do Paiva

1. Copiem o ficheiro [`passadicos-paiva.txt`](../../exercicios/ex-007/passadicos-paiva.txt) para a vossa pasta `sessao-07`.
2. Criem o ficheiro `passadicos-paiva.html` e estruturem o documento semântico do zero com base no texto:
   - `<head>` com meta viewport, meta description apelativa de 120-160 caracteres, autor e favicon.
   - `<header>` com título principal, texto de enquadramento com `<abbr>` para a UNESCO e menu com âncoras para as secções da página.
   - `<main>` dividido em 5 secções:
     - Destaques com três artigos (`<article>`) informativos.
     - Normas e segurança com lista não ordenada (`<ul>`).
     - Tabela semântica de bilheteira (`<table>`, `<caption>`, `<thead>`, `<tbody>`, `<th> scope="col"` e `scope="row"`).
     - Formulário de reserva completo e blindado com validação:
       - Nome (`required`, `minlength="3"`), E-mail (`required`), Telemóvel (`required`, `pattern="[0-9]{9}"` e `title`).
       - Data da visita (`type="date"`, `required`), Participantes (`type="number"`, `min="1"`, `max="25"`, `required`).
       - Modalidade de visita (`<select>` com `required`).
       - Checkboxes para serviços opcionais e caixa obrigatória de aceitação das normas de segurança (`required`).
       - Botões de envio e limpeza.
     - Contactos úteis com morada, link `mailto:` e link externo seguro.
   - `<footer>` com os direitos de autor institucionais.
3. Validem no validador do W3C.
4. Façam o ciclo de trabalho no Git: `git add .`, `git commit -m "Pagina dos Passadicos do Paiva com metadados e validacao"`, `git push`.

**Critérios de sucesso:**

- [ ] A pasta `sessao-07` contém `cidade.html`, `passadicos-paiva.html` e o ícone `imagens/favicon.svg`.
- [ ] Todas as páginas têm `<meta name="viewport">`, `<meta name="description">` e `<link rel="icon">`.
- [ ] O separador do navegador exibe o favicon SVG nas páginas.
- [ ] O formulário de reserva impede o envio quando os campos obrigatórios estão em branco.
- [ ] O campo de telemóvel rejeita entradas que não tenham exatamente 9 algarismos numéricos.
- [ ] O campo numérico de participantes impede valores inferiores a 1 ou superiores a 25.
- [ ] O envio só é permitido após marcação da caixa de aceitação das normas (`required`).
- [ ] O validador do W3C confirma que o código está perfeito e sem erros.
- [ ] O repositório no GitHub reflete todos os novos ficheiros e mensagens de commit.

### Missão 3: O Relatório

Respondam às seguintes questões por palavras vossas:

1. A importância da Meta Viewport:
   Para que serve a tag `<meta name="viewport" content="width=device-width, initial-scale=1.0">` e o que acontece quando abrimos um site sem esta tag num telemóvel?
   Resposta: [Preencher]

2. SEO e Meta Description:
   Onde aparece o conteúdo da tag `<meta name="description">` num motor de busca como o Google e quais são duas boas práticas essenciais na sua redação?
   Resposta: [Preencher]

3. Validação no Cliente vs no Servidor:
   Porque é que a validação nativa de HTML5 no navegador é excelente para a experiência do utilizador, mas nunca dispensa a validação adicional no servidor?
   Resposta: [Preencher]

---

### Desafio Bónus (Para os mais rápidos)

1. No campo de data da visita (`type="date"`), adicionem o atributo `min` com a data atual (por exemplo, `min="2026-11-06"`) para impedir que os utilizadores escolham datas que já passaram.
2. Utilizem o atributo `step` no campo numérico de participantes ou experimentem o atributo `autocomplete="name"` e `autocomplete="email"` para ajudar o navegador a preencher os dados do utilizador num clique.
3. Adicionem um botão secundário com o atributo `formnovalidate` para permitir testar a submissão do formulário sem acionar as validações nativas do navegador.
