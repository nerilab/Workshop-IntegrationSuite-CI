
# Hands-On Integration Suite (ES) 

Demos una descripción general de qué es (Cloud Integration) y cuáles son sus características.

Básicamente, fue construido para ser el sucesor del antiguo integrador PI/PO. Con eso, hablemos de algunas de las ventajas que tenemos al usar (Cloud Integration).

Abramos la URL de nuestro Cloud Integration.

https://dev-amazon-web-services-ncm543yw.integrationsuite.cfapps.us10-002.hana.ondemand.com/shell/home



## Paso a paso

- Consumir la API de la Colombia

- Enviar para el S4

## Passo 1

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
![TESTE](/images/Exe1-request-reply-city-save.jpg)
![Initial Page](/images/Exe1-Test-create-collection-name.png)
![Initial Page](/images/Exe1-Test-create-request.png)
![Initial Page](/images/Exe1-Test-create-request-name.png)
![Initial Page](/images/Exe1-Test-create-request-url-method.png)
![Initial Page](/images/Exe1-Test-create-request-set-body.png)
![Initial Page](/images/Exe1-Test-create-request-set-body-json.png)
![Initial Page](/images/Exe1-Test-create-request-set-auth.png)
![Initial Page](/images/Exe1-Test-request-send.png)

## Paso 2
![Initial Page](/images/Exe2-Create-local-integrate-process.png)
![Initial Page](/images/Exe2-Create-local-integrate-process-change-name.png)
![Initial Page](/images/Exe2-Local-integrate-process-add-groovy.png)
![Initial Page](/images/Exe2-Local-integrate-process-add-groovy2.png)
![Initial Page](/images/Exe2-Local-integrate-process-rename-groovy.png)
![Initial Page](/images/Exe2-Local-integrate-process-groovy-script-code.png)
![Initial Page](/images/Exe2-Local-integrate-process-groovy-script-code-save-antes.png)
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

![Initial Page](/images/Exe2-Local-integrate-process-call-local-process.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-change-name.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-select-local-process.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-select-local-process2.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-create-content.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-create-content2.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-create-content3.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-content-set-header.png)
x-csrf-token : fetch

![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-content-set-exchange.png)
jsonS4 : ${in.body}

![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-create-request-reply.png)
![Initial Page](/images/Exe2-Local-integrate-process-call-local-process-rename-request-reply.png)
![Initial Page](/images/Exe2-Local-integration-configure-comunicacion.png)
![Initial Page](/images/Exe2-Local-integration-configure-comunicacion2.png)
![Initial Page](/images/Exe2-Local-integration-configure-reciver.png)
<p>http://187.75.172.242:9222/sap/opu/odata/sap/ZGW_WORKSHOP_SAP_SRV/CitySet</p>
<p>S4_LAB</p>
<p>x-crsf-token</p>


![Initial Page](/images/Exe2-Local-integration-create-groovy.png)
![Initial Page](/images/Exe2-Local-integration-create-groovy2.png)
![Initial Page](/images/Exe2-Local-integration-create-groovy3.png)
![Initial Page](/images/Exe2-Local-integration-create-groovy-code-save.png)
## Groovy set cookie

```groovy
import com.sap.gateway.ip.core.customdev.util.Message;
import groovy.xml.*;
import java.io.*;
 
def Message processData(Message message) 
{
    def headers = message.getHeaders();
    def cookie = headers.get("Set-Cookie");
    StringBuffer bufferedCookie = new StringBuffer();
    for (Object item : cookie) 
    {
        bufferedCookie.append(item + "; ");      
    }
    message.setHeader("Cookie", bufferedCookie.toString());
    
    
    def messageLog = messageLogFactory.getMessageLog(message);
    if(messageLog != null)
    {
        messageLog.setStringProperty("Logging_Cookie", bufferedCookie.toString());
    }
    return message;
}
```

![Initial Page](/images/Exe2-Local-integration-create-groovy-code-rename.png)
![Initial Page](/images/Exe2-Local-integration-create-content-modify.png)
![Initial Page](/images/Exe2-Local-integration-rename-content-modify.png)
![Initial Page](/images/Exe2-Local-integration-create-content-modify-header2.png)
<p>X-Requested-With : X</p>
<p>Content-Type : application/json</p>

![Initial Page](/images/Exe2-Local-integration-content-modify-set-jsonbody.png)
<p>${property.jsonS4}</p>

![Initial Page](/images/Exe2-Local-integration-create-request-to-s4.png)
![Initial Page](/images/Exe2-Local-integration-create-reciver-s4.png)
![Initial Page](/images/Exe2-Local-integration-create-connection-with-request-to-reciver.png)
![Initial Page](/images/Exe2-Local-integration-setting-http-s4.png)

![Initial Page](/images/Exe2-Local-integration-http-configs.png)
<p>http://187.75.172.242:9222/sap/opu/odata/sap/ZGW_WORKSHOP_SAP_SRV/CitySet</p>
<p>S4_LAB</p>

![Initial Page](/images/Exe2-Local-integration-deploy-application.png)

![Initial Page](/images/Exe2-Teste-integracion.png)


https://api-colombia.com/
https://api-colombia.com/swagger/index.html


