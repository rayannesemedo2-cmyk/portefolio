# Relatório — Site "Rui Costa, Fotografia"

## O que foi feito
- `index.html`: página única, HTML semântico (header, nav, main, section, article, aside, figure, table com caption, blockquote, cite, abbr, footer) com comentário em cada tag.
- `css/style.css`: CSS simples, sem frameworks (o `code.html` usava Tailwind). Cores, fontes e espaços estão em variáveis no início; cada regra tem comentário.
- `images/`: as 4 fotos do zip, sem alterações.
- Responsivo com os 3 tamanhos do DESIGN.md: telemóvel (<768px), tablet (768px+) e computador (1024px+).

## Como foi garantida a fidelidade
- Todas as medidas (padding, margens, gaps, alturas, tamanhos de letra, altura de linha, espaçamento entre letras) foram tiradas das classes do `code.html`, convertidas para CSS normal.
- Comparação com `screen.png` (a 1280px, reduzido para a mesma escala): as secções começam nas mesmas posições (diferença de 1–3px) e a altura total da página é 3741px contra ~3737px no design.

## Diferenças encontradas no material (decisões tomadas)
1. **Cores:** o `DESIGN.md` (texto) diz castanho #A36F52 e preto #1C1B1A, mas o `code.html` e o `screen.png` usam #825338 e #000000. Segui o `screen.png`/`code.html`.
2. **Cantos "redondos":** no `code.html`, `rounded-full` foi redefinido para 12px (não é círculo). Por isso o retrato e a foto pequena são quadrados de cantos arredondados, como no design.
3. **Cinzento dos textos secundários:** o `DESIGN.md` diz #65635F, mas o design usa #4a4640. Segui o design.
4. **Foto "papel-algodao-arquivo.jpg"** é uma captura de ecrã de uma página web (com título "Intimate Documentary Wedding Details"), não uma fotografia. Aparece igual no `screen.png`, por isso mantive. Sugiro trocar por uma foto real.
5. **`pedido.txt`**: o LEIAME.md pede este ficheiro, mas não está no zip.
6. **Links:** como no `code.html`, os links do cabeçalho (logótipo, Início, Serviços, Contactos, Disponibilidade) são `href="#"`. Os atalhos por baixo do nome levam às secções. Os 3 botões de orçamento apontam para `contactos.html#orcamento`, página que não foi fornecida e dá erro até ser criada.
7. **Classes `destaque` e `botao`** do `code.html` foram mantidas (e-mail sublinhado e botão "Página de Contactos"), caso o enunciado as exija.
8. O `code.html` tem um `<span>` de avatar com a foto do retrato no cabeçalho; usei `retrato-rui-costa.jpg`.
9. O menu do cabeçalho some em ecrãs <768px (como no design); não há menu hambúrguer porque o design não o tem.

## Limitações da verificação
- O ambiente onde construí não tem acesso à internet, por isso **as fontes Newsreader/Manrope e os ícones Material Symbols não carregaram na minha pré-visualização**: usei letras de substituição. As larguras de texto e os ícones têm de ser confirmados no seu navegador (com internet).
- O `screen.png` tem só 548px de largura, por isso não foi possível medir pixel a pixel; a comparação foi visual e por posições das secções.

## Comparação com o site original (3.ª versão)
Como o `code.html` precisa da internet (Tailwind) para aparecer, reconstruí as 204 classes dele em CSS local e desenhei **o original e a minha página lado a lado**, no mesmo navegador e com as mesmas fontes de substituição, a 1280px, 820px e 390px. Comparei a posição e o tamanho de 93 textos e imagens e fiz a diferença de pixéis.
- Resultado: 1280px com 0,58% de pixéis diferentes; 820px 1,12%; 390px 0,52%. Tudo acima da secção "Contacto rápido" é igual ao pixel.
- Corrigi 4 diferenças que a comparação encontrou: espaçamento entre letras dos títulos grandes no tablet/computador (-0,015em e -0,02em), altura de linha da citação do testemunho (1,3), altura da legenda da foto do Douro (24px) e espaçamento entre letras dos textos de 18px e 13px.
- As diferenças que restam são só dos ícones (a fonte de ícones não carrega offline, por isso os nomes "mail", "calendar_today", "history_edu" e "format_quote" aparecem como texto) e, por consequência, a altura dos botões de contacto e o rodapé que fica logo a seguir. Com internet, os ícones têm 18px/36px e isto desaparece.
- Não há diferenças propositadas: o cabeçalho e os links ficaram exatamente como no original (incluindo o aperto do cabeçalho e dos atalhos em ecrãs pequenos).
- Resultado final a 390px: 0,31% de pixéis diferentes.

## Ajuste final (5.ª versão)
- Faltava copiar do original a regra que **esconde a barra de rolagem** (`::-webkit-scrollbar{display:none}`). Sem ela, o navegador tira cerca de 15px de largura à página e o conteúdo quebra linha de forma diferente e fica mais "compacto". Corrigido (também para Firefox).
- Copiado também: `overscroll-behavior: none` no body e o aumento de 2% do retrato ao passar o rato (500ms).
- Comparação com o original refeita a 390, 820, 1024, 1100, 1280, 1440 e 1920px: todas as posições e tamanhos iguais, exceto os ícones (fonte de ícones não carrega offline).
