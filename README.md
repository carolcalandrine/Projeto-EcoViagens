<p align="center">
  <img src="3.%20Relatório/logo.png" width="750"/>
</p>

## Contexto do Projeto

A EcoViagens é uma plataforma brasileira de turismo sustentável, dedicada à oferta de experiências ecológicas em parceria com operadores locais. Seu objetivo é promover práticas que gerem impacto positivo tanto para o meio ambiente quanto para as comunidades envolvidas. A base de dados disponível contempla diferentes dimensões e métricas, incluindo informações sobre reservas, operadores, atividades e indicadores relacionados à sustentabilidade.

Neste contexto, o presente projeto utiliza um conjunto de dados fictícios com o objetivo de analisar e avaliar o desempenho da EcoViagens no período de junho de 2024 a junho de 2025. A análise busca gerar insights relevantes para o monitoramento da performance da plataforma, apoiando a tomada de decisões estratégicas e orientadas por dados.

A partir disso, foram definidos os seguintes Indicadores-Chave de Desempenho (KPIs):

**Receita Bruta por Mês:** mensurar o volume de vendas e o nível de adesão dos clientes à plataforma;
**Taxa de Cancelamento:** identificar possíveis falhas operacionais e níveis de insatisfação dos clientes;
**Avaliação Média:** avaliar a satisfação dos usuários e a qualidade percebida dos serviços;
**Média de Práticas Sustentáveis:** mensurar o nível de adesão às práticas sustentáveis por parte dos operadores e experiências oferecidas.


## Modelagem dos Dados


A modelagem dos dados foi desenvolvida com o objetivo de organizar as informações de forma estruturada com o Diagrama de Entidade e Relacionamento (DER).
O modelo foi construído considerando as todas entidades do negócio, como:
- Ofertas
- Reservas
- Práticas Sustentáveis
- Avaliação

Essa estrutura facilita a análise no SQL e a construção de dashboards no Power BI.
![Diagrama](1.%20Modelagem-dados/diagrama.png)

Componentes de dados principais:

- Informações das reservas: identificadores, datas e o número e status dessas reservas.
- Detalhes dos Operadores: empresas ou guias que oferecem essas experiências
- Ofertas: identificador, tipo de oferta e o preço
- Dados de Clientes: nome, email, data de nascimento e cidade.
- Detalhes Avaliação: notas, comentários e data dessa avaliação.
- Práticas Sustentáveis: os tipos de prática, como...

## Análise dos Dados via SQL

Com os dados estruturados no ambiente relacional, foram desenvolvidas consultas SQL analíticas com o objetivo de responder às principais questões de negócio da plataforma EcoViagens.
Entre as análises realizadas, destacam-se:

- Como evolui o volume de reservas ao longo do tempo?  
- Quais períodos apresentam maior concentração de demanda?  
- Como se comporta o desempenho das ofertas e experiências?  
- Existem padrões relevantes no comportamento dos usuários?

As análises foram realizadas utilizando o Google BigQuery por ter alta escalabilidade, e pela velocidade da consulta com grande quantidade de dados.

**Exemplo de análise: Receita por período**<br>
A consulta abaixo foi utilizada para calcular a receita total ao longo do tempo:
```sql
SELECT
  EXTRACT(YEAR FROM data_reserva) AS ano,
  EXTRACT(MONTH FROM data_reserva) AS mes,
  FORMAT_DATE('%b', DATE(data_reserva)) AS mes_abrev,
  COUNT(*) AS qtd_reservas
FROM `ecoviagens-484814.plataforma.reservas`
WHERE UPPER(status) = 'CONCLUÍDA'
GROUP BY 
  ano, mes, mes_abrev
ORDER BY 
  ano ASC, mes ASC;
```

## Dashboard de Desempenho da Plataforma

Este projeto conta com um dashboard interativo desenvolvido no Power BI que permite analisar e monitorar o desempenho 

Gráficos:
- Visualização das Receitas e Reservas ao longo tempo
- DIstribuição de Reservas e Tickets Médios por tipo de oferta
- Avaliação do Cliente ao longo do tempo e por tipo de oferta
- Comparação das receitas das Práticas Sustentáveis e a popularidade

Monitoramento:
- Acompanhamento das métricas de desempenho: taxa de fidelização e cancelamento
- Monitoramento das:
  - Reservas concluídas
  - Receita total
  - Ticket médio
  - Avaliação média

![Relatório](3.%20Relatório/dashboard%20DS.png)

![Relatório](3.%20Relatório/dashboard%20DQ.png)

## Conclusão & Recomendações

Essa análise dos dados da plataforma Ecoviagens revelou alguns insights sobre fatores que influenciam... Nesse sentido, serão destacados os principais achados nesse estudo.

- A plataforma apresenta um volume total de **791 reservas concluídas**, indicando uma base ativa de utilização, porém ainda com potencial de crescimento

- Observa-se uma concentração de reservas em meses específicos, possivelmente associado a **períodos de férias e maior disponibilidade dos clientes**

- A maior parte das reservas está associada a **ofertas com práticas sustentáveis**, indicando que esse fator pode influenciar positivamente a decisão dos clientes

- A receita apresenta **variação ao longo dos meses**, acompanhando o volume de reservas, o que reforça a relação direta entre demanda e faturamento da plataforma

- A avaliação média de **2,99** indica um nível de satisfação **abaixo do ideal**, sugerindo a necessidade de melhorias na experiência do cliente

Nesse sentido, é importante ressaltar que, para melhorar o ambiente organizacional, existem algumas recomendações adicionais:

1. 
