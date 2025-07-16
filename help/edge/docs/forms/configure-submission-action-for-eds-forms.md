---
title: Configuración de acciones de envío para AEM Forms con Edge Delivery Services
description: Obtenga información sobre cómo configurar acciones de envío en AEM Forms mediante Edge Delivery Services. Elija entre el servicio de envío de formularios y la acción de envío a la instancia de publicación de AEM para gestionar los datos de formulario de forma segura y eficaz.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 75d8ea4f0913e690e3374d62c6e7dcc44ea74205
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 99%

---

# Configuración de los envíos de formularios: ¿dónde se dirigen los datos?

Después de que un usuario haga clic en **enviar** en el formulario, debe indicarle a Edge Delivery Services qué hacer con esos datos. Tiene dos opciones principales:

## Método 1: Uso del servicio de envío de formularios de AEM (simplificado)

Este servicio es ideal para realizar acciones comunes y sencillas, como enviar datos a una hoja de cálculo o a un correo electrónico.

**¿Qué es y cómo puede ayudarle?**

El [servicio de envío de formularios](/help/forms/forms-submission-service.md) es un punto final alojado en Adobe. Cuando su formulario envía datos a este servicio, este se encarga de realizar una acción preconfigurada. Está diseñado para ser fácil de configurar. Con las configuraciones puede enviar a hojas de cálculo o un correo electrónico:

* **Enviar a hoja de cálculo:** añada automáticamente los datos de formulario enviados como una fila nueva en una hoja de cálculo de Google o en un archivo de Microsoft Excel (almacenado en OneDrive o SharePoint).
* **Enviar correo electrónico:** envíe un correo electrónico con los datos del formulario a una o varias de las direcciones de correo electrónico que especifique.

#### Importante: Requisitos de configuración

* **Acceso a la hoja de cálculo:** para enviar datos a una hoja de cálculo de Google o a un archivo de Excel en OneDrive/SharePoint, la cuenta de servicio de Adobe (a menudo `forms@adobe.com`) suele necesitar **permisos de edición** en esa hoja de cálculo específica.
* **Programa de acceso anticipado:** algunas características de este servicio, especialmente para las hojas de cálculo, pueden formar parte de un programa de acceso anticipado. Es posible que deba solicitar acceso enviando un correo electrónico a `aem-forms-ea@adobe.com` o rellenando un formulario específico de Adobe con los detalles del proyecto. Compruebe siempre la documentación de Adobe más reciente.

**Diagrama de flujo del servicio de envío de formularios**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->

![Envío de formularios](/help/forms/assets/eds-fss.png)

Este diagrama de flujo muestra cómo el servicio de envío de formularios toma los datos enviados y los envía a una hoja de cálculo o a un correo electrónico configurados.

## Método 2: Envío a la instancia de publicación de AEM (avanzado)

Para necesidades más complejas, los [formularios (especialmente los creados con el editor universal) pueden enviar datos directamente a la instancia de publicación de AEM as a Cloud Service](/help/forms/configure-submit-actions-core-components.md). Esto desbloquea toda la potencia del back-end de AEM.

**¿Cuándo necesita enviar a la instancia de publicación de AEM?**

* Para activar flujos de trabajo de AEM personalizados después del envío.
* Para utilizar el modelo de datos de formulario (FDM) de AEM para integrar con bases de datos u otros sistemas empresariales.
* Para conectarse con servicios de terceros como Marketo, Microsoft Power Automate o Adobe Workfront Fusion.
* Para almacenar datos en ubicaciones específicas como Azure Blob Storage o listas/bibliotecas de documentos de SharePoint (no solo en hojas de cálculo simples).
* Cuando tenga una validación del lado del servidor o una lógica de procesamiento de datos complejas en AEM.

**Acciones de envío disponibles (envíos a la instancia de publicación de AEM)**

