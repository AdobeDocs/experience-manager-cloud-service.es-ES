---
title: Configuración de acciones de envío para AEM Forms con Edge Delivery Services
description: Obtenga información sobre cómo configurar acciones de envío en AEM Forms mediante Edge Delivery Services. Elija entre el servicio de envío de formularios y la acción de envío a la instancia de publicación de AEM para gestionar los datos de formulario de forma segura y eficaz.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 8f490054-f7b6-40e6-baa3-3de59d0ad290
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 12%

---

# Configuración de acciones de envío para AEM Forms

Configure la administración del envío de formularios para enrutar datos a hojas de cálculo, correo electrónico o sistemas back-end mediante AEM Forms con Edge Delivery Services.

## Guía de decisión rápida

Elija el método de envío:

| Método | Ideal para | Complejidad de configuración | Casos de uso |
|--------|----------|------------------|-----------|
| **Servicio de envío de Forms** | Captura de datos sencilla | Bajo | Formularios de contacto, encuestas, recopilación de datos básicos |
| **Envío de publicación de AEM** | Flujos de trabajo complejos | Alto | Integraciones empresariales, procesamiento personalizado, flujos de trabajo |

## Requisitos previos

Antes de configurar las acciones de envío, asegúrese de que:

- Instancia de AEM Forms as a Cloud Service
- Proyecto de Edge Delivery Services configurado
- Formulario creado con la creación de documentos o el editor universal
- Permisos necesarios para destinos de destino (hojas de cálculo, sistemas de correo electrónico o AEM)

+++ Método 1: Servicio de envío de Forms

El servicio de envío de Forms es un punto de conexión alojado en Adobe ideal para escenarios sencillos de captura de datos.

### Destinos admitidos

- **Hojas de cálculo**: Hojas de cálculo de Google, Microsoft Excel (OneDrive/SharePoint)
- **Correo electrónico**: enviar datos de formulario a direcciones de correo electrónico especificadas

### Pasos de configuración

1. **Configurar el acceso de destino**
   - Para hojas de cálculo: conceder permiso de edición a `forms@adobe.com` en hoja de cálculo de destino
   - Para correo electrónico: compruebe que se puede acceder a las direcciones de correo electrónico del destinatario

2. **Configurar el envío de formularios**
   - Abra el formulario en el entorno de creación.
   - Establecer la acción de envío en &quot;Servicio de envío de Forms&quot;
   - Especifique la URL o direcciones de correo electrónico de la hoja de cálculo
   - Guardar y publicar el formulario

3. **Envío de prueba**
   - Envío de datos de prueba mediante el formulario
   - Comprobar si los datos aparecen en el destino
   - Comprobar registros de errores si falla el envío

### Notas importantes

- La cuenta de servicio `forms@adobe.com` requiere acceso de edición en las hojas de cálculo de destino
- Las notificaciones por correo electrónico se envían inmediatamente al enviar el formulario
- La validación de datos se produce en el nivel de servicio

![Flujo de servicio de envío de Forms](/help/forms/assets/eds-fss.png)

+++

+++ Método 2: Envío de publicación de AEM

Envíe datos de formulario directamente a la instancia de publicación de AEM as a Cloud Service para un procesamiento complejo.

### Cuándo se debe utilizar AEM Publish

- Flujos de trabajo de AEM personalizados necesarios después del envío
- Integración del modelo de datos de formulario (FDM) con bases de datos
- Integraciones de servicios de terceros (Marketo, Power Automate, Workfront Fusion)
- Bibliotecas de documentos de Azure Blob Storage o SharePoint
- Lógica de procesamiento o validación compleja del lado del servidor

### Acciones de envío disponibles

- [Enviar al punto final REST](/help/forms/configure-submit-action-restpoint.md)
- [Envío de correo electrónico mediante los servicios de correo de AEM](/help/forms/configure-submit-action-send-email.md)
- [Enviar mediante el modelo de datos de formulario](/help/forms/configure-data-sources.md)
- [Invocar flujo de trabajo de AEM](/help/forms/aem-forms-workflow-step-reference.md)
- [Enviar a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Enviar a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Enviar a Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Enviar a Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Enviar a Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Enviar a Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

![Flujo de envío de publicación de AEM](/help/forms/assets/eds-aem-publish.png)

### Requisitos de configuración

#### &#x200B;1. Configuración de AEM Dispatcher

Configure Dispatcher en la instancia de publicación de AEM:

- **Permitir rutas de envío**: modifique `filters.any` para permitir las solicitudes POST a `/adobe/forms/af/submit/...`
- **Sin redirecciones**: Asegúrese de que las reglas de Dispatcher no redirijan las rutas de envío del formulario

#### &#x200B;2. Filtro de referente de OSGi

En la consola OSGi de AEM (`/system/console/configMgr`):

1. Buscar &quot;Filtro de referente de Apache Sling&quot;
2. Añada su dominio de Edge Delivery a la lista &quot;Permitir hosts&quot;
3. Incluir dominios como `https://your-eds-domain.hlx.page`

#### &#x200B;3. Reglas de redireccionamiento de CDN

Configure su CDN de Edge Delivery para dirigir los envíos:

- Enrutar solicitudes de `/adobe/forms/af/submit/...` a la instancia de publicación de AEM
- La implementación varía según el proveedor de CDN (Fastly, Akamai, Cloudflare)

#### &#x200B;4. Configuración de formularios

1. Crear formularios en el editor universal
2. Configurar la acción de envío para segmentar la acción de AEM Forms
3. Especificar ruta de extremo de envío
4. Publicar formulario en el sitio de Edge Delivery

+++

+++ Incrustación de formularios (opcional)

Incrustar formularios creados en una ubicación en diferentes páginas o sitios web.

### Casos de uso

- Reutilización de formularios estándar en varias páginas de aterrizaje
- Incluir formularios especializados en contenido creado en documentos
- Mantener un solo formulario en varios proyectos EDS

### Configuración de CORS

Configure el uso compartido de recursos de origen cruzado en el origen del formulario:

1. **Agregar encabezados CORS** a las respuestas de origen de formulario:
   - `Access-Control-Allow-Origin: https://your-host-domain.com`
   - `Access-Control-Allow-Methods: GET, OPTIONS`
   - `Access-Control-Allow-Headers: Content-Type`

2. **Ejemplo de configuración**:

       &#x200B;# Configuración del sitio que aloja el formulario
       encabezados:
       - ruta: /forms/**
       personalizado:
       Access-Control-Allow-Origin: https://host-domain.com
       Métodos-Permiso-Control-Acceso: GET, OPTIONS
   

### Pasos de incrustación

1. **Crear y publicar formulario**
   - Crear formularios mediante la creación de documentos o el editor universal
   - Configuración del método de envío (FSS o AEM Publish)
   - Publicar en URL independiente

2. **Configurar CORS**
   - Configuración de encabezados CORS en el sitio de origen del formulario
   - Permitir que el dominio de la página host recupere el formulario

3. **Incrustar en la página host**
   - Añadir bloque de incrustación de formulario a la página de host
   - Apuntar bloque a URL de formulario publicado
   - Publicar página de host

![Arquitectura de formulario incrustado](/help/forms/assets/eds-embedded-form.png)

+++

+++ Problemas comunes

| Problema | Solución |
|-------|----------|
| **Error al enviar el formulario** | Compruebe los errores de la consola, compruebe la URL del extremo y confirme los permisos |
| **El formulario incrustado no aparece** | Configure los encabezados CORS en el origen del formulario y compruebe la URL del formulario |
| **Errores 403/401 con AEM** | Actualizar el filtro de referente de Sling, comprobar la configuración de autenticación |
| **Los datos no llegan a la hoja de cálculo** | Verificar que `forms@adobe.com` tenga acceso de edición, comprobar URL de hoja de cálculo |
| **Errores CORS** | Agregar los encabezados adecuados de `Access-Control-Allow-Origin` al origen del formulario |

+++

## Ejemplos de configuración

+++ Formulario basado en documentos con envío de hoja de cálculo

1. Crear una estructura de formulario en Google Docs/Hojas
2. Configurar el extremo del servicio de envío de Forms
3. Conceder acceso de edición de `forms@adobe.com` a la hoja de cálculo de destino
4. Publicar documento en el sitio de Edge Delivery
5. Probar el envío de formularios y el flujo de datos

+++

+++ Formulario de editor universal con flujo de trabajo AEM

1. Crear formularios en el editor universal
2. Configure la acción de envío para &quot;Invocar el flujo de trabajo de AEM&quot;
3. Configuración de Dispatcher y el filtro de referente en AEM Publish
4. Configurar reglas de enrutamiento de CDN
5. Publicación de formularios y ejecución de flujo de trabajo de prueba

+++

## Prácticas recomendadas

- **Usar el servicio de envío de Forms** para escenarios sencillos de captura de datos
- **Elija Publicación de AEM** cuando se requieran integraciones o procesamiento complejos
- **Realizar pruebas exhaustivas** en el entorno de ensayo antes de la implementación de producción
- **Supervisar los envíos** mediante registros de AEM y errores de consola
- **Implementar la administración de errores adecuada** para los envíos erróneos
- **Validar datos** tanto a nivel de cliente como de servidor
- **Usar HTTPS** para todos los envíos de formularios y la transmisión de datos

## Temas relacionados

- [Creación basada en documentos con EDS Forms](/help/edge/docs/forms/tutorial.md)
- [Editor universal con EDS Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Servicio de envío de formularios de AEM Forms](/help/forms/forms-submission-service.md)
- [Configuración de fuentes de datos](/help/forms/configure-data-sources.md)
- [Referencia de flujo de trabajo AEM Forms](/help/forms/aem-forms-workflow-step-reference.md)
