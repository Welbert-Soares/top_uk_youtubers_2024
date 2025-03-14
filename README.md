# Portfólio de Dados: Excel para Power BI

![excel-to-powerbi-animated-diagram](/docs/assets/images/kaggle_to_powerbi.gif)

# Índice

- [Objetivo](#objective)
- [Fonte de Dados](#data-source)
- [Etapas](#stages)
- [Design](#design)
  - [Mockup](#mockup)
  - [Ferramentas](#tools)
- [Desenvolvimento](#development)
  - [Pseudocódigo](#pseudocode)
  - [Exploração de Dados](#data-exploration)
  - [Limpeza de Dados](#data-cleaning)
  - [Transformar os Dados](#transform-the-data)
  - [Criar a Visualização SQL](#create-the-sql-view)
- [Testes](#testing)
  - [Testes de Qualidade de Dados](#data-quality-tests)
- [Visualização](#visualization)
  - [Resultados](#results)
  - [Medidas DAX](#dax-measures)
- [Análise](#analysis)
  - [Descobertas](#findings)
  - [Validação](#validation)
  - [Descoberta](#discovery)
- [Recomendações](#recommendations)
  - [ROI Potencial](#potential-roi)
  - [Potenciais Cursos de Ação](#potential-courses-of-actions)
- [Conclusão](#conclusion)

# Objetivo

- Qual é o principal ponto de dor?

O Chefe de Marketing quer descobrir quem são os principais YouTubers em 2024 para decidir quais seriam os melhores para realizar campanhas de marketing ao longo do ano.

- Qual é a solução ideal?

Criar um painel que forneça insights sobre os principais YouTubers do Reino Unido em 2024, incluindo:

- contagem de assinantes
- total de visualizações
- total de vídeos, e
- métricas de engajamento

Isso ajudará a equipe de marketing a tomar decisões informadas sobre com quais YouTubers colaborar para suas campanhas de marketing.

## História do Usuário

Como Chefe de Marketing, quero usar um painel que analise dados de canais do YouTube no Reino Unido.

Este painel deve me permitir identificar os canais de melhor desempenho com base em métricas como base de assinantes e visualizações médias.

Com essas informações, posso tomar decisões mais informadas sobre quais YouTubers são adequados para colaborar, maximizando assim a eficácia de cada campanha de marketing.

# Fonte de Dados

- Quais dados são necessários para alcançar nosso objetivo?

Precisamos de dados sobre os principais YouTubers do Reino Unido em 2024, incluindo:

- nomes dos canais
- total de assinantes
- total de visualizações
- total de vídeos enviados

- De onde vêm os dados?
  Os dados são provenientes do Kaggle (um extrato do Excel), [veja aqui para encontrá-los.](https://www.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download)

# Etapas

- Design
- Desenvolvimento
- Testes
- Análise

# Design

## Componentes necessários do painel

- O que o painel deve conter com base nos requisitos fornecidos?

Para entender o que deve conter, precisamos descobrir quais perguntas o painel precisa responder:

1. Quem são os 10 principais YouTubers com mais assinantes?
2. Quais 3 canais enviaram mais vídeos?
3. Quais 3 canais têm mais visualizações?
4. Quais 3 canais têm a maior média de visualizações por vídeo?
5. Quais 3 canais têm a maior proporção de visualizações por assinante?
6. Quais 3 canais têm a maior taxa de engajamento de assinantes por vídeo enviado?

Por enquanto, estas são algumas das perguntas que precisamos responder, isso pode mudar à medida que avançamos em nossa análise.

## Mockup do Painel

- Como deve ser?

Alguns dos visuais de dados que podem ser apropriados para responder às nossas perguntas incluem:

1. Tabela
2. Mapa de árvore
3. Cartões de pontuação
4. Gráfico de barras horizontal

![Dashboard-Mockup](/docs/assets/images/dashboard_mockup.png)

## Ferramentas

| Ferramenta | Finalidade                                              |
| ---------- | ------------------------------------------------------- |
| Excel      | Explorar os dados                                       |
| SQL Server | Limpar, testar e analisar os dados                      |
| Power BI   | Visualizar os dados por meio de painéis interativos     |
| GitHub     | Hospedar a documentação do projeto e controle de versão |
| Mokkup AI  | Projetar o wireframe/mockup do painel                   |

# Desenvolvimento

## Pseudocódigo

- Qual é a abordagem geral para criar esta solução do início ao fim?

1. Obter os dados
2. Explorar os dados no Excel
3. Carregar os dados no SQL Server
4. Limpar os dados com SQL
5. Testar os dados com SQL
6. Visualizar os dados no Power BI
7. Gerar as descobertas com base nos insights
8. Escrever a documentação + comentários
9. Publicar os dados no GitHub Pages

## Notas de exploração de dados

Esta é a etapa em que você faz uma varredura do que há nos dados, erros, inconsistências, bugs, caracteres estranhos e corrompidos, etc.

- Quais são suas observações iniciais com este conjunto de dados? O que chamou sua atenção até agora?

1. Existem pelo menos 4 colunas que contêm os dados necessários para esta análise, o que sinaliza que temos tudo o que precisamos do arquivo sem precisar contatar o cliente para mais dados.
2. A primeira coluna contém o ID do canal com o que parece ser IDs de canal, que são separados por um símbolo @ - precisamos extrair os nomes dos canais disso.
3. Algumas das células e nomes de cabeçalho estão em um idioma diferente - precisamos confirmar se essas colunas são necessárias e, em caso afirmativo, precisamos abordá-las.
4. Temos mais dados do que precisamos, então algumas dessas colunas precisariam ser removidas.

## Limpeza de dados

- Como esperamos que os dados limpos se pareçam? (O que deve conter? Quais restrições devemos aplicar a ele?)

O objetivo é refinar nosso conjunto de dados para garantir que esteja estruturado e pronto para análise.

Os dados limpos devem atender aos seguintes critérios e restrições:

- Apenas colunas relevantes devem ser retidas.
- Todos os tipos de dados devem ser apropriados para o conteúdo de cada coluna.
- Nenhuma coluna deve conter valores nulos, indicando dados completos para todos os registros.

Abaixo está uma tabela que descreve as restrições em nosso conjunto de dados limpo:

| Propriedade       | Descrição |
| ----------------- | --------- |
| Número de Linhas  | 100       |
| Número de Colunas | 4         |

E aqui está uma representação tabular do esquema esperado para os dados limpos:

| Nome da Coluna         | Tipo de Dados | Nulável |
| ---------------------- | ------------- | ------- |
| nome_do_canal          | VARCHAR       | NÃO     |
| total_de_assinantes    | INTEGER       | NÃO     |
| total_de_visualizações | INTEGER       | NÃO     |
| total_de_vídeos        | INTEGER       | NÃO     |

- Quais etapas são necessárias para limpar e moldar os dados no formato desejado?

1. Remover colunas desnecessárias selecionando apenas as que você precisa
2. Extrair nomes de canais do YouTube da primeira coluna
3. Renomear colunas usando aliases

### Transformar os dados

```sql
/*
# 1. Selecione as colunas necessárias
# 2. Extraia o nome do canal da coluna 'NOMBRE'
*/

-- 1.
SELECT
    SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) -1) AS channel_name,  -- 2.
    total_subscribers,
    total_views,
    total_videos

FROM
    top_uk_youtubers_2024
```

### Criar a Visualização SQL

```sql
/*
# 1. Crie uma visualização para armazenar os dados transformados
# 2. Converta o nome do canal extraído para VARCHAR(100)
# 3. Selecione as colunas necessárias da tabela SQL top_uk_youtubers_2024
*/

-- 1.
CREATE VIEW view_uk_youtubers_2024 AS

-- 2.
SELECT
    CAST(SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) -1) AS VARCHAR(100)) AS channel_name, -- 2.
    total_subscribers,
    total_views,
    total_videos

-- 3.
FROM
    top_uk_youtubers_2024

```

# Testes

- Quais testes de qualidade e validação você vai criar?

Aqui estão os testes de qualidade de dados realizados:

## Verificação de contagem de linhas

```sql
/*
# Conte o número total de registros (ou linhas) na visualização SQL
*/

SELECT
    COUNT(*) AS no_of_rows
FROM
    view_uk_youtubers_2024;

```

![Verificação de contagem de linhas](/docs/assets/images/1_row_count_check.png)

## Verificação de contagem de colunas

### Consulta SQL

```sql
/*
# Conte o número total de colunas (ou campos) na visualização SQL
*/


SELECT
    COUNT(*) AS column_count
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'view_uk_youtubers_2024'
```

### Saída

![Verificação de contagem de colunas](/docs/assets/images/2_column_count_check.png)

## Verificação de tipo de dados

### Consulta SQL

```sql
/*
# Verifique os tipos de dados de cada coluna da visualização verificando a visualização do SCHEMA DE INFORMAÇÃO
*/

-- 1.
SELECT
    COLUMN_NAME,
    DATA_TYPE
FROM
    INFORMATION_SCHEMA.COLUMNS
WHERE
    TABLE_NAME = 'view_uk_youtubers_2024';
```

### Saída

![Verificação de tipo de dados](/docs/assets/images/3_data_type_check.png)

## Verificação de contagem de duplicatas

### Consulta SQL

```sql
/*
# 1. Verifique linhas duplicadas na visualização
# 2. Agrupe pelo nome do canal
# 3. Filtre para grupos com mais de uma linha
*/

-- 1.
SELECT
    channel_name,
    COUNT(*) AS duplicate_count
FROM
    view_uk_youtubers_2024

-- 2.
GROUP BY
    channel_name

-- 3.
HAVING
    COUNT(*) > 1;
```

### Saída

![Verificação de contagem de duplicatas](/docs/assets/images/4_duplicate_records_check.png)

# Visualização

## Resultados

- Como o painel deve ser?

![GIF do Painel do Power BI](/docs/assets/images/top_uk_youtubers_2024.gif)

Este mostra os Top UK Youtubers em 2024 até agora.

## Medidas DAX

### 1. Total de Assinantes (M)

```sql
Total Subscribers (M) =
VAR million = 1000000
VAR sumOfSubscribers = SUM(view_uk_youtubers_2024[total_subscribers])
VAR totalSubscribers = DIVIDE(sumOfSubscribers,million)

RETURN totalSubscribers

```

### 2. Total de Visualizações (B)

```sql
Total Views (B) =
VAR billion = 1000000000
VAR sumOfTotalViews = SUM(view_uk_youtubers_2024[total_views])
VAR totalViews = ROUND(sumOfTotalViews / billion, 2)

RETURN totalViews

```

### 3. Total de Vídeos

```sql
Total Videos =
VAR totalVideos = SUM(view_uk_youtubers_2024[total_videos])

RETURN totalVideos

```

### 4. Média de Visualizações por Vídeo (M)

```sql
Average Views per Video (M) =
VAR sumOfTotalViews = SUM(view_uk_youtubers_2024[total_views])
VAR sumOfTotalVideos = SUM(view_uk_youtubers_2024[total_videos])
VAR  avgViewsPerVideo = DIVIDE(sumOfTotalViews,sumOfTotalVideos, BLANK())
VAR finalAvgViewsPerVideo = DIVIDE(avgViewsPerVideo, 1000000, BLANK())

RETURN finalAvgViewsPerVideo

```

### 5. Taxa de Engajamento de Assinantes

```sql
Subscriber Engagement Rate =
VAR sumOfTotalSubscribers = SUM(view_uk_youtubers_2024[total_subscribers])
VAR sumOfTotalVideos = SUM(view_uk_youtubers_2024[total_videos])
VAR subscriberEngRate = DIVIDE(sumOfTotalSubscribers, sumOfTotalVideos, BLANK())

RETURN subscriberEngRate

```

### 6. Visualizações por Assinante

```sql
Views Per Subscriber =
VAR sumOfTotalViews = SUM(view_uk_youtubers_2024[total_views])
VAR sumOfTotalSubscribers = SUM(view_uk_youtubers_2024[total_subscribers])
VAR viewsPerSubscriber = DIVIDE(sumOfTotalViews, sumOfTotalSubscribers, BLANK())

RETURN viewsPerSubscriber

```

# Análise

## Descobertas

- O que encontramos?

Para esta análise, vamos nos concentrar nas perguntas abaixo para obter as informações que precisamos para nosso cliente de marketing -

Aqui estão as principais perguntas que precisamos responder para nosso cliente:

1. Quem são os 10 principais YouTubers com mais assinantes?
2. Quais 3 canais enviaram mais vídeos?
3. Quais 3 canais têm mais visualizações?
4. Quais 3 canais têm a maior média de visualizações por vídeo?
5. Quais 3 canais têm a maior proporção de visualizações por assinante?
6. Quais 3 canais têm a maior taxa de engajamento de assinantes por vídeo enviado?

### 1. Quem são os 10 principais YouTubers com mais assinantes?

| Rank | Channel Name      | Subscribers (M) |
| ---- | ----------------- | --------------- |
| 1    | NoCopyrightSounds | 33.60           |
| 2    | DanTDM            | 28.60           |
| 3    | Dan Rhodes        | 26.50           |
| 4    | Miss Katy         | 24.50           |
| 5    | Mister Max        | 24.40           |
| 6    | KSI               | 24.10           |
| 7    | Jelly             | 23.50           |
| 8    | Dua Lipa          | 23.30           |
| 9    | Sidemen           | 21.00           |
| 10   | Ali-A             | 18.90           |

### 2. Quais 3 canais enviaram mais vídeos?

| Rank | Channel Name    | Videos Uploaded |
| ---- | --------------- | --------------- |
| 1    | GRM Daily       | 14,696          |
| 2    | Manchester City | 8,248           |
| 3    | Yogscast        | 6,435           |

### 3. Quais 3 canais têm mais visualizações?

| Rank | Channel Name | Total Views (B) |
| ---- | ------------ | --------------- |
| 1    | DanTDM       | 19.78           |
| 2    | Dan Rhodes   | 18.56           |
| 3    | Mister Max   | 15.97           |

### 4. Quais 3 canais têm a maior média de visualizações por vídeo?

| Channel Name | Averge Views per Video (M) |
| ------------ | -------------------------- |
| Mark Ronson  | 32.27                      |
| Jessie J     | 5.97                       |
| Dua Lipa     | 5.76                       |

### 5. Quais 3 canais têm a maior proporção de visualizações por assinante?

| Rank | Channel Name     | Views per Subscriber |
| ---- | ---------------- | -------------------- |
| 1    | GRM Daily        | 1185.79              |
| 2    | Nickelodeon      | 1061.04              |
| 3    | Disney Junior UK | 1031.97              |

### 6. Quais 3 canais têm a maior taxa de engajamento de assinantes por vídeo enviado?

| Rank | Channel Name | Subscriber Engagement Rate |
| ---- | ------------ | -------------------------- |
| 1    | Mark Ronson  | 343,000                    |
| 2    | Jessie J     | 110,416.67                 |
| 3    | Dua Lipa     | 104,954.95                 |

### Notas

Para esta análise, vamos priorizar analisar as métricas que são importantes para gerar o ROI esperado para nosso cliente de marketing, que são os canais do YouTube com mais

- assinantes
- total de visualizações
- vídeos enviados

## Validação

### 1. YouTubers com mais assinantes

#### Descrição do Cálculo

Ideia de campanha = colocação de produto

1. NoCopyrightSounds

- Média de visualizações por vídeo = 6,92 milhões
- Custo do produto = $5
- Unidades potenciais vendidas por vídeo = 6,92 milhões x 2% taxa de conversão = 138,400 unidades vendidas
- Receita potencial por vídeo = 138,400 x $5 = $692,000
- Custo da campanha (taxa única) = $50,000
- **Lucro líquido = $692,000 - $50,000 = $642,000**

b. DanTDM

- Média de visualizações por vídeo = 5,34 milhões
- Custo do produto = $5
- Unidades potenciais vendidas por vídeo = 5,34 milhões x 2% taxa de conversão = 106,800 unidades vendidas
- Receita potencial por vídeo = 106,800 x $5 = $534,000
- Custo da campanha (taxa única) = $50,000
- **Lucro líquido = $534,000 - $50,000 = $484,000**

c. Dan Rhodes

- Média de visualizações por vídeo = 11,15 milhões
- Custo do produto = $5
- Unidades potenciais vendidas por vídeo = 11,15 milhões x 2% taxa de conversão = 223,000 unidades vendidas
- Receita potencial por vídeo = 223,000 x $5 = $1,115,000
- Custo da campanha (taxa única) = $50,000
- **Lucro líquido = $1,115,000 - $50,000 = $1,065,000**

Melhor opção da categoria: Dan Rhodes

#### Consulta SQL

```sql
/*
# 1. Defina variáveis
# 2. Crie um CTE que arredonda a média de visualizações por vídeo
# 3. Selecione a coluna que você precisa e crie colunas calculadas a partir das existentes
# 4. Filtre os resultados por canais do YouTube
# 5. Ordene os resultados por lucros líquidos (do maior para o menor)
*/


-- 1.
DECLARE @conversionRate FLOAT = 0.02;		-- A taxa de conversão @ 2%
DECLARE @productCost FLOAT = 5.0;			-- O custo do produto @ $5
DECLARE @campaignCost FLOAT = 50000.0;		-- O custo da campanha @ $50.000


-- 2.
WITH ChannelData AS (
    SELECT
        channel_name,
        total_views,
        total_videos,
        ROUND((CAST(total_views AS FLOAT) / total_videos), -4) AS rounded_avg_views_per_video
    FROM
        youtube_db.dbo.view_uk_youtubers_2024
)

-- 3.
SELECT
    channel_name,
    rounded_avg_views_per_video,
    (rounded_avg_views_per_video * @conversionRate) AS potential_units_sold_per_video,
    (rounded_avg_views_per_video * @conversionRate * @productCost) AS potential_revenue_per_video,
    ((rounded_avg_views_per_video * @conversionRate * @productCost) - @campaignCost) AS net_profit
FROM
    ChannelData


-- 4.
WHERE
    channel_name in ('NoCopyrightSounds', 'DanTDM', 'Dan Rhodes')


-- 5.
ORDER BY
  net_profit DESC

```

#### Saída

![Mais assinantes](/docs/assets/images/youtubers_with_the_most_subs.png)

### 2. YouTubers com mais vídeos enviados

### Descrição do Cálculo

Ideia de campanha = série de vídeos patrocinados

1. GRM Daily

- Média de visualizações por vídeo = 510,000
- Custo do produto = $5
- Unidades potenciais vendidas por vídeo = 510,000 x 2% taxa de conversão = 10,200 unidades vendidas
- Receita potencial por vídeo = 10,200 x $5= $51,000
- Custo da campanha (11-videos @ $5,000 each) = $55,000
- **Net profit = $51,000 - $55,000 = -$4,000 (potential loss)**

b. **Manchester City**

- Average views per video = 240,000
- Product cost = $5
- Potential units sold per video = 240,000 x 2% conversion rate = 4,800 units sold
- Potential revenue per video = 4,800 x $5= $24,000
- Campaign cost (11-videos @ $5,000 each) = $55,000
- **Net profit = $24,000 - $55,000 = -$31,000 (potential loss)**

b. **Yogscast**

- Average views per video = 710,000
- Product cost = $5
- Potential units sold per video = 710,000 x 2% conversion rate = 14,200 units sold
- Potential revenue per video = 14,200 x $5= $71,000
- Campaign cost (11-videos @ $5,000 each) = $55,000
- **Net profit = $71,000 - $55,000 = $16,000 (profit)**

Best option from category: Yogscast

#### SQL query

```sql
/*
# 1. Defina variáveis
# 2. Crie um CTE que arredonda a média de visualizações por vídeo
# 3. Selecione as colunas que você precisa e crie colunas calculadas a partir das existentes
# 4. Filtre os resultados por canais do YouTube
# 5. Ordene os resultados por lucros líquidos (do maior para o menor)
*/


-- 1.
DECLARE @conversionRate FLOAT = 0.02;           -- The conversion rate @ 2%
DECLARE @productCost FLOAT = 5.0;               -- The product cost @ $5
DECLARE @campaignCostPerVideo FLOAT = 5000.0;   -- The campaign cost per video @ $5,000
DECLARE @numberOfVideos INT = 11;               -- The number of videos (11)


-- 2.
WITH ChannelData AS (
    SELECT
        channel_name,
        total_views,
        total_videos,
        ROUND((CAST(total_views AS FLOAT) / total_videos), -4) AS rounded_avg_views_per_video
    FROM
        youtube_db.dbo.view_uk_youtubers_2024
)


-- 3.
SELECT
    channel_name,
    rounded_avg_views_per_video,
    (rounded_avg_views_per_video * @conversionRate) AS potential_units_sold_per_video,
    (rounded_avg_views_per_video * @conversionRate * @productCost) AS potential_revenue_per_video,
    ((rounded_avg_views_per_video * @conversionRate * @productCost) - (@campaignCostPerVideo * @numberOfVideos)) AS net_profit
FROM
    ChannelData


-- 4.
WHERE
    channel_name IN ('GRM Daily', 'Man City', 'YOGSCAST Lewis & Simon ')


-- 5.
ORDER BY
    net_profit DESC;
```

#### Output

![Most videos](/docs/assets/images/youtubers_with_the_most_videos.png)

### 3. YouTubers com mais visualizações

#### Descrição do Cálculo

Ideia de campanha = Influencer marketing

a. DanTDM

- Average views per video = 5.34 million
- Product cost = $5
- Potential units sold per video = 5.34 million x 2% conversion rate = 106,800 units sold
- Potential revenue per video = 106,800 x $5 = $534,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $534,000 - $130,000 = $404,000**

b. Dan Rhodes

- Average views per video = 11.15 million
- Product cost = $5
- Potential units sold per video = 11.15 million x 2% conversion rate = 223,000 units sold
- Potential revenue per video = 223,000 x $5 = $1,115,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $1,115,000 - $130,000 = $985,000**

c. Mister Max

- Average views per video = 14.06 million
- Product cost = $5
- Potential units sold per video = 14.06 million x 2% conversion rate = 281,200 units sold
- Potential revenue per video = 281,200 x $5 = $1,406,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $1,406,000 - $130,000 = $1,276,000**

Best option from category: Mister Max

#### SQL query

```sql
/*
# 1. Defina variáveis
# 2. Crie um CTE que arredonda a média de visualizações por vídeo
# 3. Selecione as colunas que você precisa e crie colunas calculadas a partir das existentes
# 4. Filtre os resultados por canais do YouTube
# 5. Ordene os resultados por lucros líquidos (do maior para o menor)
*/



-- 1.
DECLARE @conversionRate FLOAT = 0.02;        -- The conversion rate @ 2%
DECLARE @productCost MONEY = 5.0;            -- The product cost @ $5
DECLARE @campaignCost MONEY = 130000.0;      -- The campaign cost @ $130,000



-- 2.
WITH ChannelData AS (
    SELECT
        channel_name,
        total_views,
        total_videos,
        ROUND(CAST(total_views AS FLOAT) / total_videos, -4) AS avg_views_per_video
    FROM
        youtube_db.dbo.view_uk_youtubers_2024
)


-- 3.
SELECT
    channel_name,
    avg_views_per_video,
    (avg_views_per_video * @conversionRate) AS potential_units_sold_per_video,
    (avg_views_per_video * @conversionRate * @productCost) AS potential_revenue_per_video,
    (avg_views_per_video * @conversionRate * @productCost) - @campaignCost AS net_profit
FROM
    ChannelData


-- 4.
WHERE
    channel_name IN ('Mister Max', 'DanTDM', 'Dan Rhodes')


-- 5.
ORDER BY
    net_profit DESC;

```

#### Output

![Most views](/docs/assets/images/youtubers_with_the_most_views.png)

## Descoberta

- O que aprendemos?

Aprendemos que

1. NoCopyrightSOunds, Dan Rhodes e DanTDM são os canais com mais assinantes no Reino Unido
2. GRM Daily, Man City e Yogscast são os canais com mais vídeos enviados
3. DanTDM, Dan RHodes e Mister Max são os canais com mais visualizações
4. Canais de entretenimento são úteis para alcance mais amplo, pois os canais que postam consistentemente nos seus plataformas e geram mais engajamento são focados em entretenimento e música

## Recomendações

- O que você recomenda com base nas descobertas obtidas?

1. Dan Rhodes é o melhor canal do YouTube para colaborar se quisermos maximizar visibilidade porque este canal tem mais assinantes do YouTube no Reino Unido
2. Embora GRM Daily, Man City e Yogcasts sejam editores regulares nos YouTube, pode ser que valha a pena considerar se colaborar com eles com o orçamento atual caps são um esforço para o retorno do investimento, pois o retorno do investimento potencial é significativamente menor comparado aos outros canais.
3. Mister Max é o melhor YouTuber para colaborar se estivermos interessados em maximizar alcance, mas colaborar com DanTDM e Dan Rhodes pode ser uma opção melhor de longo prazo considerando o fato de que ambos têm grandes bases de assinantes e estão média significativamente alto número de visualizações.
4. Os 3 canais principais para formar colaborações são NoCopyrightSounds, DanTDM e Dan Rhodes com base desta análise, porque eles atraem mais engajamento nos seus canais consistentemente.

### ROI Potencial

- Qual ROI esperamos se tomarmos este curso de ação?

1. Configurar um acordo de colaboração com Dan Rhodes faria o cliente um lucro líquido de $1,065,000 por vídeo
2. Um contrato de marketing de influenciador com Mister Max pode ver o cliente gerar um lucro líquido de $1,276,000
3. Se optarmos por uma campanha de colocação de produtos com DanTDM, isso poderia gerar o cliente aproximadamente $484,000 por vídeo. Se avançarmos com um acordo de marketing de influenciador, isso faria o cliente um lucro líquido de um único de $404,000.
4. NoCopyrightSounds poderia lucrar o cliente $642,000 por vídeo também (o que também vale considerar)

### Action plan

- Qual curso de ação devemos tomar e por quê?

Com base em nossa análise, acreditamos que o melhor canal para avançar um acordo de parceria de longo prazo para promover os produtos do cliente é o canal Dan Rhodes.

Vamos ter conversas com o cliente de marketing para prever o que eles também esperam desta colaboração. Uma vez observamos que estamos atingindo os marcos esperados, avançaremos com possíveis parcerias com canais NoCopyrightSounds, Mister Max e DanTDM no futuro.

- Quais etapas tomamos para implementar as decisões recomendadas de forma eficaz?

1. Entrar em contato com as equipes por trás de cada um desses canais, começando com Dan Rhodes
2. Negociar contratos dentro dos orçamentos alocados para cada campanha de marketing
3. Iniciar as campanhas e rastrear o desempenho de cada uma contra os KPI
4. Revisar como as campanhas foram, coletar insights e otimizar com base em feedback de clientes convertidos e públicos de cada canal
