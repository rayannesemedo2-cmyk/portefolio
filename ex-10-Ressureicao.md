Missão 4: O Relatório
Respondam às perguntas por palavras vossas:

Flexbox: Num contentor flexível, qual é a diferença entre justify-content e align-items? E o que muda quando escrevemos flex-direction: column? Resposta: [
    A propriedade `justify-content` decide onde ficam os itens no "eixo principal".
    A propriedade `align-items` decide onde ficam os itens no "eixo transversal" (o vertical).
    A propriedade `flex-direction`muda o eixo principal:
`row`: os itens ficam em linha, da esquerda para a direita (é o valor por omissão).
`column`: os itens ficam em coluna, de cima para baixo. Então `justify-content` passa a trabalhar na vertical e `align-items` na horizontal.]

Flexbox ou Grid: Deem um exemplo de uma parte de uma página onde usariam Flexbox e outro onde usariam Grid. Expliquem porquê. Resposta: [O "Flexbox" arruma caixas "numa direção" (uma fila que pode mudar de linha). Quando queremos linhas "e"colunas ao mesmo tempo, como uma folha quadriculada, um tabuleiro de xadrez ou uma caixa de ovos, usamos o "Grid".]

A unidade fr: Uma grelha tem grid-template-columns: 1fr 2fr 1fr. Que coluna é a mais larga? Quantas vezes é mais larga do que as outras? Resposta: [`grid-template-columns` diz quantas colunas há e qual a largura de cada uma. Aqui há dois valores, por isso há duas colunas.
`fr`(de _fraction_, "fração") é uma unidade criada para as grelhas: reparte o espaço livre. `1fr 1fr` são duas colunas iguais; `2fr 1fr` seria uma coluna com o dobro da largura da outra.]

Mobile-first: O que quer dizer "mobile-first"? Porque é que as nossas media queries usam min-width e não max-width? Resposta: [Mobile-first significa começar por criar o site a pensar primeiro nos telemóveis e depos adaptar o design aos ecãS maiores. Utilizamos min-width porque permite acrescentar estilos quando o ecã atinge uma determinada largura, melhorando a apresentação em tablets e comprutadores.
]

A meta viewport: O que acontece a uma página sem <meta name="viewport"> quando a abrimos num telemóvel? Resposta: [Sem a etiqueya<meta name="viewport">, o telemóvel pode apresentar a página como se tivesse uma largura de computador, fazendo com que o conteúdo fique muito pequeno e obrigando o utilizador a ampliar ou deslocar a página para conseguir ler.]