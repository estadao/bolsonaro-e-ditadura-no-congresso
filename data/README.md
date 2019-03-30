# bolsonaro-e-ditadura-no-congresso

Esse é o código fonte para a [matéria](https://www.estadao.com.br/infograficos/politica,bolsonaro-mencionou-a-ditadura-em-1-3-de-seus-discursos-como-deputado,982285) que conta quantas vezes o presidente Jair Bolsonaro mencionou a ditadura militar brasileira no período em que foi deputado federal.

## Breve descrição da metodologia

A reportagem usou um programa de computador para acessar todos os discursos de Jair Bolsonaro em plenário que estão disponíveis no setor de Notas Taquigráficas do site da Câmara dos Deputados.

Discursos anteriores à 2001 não estão transcritos no site – há apenas um link para o documento do Congresso, em PDF, que contém todos os pronunciamentos feitos por qualquer deputado na data. Assim, como não houve tempo hábil para processá-los até a publicação, eles foram descartados.

Já com todos os pronunciamentos de Bolsonaro no período em mãos, definimos uma série de palavras-chave relacionadas à ditadura militar brasileira. São termos como “31 de março”, “regime militar”, “Comissão da Verdade”, “Castelo Branco”, “VAR-Palmares” ou “Marighella”, por exemplo. 

Em seguida, selecionamos todos os discursos que continham ao menos uma destas palavras. Estes pronunciamentos foram lidos na íntegra para verificar se os termos usados se referem de fato ao regime militar.

Os discursos que passaram por essa última checagem são os 252 que foram destacados nessa reportagem. Os trechos selecionados para exibição também foram escolhidos manualmente.

## Conteúdo do repositório

### Diretório `code`

Contém os arquivos `.ipynb` que foram usados para raspar os dados do site da Câmara e montar a análise.

Devem ser executados na seguinte ordem:

1. `pega-links.ipynb`: executa uma busca textual para encontrar os discursos e salva os URLs onde eles estão armazenados

2. `pega-pronunciamentos-html.ipynb`: Usa o csv gerados em `pega-links` para extrair, via BeautifulSoup, os pronunciamentos para os quais existem conteúdo em HTML. Também há a opção de salvar PDFs para pronunciamentos que não foram transcritos, ainda.

3. `formata-texto.ipynb`: Acessa os arquivos .txt gerados em `pega-pronunciamentos-html` e usa expressões regulares para extrair apenas os trechos em que determinado deputado – no caso, Bolsonaro – falou.

4. `buscador-da-ditadura.ipynb`: Usa o arquivo csv gerado em `formata-texto`. Define uma série de palavras-chave relacionadas à ditadura militar e verifica quais entradas da planilha contém qualquer um desses termos. **O output gerado foi checado manualmente para garantir que não pegamos falsos positivos!**

5. `parseia-json.ipynb`: Usa o arquivo com os discursos **já checado manualmente**. Transforma esses dados em um arquivo .json para gerar as visualizações de dados.

### Diretório `data`

`tables`: Ao executar `pega-links`, nesse diretório serão salvos os arquivos .csv com os links que precisam ser raspados.

`txts`: Ao executar `pega-pronunciamentos-html`, esse diretório será preenchido com os discursos raspados do site da Câmara.

`pdfs`: Ao executar `pega-pronunciamentos-html`, esse diretório será preenchido com os discursos baixados do site da Câmara. **Eles não foram usados nesta análise**.

`csvs`: Diversos csvs gerados ao longo do fluxo de trabalho são salvos aqui, a saber: 

  - Os discursos formatados em `formata-texto`
  - Os discrusos classificados por `buscador-da-ditadura`

  Além disso, o diretório contém o arquivo `DISCURSOS-CHECADOS-MANUALMENTE`, que é a base de dados que alimentou a matéria, e `sneakpeek`, que é uma tabela com trechos que foram destacados no corpo da reportagem. Estes foram criados e checados a mão.

`jsons`: Os arquivos necessários para gerar a visualização de dados do site.
