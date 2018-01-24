# 1. Introdução

O presente documento tem como objetivo especificar os interfaces necessários para a implementação do workflow de integração com o produto de gestão hospitalar HMS-PACS.

O interface será implementado com recurso ao standard HL7, na sua versão 2.4. 
O documento pressupõe conhecimento prévio e consolidado acerca do standard.

***

# 2. Especificação técnica

Neste capitulo, encontram-se especificadas as mensagens a trocar no âmbito dos interfaces com o HMS-PAS bem como a identificação dos campos mais relevantes a incluir nas mesmas e o respetivo significado. Podem também ser consultados alguns exemplos de mensagens válidas no respetivos interfaces.

##  2.1. Patient Administration

Os eventos descritos abaixo apenas são suportados numa determinada instituição caso a solução de gestão hospitalar (HIS) da Glintt HS esteja instalada.

### 2.1.1. ADT^A08 - Update Patient Information

![ADT^A08](adt^a08_gh.png)

##### 2.1.1.1. Âmbito

Esta mensagem é utilizada para notificar os sistemas de destino de que ocorreu uma alteração dos dados demográficos de um dado utente. Pode também ser utilizada para notificar outros eventos como sejam a mudança de responsável por um utente, ou o seu falecimento, através de uma notificação do óbito.

##### 2.1.1.2. Segmentos suportados

| ADT^A08^ADT_A01 | Descrição do segmento            |
|:---------------:|:---------------------------------|    
| MSH		  	  |Message header                  	 |        
| EVN  	 	      |Event type			    		 |
| PID		  	  |Patient identification            |        
| [{ NK1 }]  	  |Next of Kin / Associated Parties  |
| PV1		  	  |Patient visit                  	 |        
| [{  	 	      |--- INSURANCE begin			     |
| IN1		  	  |Insurance                  	 	 |        
| IN2  	 	      |Insurance Additional Info	     |
| }]		  	  |--- INSURANCE end                 |        
| [{ NTE }]  	  |Notes and Comments 			     |

##### 2.1.1.3. Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente (GH)                  |        
| PID.5   |Nome do utente			    			 |
| PID.7   |Data de nascimento                   					 | 
| PID.8   |Sexo                   					 |        
| PID.11  |Morada			    			 		 |
| PID.13  |Contactos			    			 	 |
| PID.19  |Número de SNS			    			 |

##### 2.1.1.4. Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766||||
PV1||N|
```

### 2.1.2. Detalhe dos segmentos

##### 2.1.2.1. PID

| Campo   					   | Tipo de dados |Descrição 				   | Campo HL7 |
|:----------------------------:|:-------------:|:--------------------------|:---------:| 
| Patient Identifier List - ID |VARCHAR(12)    |Identificador do utente    | PID.3.1   |

***

##  2.2. Order Management

Os eventos descritos abaixo apenas são suportados numa determinada instituição caso a solução de gestão hospitalar (HIS) da Glintt HS esteja instalada.

#### 2.2.1. OML^O21 - Order management laboratory 
