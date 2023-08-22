
# Hands-On Integration Suite (ES) 

Demos una descripción general de qué es (Cloud Integration) y cuáles son sus características.

Básicamente, fue construido para ser el sucesor del antiguo integrador PI/PO. Con eso, hablemos de algunas de las ventajas que tenemos al usar (Cloud Integration).

Abramos la URL de nuestro Cloud Integration.

https://dev-amazon-web-services-ncm543yw.authentication.us10.hana.ondemand.com/login



## Paso a paso

- [Entrar al sistema](https://shields.io/)

- [Entrar al sistema](https://shields.io/)


## Screenshots
Paso 1
![Login](/images/Login.jpg)
![Initial Page](/images/Initial-Page.jpg)
![Initial Page](/images/Initial-Page-Integration.jpg)
![Initial Page](/images/Create-Packge.jpg)
![Initial Page](/images/Create-Packge-Info.jpg)
![Initial Page](/images/Create-Packge-Artifacts.jpg)
![Initial Page](/images/Create-Integration-Flow.jpg)
![Initial Page](/images/Create-Integration-Flow-Info.jpg)
![Initial Page](/images/Integration-Flow-Open.jpg)
![Initial Page](/images/Integration-Flow-Edit.jpg)



![Initial Page](/images/Exe1-Set-URL-to-Start-Integration.jpg)
![Initial Page](/images/Exe1-Set-URL-to-Start-Integration-Info.jpg)

![Initial Page](/images/Exe1-Add-first-flow-step.jpg)
![Initial Page](/images/Exe1-crete-groovy-get-city.jpg)
![Initial Page](/images/Exe1-crete-groovy-script.jpg)
![Initial Page](/images/Exe1-crete-groovy-script-save.jpg)
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
![Initial Page](/images/Exe1-change-name-groovy-script.jpg)
![Initial Page](/images/Exe1-add-request-reply.jpg)
![Initial Page](/images/Exe1-change-name-request-reply-city1.jpg)
![Initial Page](/images/Exe1-change-name-request-reply-city2.jpg)
![Initial Page](/images/Exe1-request-reply-city-connector.jpg)
![Initial Page](/images/Exe1-request-reply-city-http.jpg)
![Initial Page](/images/Exe1-request-reply-city-http-info-connection.jpg)
información:

https://api-colombia.com/api/v1/City/name/${property.city}

![Initial Page](/images/Exe1-request-reply-city-save.jpg)

![Initial Page](/images/Exe1-request-reply-city-deploy.jpg)
![Initial Page](/images/Exe1-request-reply-city-deploy-1.jpg)
![Initial Page](/images/Exe1-request-reply-city-deploy-2.jpg)
![Initial Page](/images/Exe1-view-integration.jpg)
![Initial Page](/images/Exe1-view-integration-all-integrations.jpg)
![Initial Page](/images/Exe1-view-integration-get-url.jpg)
AQUII
![TESTE](/images/Exe1-Test-create-collection.jpg)
![Initial Page](/images/Exe1-Test-create-collection-name.jpg)
![Initial Page](/images/Exe1-Test-create-request.jpg)
![Initial Page](/images/Exe1-Test-create-request-name.jpg)
![Initial Page](/images/Exe1-Test-create-request-url-method.jpg)
![Initial Page](/images/Exe1-Test-create-request-set-body.jpg)
![Initial Page](/images/Exe1-Test-create-request-set-body-json.jpg)
![Initial Page](/images/Exe1-Test-create-request-set-auth.jpg)
![Initial Page](/images/Exe1-Test-request-send.jpg)

![Initial Page](/images/XXXXXXx.jpg)
![Initial Page](/images/XXXXXXx.jpg)
![Initial Page](/images/XXXXXXx.jpg)
![Initial Page](/images/XXXXXXx.jpg)
![Initial Page](/images/XXXXXXx.jpg)
![Initial Page](/images/XXXXXXx.jpg)




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

## Groovy set JSON to S4

```groovy
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import groovy.json.*;

def Message processData(Message message) {
    
    def body = message.getBody(String)
    def jsonParser = new JsonSlurper()
    def jsonObject = jsonParser.parseText(body)
    def builder = new JsonBuilder()
    println(jsonObject.size)
    if (jsonObject.size > 0){
        def obj = jsonObject[0]
        def json = builder {
            "CREATEBY" new String(message.getProperty("name").getBytes("UTF8"))
            "ID" obj.id ?: 0
            "DESCRIPTION" obj.description ?: ""
            "NAME" obj.name ?: ""
            "SURFACE" obj.surface ?: 0
            "POPULATION" obj.population ?: 0
            "POSTALCODE" obj.postalCode ?: ""
            "DEPARTMENTID" obj.departmentId ?: ""
            "DEPARTMENT" obj.department ?: ""
            "TOURISTATTRACTIO" obj.touristAttractions ?: ""
            "PRESIDENTS" obj.presidents ?: ""
        }

        message.setBody(JsonOutput.prettyPrint(JsonOutput.toJson(json)))
    }else{
        message.setBody()
    }
  
    return message;
}
```

