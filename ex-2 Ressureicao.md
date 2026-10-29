### Missao 4: O Relatorio

Entreguem as respostas:

1. Os erros:
   Quais foram os 6 erros que encontraram no `erros.html`? Para cada um, escrevam a linha e o que corrigiram.
   Resposta: 
   [Erro: A tag <title>Doces de Portugal nao tem o fecho correspondente.
   Correcao: Adicionar </title> no final da linha (ficando <title>Doces de Portugal</title>).
  
   Erro: Abre com <h1> mas fecha com </h2>.
   Correcao: Substituir o </h2> por </h1>
   
   Erro: <strong>enorme <em>variedade</strong></em> cruza as tags incorretamente (<strong> fecha antes de <em>).
   Correcao: Fechar primeiro a tag interior e depois a exterior: <strong>enorme <em>variedade</em></strong>.
   
   Erro: O paragrafo <p>Nasceu no Mosteiro dos Jerinimos, em Lisboa. nao tem a tag de fecho.
   Correcao: Adicionar </p> no final da linha
   
   Erro: <h2>Ovos moles<h2> abre com <h2> e repete <h2> em vez de fechar.
   Correcao: Alterar o segundo <h2> para </h2>
   
   Erro: O comentario <!-- Bola de Berlim -> termina apenas com um hifen (->) em vez de dois.
   Correcao: Corrigir para --> (ficando <!-- Bola de Berlim -->).]

2. A pagina em branco:
   Porque e que o `erros.html` aparecia todo em branco no inicio?
   Resposta: [Porque o ficheiro estava inicialmente vazio (sem conteudo escrito dentro da tag <body>),]

3. Os titulos:
   Na receita, porque e que os passos sao `h3` e nao `h2`?
   Resposta: [Para manter uma hierarquia semantica correta no documento HTML. Normalmente, o titulo principal da receita e um h1, as seccoes principais (como "Ingredientes" ou "Modo de Preparacao") usam h2, e os passos individuais ou subsecoes dentro dessas seccoes usam h3 para ficarem estruturalmente organizados logo abaixo dos h2.]