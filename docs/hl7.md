#Introdução

Este documento contém a especificação técnica de integração entre o sistema Globalcare, da Glintt, e sistemas informáticos terceiros, recorrendo ao protocolo HL7. As mensagens especificadas estão em conformidade com a versão v2.4 do protocolo, versão utilizada nesta especificação.

##Message encoding

A codificação de caracteres especiais é especificada pela norma ISO 8859-15. Apenas são permitidos caracteres US-ASCII. Todos os restantes caracteres devem ser escaped em hexadecimal no formato definido pelo standard \Xxxx\. 

**Exemplo:** O Jo\XE3\o encontra-se de p\XE9\ssima sa\XFA\de!

***

#Common

###MSH

###EVN

###MSA

###NTE

***

#Patient Administration

##ADT^A01 - Admit/Visit Notification

![ADT^A01](adt^a01.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```


##ADT^A04 - Register a Patient

![ADT^A04](adt^a04.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ADT^A08 - Update Patient Information

![ADT^A08](adt^a08.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```
 
##ADT^A34 - Merge Patient Information - Patient ID only

![ADT^A34](adt^a34.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ADT^A02 - Transfer a Patient

![ADT^A02](adt^a02.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ADT^A03 - Discharge/End Visit

![ADT^A03](adt^a03.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ADT^A11 - Cancel Admit/Visit Notification

![ADT^A11](adt^a11.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ADT^A13 - Cancel Discharge/End Visit

![ADT^A13](adt^a13.png)

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

***

#Order Management

##OML^O21 - Laboratory Order Management

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

##ORL^O22 - General Laboratory Order Response Message To Any ORL

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

***

#Observation Reporting

##ORU^R01 - Unsolicited Observation Management

####Campos relevantes

| Campo   | Descrição                                |
|:-------:|:-----------------------------------------|    
| PID.3.1 |Identificador do utente                   |        
| PID.5   |Nome do utente			    			 |

####Exemplos

```
MSH|^~\&|GH|CHLN|CHLN-B|CHLN|20180105102001||ADT^A08|28526100|P|2.4|||AL
EVN|A28|20180105102001
PID||||129423084^^^NIF^PT~10140648944^^^N_BENEF~6227141^^^N_BI|TESTES^UTENTE DE||19550527000000|F||||||||S|||99887766|||||||||||||||||||
PV1||N|
```

