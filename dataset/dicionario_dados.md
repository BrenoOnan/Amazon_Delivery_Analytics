# 📖 Dicionário de Dados - Amazon Delivery Analytics

Este documento descreve as variáveis presentes na base de dados bruta (`amazon_delivery.csv`) utilizada no projeto de análise de tempo de entrega e logística.

| Nome da Coluna | Tipo de Dado | Descrição |
| :--- | :--- | :--- |
| **Order_ID** | Texto | Identificador único de cada pedido realizado. |
| **Agent_Age** | Número Inteiro | Idade do entregador (agente) responsável pela entrega. |
| **Order_Rating** | Texto / Numérico | Avaliação dada pelo cliente ao pedido/entrega. *Contém alguns valores nulos que precisam de tratamento.* |
| **Order_Date** | Data | Data em que o pedido foi realizado pelo cliente. |
| **Order_Time** | Hora | Horário exato em que o pedido foi registado no sistema. |
| **Pickup_Time** | Hora | Horário em que o entregador retirou o pedido no centro de distribuição/loja para iniciar a rota. |
| **Weather** | Texto | Condição climática no momento da entrega (ex: *Sunny, Stormy, Fog, Sandstorms*). |
| **Traffic** | Texto | Condição do trânsito na região durante a rota (ex: *High, Jam, Low, Medium*). |
| **Vehicle** | Texto | Tipo de veículo utilizado pelo entregador (ex: *motorcycle, scooter, van, bicycle*). |
| **Area** | Texto | Classificação da área geográfica da entrega (ex: *Urban, Metropolitan, Semi-Urban*). |
| **Delivery_Time** | Número Inteiro | Tempo total de entrega (em minutos) decorrido entre a recolha do pedido e a chegada ao cliente final. |
| **Category** | Texto | Categoria do produto comprado pelo cliente (ex: *Electronics, Clothing, Grocery*). |


---

### 🛠️ Notas sobre o Tratamento de Dados (ETL)
Durante a importação da base de dados original, constatou-se a presença de três colunas residuais e vazias (`Unnamed: 12`, `Unnamed: 13` e `Unnamed: 14`). Estas colunas foram geradas por erros de formatação na exportação do sistema de origem e foram **removidas** durante a etapa de limpeza e transformação de dados no Power Query.
E colunas latitude que foram excluidas, são dados que não serão utilizados.