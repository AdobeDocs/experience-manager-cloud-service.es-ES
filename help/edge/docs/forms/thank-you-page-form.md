---
title: Configuración de la página de agradecimiento para EDS Forms
description: Configuración de la página de agradecimiento para EDS Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---


# Configurar redirecciones de bloques de formularios

Tiene la opción de configurar el bloque de formulario para redirigir a una página diferente del sitio web en lugar de la página de agradecimiento predeterminada,. Para configurar otra página como destino de redirección

1. Abra el archivo `[EDS Project]/blocks/form/form.js` para editarlo.

   ![código para el nodo de agradecimiento](/help/edge/assets/change-thankyou-node.png)

1. Cambie el `thankyou` nodo en la siguiente línea al nodo que elija:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Por ejemplo,

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > Asegúrese de que se crea una página de documento con el mismo nombre en la carpeta del proyecto del servicio de envío perimetral en Microsoft SharePoint o en Hojas de cálculo de Google, si aún no se ha creado.


1. Continúe protegiendo la carpeta actualizada &quot;form.js&quot; y sus archivos subyacentes en el proyecto del servicio de entrega de Edge en GitHub. Esta actualización garantiza que el formulario ahora redireccione al nodo actualizado según se haya especificado.
