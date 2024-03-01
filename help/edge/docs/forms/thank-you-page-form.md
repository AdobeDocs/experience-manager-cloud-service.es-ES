---
title: Configuración de la página de agradecimiento para EDS Forms
description: Aprenda a configurar las páginas de agradecimiento y la redirección de EDS Forms para optimizar la experiencia del usuario y optimizar los recorridos del usuario.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Configuración de las páginas de agradecimiento y la redirección en bloques de Forms adaptables

Las páginas de agradecimiento y la redirección son aspectos vitales de la mejora de la experiencia del usuario, ya que proporcionan a los usuarios confirmación, una comunicación clara y una navegación fluida después del envío del formulario.

## Configuración de las páginas de agradecimiento

Las páginas de agradecimiento sirven como un reconocimiento tranquilizador para los usuarios y permiten a las organizaciones comunicar información esencial a la vez que refuerzan la identidad de la marca. Siga estos pasos para configurar una página de agradecimiento para EDS Forms:

1. AEM Acceda a la carpeta del proyecto Entrega de Edge de la red de trabajo en Microsoft SharePoint o Google Workspace.
1. Cree un archivo de Microsoft Word o Google Docs llamado &quot;thank you&quot; dentro del directorio del proyecto.
1. Añada su mensaje de agradecimiento al archivo &quot;thank you&quot;.
   ![Ejemplo de página de agradecimiento](/help/edge/assets/sample-thankyou-page.png)
1. Utilice el AEM Sidekick para previsualizar y publicar el archivo &quot;gracias&quot;.

## Redirigir usuarios después del envío

La redirección facilita recorridos de usuario sin problemas al guiar a los usuarios a destinos relevantes, optimizar la participación y aumentar las tasas de conversión.

De forma predeterminada, el bloque de Forms adaptable redirige a los usuarios a la página de &quot;agradecimiento&quot;. Para redirigir a los usuarios a una página que no sea la página de agradecimiento predeterminada, tiene dos opciones:

* reemplace la página de agradecimiento existente por una página diferente o
* redirija la página &quot;agradecimiento&quot; a otra página de su elección.

### Reemplazar la página de agradecimiento existente

1. Abra el &quot;[Proyecto EDS]Archivo /blocks/form/form.js&quot; para editar.
1. Cambie el `thankyou` página de la siguiente línea a la página que elija:

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   Por ejemplo,

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > Asegúrese de que existe una página con el mismo nombre en la carpeta del proyecto del servicio de envío perimetral en Microsoft SharePoint o Google Workspace. Si la página no existe, proceda a crearla y publicarla.

1. Continúe protegiendo la carpeta &quot;form.js&quot; actualizada y sus archivos subyacentes al proyecto del servicio de entrega de Edge en GitHub. Esta actualización garantiza que el formulario ahora se redirija a la página actualizada según se haya especificado.

1. Asegúrese de que la página exista en la carpeta del proyecto EDS y publíquela.


### Usar redirecciones de sitios web

Configure un redireccionamiento de sitio web para dirigir la página de &quot;agradecimiento&quot; a una página diferente. Consulte la [Documentación de redirecciones](https://www.aem.live/docs/redirects) para obtener instrucciones detalladas.


