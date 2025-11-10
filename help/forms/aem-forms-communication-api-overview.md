---
title: 'API de comunicaciones AEM Forms: Información general'
description: Información general sobre las API de comunicaciones de AEM Forms, incluidos los métodos de autenticación y la referencia completa de la API
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 11%

---


# API de comunicaciones AEM Forms: Información general

Las API de comunicaciones de AEM Forms proporcionan un completo conjunto de API nativas de la nube diseñadas para ayudar a las empresas a automatizar los flujos de trabajo de los documentos.

Las API de AEM Forms están estructuradas y se accede a ellas a través de dos consolas principales:

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/): Adobe Developer Console es la puerta de enlace a las API de Adobe, los eventos, el tiempo de ejecución y App Builder.

* [AEM Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console): AEM Developer Console proporciona herramientas para depurar e inspeccionar entornos de AEM as a Cloud Service.

Cada consola proporciona acceso a diferentes API y servicios para tareas de procesamiento, generación, conversión, cifrado y comunicación de documentos. Las API admiten diferentes [métodos de autenticación](#authentication-methods).

## Métodos de autenticación

Las API admiten varios métodos de autenticación para la integración segura entre sus aplicaciones y los servicios de Adobe:

| Aspecto | Servidor a servidor OAuth (recomendado) | JWT (token web JSON) |
|-------------|------------------------------------------|---------------------------|
| Descripción | Método moderno y seguro para acceder a la API sin interacción del usuario. | Método antiguo que utiliza tokens firmados para el acceso. |
| Configurar ubicación | ADOBE DEVELOPER CONSOLE y AEM DEVELOPER CONSOLE | Solo AEM Developer Console |
| Seguridad | Alto: utiliza credenciales y ámbitos del cliente | Moderado: depende de la administración de claves |
| Escalabilidad | Altamente escalable para integraciones back-end | Limitado, adecuado para uso heredado |
| Administración de tokens | Generación y renovación automáticas | Firma y rotación manuales de tokens |
| Estado | Recomendado | Obsoleto |


>[!NOTE]
>
> Haga clic en los vínculos siguientes para obtener más información sobre :-
> 
> * [Servidor a servidor OAuth (recomendado)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)
> * [JWT (token web JSON)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## Resumen de clasificación de API

Todas las API de AEM Forms se dividen en dos partes principales:

* [API de tiempo de ejecución y entrega de formularios adaptables](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [API de comunicación de AEM Forms](#aem-forms-communications-apis)

| Detalles | API de tiempo de ejecución y entrega de formularios adaptables | API de comunicación |
|--------------|----------------------------|--------------------------|
| Función | Administrar las operaciones de tiempo de ejecución y entrega de formularios adaptables | Generación y manipulación de documentos |
| Casos de uso | - Procesamiento de formularios<br>- Relleno previo de datos<br>- Envíos de formularios<br>- Administración de borradores | - Generación de PDF<br>- Combinación de documentos<br>- Procesamiento por lotes<br>- Operaciones de impresión |
| Método de autorización | Admite métodos de autenticación de servidor a servidor/usuario de OAuth. | Solo admite la autenticación de servidor a servidor OAuth. |

### API de comunicaciones de AEM Forms

Las API de comunicación son el enfoque principal de las operaciones centradas en los documentos.

En la tabla siguiente se enumeran todas las [API de comunicaciones de AEM Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/) junto con los métodos de autenticación y modelos de ejecución admitidos:

#### API de generación de documentos

| Punto final de API | Modelo de ejecución | Método de autenticación |
| ------------------ | ---------------- | --------------------------- |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Asincrónica/Por Lotes | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


#### API de manipulación de documentos

| Punto final de API | Modelo de ejecución | Método de autenticación |
| ------------------ | ---------------- | --------------------------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |

#### API de conversión de documentos

| Punto final de API | Modelo de ejecución | Método de autenticación |
|----------------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API de extracción de documento

| Punto final de API | Modelo de ejecución | Método de autenticación |
|----------------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API de transformación de documento


| Punto final de API | Modelo de ejecución | Método de autenticación |
|----------------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### API de Document Assurance

| Punto final de API | Modelo de ejecución | Método de autenticación |
|----------------|---------|----------------------|
| [/adobe/document/assurance/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/secure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assurance/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assurance/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assurance/certificfy](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | Sincrónica | [Servidor OAuth a servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


## Próximos pasos

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