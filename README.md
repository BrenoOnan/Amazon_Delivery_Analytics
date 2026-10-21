# Amazon_Delivery_Analytics

Análise de logística e tempo de entrega (Supply Chain). Abordando prototipagem no Excel e automação de ETL e dashboards com Power Query e Power BI. Dados oficiais da **Amazon Delivery**

# Tratamento e limpeza dos dados

Os dados passaram por um processo de limpeza e organização, incluindo a remoção de 4 colunas de longitude que não seriam utilizadas na análise. Também foi criada uma nova coluna chamada status_entrega, para classificar as entregas como Rápidas, Regulares ou Atrasadas, utilizando o tempo médio geral de entrega como referência.

Durante o processo, foram identificadas 90 linhas com dados ausentes ou incompletos, incluindo valores de order_time, traffic e weather. Para organizar essas informações, os valores ausentes de order_time foram definidos como null, enquanto os campos vazios de traffic e weather foram preenchidos com "Não informado", entrando como dados que não foram informado.

Após essas etapas, os dados ficaram organizados e preparados para a criação dos indicadores e dashboards no Power BI.

# Objetivo

Além de apresentar indicadores sobre a eficiência das entregas por veículo, tráfego e região, decidi criar 3 KPIs para destacar os status das entregas: Rápida, Regular e Atrasada. Dessa forma, durante a análise do dashboard, é possível avaliar o desempenho das entregas em cada área e identificar possíveis gargalos que podem estar afetando a eficiência do delivery.

Também foram criados 3 gráficos: Área, Veículo e Tráfego, tornando o dashboard dinâmico e permitindo cruzar informações para analisar situações específicas, como o desempenho de cada veículo em determinada área. Assim, é possível explorar os dados de diferentes formas e identificar fatores que podem influenciar o tempo de entrega.

# 🧠 Modelagem e Medidas DAX

Para alimentar os KPIs e garantir a dinâmica do relatório, foram criadas medidas estruturadas em DAX, divididas entre métricas base, contagens segmentadas e cálculo de contexto.

## 1. Medida Base (Volume Total de Entregas)

Como a base trabalha com identificadores alfanuméricos, utilizou-se a contagem de linhas para estabelecer o total de pedidos:

```dax
Total Pedidos = COUNTROWS(amazon_delivery)
```

## 2. Status de Entrega

```dax
Pedidos Atrasados = 
FORMAT(
    CALCULATE(
        [Total Pedidos],
        amazon_delivery[status_entrega] = "atrasada"
    ),
    "#,##0"
)
```

Ela separa cada status dentro da coluna de status_entrega, sendo possível criar cada KPI separado com o seu respectivo valor. O mesmo foi feito para Rápida e Regular.

## 3. Percentuais de status da entrega (Distribuição)

```dax
% Atrasado = 
DIVIDE(
    CALCULATE([Total Pedidos], amazon_delivery[status_entrega] = "atrasada"),
    [Total Pedidos],
    0
)
```

Dentro do rótulo de referência do KPI, vai indicar a porcentagem da eficiência das entregas.

## 4. Percentual geral de representatividade por área

```dax
% Pedidos Rótulo = 
VAR Pct = DIVIDE([total pedidos], CALCULATE([total pedidos], ALL(amazon_delivery[Area])), 0)
VAR AreaNome = SELECTEDVALUE(amazon_delivery[Area], "Total")

RETURN
IF(
    ISFILTERED(amazon_delivery[Area]),
    AreaNome & ": " & FORMAT(Pct, "0.0%"),
    "100% do total"
)
```

Por ser uma medida avançada, conversei com a IA e procurei a melhor forma de representar o valor percentual dentro deste indicador.


👉 [Clique aqui para ver os Insights e Respostas de Negócio](./powerbi_solution/insights_respostas.md).
