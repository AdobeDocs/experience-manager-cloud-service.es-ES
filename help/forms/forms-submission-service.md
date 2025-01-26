---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: ae31df22c723c58addd13485259e92abb4d4ad54
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# Servicio de envío de Forms con Edge Delivery Services Forms

El servicio de envío de Forms le permite almacenar datos de los envíos de formularios en cualquier hoja de cálculo, como OneDrive, SharePoint o Hojas de cálculo de Google, lo que le permite acceder y administrar fácilmente los datos del formulario en su plataforma de hoja de cálculo preferida.

![servicio de envío de Forms](/help/forms/assets/form-submission-service.png)

## Ventajas de utilizar el servicio de envío de Forms

Algunas ventajas de utilizar el servicio de envío de Forms con hojas de cálculo son:

* **Integración directa**: puede configurar formularios para enviar datos directamente a una hoja de cálculo especificada, lo que elimina la necesidad de transferir datos manualmente.
* **Estructura de datos**: al configurar el envío, puede asignar campos de formulario a columnas de hoja de cálculo correspondientes para el almacenamiento de datos organizado.
* **Control de acceso**: puede aprovechar los permisos existentes para controlar quién puede tener acceso a los datos de formulario enviados y modificarlos, en función del servicio de hoja de cálculo elegido.

## Requisitos previos

A continuación se muestran los requisitos previos para utilizar el servicio de envío de Forms:

* AEM Asegúrese de que el proyecto de tenga la última versión del bloque de formulario adaptable.
* Asegúrese de que el repositorio de Git se añada a la lista de permitidos para utilizar el servicio de envío de Forms. [mailto:aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) con su nombre de organización de GitHub y el nombre de repositorio para que se añadan a la lista de permitidos para utilizar el servicio de envío de Forms.

## Configuración del servicio de envío de Forms

AEM Cree un nuevo proyecto de configurado con el bloque de Forms adaptable. AEM Consulte el artículo [Introducción - Tutorial para desarrolladores](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) para aprender a crear un nuevo proyecto de. Actualice el archivo `fstab.yaml` en el proyecto. Reemplace la referencia existente por la ruta de acceso a la carpeta que ha compartido con el `forms@adobe.com`

