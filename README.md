# amazon-reviews-analysis

## Projeto 2 - Megadados

**Alunos: Antonio Fuziy, Victor Vergara e André Tavernaro** 

___

### Tarefa 1

- `Quantos reviews existem?`

  Como o Dataset fornecido mostra todos os reviews existentes, para conta-los basta realizar um `count()` do dataframe 
  
  **Resposta: 150.962.278 milhões de reviews**

- `Quantos clientes existem?`

  O dataframe de reviews apresenta uma coluna de id's dos clientes, dessa forma para contar quantos clientes existem no dataset é necessário apenas realizar um `distinct().count()` na coluna de `customer_id`, assim obtém-se o número de clientes no dataset. 

  **Resposta: 33.497.620 milhões de clientes**

- `Quantos produtos existem?`

  Utilizando o dataset de reviews pode-se utilizar a coluna de `product_id` para contar quantos produtos existem no dataset, dessa forma é necessário apenas realizar um `distinct().count()`.

  **Resposta: 21.390.118 milhões de produtos**

- `Quantos reviews existem para cada star_rating (de 1 a 5 estrelas)?`

  Por último, para calcular quantos reviews existem por star_rating, é necessário agrupar os dados por `star_rating` utilizando a função `groupBy("star_rating")` e realizar o `count()` desse agrupamento, além de filtrar a coluna de `star_rating` para considerar apenas os reviews com star rating entre 1 a 5 estrelas.

  **Resposta:**
  
  |star_rating|   count  |
  |:---------:|:--------:|
  |     3     |12.133.772|
  |     1     |12.099.424|
  |     5     |93.199.322|
  |     4     |26.223.155|
  |     2     | 7.304.329|

  **Conceito A:**

  |product_id|marketplace|customer_id|     review_id|product_parent| product_title|product_category|star_rating|helpful_votes|total_votes|vine|verified_purchase|     review_headline|         review_body|        review_date|count|
  |---------:|----------:|:---------:|:------------:|:------------:|:------------:|:--------------:|:---------:|:-----------:|:---------:|:---|:---------------:|:------------------:|:------------------:|:-----------------:|:----|
  |B009UX2YAC|         US|   35276812|R2NCHRMM2P2G08|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                N|                cool|Because then I co...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|    1820505|R3HG3ZO14XXO8B|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|         awesomeness|This game is awes...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|   47135102|R3CREU7S2NHXS1|     879319057|Subway Surfers|     Mobile_Apps|          4|            0|          0|   N|                Y|       surfer subway|I enjoyed it ,  i...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|    8760529|R2DVV5V92T6CZ9|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|          I LOVED IT|It was the best g...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|    8996236| RYWDQ9H2YQCET|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|            fun game|Great family fun ...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|   15789766|R182BCKVIUMIJ6|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|             awesome|This game is so a...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|    2656680| RK5K5103LKLEX|     879319057|Subway Surfers|     Mobile_Apps|          3|            0|          0|   N|                Y|temple run is better|Thus game is ok b...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|    3728152|R3PE3T84BBRUY4|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|          great game|I love the update...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|   43385556|R3MFYKLM3JJDTC|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|        love it!!!!!|My two young chil...|2014-04-16 00:00:00|10311|
  |B009UX2YAC|         US|   49563096|R15BV3TQXDKG6R|     879319057|Subway Surfers|     Mobile_Apps|          5|            0|          0|   N|                Y|          Great game|I love this app a...|2014-04-16 00:00:00|10311|

___

### Tarefa 2

Primeiramente para realizar a identificação dos bots foi feito a um `groupBy("customer_id")` para observarmos quantos reviews cada cliente tinha, a partir disso realizou-se um describe da coluna de `count` **(resultado do groupBy citado anteriormente)**, assim extraiu-se a média e o desvio padrão de reviews por cliente e foram representados abaixo:

**desvio padrão: 20.132207420736695**

**média: 4.506656831142033**

A distribuição normal tem como propriedade que 99,7% dos resultados estão dentro de  μ ± 3σ, assim quem está fora dessa área são outliers, no caso os outliers sendo os bots.

Assim podemos consideramos que é um bot tendo acima de 65 reviews. 


Através desse valor obtido pelo cálculo anterior, filtrou-se os dados e manteve-se apenas os reviews referentes aos bots, dessa forma foi possível identificar quantos bots foram identificados, esse valor obtido foi de **183.291 mil bots**.

Além disso, utilizando o dataframe apenas de bots, foi possível realizar um `groupBy("product_category")`, assim obteve-se em quais os tipos de produto os bots mais davam reviews, sendo o top 10 mostrado abaixo:

|    product_category|  count|
|:------------------:|:-----:|
|               Books|4160547|
|Digital_Ebook_Pur...|3910182|
|           Video DVD|1388530|
|               Music|1135873|
|                Home| 947025|
|Health & Personal...| 825562|
|                  PC| 770871|
|             Kitchen| 756903|
|              Beauty| 738251|
|            Wireless| 717410|


Por fim, para essa tarefa utilizou-se o dataframe de bots para observar se os reviews eram em sua maioria positivos, negativos ou neutros, por conseguinte para que isso fosse possível foi necessário realizar um agrupamento por id dos clientes (`groupBy("customer_id").count()`) e realizar um join desse agrupamento com o dataframe dos bots, assim extraiu-se os clientes que tinham star_rating igual a 5 para positivo, igual a 4 para neutro e menor ou igual a 3 para negativo, resultando em **14.794.170 milhões** reviews positivos, **4.912.845 milhões** reviews neutros e **4.207.732 milhões** reviews negativos, considerando o número de bots encontrados anteriormente.

___

### Tarefa 3

Para construir um classificador de reviews utilizando o Naive-Bayes foi necessário realizar alguns passos:

- **Classificar cada review e separar em um dataframe junto do review_body**
    Para que isso fosse feito realizou-se a remoção de todos os valores NULL e a criação de uma nova coluna `rating_labels` para classificar cada review e a partir disso usar essas duas colunas para contruir o modelo Naivo-Bayes. 

- **Pipeline Stages**
    Criação dos RegexTokenizer para inputar a coluna de entrada `review_body` a qual representa o comentário dado que o produto recebeu;

    Criação do Count Vectorize e do StringIndexer para inputar a coluna com as classificações dos reviews em positivo, negativo e neutro;

    Juntando features pelo VectorAssembler;

    Criando Pipeline através da variável `stages`.

- **Divisão do dataset em treino (70%) e teste(30%)**

- **Implementação do Naive-Bayes**
    Realiza a implementação do modelo e mostra a tabela com as probabilidades de cada predição possível por classificação do review. 

- **Predição e Acurácia do modelo**
    Mostra a acurácia do modelo através do classificador binário.

    **A acurácia obtida foi de 74%**


