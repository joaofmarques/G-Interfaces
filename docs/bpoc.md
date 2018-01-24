# Introdução

O presente documento tem como objetivo detalhar os interfaces necessários para a implementação do workflow de integração com o produto BPOC.

O interface será implementado com recurso ao standard HL7, na sua versão 2.4. 

# Especificação funcional



## Workflow

Apesar do diagrama abaixo fazer referência a produtos Globalcare, pretende-se que o fluxo a implementar seja agnóstico relativamente ao ecossistema onde se encontra inserido, funcionando de forma semelhante consoante integra com produtos internos ou com produtos de terceiros.

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
| **1** |Quando é realizada uma requisição de um MCDT que implique uma colheita, esta deve ser notificada ao BST. **Informação a passar para BST:** Número da requisição, prioridade, data do pedido, informação clínica e estado. Em simultâneo com o envio dos dados da requisição, deve ser também passado o histórico de problemas, diagnósticos, alergias e reacções adversas ativas do utente.|CLINICAL-MED|BST;SIBAS;SISLAB|        
| **2** |Quando a informação de uma requisição com colheita pendente é atualizada, esta deve ser também atualizada no BST.|CLINICAL-MED|BST;SIBAS;SISLAB|        
| **3** |Quando uma requisição com colheita pendente é cancelada, o BST deve ser informado.|CLINICAL-MED|BST;SIBAS;SISLAB|        
| **4** |O BST irá receber todas as atualizações de utentes ocorridas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **5** |O BST irá receber todas as fusões de utentes ocorridas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **6** |O BST irá receber todas as notificações de óbitos registados no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **7** |O BST irá receber todas as admissões registadas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **8** |O BST irá receber todos os cancelamentos de admissões registados no HMS-PAS, devendo descartar aqueles que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **9** |O BST irá receber todas as transferências registadas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **10** |O BST irá receber todas as altas registadas no HMS-PAS, devendo descartar aquelas que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **11** |O BST irá receber todos os cancelamentos de altas registados no HMS-PAS, devendo descartar aqueles que se refiram a utentes que não existam no sistema.|HMS-PAS     |BST  	      |
| **12** |O laboratório pode adicionar MCDTs à requisição. Esta situação deve ser comunicada ao BST e CLINICAL-MED|SIBAS;SISLAB|BST;CLINICAL-MED|
| **13** |O laboratório pode cancelar MCDTs constantes da requisição. Esta situação deve ser comunicada ao BST e CLINICAL-MED|SIBAS;SISLAB|BST;CLINICAL-MED|
| **14** |Cada nova colheita disponibilizada no BST deve estar visível para a enfermagem, como tal deve ser criado na enfermagem uma intervenção no Clinical-ENF.     		      |BST         |CLINICAL-ENF|
| **15** |A informação dos tubos deve ser fornecida ao BST pelos serviços executantes.|SIBAS;SISLAB|BST  	      |
| **16** |A relação entre os MCDTs a colher e os respetivos tubos deve ser enviada ao BST.|SISLAB      |BST  	      |
| **17** |O SISLAB deve enviar ao BST os procedimentos associados aos tubos. A colheita do tubo em questão deve ter em conta o tempo em minutos que depende do procedimento.       		|SISLAB      |BST  	      |
| **18**|No SISLAB, cada análise pode ter um conjunto de informações associadas. Essas informações devem ser enviadas para o BST, sendo que no SISLAB já contém o valor da chave a introduzir no BST.|SISLAB      |BST  	      |
| **19** |No BST vai ser possível o registo de observações da colheita associadas ao doente. Essas observações registadas devem ser integradas no Clinical-ENF.       		       |BST         |CLINICAL-ENF|
| **20** |A impressão de etiquetas deve ser notificada ao SISLAB.|BST         |SISLAB	  |
| **21** |Quando uma colheita é registada no BST, esse evento deve ser notificado aos sistemas subscritores.|BST         |HMS-PAS;SIBAS;SISLAB|
| **22** |Quando uma amostra é cancelada no BST, esse evento deve ser notificado aos sistemas subscritores.|BST         |HMS-PAS;SIBAS;SISLAB|
| **23** |Para cada amostra colhida, o laboratório pode inativar uma amostra e pedir uma nova. Quando o laboratório pedir nova amostra, o interface deve colocar a amostra no BST como rejeitada com o respetivo motivo, e criar uma nova amostra pendente de colheita com a informação a ser disponibilizada pelo laboratório.|SISLAB      |BST  	      |
| **24** |As unidades sanguíneas devem ser disponibilizadas no BST a partir do momento que for dada essa indicação no SIBAS.|SIBAS       |BST  	      |
| **25** |Sempre que o estado de uma transfusão é alterado do lado do BST, esta deve ser notificada para os sistemas subscitores.|BST         |SIBAS	  	  |
| **26** |Sempre que são efetuados registos de sinais vitais no BST, esta informação deve ser notificada para os sistemas subscitores.|BST         |CLINICAL-ENF;SIBAS|
| **27**|Sempre que são efetuados registos de reacções adversas no BST, esta informação deve ser notificada para os sistemas subscitores.|BST         |CLINICAL-MED;SIBAS|

#### 4. MCDT Order Management

| # | Descrição                                 | Origem     | Destino    |
|:-:|:----------------------------------------- |:----------:|:----------:| 
| **1** | |EHR|BedsideNurse|  

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

##Conectores

De forma a montar o circuito funcional especificado, será necessário instalar os seguintes conectores de integração:

