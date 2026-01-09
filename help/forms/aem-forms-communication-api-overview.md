---
title: 'API de comunicaciones AEM Forms: Información general'
description: Información general sobre las API de comunicaciones de AEM Forms, incluidos los métodos de autenticación y la referencia completa de la API
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 7%

---


# API de AEM Forms: Información general

Las API de AEM Forms proporcionan un completo conjunto de API nativas de la nube diseñadas para ayudar a las empresas a automatizar los flujos de trabajo de los documentos.

Las API de AEM Forms están estructuradas y se accede a ellas a través de dos consolas principales:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/): Adobe Developer Console es la puerta de enlace a las API de Adobe, los eventos, el tiempo de ejecución y App Builder.

* [AEM Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console): AEM Developer Console proporciona acceso a detalles, configuraciones, cuentas técnicas y credenciales de servicio a nivel de entorno para admitir tareas operativas y de integración.

Diferentes API admiten diferentes [métodos de autenticación](#authentication-methods).

## Métodos de autenticación

Las distintas API de Forms utilizan diferentes métodos de autenticación en función de su cronología de lanzamiento:

* [Servidor a servidor de OAuth](/help/forms/oauth-api-authetication.md)
* [Servidor a servidor JWT (token web JSON)](/help/forms/jwt-api-authentication.md)

Las API anteriores admiten la autenticación de servidor a servidor basada en JWT, que se configura y administra mediante AEM Developer Console. Las API más recientes utilizan la autenticación de servidor a servidor OAuth y se configuran mediante Adobe Developer Console.

>[!NOTE]
>
> Adobe está estandarizando el método de autenticación en todas las API y está incorporando gradualmente las API a Adobe Developer Console, que admite el método de autenticación de servidor a servidor OAuth.

## Resumen de clasificación de API

Todas las API de AEM Forms se dividen en dos partes principales:

* [API de tiempo de ejecución y entrega de formularios adaptables](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [API de comunicación de AEM Forms](#aem-forms-communications-apis)

| Detalles | API de tiempo de ejecución y entrega de formularios adaptables | API de comunicación |
|--------------|----------------------------|--------------------------|
| Función | Administrar las operaciones de tiempo de ejecución y entrega de formularios adaptables | Generación y manipulación de documentos |
| Casos de uso | - Procesamiento de formularios<br>- Relleno previo de datos<br>- Envíos de formularios<br>- Administración de borradores | - Generación de PDF<br>- Combinación de documentos<br>- Procesamiento por lotes<br>- Operaciones de impresión |
| Método de autorización | Admite métodos de autenticación de servidor a servidor/usuario de OAuth. | Admite la autenticación de servidor a servidor, ya sea JWT o OAuth según la API. Una API no puede admitir ambos métodos de autenticación. |

### API de comunicaciones de AEM Forms

Las API de comunicación son el enfoque principal de las operaciones centradas en los documentos.

En la tabla siguiente se enumeran todas las [API de comunicaciones de AEM Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) junto con los métodos de autenticación y modelos de ejecución admitidos:

#### API de generación de documentos


| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Crea una nueva configuración por lotes para los trabajos de generación de documentos. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Recupera detalles de una configuración de lote específica. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Devuelve una lista de todas las configuraciones por lotes disponibles. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Inicia una ejecución de generación de resultados por lotes utilizando una configuración. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Recupera el estado de ejecución de un trabajo por lotes. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Enumera todas las instancias en ejecución para una configuración por lotes específica. | Asincrónica/Por Lotes | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Genera resultados de PDF de forma sincrónica en función de plantillas y datos. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Genera formatos de salida listos para imprimir (por ejemplo, PCL, PostScript). | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Genera salida AFP para impresión de gran volumen. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Procesa un formulario PDF Forms (XFA/XDP) con datos combinados. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Recupera el estado de un trabajo de generación de formularios de PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Obtiene el resultado de un trabajo de formulario de PDF completado. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |


#### API de manipulación de documentos

| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Ejecuta instrucciones DDX para combinar, dividir o manipular archivos PDF. | Sincrónica | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Convierte un documento de PDF al formato PDF/A. | Sincrónica | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Valida si un PDF cumple el estándar PDF/A. | Sincrónica | [JWT](/help/forms/jwt-api-authentication.md) |

#### API de conversión de documentos

| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Convierte un formulario PDF en formato XDP. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |

#### API de extracción de documento

| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Extrae propiedades e información estructural de una PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Extrae los derechos de uso incrustados en un PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Extrae metadatos como título, autor y palabras clave. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Extrae datos de formulario (XML/JSON) de PDF forms. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Extrae la configuración de seguridad, como permisos y cifrado. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |

#### API de transformación de documento


| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Actualiza o agrega metadatos en un documento de PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Agrega un campo de firma digital a un PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Borra el contenido de un campo de firma. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Quita un campo de firma de un PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |

#### API de Document Assurance

| Punto final de API | Descripción | Modelo de ejecución | Método de autenticación |
|---------|-------|---------|----------------------|
| [/adobe/document/assurance/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Aplica derechos de uso a un PDF (por ejemplo, comentario, relleno, firma). | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/secure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Codifica un PDF con contraseña o seguridad de certificado. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assurance/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Descifra un documento de PDF protegido. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assurance/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Firma digitalmente un documento de PDF. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assurance/certificfy](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Certifica un PDF con un certificado digital. | Sincrónica | [OAuth](/help/forms/oauth-api-authetication.md) |


## Pasos relacionados

Obtenga información sobre cómo establecer el entorno para las API de comunicaciones de Forms sincrónicas (bajo demanda) y asincrónicas (por lotes):

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="API sincrónicas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="API sincrónicas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="API de comunicaciones de AEM Forms: sincrónicas">API de comunicaciones de AEM Forms: sincrónicas</a>
                    </p>
                    <p class="is-size-6">Aprenda a configurar un entorno para las API de comunicaciones de Forms sincrónicas (bajo demanda) que generan o procesan documentos al instante. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Más información</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="API de comunicaciones de AEM Forms: asincrónicas" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="API asíncronas"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="API asíncronas">API de comunicaciones de AEM Forms: asincrónicas (por lotes)</a>
                    </p>
                    <p class="is-size-6">Aprenda a configurar el entorno para las API de comunicaciones de Forms asincrónicas (por lotes) que generan o procesan varios documentos de forma programada.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Más información</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [Introducción a Comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Arquitectura de AEM Forms as a Cloud Service para Formularios adaptables y API de comunicaciones](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Procesamiento de comunicaciones: API sincrónicas](/help/forms/aem-forms-cloud-service-communications.md)
>* [Procesamiento de comunicaciones: API por lotes](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Procesamiento de comunicaciones - API a petición](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
