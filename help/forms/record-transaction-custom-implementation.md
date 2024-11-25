---
title: Registrar una transacción para implementaciones personalizadas
description: Utilice la API TransactionRecorder para registrar acciones que no se contabilizan como transacciones automáticamente.
feature: Adaptive Forms, Foundation Components
exl-id: cb584f78-30af-4a58-be99-843352e8249c
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: ht
source-wordcount: '193'
ht-degree: 100%

---

# Registrar una transacción para implementaciones personalizadas {#record-a-transaction-for-custom-implementations}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-osgi/record-transaction-custom-implementation) |
| AEM as a Cloud Service | Este artículo |

Utilice la API TransactionRecorder para registrar acciones que no se contabilizan como transacciones automáticamente.

Puede utilizar un código personalizado para enviar un formulario de PDF. O bien, puede enviar un formulario mediante métodos personalizados en lugar de utilizar los métodos de envío proporcionados con AEM Forms. Ninguna de las acciones e implementaciones personalizadas de las API de AEM Forms mencionadas anteriormente se contabiliza como una transacción. AEM Forms proporciona una API, [TransactionRecorder](https://javadoc.io/doc/com.adobe.aem/aem-forms-sdk-api/latest/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar este tipo de acciones como transacciones.

Para registrar una transacción, escriba el [servlet estándar de sling](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=es) y llame a dicho servlet desde un cliente para registrar una transacción. Puede llamar al servlet mediante AJAX o mediante cualquier otro método estándar.

## Código de ejemplo del lado del servidor {#sample-server-sided-code}

Puede utilizar el siguiente código de ejemplo para ejecutar la API TransactionRecorder desde una clase Java™ mediante un paquete OSGi personalizado.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Ejemplo de código del lado del cliente {#sample-client-side-code}

Puede utilizar el siguiente código de ejemplo para llamar al servlet que tiene la API `TransactionRecorder`.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Artículos relacionados {#related-articles}

* [API facturables de informes de transacciones](/help/forms/transaction-reports-billable-apis.md)
