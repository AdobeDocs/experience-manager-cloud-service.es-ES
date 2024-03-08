---
title: Configurar la página de agradecimiento o el formulario de redirección después del envío
description: Aprenda a configurar las páginas de agradecimiento y la redirección del bloque de Forms para optimizar la experiencia del usuario y optimizar sus recorridos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# Mostrar la página de agradecimiento o el formulario de redirección después del envío

Una vez que un usuario envía un formulario, es crucial proporcionar una experiencia fluida a través de una página de agradecimiento o una redirección. Estos elementos no solo confirman el envío correcto, sino que también aumentan la satisfacción del usuario y lo guían en su recorrido.

* **Página de agradecimiento**: una página de agradecimiento es la piedra angular de la experiencia del usuario, ya que ofrece garantías y transmite información importante a la vez que refuerza la identidad de la marca. Sirve como un reconocimiento directo de la acción del usuario, fomentando un sentido de finalización y satisfacción.

* **Redirigir**: una redirección desempeña un papel fundamental en la dirección de usuarios hacia destinos relevantes, la optimización de la participación y, en última instancia, el aumento de las tasas de conversión. Al guiar a los usuarios sin problemas al siguiente paso de su recorrido, una redirección garantiza una experiencia de navegación fluida. Por ejemplo, redirigir al usuario a la página de pagos después de recopilar los detalles iniciales.

En el bloque de Forms adaptable, el comportamiento predeterminado es mostrar una página de agradecimiento. Sin embargo, tiene la flexibilidad de adaptar esta experiencia para satisfacer sus necesidades específicas. Las opciones incluyen:

* [Configuración de la página y el mensaje de agradecimiento para que se ajusten a los objetivos de marca y comunicación](#configuring-the-thank-you-page-and-message)
* [Redirigir a los usuarios a otra página después del envío para realizar más acciones](#redirect-users-to-another-page-post-submission)

## Configuración de la página y el mensaje de agradecimiento

El comportamiento predeterminado del bloque de Forms adaptable es mostrar la página de &quot;agradecimiento&quot; en el envío. Siga estos pasos para configurar la página de &quot;agradecimiento&quot; para su bloque de Forms adaptable:

1. AEM Acceda a la carpeta del proyecto Entrega de Edge de la red de trabajo en Microsoft SharePoint o Google Workspace.
1. Cree un archivo de Microsoft Word o Google Docs llamado &quot;thank you&quot; dentro del directorio del proyecto.
1. Añada su mensaje de agradecimiento al archivo &quot;thank you&quot;. </br>

   ![Ejemplo de página de agradecimiento](/help/edge/assets/sample-thankyou-page.png)

1. Utilice AEM Sidekick para previsualizar y publicar el archivo &quot;gracias&quot;.

El bloque de Forms adaptable muestra la página de &quot;agradecimiento&quot; al enviar el formulario.

## Redirigir a los usuarios a otra página después del envío

De forma predeterminada, el bloque de Forms adaptable redirige a los usuarios a la página de &quot;agradecimiento&quot;. Para redirigir a los usuarios a una página que no sea la página de agradecimiento predeterminada, tiene dos opciones:

* [Reemplace la página &quot;agradecimiento&quot; por una página diferente](#replace-the-existing-thankyou-page)
* [Usar redirecciones de sitios web para la redirección de páginas de &quot;agradecimiento&quot;](#use-website-redirects-for-thankyou-page-redirection)

### Sustituya la página de &quot;agradecimiento&quot;.

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
   > Asegúrese de que existe una página con el mismo nombre en la carpeta de proyecto de los Edge Delivery Services en Microsoft SharePoint o en Google Workspace. Si la página no existe, proceda a crearla y publicarla.

1. Continúe protegiendo la carpeta &quot;form.js&quot; actualizada y sus archivos subyacentes al proyecto de Edge Delivery Services en GitHub. Esta actualización garantiza que el formulario ahora se redirija a la página actualizada según se haya especificado.

1. Asegúrese de que la página exista en la carpeta del proyecto EDS y publíquela.


### Usar redirecciones de sitios web para la redirección de páginas de &quot;agradecimiento&quot;

Redirigir a un usuario a otra página después del envío del formulario puede mejorar la experiencia del usuario al proporcionar información relevante, confirmar las acciones y guiar a los usuarios hacia los resultados deseados. Por ejemplo,

* una vez que un usuario completa un formulario de compra, se le redirige a una página de pago para completar la transacción de forma segura.
* al enviar un formulario de registro para un evento o seminario web, se redirige a los usuarios a una página de confirmación que muestra los detalles del evento, como la fecha, la hora y la ubicación.

Para redirigir la página de &quot;agradecimiento&quot; a una página diferente, use [redirecciones de sitios web](https://www.aem.live/docs/redirects) hoja de cálculo.


## Más información

* [Componentes de formulario](/help/edge/docs/forms/form-components.md)
* [Propiedades del campo de formulario](/help/edge/docs/forms/eds-form-field-properties)
* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)
