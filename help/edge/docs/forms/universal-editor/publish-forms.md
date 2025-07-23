---
title: Publicación de formularios de AEM para Edge Delivery Services.
description: Publique sus formularios de Edge Delivery Services de forma rápida y fluida.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: ht
source-wordcount: '477'
ht-degree: 100%

---

# Publicación del formulario adaptable en Edge Delivery Services

<span class="preview"> Es una función de la versión preliminar y se puede acceder a ella a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal de versiones preliminares</a>. </span>


Cuando el formulario esté terminado y listo para usarse, puede publicarlo para que sus clientes puedan acceder a él para recopilar y enviar datos. La publicación garantiza que el formulario esté disponible en Edge Delivery, lo que permite a los usuarios interactuar con él sin problemas. Este proceso permite a los clientes rellenar y enviar el formulario en tiempo real, lo que garantiza una captura de datos eficiente y un procesamiento optimizado.

## Requisitos previos

* Un formulario creado con la **plantilla de Edge Delivery Services (EDS)**. [Más información](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) sobre la creación de un formulario basado en EDS.

## Publicación del formulario

Puede publicar cualquier **formulario adaptable basado en EDS** en Edge Delivery siguiendo estos pasos:

<!--1. Select the **Adaptive Form** that you want to publish and click the **Edit** ![edit icon](/help/forms/assets/edit.svg) icon.
   ![Select EDS-Based Form](/help/forms/assets/select-eds-based-form.png)-->

1. Abra el formulario adaptable en el editor y haga clic en el icono **Publicar** en el carril superior.
   ![Haga clic en Publicar](/help/forms/assets/publish-icon-eds-form.png)

1. Al hacer clic en **Publicar**, aparece una pantalla o una ventana emergente que muestra los recursos de publicación, incluido el título del formulario. En este ejemplo, se usa la plantilla **Wknd_Form**.
   ![Publicación al hacer clic](/help/forms/assets/on-click-publish.png)

1. Vuelva a hacer clic en **Publicar** y aparecerá una ventana emergente de confirmación que indica que el formulario se ha publicado.
   ![Éxito de publicación](/help/forms/assets/publish-success.png)

1. Para comprobar el estado de publicación del formulario, vuelva a hacer clic en **Publicar**.
   ![Estado de publicación](/help/forms/assets/publish-status.png)

1. Para **cancelar la publicación** de un formulario, ábralo en el editor, haga clic en el menú de tres puntos en la esquina superior derecha y haga clic en **Cancelar la publicación**.
   ![Cancelar publicación](/help/forms/assets/unpublish--form.png)

## Habilitar el envío de formularios en Edge Delivery mediante la configuración de un filtro de referente para AEM Publisher

Para garantizar el envío seguro del formulario, debe configurar un **Filtro de referente** en AEM Publisher. Este filtro garantiza que solo las solicitudes autorizadas de Edge Delivery puedan realizar operaciones de escritura (POST, PUT, DELETE, COPY, MOVE), lo que evita modificaciones no autorizadas. A continuación se indican los pasos necesarios para configurar un filtro de referente para AEM Publisher:

### Actualización de la URL de instancia de AEM en Edge Delivery

Modifique `submitBaseUrl` en el archivo **constant.js** dentro del bloque del formulario para especificar la URL de la instancia de AEM:

**Para la configuración de nube:**

```js
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';
```
**Para desarrollo local:**

```js
export const submitBaseUrl = 'http://localhost:4503';
```

### Modificación de la configuración de CORS

Ajuste la **configuración de CORS** para permitir las solicitudes de envío de formularios de los dominios de Edge Delivery. Consulte la [Guía de configuración de CORS](https://experienceleague.adobe.com/es/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors) para obtener más información.

**Ejemplo de configuración de CORS:**

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Franklin Stage
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  

# Franklin Live
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```
Para el desarrollo local, consulte la [documentación](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter) para habilitar CORS desde su **URL de host de IU de desarrollo**.

### Configuración del Filtro de referente

Configure **Filtro de referente** en AEM Cloud Service mediante Cloud Manager. [Más información](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) acerca de la configuración del filtro de referente en una instancia de AEM Cloud Service mediante un administrador de nube.

**Configuración JSON para el filtro de referente:**

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

Esta configuración especifica qué métodos HTTP se filtran, qué referentes se permiten y qué agentes de usuario se excluyen del filtro. Al implementar estas configuraciones, **los envíos de formularios a través de Edge Delivery** se protegerán y restringirán solo a fuentes autorizadas.

### Acceso al formulario adaptado publicado

Ahora se puede acceder al formulario adaptable a través de **Edge Delivery** con el siguiente formato de dirección URL:

```
https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
```

Por ejemplo, la dirección URL de **Wknd-Form** es:

```
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form
```


## Vea también

{{universal-editor-see-also}}

