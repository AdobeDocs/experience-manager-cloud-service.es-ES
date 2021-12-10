---
title: ¿Cómo se añade información de los datos de usuario a los metadatos de envío de formulario?
description: Aprenda a añadir información a los metadatos de un formulario enviado con los datos proporcionados por el usuario. Descubra más información sobre cómo ver los metadatos de envío de formulario actualizados en el repositorio CRX.
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---


# Adición de información de datos de usuario a metadatos de envío de formulario {#adding-information-from-user-data-to-form-submission-metadata}

Puede utilizar valores introducidos en un elemento del formulario para calcular los campos de metadatos de un borrador o un envío de formulario. Los metadatos le permiten filtrar el contenido en función de los datos del usuario. Por ejemplo, un usuario introduce John Doe en el campo de nombre del formulario. Puede utilizar esta información para calcular los metadatos que pueden categorizar este envío bajo las iniciales JD.

Para calcular los campos de metadatos con los valores introducidos por el usuario, agregue elementos del formulario en los metadatos. Cuando un usuario introduce un valor en ese elemento, una secuencia de comandos utiliza el valor para calcular la información. Esta información se añade en los metadatos. Cuando se agrega un elemento como campo de metadatos, se proporciona una clave para él. La clave se añade como campo en los metadatos y la información calculada se registra en él.

Por ejemplo, una empresa de seguros de salud publica un formulario. En este formulario, un campo captura la edad de los usuarios finales. El cliente desea comprobar todos los envíos de un intervalo de edad concreto después de que varios usuarios envíen el formulario. En lugar de pasar por todos los datos que se complican con el aumento del número de formularios, los metadatos adicionales ayudan al cliente. El autor del formulario puede configurar qué propiedades/datos rellenados por el usuario final se almacenan en el nivel superior para que la búsqueda sea más sencilla. Los metadatos adicionales son la información rellenada por el usuario almacenada en el nivel superior del nodo de metadatos, según la configuración del autor.

Considere otro ejemplo de un formulario que captura el ID de correo electrónico y el número de teléfono. Cuando un usuario visita este formulario de forma anónima y abandona el formulario, el autor puede configurar el formulario para guardar automáticamente el id de correo electrónico y el número de teléfono. Este formulario se guarda automáticamente y el número de teléfono y el id de correo electrónico se almacenan en el nodo de metadatos del borrador. Un caso de uso de esta configuración es el panel de administración de posibles clientes.

## Adición de elementos de formulario a metadatos {#adding-form-elements-to-metadata}

Realice los siguientes pasos para agregar un elemento en los metadatos:

1. Abra el formulario adaptable en modo de edición.\
   Para abrir el formulario en modo de edición, en el administrador de formularios, seleccione el formulario y pulse **[!UICONTROL Apertura]**.
1. En el modo de edición, seleccione un componente y pulse ![nivel de campo](assets/select_parent_icon.svg) > **[!DNL Adaptive Form Container]** y, a continuación, toque ![cmppr](assets/configure-icon.svg).
1. En la barra lateral, haga clic en **[!DNL Metadata]**.
1. En la sección Metadatos , haga clic en **[!DNL Add]**.
1. Utilice el campo Value de la pestaña Metadata para añadir secuencias de comandos. Las secuencias de comandos que agregue recopilan datos de elementos del formulario y calculan valores que se alimentan de los metadatos.

   Por ejemplo, **[!DNL true]** se registra en los metadatos si la edad introducida es buena a 21, y **[!DNL false]** se registra si es menor que 21. La siguiente secuencia de comandos se introduce en la pestaña Metadatos :

   `(agebox.value >= 21) ? true : false`

   ![Secuencia de comandos de metadatos](assets/add-element-metadata.png)

   Secuencia de comandos introducida en la ficha Metadatos

1. Haga clic **[!DNL OK]**.

Una vez que un usuario introduce datos en el elemento seleccionado como campo de metadatos, la información calculada se registra en los metadatos. Puede ver los metadatos en el repositorio que configuró para almacenarlos.

## Visualización de metadatos de envío de formulario actualizados: {#seeing-updated-form-nbsp-submission-metadata}

Por ejemplo, los metadatos se almacenan en el repositorio CRX. Los metadatos tienen el siguiente aspecto:

![Metadatos](assets/metadata_entry_new.png)

Si agrega un elemento de casilla de verificación en los metadatos, los valores seleccionados se almacenan como una cadena separada por comas. Por ejemplo, se agrega un componente de casilla de verificación al formulario y se especifica su nombre como `checkbox1`. En las propiedades del componente de la casilla de verificación, agregue los elementos Licencia de conducción, Número de seguridad social y Pasaporte para los valores 0, 1 y 2.

![Almacenamiento de varios valores desde una casilla de verificación](assets/checkbox-metadata.png)

Se selecciona el contenedor Formulario adaptable y, en las propiedades del formulario, se agrega una clave de metadatos `cb1` qué tiendas `checkbox1.value`y publicar el formulario. Cuando un cliente rellena el formulario, el cliente selecciona las opciones Pasaporte y Número de seguridad social en el campo de casilla de verificación. Los valores 1 y 2 se almacenan como 1, 2 en el campo cb1 de los metadatos de envío.

![Entrada de metadatos de varios valores seleccionados en un campo de casilla de verificación](assets/metadata-entry.png)

>[!NOTE]
>
>El ejemplo anterior es solo para fines de aprendizaje. Asegúrese de buscar metadatos en la ubicación correcta, tal y como está configurada en su [!DNL Experience Manager Forms] implementación.