Puede [configurar el servicio de envío de Forms manualmente](#configuring-the-forms-submission-service-manually) o [configurar el servicio de envío de Forms mediante la API](#configuring-the-forms-submission-service-using-api).

### Configuración manual del servicio de envío de Forms

![Flujo de trabajo para el servicio de envío de formularios](/help/forms/assets/forms-submission-service-workflow.png)

#### 1. Crear un formulario con una definición de formulario

Crear un formulario con Hojas de cálculo de Google o Microsoft Excel. Para aprender a crear un formulario con una definición de formulario en Microsoft Excel o Google Sheets, [haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms).

La siguiente captura de pantalla muestra la definición del formulario utilizada para crear el formulario:

![Definición de formulario](/help/forms/assets/form-submission-definition.png)

#### 2. Active la hoja de cálculo para aceptar datos.

Una vez creado y previsualizado el formulario, habilite la hoja de cálculo correspondiente para que comience a recibir datos. agregar una hoja nueva como `incoming`. Puede [habilitar manualmente la hoja de cálculo para aceptar datos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data).

![Hoja entrante](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> AEM Si la hoja `incoming` no existe, no se enviará ningún dato a este libro de trabajo, ya que no se enviará ningún dato a la hoja de cálculo .

#### 3. Comparta la hoja de cálculo y genere un vínculo.

Para compartir la hoja de cálculo en la cuenta de `forms@adobe.com` y generar un vínculo, realice los siguientes pasos:

1. En Excel o Google Sheets, haga clic en el botón **Compartir** en la esquina superior derecha.
1. Agregue la cuenta de `forms@adobe.com` y
haz clic en el icono del ojo, selecciona el acceso de **Editar** y haz clic en **Enviar**.

   ![Compartir hoja entrante](/help/forms/assets/form-submission-share-incoming.png)

1. Para copiar el vínculo de la hoja de cálculo, haga clic en el botón **Compartir** en la esquina superior derecha y seleccione **Copiar vínculo**.

   ![Copiar vínculo de la hoja entrante](/help/forms/assets/form-submission-copy-link.png)

#### 4. Vincule la hoja de cálculo en la definición del formulario

Para configurar el servicio de envío de Forms con Google Sheets o Microsoft Excel, realice los siguientes pasos:

1. Abra la hoja de cálculo que contiene la definición del formulario.
1. En la fila correspondiente al campo **Enviar**, pegue el vínculo de hoja de cálculo copiado en la columna **Acción**.

   ![Vincular una hoja de cálculo](/help/forms/assets/form-submission-sheet-linking.png)

1. Obtenga una vista previa y publique la hoja con el [AEM Sidekick](https://www.aem.live/docs/sidekick) con el servicio de envío de formularios actualizado.

>[!NOTE]
>
> Puede consultar la [hoja de cálculo](/help/forms/assets/spreadsheet.xlsx) para usar el servicio de envío de Forms.

### Configuración del servicio de envío de Forms mediante API

También puede enviar una solicitud **POST** al formulario para actualizar la hoja `incoming` con datos.

>[!NOTE]
>
> * AEM Si la hoja `incoming` no existe, no se enviará ningún dato a este libro de trabajo, ya que no se enviará ningún dato a la hoja de cálculo .
> * Compartir la hoja `incoming` con Adobe Experience Manager el `forms@adobe.com` y conceder acceso de edición.
> * Previsualizar y publicar la hoja `incoming` en la barra de tareas.

Para saber cómo dar formato a la solicitud de POST para configurar su hoja, consulte la [documentación de API](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/). Puede ver el ejemplo que se proporciona a continuación:

Puede utilizar herramientas como curl o Postman para ejecutar esta solicitud de POST, como se muestra a continuación.

* **Usando Postman**:

Por ejemplo, envíe la solicitud siguiente en Postman después de reemplazar:
* `{id}` con su ID de formulario
* `site or repository` con su nombre de sitio o repositorio de GitHub
* `organization` con su nombre de usuario de GitHub

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

Al hacer clic en el botón **Enviar** en Postman, se devuelve una respuesta `201 Created` y la hoja `incoming` se actualiza con los datos enviados.

![pantalla de postman](/help/forms/assets/postman-api.png)

* **Usando el comando Curl**:

Por ejemplo, ejecute el siguiente comando en el terminal o símbolo del sistema después de reemplazar:
* `{id}` con su ID de formulario
* `site or repository` con su nombre de sitio o repositorio de GitHub
* `organization` con su nombre de usuario de GitHub


>[!BEGINTABS]

>[!TAB Para macOS]

    &quot;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
    —encabezado &quot;Content-Type: application/json&quot; \
    —encabezado &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; \
    —data &#39;{
    &quot;data&quot;: {
    &quot;startDate&quot;: &quot;2025-01-10&quot;,
    &quot;endDate&quot;: &quot;2025-01-25&quot;,
    &quot;destino&quot;: &quot;Australia&quot;,
    &quot;clase&quot;: &quot;Primera clase&quot;,
    &quot;presupuesto&quot;: &quot;2000&quot;,
    &quot;importe&quot;: &quot;1000000&quot;,
    &quot;nombre&quot;: &quot;Joe&quot;,
    &quot;edad&quot;: &quot;35&quot;,
    &quot;suscribirse&quot;: null,
    &quot;correo electrónico&quot;: &quot;mary@gmail.com&quot;
    }
    &#39;&#39;&#39;
    
    

>[!TAB Para el SO Windows]

    &quot;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
    —encabezado &quot;Content-Type: application/json&quot; ^
    —encabezado &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; ^
    —data &quot;{\&quot;data\&quot;: {\&quot;startDate\&quot;: \&quot;2025-01-10\&quot;, \&quot;endDate\&quot;: \&quot;2025-01-25\&quot;, \&quot;destination\&quot;: \&quot;Australia\&quot;, \&quot;class\&quot;: \&quot;First Class\&quot;, \&quot;budget\&quot;: \&quot;2000\&quot;, \&quot;amount\&quot;: \&quot;1000000\&quot;, \&quot;name\&quot;: \&quot;Joe\&quot;, \&quot;age\&quot;: \&quot;35\&quot;, \&quot;subscribe\&quot;: null, \&quot;email\&quot;: \&quot;mary@gmail.com\&quot;}&quot;
    
    &quot;

>[!ENDTABS]

La solicitud de POST mencionada anteriormente actualiza la hoja `incoming` con la siguiente respuesta:

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

La siguiente pantalla muestra la captura de pantalla de la hoja `incoming` actualizada por el envío de datos mediante API:

![hoja actualizada](/help/forms/assets/updated-sheet.png)

## Consulte también

{{see-more-forms-eds}}
