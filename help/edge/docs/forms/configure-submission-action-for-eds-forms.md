---
title: Configuración de acciones de envío para AEM Forms con Edge Delivery Services
description: Obtenga información sobre cómo configurar acciones de envío en AEM Forms mediante Edge Delivery Services. Elija entre el servicio de envío de formularios y la acción de envío a la instancia de publicación de AEM para gestionar los datos de formulario de forma segura y eficaz.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2d16a9bd1f498dd0f824e867fd3b5676fb311bb3
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 79%

---

# Configurar acciones de envío para formularios de AEM Forms

Configure el control del envío de formularios para enrutar datos a hojas de cálculo, correo electrónico o sistemas back-end mediante AEM Forms con Edge Delivery Services.

## Guía de decisión rápida

Elija el método de envío:

| Método | Ideal para | Complejidad de la configuración | Casos de uso |
|--------|----------|------------------|-----------|
| **Servicio de envío de formularios** | Captura de datos sencilla | Bajo | Formularios de contacto, encuestas, recopilación de datos básicos |
| **Envío a la instancia de publicación de AEM** | Flujos de trabajo complejos | Alto | Integraciones empresariales, procesamiento personalizado, flujos de trabajo |

## Requisitos previos

Antes de configurar las acciones de envío, asegúrese de que:

- Instancia de AEM Forms as a Cloud Service
- Proyecto de Edge Delivery Services configurado
- Formulario creado mediante la creación de documentos o el editor universal
- Permisos necesarios para destinos objetivo (hojas de cálculo, sistemas de correo electrónico o AEM)

+++ Método 1: Servicio de envío de formularios

El servicio de envío de formularios es un punto final hospedado en Adobe ideal para situaciones sencillas de captura de datos.

### Destinos admitidos

- **Hojas de cálculo**: Hojas de cálculo de Google, Microsoft Excel (OneDrive/SharePoint)
- **Correo electrónico**: enviar datos de formulario a direcciones de correo electrónico especificadas

### Pasos de configuración

1. **Configurar el acceso de destino**
   - Para hojas de cálculo: conceder permiso de edición a `forms@adobe.com` en hoja de cálculo de destino
   - Para correo electrónico: compruebe que se puede acceder a las direcciones de correo electrónico del destinatario

2. **Configurar el envío de formularios**
   - Abrir el formulario en el entorno de creación
   - Establecer la acción de envío en “Servicio de envío de formularios”
   - Especificar la URL o las direcciones de correo electrónico de la hoja de cálculo de destino
   - Guardar y publicar el formulario

3. **Envío de prueba**
   - Enviar datos de prueba mediante el formulario
   - Comprobar si los datos aparecen en el destino
   - Comprobar registros de errores si el envío falla

### Notas importantes

- La cuenta de servicio `forms@adobe.com` requiere acceso de edición en las hojas de cálculo de destino
- Las notificaciones por correo electrónico se envían inmediatamente al enviar el formulario
- La validación de datos se produce en el nivel de servicio

![Flujo del servicio de envío de formularios](/help/forms/assets/eds-fss.png)

+++

+++ Método 2: Envío de publicación de AEM

Envíe datos de formulario directamente a la instancia de publicación de AEM as a Cloud Service para un procesamiento complejo.

### Cuándo se debe utilizar la publicación de AEM

- Flujos de trabajo de AEM personalizados necesarios después del envío
- Integración del modelo de datos de formulario (FDM) con bases de datos
- Integraciones de servicios de terceros (Marketo, Power Automate, Workfront Fusion)
- Bibliotecas de documentos de Azure Blob Storage o SharePoint
- Lógica de procesamiento o validación compleja del lado del servidor

### Acciones de envío disponibles

