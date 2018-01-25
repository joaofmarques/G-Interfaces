# Introdução

O presente documento tem como objetivo detalhar os interfaces necessários para a implementação do workflow de integração com uma solução BPOC.


# Especificação funcional



## Workflow

O diagrama abaixo faz referência a um conjunto de interações entre sistemas que determinam o fluxo de informação a implementar com vista à disponibilização de uma solução de BPOC totalmente integrada. Este fluxo deve ser agnóstico relativamente a quaisquer que sejam os sistemas residentes no ecossistema onde se pretender instalar a solução, funcionando numa lógica de ativação de serviços.

![Workflow](bpoc.png)

#### 1. Master Files

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |HIS|BedsideNurse| 

#### 2. Master Files (Medication)

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |Pharmacy/Logistics|BedsideNurse|  

#### 3. Patient Basic Administration

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:|           
| **1** |O BedsideNurse irá receber todas as atualizações de utentes ocorridas no HIS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **2** |O BedsideNurse irá receber todas as fusões de utentes ocorridas no HIS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **3** |O BedsideNurse irá receber todas as notificações de óbitos registados no HIS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **4** |O BedsideNurse irá receber todas as admissões registadas no HIS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **5** |O BedsideNurse irá receber todos os cancelamentos de admissões registados no HIS, devendo descartar aqueles que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **6** |O BedsideNurse irá receber todas as transferências registadas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **7** |O BedsideNurse irá receber todas as altas registadas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |
| **8** |O BedsideNurse irá receber todos os cancelamentos de altas registados no HMS-PAS, devendo descartar aqueles que se refiram a utentes que não existam no sistema.|HIS     |BedsideNurse  	      |

#### 4. MCDT Order Management

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** |Quando é realizada uma requisição de um MCDT que implique uma colheita, esta deve ser notificada ao BedsideNurse. **Informação a passar para BSN:** Número da requisição, prioridade, data do pedido, informação clínica e estado. Em simultâneo com o envio dos dados da requisição, deve ser também passado o histórico de problemas, diagnósticos, alergias e reacções adversas ativas do utente.|EHR|BedsideNurse|        
| **2** |Quando a informação de uma requisição com colheita pendente é atualizada, esta deve ser também atualizada no BedsideNurse.|EHR|BedsideNurse|        
| **3** |Quando uma requisição com colheita pendente é cancelada, o BedsideNurse deve ser informado.|EHR|BedsideNurse| 

#### 5. MCDT Harvest

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |LIS|BedsideNurse|  

#### 6. MCDT Transfusions

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |LIS|BedsideNurse|  

#### 7. Pharmacy Order Management

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |HIS|BedsideNurse|  

#### 8. Pharmacy Stock Movement

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |BedsideNurse|Pharmacy/Logistics|  

#### 9. Nursing Order Management

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |BedsideNurse|EHR|  


***

# Especificação técnica

O interface será implementado com recurso ao standard HL7, na sua versão 2.4. 

No capítulo abaixo, encontram-se detalhados todos os conectores de interfaces que são necessários instalar neste âmbito.

##Conectores

De forma a montar o circuito funcional especificado, será necessário instalar os seguintes conectores de integração:

