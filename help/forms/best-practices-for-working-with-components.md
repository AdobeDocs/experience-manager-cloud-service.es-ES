---
title: Prácticas recomendadas para trabajar con componentes
seo-title: Best practices for working with components
description: Algunas prácticas recomendadas y puntos clave que deben tenerse en cuenta a la hora de trabajar con los componentes de los formularios adaptables
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 100%

---


# Prácticas recomendadas para trabajar con componentes{#best-practices-for-working-with-components}

Estas son algunas de las prácticas recomendadas y los puntos clave que deben tenerse en cuenta a la hora de trabajar con componentes de formulario adaptable:

* Cada componente tiene propiedades asociadas que controlan su aspecto y su funcionalidad. Para configurar las propiedades de un componente, pulse el componente y pulse ![Propiedades](assets/Smock_Wrench_18_N.svg) para abrir las propiedades del componente en el explorador de propiedades.
* Cada componente se identifica con su nombre de elemento. Al pulsar ![Propiedades](assets/Smock_Wrench_18_N.svg), puede cambiar el nombre del componente cambiando el valor del campo **[!UICONTROL Nombre del elemento]** en el explorador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permite ningún otro tipo de caracteres especiales, y el nombre del elemento debe comenzar con una letra.

* Puede modificar la propiedad Título de los componentes de un formulario adaptable en línea en el Editor de formularios sin abrir el Explorador de propiedades siempre que el título esté visible en el formulario. Para ello:

   1. Pulse para seleccionar un componente que tenga la propiedad **[!UICONTROL Título]** y cuya propiedad **[!UICONTROL Ocultar título]** esté deshabilitada.

   1. Pulse ![el icono Editar](assets/Smock_Edit_18_N.svg) para poder editar el título.

   1. Modifique el título y pulse la tecla Retroceso o pulse en cualquier sitio fuera del componente para guardar los cambios. Pulse la tecla Esc para descartar los cambios.

* Algunos componentes de los formularios adaptables, como Correo electrónico y Teléfono, incluyen patrones de validación listos para usar. Sin embargo, puede especificar una validación personalizada actualizando el campo **[!UICONTROL Patrón de validación]** en el acordeón Patrones de las propiedades del componente. Consulte las descripciones de componentes de la tabla anterior para obtener más información sobre las validaciones predeterminadas.

* Los campos de formulario adaptable, como Cuadro numérico y Correo electrónico, se pueden configurar para incluir tipos de entrada HTML5 especializados. Cuando estos campos están enfocados en dispositivos móviles y tabletas, el teclado muestra inicialmente el alfabeto, los números y los caracteres específicos que se utilizan normalmente para introducir información en los campos. Esto permite a los usuarios introducir la información rápidamente sin tener que alternar entre conjuntos de caracteres en el teclado. Para permitir entradas especializadas en un componente, active la casilla de verificación **[!UICONTROL Usar número de tipo HTML]** en las propiedades de ese componente.

* Puede habilitar un componente Cuadro de texto para que acepte texto enriquecido. Para habilitar el texto enriquecido en un cuadro de texto, active la casilla de verificación **[!UICONTROL Permitir texto enriquecido]** en las propiedades del componente.

* Puede activar los componentes Cuadro de texto, Correo electrónico y Teléfono para rellenar automáticamente los valores de campos como Nombre, Dirección, Tarjeta de crédito, Teléfono y Correo electrónico a partir de la información almacenada en la configuración de relleno automático del explorador. Para habilitar esta función, seleccione **[!UICONTROL Habilitar relleno automático]** en las propiedades del componente y seleccione un **[!UICONTROL atributo de relleno automático]**. Cuando un usuario rellena un formulario adaptable, los valores se sugieren desde el perfil de relleno automático del explorador o se basan en los valores rellenados anteriormente por el usuario. Tenga en cuenta que el relleno automático funciona si la configuración de relleno automático está activada en el explorador del usuario.

* Especifique valores para los elementos de Botón de opción y Casilla de verificación en el formato `{value}={text}` desde las propiedades de los componentes.
* De forma predeterminada, el componente Archivo adjunto permite al usuario adjuntar un único archivo. Sin embargo, puede configurar las propiedades del componente para que admita varios archivos adjuntos. Además, si un usuario adjunta varios archivos con el mismo nombre de archivo, los archivos adjuntos pueden causar algunos problemas. Por lo tanto, se recomienda asociar un identificador único a cada archivo adjunto enviado cuando se envía el formulario. Para ello:

   1. En el servidor de [!DNL AEM Forms], vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
   1. Busque y pulse **[!UICONTROL Servicio de configuración de formularios adaptables]**.
   1. En el cuadro de diálogo Servicio de configuración de formularios adaptables, active la opción **[!UICONTROL Asignar nombres de archivo únicos]**. De forma predeterminada, está desactivada.

* Para permitir que los usuarios adjunten un PDF mediante el explorador Safari, asegúrese de que agrega **aplicación/pdf** a la propiedad Tipos de archivo compatibles del componente Archivo adjunto. Los formularios adaptables creados con versiones anteriores de [!DNL AEM Forms] pueden contener **.pdf** en lugar de **aplicación/pdf** en la propiedad Tipos de archivo compatibles.

>[!NOTE]
>
>Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.