* [Enviar a un punto final REST](/help/forms/configure-submit-action-restpoint.md)
* [Enviar correo electrónico (mediante los servicios de correo de AEM)](/help/forms/configure-submit-action-send-email.md)
* [Enviar mediante el modelo de datos de formulario (FDM)](/help/forms/configure-data-sources.md)
* [Invocar un flujo de trabajo de AEM](/help/forms/aem-forms-workflow-step-reference.md)
* [Enviar a SharePoint (como elementos de lista o documentos)](/help/forms/configure-submit-action-sharepoint.md)
* [Enviar a OneDrive (como documentos)](/help/forms/configure-submit-action-onedrive.md)
* [Enviar a Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Enviar a Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Enviar a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Enviar a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> Incluso si se dirige a una hoja de cálculo de Google o documento Excel desde la instancia de publicación de AEM, implica pasos de configuración diferentes a los del servicio de envío de formularios directo.

**Diagrama de flujo de envío a la instancia de publicación de AEM**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![Diagrama de flujo de envío a la instancia de publicación de AEM](/help/forms/assets/eds-aem-publish.png)
Este diagrama de flujo muestra un formulario que se envía a la instancia de publicación de AEM, que luego gestiona tareas back-end complejas.

### Servicio de envío de formularios frente a envíos a la instancia de publicación de AEM

| Función | Servicio de envío de formularios | Envíos a la instancia de publicación de AEM |
| :- | :- | :-- |
| **Es ideal para lo siguiente** | Captura sencilla de datos a hojas de cálculo y notificaciones por correo electrónico | Flujos de trabajo complejos, integraciones empresariales, lógica personalizada |
| **Creación de formularios** | Buena opción para formularios basados en documentos; opción correcta para formularios del editor universal sencillos | La mejor opción para los formularios creados con el editor universal |
| **Esfuerzo de configuración** | Bajo (a menudo, configuración simple) | Más alto (necesita la instancia de publicación de AEM, Dispatcher, OSGi, configuración de CDN) |
| **Sistema back-end** | Servicio alojado en Adobe | La instancia de publicación de AEM as a Cloud Service |
| **Flexibilidad** | Limitado a hoja de cálculo/correo electrónico | Muy flexible, gama completa de acciones de AEM Forms |
| **Ejemplo** | Datos del formulario de contacto a una hoja de cálculo de Google | Solicitud de préstamo que activa un flujo de trabajo de aprobación AEM |

## Cómo incrustar formularios en diferentes sitios o páginas

A veces, desea mostrar un formulario que se ha creado y administrado en un lugar (por ejemplo, un “sitio de formularios” central) en una página web o sitio diferente.

### ¿Por qué incrustar un formulario?

* Tiene un formulario “Contáctenos” estándar creado con el editor universal que debe aparecer en varias páginas de destino creadas con la creación basada en documentos.
* El contenido principal de su sitio web se encuentra en la creación de documentos (DA), y debe incluir un formulario especializado.
* Desea reutilizar un formulario único y bien mantenido en varios proyectos de EDS diferentes.

### Cómo funciona técnicamente la incrustación de formularios

La página donde desea que aparezca el formulario (llamémosla “página host”) contendrá código (normalmente un bloque o script especial). Cuando un usuario visita la página host, este código realiza una solicitud a la URL donde se aloja el formulario real (llamémoslo “fuente del formulario”). A continuación, la fuente del formulario devuelve su HTML, que la página host inserta y muestra.

**Arquitectura de formulario incrustado**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->

![Arquitectura de formulario incrustado](/help/forms/assets/eds-embedded-form.png)
Este diagrama muestra la página host obteniendo el código HTML de la fuente del formulario y mostrándolo. El envío utiliza el punto final configurado del formulario original.

## Configuración de CORS para formularios integrados

[CORS (intercambio de recursos de origen cruzado)](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) es una función de seguridad para el explorador. Si la página host (por ejemplo, `site-a.com`) intenta recuperar un formulario de un dominio diferente (por ejemplo, `forms-site-b.com`), el explorador lo bloqueará a menos que `forms-site-b.com` lo permita explícitamente a través de encabezados CORS.

Si no hay encabezados CORS correctos en **el servidor de la fuente de formulario**, el explorador evita que la página host cargue el formulario, por lo que el formulario incrustado no aparecerá.

### Cómo configurar CORS en el sitio que aloja su formulario?

Debe configurar el servidor que aloja **la fuente del formulario** para enviar encabezados HTTP específicos en su respuesta. El método exacto depende de la configuración de EDS (por ejemplo, para proyectos Franklin, esto se suele hacer en un archivo de configuración `helix-config.yaml` o similar en el repositorio de GitHub que controla el comportamiento de la CDN o la lógica de trabajador perimetral).
Encabezados clave para añadir a las respuestas de la fuente de formulario:

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (por ejemplo, `https://your-site.com`). Para las pruebas, podría usar `*`, pero para la producción, especifique el dominio o dominios exactos.
* `Access-Control-Allow-Methods: GET, OPTIONS` (es posible que necesite `POST` si el envío del formulario en sí también es de origen cruzado, pero normalmente los envíos van a un punto final independiente, a menudo del mismo origen o configurado específicamente).
* `Access-Control-Allow-Headers: Content-Type` (y cualquier otro encabezado personalizado que pueda usar la recuperación de formularios).

**Ejemplo (conceptual para un archivo de configuración):**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## Consideraciones adicionales: CDN y varias bases de códigos (Helix 4)

* **Reglas de CDN:** su CDN puede ofrecer formas de solicitudes de proxy. Por ejemplo, una solicitud a `host-page.com/embedded-form` podría ser enrutada internamente por la red de distribución de contenido (CDN) para recuperar contenido de `form-source.com/actual-form`, haciendo que aparezca como del mismo origen para el explorador. Su configuración puede resultar compleja.
* **Múltiples bases de código (Helix 4):** si su página host y fuente de formulario están en diferentes repositorios de GitHub (común en las configuraciones de Helix 4), asegúrese de que cualquier “bloque de formulario” de JavaScript necesario para procesar o administrar el formulario esté disponible en la base de código de la página host, o que el formulario que HTML obtuvo de la fuente de formulario sea autónomo y contenga todo el JavaScript necesario. Los documentos originales mencionan que “para helix4 con diferentes bases de códigos, debe añadir el bloque de formulario en ambas bases de códigos”.

### Configuraciones arquitectónicas comunes y pasos de configuración

A continuación se indican algunas formas comunes de configurar los formularios, combinando los métodos de creación con las estrategias de envío, junto con los puntos de configuración clave.

#### Formulario basado en documentos con envío a hoja de cálculo/correo electrónico

Esta es la configuración más sencilla. El formulario se crea en Word/Documentos de Google y se envían datos a una hoja de cálculo o un correo electrónico a través del servicio de envío de formularios.

1. Defina el formulario en un documento/hoja de cálculo de Google o documento Word utilizando la estructura de tabla o el bloque de formulario especificados.
1. En el documento (o en la configuración relacionada), especifique la URL de la hoja de cálculo de destino o la dirección de correo electrónico para el servicio de envío de formularios.
1. Asegúrese de que `forms@adobe.com` (o la cuenta de servicio correspondiente) tenga acceso de edición en la hoja de cálculo de destino.
1. Publique el documento en el sitio de Edge Delivery.

**Arquitectura basada en documentos + servicio de envío de formularios**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![Arquitectura basada en documentos + servicio de envío de formularios](/help/forms/assets/eds-doc-fss.png)

#### Formulario del editor universal con envío a hoja de cálculo/correo electrónico

Utiliza el editor universal visual para generar el formulario, pero sigue utilizando el servicio de envío de formularios simple para capturar datos.

1. Cree el formulario con el editor universal en AEM.
1. Configure la acción de envío del formulario en el editor universal para utilizar la opción “Enviar al servicio de envío de formularios”.
1. Especifique la URL o correo electrónico de la hoja de cálculo de destino.
1. Si usa hojas de cálculo, asegúrese de que `forms@adobe.com` tenga acceso de edición.
1. Publique la página que contiene el formulario de AEM en el sitio de Edge Delivery.

   **Arquitectura de editor universal + servicio de envío de formularios**

   ![Arquitectura de editor universal + servicio de envío de formularios](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### Formulario del editor universal con envío a la instancia de publicación de AEM (avanzado)

Esta configuración utiliza el editor universal para la creación de formularios y la instancia de publicación de AEM para un procesamiento back-end eficaz (flujos de trabajo, FDM, etc.). Esto requiere más configuración.

1. **Crear formulario en el editor universal:** genere su formulario en el editor universal. Configure su acción de envío para que apunte a una acción de AEM Forms (por ejemplo, “Invocar un flujo de trabajo de AEM” o “Enviar mediante un modelo de datos de formulario”).
1. **Configuración de AEM Dispatcher (en su nivel de instancia de publicación de AEM):**
   * **Sin redirecciones:** asegúrese de que las reglas de Dispatcher no *redirijan* las solicitudes realizadas a las rutas `/adobe/forms/af/submit/...`.
   * **Permitir envíos:** modifique sus filtros de Dispatcher (por ejemplo, en `filters.any`) para `allow` solicitudes POST a `/adobe/forms/af/submit/...` explícitamente desde el dominio o las direcciones IP de su sitio Edge Delivery.
1. **Filtro de referente OSGi en AEM (en su nivel de instancia de publicación de AEM):**
   * En la consola OSGi de AEM (`/system/console/configMgr`), busque y configure el “Filtro de referente de Apache Sling”.
   * Añada el o los dominios de su sitio Edge Delivery (por ejemplo, `https://your-eds-domain.hlx.page` o `https://your-custom-eds-domain.com`) a la lista “Permitir hosts” o “Permitir RegExp de hosts”. Esto indica a AEM que acepte envíos procedentes del sitio de EDS.
1. **Regla de redirección de CDN (en su CDN de Edge Delivery):**
   * El sitio de Edge Delivery (por ejemplo, `your-eds-domain.hlx.page`) debe enrutar correctamente las solicitudes de envío a la instancia de publicación de AEM.
   * Cuando se envía el formulario de la página de EDS, puede que se dirija a una ruta relativa como `/adobe/forms/af/submit/...`. Necesita una regla en su CDN de Edge Delivery (o trabajador perimetral) que diga: “Si una solicitud llega a `your-eds-domain.hlx.page/adobe/forms/af/submit/...`, reenvíela (proxy o redirección) a `your-aem-publish-instance.com/adobe/forms/af/submit/...`”.
   * La implementación exacta depende de su proveedor de CDN (por ejemplo, Fastly VCL, Akamai Property Manager o Cloudflare Workers).
1. **(Opcional) `constants.js` para desarrollo (en el código base de su proyecto EDS):**
   * Para el desarrollo local o si los scripts de formulario del lado del cliente necesitan conocer la URL de publicación de AEM completa, puede configurarla en un archivo de configuración `constants.js` o similar dentro del repositorio de GitHub del proyecto de Edge Delivery. Ejemplo:

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **Publicar:** publique la página de formulario de AEM en EDS y asegúrese de que todas las configuraciones de AEM estén activas en la instancia de publicación de AEM.

   **Arquitectura de editor universal + instancia de publiación de AEM**

![Arquitectura de editor universal + instancia de publiación de AEM](/help/forms/assets/eds-aem-publish.png)

Aquí se muestra el flujo: el usuario envía en el sitio de EDS, la CDN enruta a AEM Dispatcher y la instancia de publicación de AEM lo procesa.

#### Incrustar un formulario en una página de creación de documentos (DA)

El contenido principal de su sitio web se crea en la creación de documentos (DA). Puede crear el formulario utilizando la creación basada en documentos o el editor universal por separado y, a continuación, incrustarlo en la página de creación de documentos.

1. **Crear y publicar el formulario:**
   * Utilice la creación basada en documentos O el editor universal para crear el formulario.
   * Configure su método de envío (ya sea al servicio de envío de formularios o a la instancia de publicación de AEM, según la configuración 1, 2 o 3).
   * Publique este formulario para que esté activo en su propia URL de Edge Delivery (por ejemplo, `.../forms/my-special-form`).
1. **Configurar CORS:** en el sitio o proyecto de Edge Delivery que aloja este formulario independiente, asegúrese de que los encabezados CORS estén configurados para permitir que el dominio del sitio de creación de documentos lo recupere.
1. **Crear página en la creación de documentos:** cree o edite su página en la creación de documentos.
1. **Incrustar bloque de formulario:** use el bloque apropiado en la creación de documentos para incrustar una URL externa. Apunte este bloque a la URL del formulario independiente publicado.
1. **Publicar página de creación de documentos:** publique su página de creación de documentos. Ahora recuperará y mostrará el formulario.

   **Formularios incrustados en la arquitectura de creación de documentos**

   ![Formularios incrustados en la arquitectura de creación de documentos](/help/forms/assets/eds-forms-embedd-da.png)

   Esto muestra una página de creación de documentos que extrae un formulario de otra ubicación de EDS. El formulario incrustado administra su propio envío.

## Resolución de problemas

* **El envío del formulario no funciona.**
   * **Compruebe los errores de la consola:** abra la consola de desarrollador del explorador (normalmente con la tecla F12) y busque los errores en la pestaña Red o en la pestaña Consola cuando realice el envío.
   * **Verificar URL de envío:** ¿intenta enviar el formulario al punto final correcto (URL del servicio de envío de formularios o su ruta de instancia de publicación de AEM)?
   * **Servicio de envío de formularios:** si se envía a una hoja de cálculo, ¿se ha concedido acceso de edición a `forms@adobe.com`? ¿Es correcta la URL de la hoja de cálculo?
   * **Envíos a la instancia de publicación de AEM:**
      * ¿Permite Dispatcher realizar solicitudes POST a `/adobe/forms/af/submit/...`?
      * ¿Está configurado el filtro de referente de Sling en la instancia de publicación de AEM para permitir su dominio de EDS?
      * ¿Funcionan correctamente las reglas de redirección de CDN para `/adobe/forms/af/submit/...`?

* **Mi formulario incrustado no aparece.**

   * **CORS**: este es el motivo más común. Compruebe la consola del explorador para ver si hay errores de CORS. Asegúrese de que el sitio que *aloja* el formulario tenga los encabezados `Access-Control-Allow-Origin` correctos.
   * **¿Es correcta la URL del formulario?** ¿El código incrustado en la página host apunta a la URL del formulario activa correcta?
   * **Bloques de JavaScript:** si el formulario se basa en un “bloque de formulario” de JavaScript específico para el procesamiento, ¿está disponible el código de ese bloque en la página host?

* **Obtengo un mensaje “403 prohibido” o “401 no autorizado” al enviar a la instancia de publicación de AEM.**

   * Esto suele deberse a que el filtro de referente de Sling en la instancia de publicación de AEM no permite solicitudes desde el dominio de EDS. Compruebe su configuración.
   * También podría ser un problema de autenticación/autorización si el punto final de envío de AEM lo requiere, aunque los envíos de formularios estándar suelen ser anónimos.

## Siguientes pasos

Esta guía proporciona información general sobre el uso de formularios con Edge Delivery Services de AEM. Para obtener instrucciones paso a paso más detalladas sobre configuraciones específicas, consulte la documentación oficial de Adobe Experience Manager:

* [Creación basada en documentos con formularios de Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [Editor universal con formularios de Edge Delivery Services](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Creación de documentos (DA) e incrustación de contenido](https://www.aem.live/developer/da-tutorial)
* [Servicio de envío de formularios de AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
