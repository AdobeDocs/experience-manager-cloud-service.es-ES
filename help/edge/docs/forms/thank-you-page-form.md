---
title: Mostrar un mensaje de agradecimiento personalizado después del envío del formulario
description: Aprenda a configurar las páginas de agradecimiento y la redirección del bloque de Forms para optimizar la experiencia del usuario y optimizar sus recorridos.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 25%

---

# Mostrar un mensaje de agradecimiento personalizado después del envío del formulario

Una vez que un usuario envía un formulario, es crucial proporcionar una experiencia fluida a través de un mensaje de agradecimiento. No solo confirma el envío correcto, sino que también aumenta la satisfacción del usuario y lo guía en su recorrido.

* **Mensaje de agradecimiento**: Un mensaje de agradecimiento es la piedra angular de la experiencia del usuario, ya que ofrece tranquilidad y transmite información importante a la vez que refuerza la identidad de la marca. Sirve como un reconocimiento directo de la acción del usuario, fomentando un sentido de finalización y satisfacción.

* **Redireccionamiento**: una redirección desempeña un papel fundamental en la dirección de usuarios hacia destinos relevantes, la optimización de la participación y, en última instancia, el aumento de las tasas de conversión. Al guiar a los usuarios sin problemas al siguiente paso de su recorrido, una redirección garantiza una experiencia de navegación fluida. Por ejemplo, redirigir al usuario a la página de pagos después de recopilar los detalles iniciales.

El comportamiento predeterminado del bloque de Formularios adaptables es mostrar el siguiente mensaje de agradecimiento al enviarlo. El mensaje se muestra en la parte superior del formulario cuando el envío del formulario se realiza correctamente.

![mensaje de agradecimiento predeterminado](/help/edge/assets/thank-you-message.png)

Sin embargo, tiene la flexibilidad de adaptar esta experiencia para satisfacer sus necesidades específicas. Las opciones incluyen:

* Mostrar un mensaje de agradecimiento personalizado después del envío del formulario
* Redirija a los usuarios a otra página después del envío para realizar más acciones

>[!NOTE]
>
> Puede consultar la siguiente [hoja de cálculo de consultas](/help/edge/docs/forms/assets/enquiry.xlsx) para personalizar el mensaje de agradecimiento según sus necesidades.

## Configurar un mensaje de agradecimiento personalizado

Si desea mostrar un mensaje de agradecimiento personalizado tras el envío correcto del formulario, puede configurar la hoja de cálculo para que se muestre.

Siga los siguientes pasos para configurar un mensaje de agradecimiento personalizado para su bloque de Formularios adaptables:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.
1. Agregue un mensaje de agradecimiento personalizado en la columna `value` para el tipo de campo `submit` en la hoja de cálculo.

   ![Mensaje de agradecimiento personalizado](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Por ejemplo, agregue el mensaje `Submission Successful!` en la columna `value` para el tipo de campo `submit`.

1. Previsualice y publique la hoja usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Mensaje de agradecimiento personalizado](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Redirigir a los usuarios a otra página después del envío

Redirigir a un usuario a otra página después del envío del formulario puede mejorar la experiencia del usuario al proporcionar información relevante, confirmar las acciones y guiar a los usuarios hacia los resultados deseados. Por ejemplo,

* una vez que un usuario completa un formulario de compra, se le redirige a una página de pago para completar la transacción de forma segura.
* al enviar un formulario de registro para un evento o seminario web, se redirige a los usuarios a una página de confirmación que muestra los detalles del evento, como la fecha, la hora y la ubicación.

Siga los siguientes pasos para redirigir a los usuarios a otra página:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.
1. Pegue la dirección URL en la columna `value` para el tipo de campo `submit` en la hoja de cálculo para redirigir al usuario cuando el formulario se envíe correctamente.
Para redirigir la página a otra diferente, usa la URL de la página [Documentación de Edge Delivery](https://www.aem.live/docs/).

   ![URL de redireccionamiento de agradecimiento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Previsualice y publique la hoja usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Redirigir mensaje de agradecimiento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

También puede crear un nuevo archivo de documento y agregar su URL de vista previa en la columna `value` para el tipo de campo `submit`.

Una vez que un usuario envía un formulario, es importante proporcionar un mensaje de agradecimiento claro. Confirma que el envío se ha realizado correctamente y mejora la satisfacción del usuario.

## Ver también

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}