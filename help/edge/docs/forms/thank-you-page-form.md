---
title: Mostrar un mensaje de agradecimiento personalizado después del envío del formulario
description: Aprenda a configurar las páginas de agradecimiento y la redirección del bloque de Forms para optimizar la experiencia del usuario y optimizar sus recorridos.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 100%

---

# Mostrar un mensaje de agradecimiento personalizado después del envío del formulario

Una vez que un usuario envía un formulario, es crucial proporcionar una experiencia fluida a través de un mensaje de agradecimiento. Esto no solo confirma el envío correcto, sino que también aumenta la satisfacción del usuario y le guía en su recorrido. 

- **Mensaje de agradecimiento**: un mensaje de agradecimiento es la piedra angular de la experiencia del usuario, ya que ofrece tranquilidad y transmite información importante a la vez que refuerza la identidad de marca. Sirve como reconocimiento directo de la acción del usuario, fomentando un sentido de realización y satisfacción.

- **Redirigir**: la redirección desempeña una función esencial en dirigir a los usuarios hacia los destinos relevantes, optimizando con ello la participación y, en última instancia, el aumento de las tasas de conversión. Al guiar a los usuarios de modo óptimo al siguiente paso de su recorrido, la redirección garantiza una experiencia de navegación fluida. Por ejemplo, redirigir al usuario a la página de pago después de recopilar los detalles iniciales.

El comportamiento predeterminado del bloque de Formularios adaptables es mostrar el siguiente mensaje de agradecimiento al enviarlo. El mensaje se muestra en la parte superior del formulario cuando el envío del formulario se realiza correctamente.

![mensaje de agradecimiento predeterminado](/help/edge/assets/thank-you-message.png)

Sin embargo, tiene la flexibilidad de adaptar esta experiencia para satisfacer sus necesidades específicas. Las opciones que se incluyen son:

- Mostrar un mensaje de agradecimiento personalizado después del envío del formulario
- Redirigir a los usuarios a otra página después del envío para realizar más acciones

>[!NOTE]
>
> Puede consultar la siguiente [hoja de cálculo de consulta](/help/edge/docs/forms/assets/enquiry.xlsx) para personalizar el mensaje de agradecimiento según sus necesidades.

## Configuración de un mensaje de agradecimiento personalizado

Si desea mostrar un mensaje de agradecimiento personalizado tras el envío correcto del formulario, puede configurar la hoja de cálculo para que lo muestre.

Siga los siguientes pasos para configurar un mensaje de agradecimiento personalizado para su bloque de Formularios adaptables:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.
1. Añada un mensaje de agradecimiento personalizado en la columna `value` para el tipo de campo `submit` de la hoja de cálculo.

   ![Mensaje de agradecimiento personalizado](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Por ejemplo, añada el mensaje `Submission Successful!` en la columna `value` para el tipo de campo `submit`.

1. Previsualice y publique la hoja usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Mensaje de agradecimiento personalizado](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Redirección de los usuarios a otra página después del envío

Redirigir a un usuario a otra página después del envío del formulario puede mejorar la experiencia del usuario al proporcionar información relevante, confirmar las acciones y guiar a los usuarios hacia los resultados deseados. Por ejemplo,

- una vez que un usuario termina un formulario de compra, se le redirige a una página de pago para que complete la transacción de forma segura.
- al enviar un formulario de registro para un evento o seminario web, se redirige a los usuarios a una página de confirmación que muestra los detalles del evento, como fecha, hora y ubicación.

Siga los siguientes pasos para redirigir a los usuarios a otra página:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.
1. Pegue la dirección URL en la columna `value` para el tipo de campo `submit` de la hoja de cálculo para redirigir al usuario cuando el envío del formulario se realiza correctamente.
Para redirigir la página a otra página diferente, use la URL de la página [Documentación de Edge Delivery](https://www.aem.live/docs/).

   ![URL de redirección del mensaje de agradecimiento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Previsualice y publique la hoja usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Redirigir mensaje de agradecimiento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

También puede crear un nuevo archivo de documento y añadir su URL de vista previa en la columna `value` para el tipo de campo `submit`.

Una vez que un usuario envía un formulario, es importante proporcionar un mensaje de agradecimiento claro. Confirma que el envío se ha realizado correctamente y mejora la satisfacción del usuario.