- [Enviar al punto final REST](/help/forms/configure-submit-action-restpoint.md)
- [Enviar correo electrónico a través de servicios de correo de AEM](/help/forms/configure-submit-action-send-email.md)
- [Enviar mediante el modelo de datos de formulario](/help/forms/configure-data-sources.md)
- [Invocar el flujo de trabajo de AEM](/help/forms/aem-forms-workflow-step-reference.md)
- [Enviar a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Enviar a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Enviar a Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Enviar a Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Enviar a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Enviar a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![Flujo de envío de publicación de AEM](/help/forms/assets/eds-aem-publish.png)

### Requisitos de configuración

#### &#x200B;1. Actualizar la URL de instancia de AEM en Edge Delivery

Actualice la URL de instancia de AEM Cloud Service en el archivo `constant.js` del bloque `form` en `submitBaseUrl`. Puede configurar la URL en función de su entorno:

**Para la instancia de Cloud Service**

```js
export const submitBaseUrl = '<aem-publish-instance-URL>';
```

**Para desarrollo local**

```js
export const submitBaseUrl = 'http://localhost:<port-number>';
```

#### &#x200B;2. Filtro de referente de OSGi

Configure el Filtro de referente para permitir los dominios de sitio específicos de Edge Delivery:

1. Crear o actualizar el archivo de configuración de OSGi: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Agregue la siguiente configuración con los dominios de sitio específicos:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Implementar la configuración mediante Cloud Manager

Para obtener la configuración detallada del filtro de referente de OSGi, consulte la guía [Filtro de referente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter).

#### &#x200B;3. Problemas del CORS (Intercambio de Recursos de Origen Cruzado)

Configure las opciones de CORS en AEM para permitir solicitudes de los dominios de sitio específicos de Edge Delivery:

**Host local de desarrollador**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true
```

**Sitios de Edge Delivery: agregue cada dominio de sitio individualmente**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true
```

**Dominios Franklin heredados (si todavía están en uso)**

```apache
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Reemplace `main--abc--adobe.aem.live` y `main--abc1--adobe.aem.live` por sus dominios de sitio reales. Cada sitio alojado desde el mismo repositorio requiere una entrada de configuración CORS independiente.

Para obtener información detallada sobre la configuración de CORS, consulte la [Guía de configuración de CORS](https://experienceleague.adobe.com/es/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).


Para habilitar CORS para su entorno de desarrollo local, consulte el artículo de [Comprender el Intercambio de Recursos de Origen Cruzado (CORS)](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing).

<!--
#### 4. CDN Redirect Rules

Configure your Edge Delivery CDN to route submissions:

- Route requests from `/adobe/forms/af/submit/...` to your AEM Publish instance
- Implementation varies by CDN provider (Fastly, Akamai, Cloudflare)-->

#### &#x200B;4. Configuración de formularios

1. Crear formulario en el editor universal
2. Configurar la acción de envío para dirigirla a la acción de AEM Forms
3. Especificar ruta de punto final de envío
4. Publicar formulario en el sitio de Edge Delivery

+++
<!--
+++ Form Embedding

Embed forms created in one location into different web pages or sites.

### Use Cases

- Reuse standard forms across multiple landing pages
- Include specialized forms in Document-Authored content
- Maintain single form across multiple EDS projects

### CORS Configuration

Configure Cross-Origin Resource Sharing on the form source:

1. **Add CORS Headers** to form source responses:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`  
   - `Access-Control-Allow-Headers: Content-Type`

2. **Example Configuration**:

        # Configuration for site hosting the form
        headers:
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS

### Embedding Steps

1. **Create and Publish Form**
   - Build form using Document Authoring or Universal Editor
   - Configure submission method (FSS or AEM Publish)
   - Publish to standalone URL

2. **Configure CORS**
   - Set up CORS headers on form source site
   - Allow host page domain to fetch form

3. **Embed in Host Page**
   - Add form embedding block to host page
   - Point block to published form URL
   - Publish host page

![Embedded Form Architecture](/help/forms/assets/eds-embedded-form.png)

+++-->

+++ Problemas comunes

| Problema | Solución |
|-------|----------|
| **Error al enviar el formulario** | Comprobar los errores de la consola, verificar la URL del punto final y confirmar permisos |
| **El formulario incrustado no aparece** | Configurar los encabezados CORS en el origen del formulario y verificar la URL del formulario |
| **Errores 403/401 con AEM** | Actualizar el filtro de referente de Sling, comprobar la configuración de autenticación |
| **Los datos no llegan a la hoja de cálculo** | Verificar que `forms@adobe.com` tiene acceso de edición, comprobar la URL de hoja de cálculo |
| **Errores CORS** | Agregar los encabezados `Access-Control-Allow-Origin` adecuados a la fuente del formulario |

+++

## Ejemplos de configuración

+++ Formulario basado en documentos con envío de hoja de cálculo

1. Crear estructura de formulario en Hojas de cáclculo o Documentos de Google
2. Configurar punto final de servicio de envío de formularios
3. Conceder acceso de edición de `forms@adobe.com` a la hoja de cálculo de destino
4. Publicar el documento en el sitio de Edge Delivery.
5. Probar el envío de formularios y el flujo de datos

+++

+++ Formulario de editor universal con flujo de trabajo de AEM

1. Generar formulario en el editor universal
2. Configurar la acción de envío para “Invocar flujo de trabajo de AEM”
3. Configurar Dispatcher y el filtro de referente en publicación de AEM
4. Configurar reglas de enrutamiento de CDN
5. Publicar formularios y probar la ejecución del flujo de trabajo

+++

## Prácticas recomendadas

- **Usar el servicio de envío de formularios** para escenarios sencillos de captura de datos
- **Elegir la publciación de AEM** cuando se requieran integraciones o procesamiento complejos
- **Realizar pruebas exhaustivas** en el entorno de ensayo antes de la implementación de producción
- **Monitorizar los envíos** mediante registros de AEM y errores de consola
- **Implementar el control de errores adecuado** para los envíos fallidos
- **Validar datos** tanto a nivel de cliente como de servidor
- **Usar HTTPS** para todos los envíos de formularios y la transmisión de datos

## Temas relacionados

- [Creación basada en documentos con formularios EDS](/help/edge/docs/forms/tutorial.md)
- [Editor universal con formularios EDS](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Servicio de envío de formularios de AEM Forms](/help/forms/forms-submission-service.md)
- [Configurar fuentes de datos](/help/forms/configure-data-sources.md)
- [Referencia de flujo de trabajo de formularios de AEM](/help/forms/aem-forms-workflow-step-reference.md)
