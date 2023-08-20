
# Hands-On Integration Suite (ES) 

Demos una descripción general de qué es (Cloud Integration) y cuáles son sus características.

Básicamente, fue construido para ser el sucesor del antiguo integrador PI/PO. Con eso, hablemos de algunas de las ventajas que tenemos al usar (Cloud Integration).

Abramos la URL de nuestro Cloud Integration.

https://dev-amazon-web-services-ncm543yw.authentication.us10.hana.ondemand.com/login



## Paso a paso

- [Entrar al sistema](https://shields.io/)

- [Entrar al sistema](https://shields.io/)


## Screenshots

![Login](https://github.com/nerilab/Workshop-IntegrationSuite-CI/blob/main/images/Login.jpg)


## Groovy Get Name and City

```groovy
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import groovy.json.*;

def Message processData(Message message) {
    
    def body = message.getBody(String)
    def jsonParser = new JsonSlurper()
    def jsonObject = jsonParser.parseText(body)

    message.setProperty("name", jsonObject.name)
    message.setProperty("city", jsonObject.city)
    
    return message;
}
```

https://api-colombia.com/
https://api-colombia.com/swagger/index.html