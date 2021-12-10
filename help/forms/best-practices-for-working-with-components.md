---
title: Prácticas recomendadas para trabajar con componentes
seo-title: Best practices for working with components
description: Algunas prácticas recomendadas y puntos clave que deben tenerse en cuenta al trabajar con componentes del formulario adaptable
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Prácticas recomendadas para trabajar con componentes{#best-practices-for-working-with-components}

Algunas prácticas recomendadas y puntos clave que deben tenerse en cuenta al trabajar con componentes de formulario adaptable son las siguientes:

* Cada componente tiene propiedades asociadas que controlan su aspecto y funcionalidad. Para configurar las propiedades de un componente, pulse el componente y pulse ![propiedades](assets/Smock_Wrench_18_N.svg) para abrir las propiedades del componente en el navegador Propiedades.
* Un componente se identifica con su nombre de elemento. Al tocar ![propiedades](assets/Smock_Wrench_18_N.svg), puede cambiar el nombre del componente cambiando el **[!UICONTROL Nombre del elemento]** valor de campo en el navegador de propiedades. El campo Nombre de elemento solo acepta letras, números, guiones (-) y guiones bajos (_). No se permiten otros caracteres especiales y el nombre del elemento debe comenzar con una letra.

* Puede modificar la propiedad Título de un componente Formulario adaptable en línea en el editor de formularios sin abrir el explorador Propiedades siempre que el título esté visible en el formulario. Para ello:

   1. Toque para seleccionar un componente que tenga una **[!UICONTROL Título]** y cuyo **[!UICONTROL Ocultar título]** está deshabilitada.

   1. Toque ![Icono Editar](assets/Smock_Edit_18_N.svg) para que el título se pueda editar.

   1. Modifique el título y pulse la tecla Retorno o pulse cualquier lugar fuera del componente para guardar los cambios. Pulse la tecla Esc para descartar los cambios.

* Algunos componentes de Formulario adaptable, como Correo electrónico y Teléfono, incluyen patrones de validación predeterminados. Sin embargo, puede especificar la validación personalizada actualizando la variable **[!UICONTROL Patrón de validación]** en el acordeón Patrones de las propiedades del componente. Consulte las descripciones de componentes de la tabla anterior para obtener más información sobre las validaciones predeterminadas.

* Los campos de Forms adaptables, como Cuadro numérico y Correo electrónico, se pueden configurar para incluir tipos de entrada de HTML5 especializados. Cuando estos campos están enfocados en dispositivos móviles y tabletas, el teclado muestra el alfabeto, los números y los caracteres específicos por adelantado que normalmente se utilizan para introducir información en los campos. Ayuda a los usuarios a introducir la información rápidamente sin tener que alternar entre conjuntos de caracteres en el teclado. Para permitir la entrada especializada de un componente, active la variable **[!UICONTROL Usar número de tipo de HTML]** en sus propiedades de componente.

* Puede habilitar un componente Cuadro de texto para que acepte Texto enriquecido. Para habilitar el texto enriquecido para un cuadro de texto, active la variable **[!UICONTROL Permitir texto enriquecido]** en las propiedades del componente.

* Puede activar los componentes Cuadro de texto, Correo electrónico y Teléfono para rellenar automáticamente los valores de campos como nombre, dirección, tarjeta de crédito, teléfono y correo electrónico a partir de la información almacenada en la configuración de relleno automático del explorador. Para habilitar esta función, seleccione **[!UICONTROL Habilitar relleno automático]** en las propiedades del componente y seleccione una **[!UICONTROL Atributo de relleno automático]**. Cuando un usuario rellena un formulario adaptable, los valores se sugieren desde el perfil de relleno automático del explorador o se basan en los valores rellenados anteriormente por el usuario. Tenga en cuenta que el llenado automático funciona si la configuración de llenado automático está activada en el explorador del usuario.

* Especifique valores para los elementos de Botón de opción y Casilla de verificación en `{value}={text}` en las propiedades de los componentes.
* El componente Archivo adjunto, de forma predeterminada, permite al usuario adjuntar un solo archivo. Sin embargo, puede configurar las propiedades del componente para que admitan varios archivos adjuntos. Además, si un usuario adjunta varios archivos con el mismo nombre de archivo, los archivos adjuntos pueden causar algunos problemas. Por lo tanto, se recomienda asociar un identificador único para cada archivo adjunto enviado en el envío del formulario. Para ello:

   1. En su [!DNL AEM Forms] servidor, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
   1. Buscar y pulsar **[!UICONTROL Servicio de configuración adaptable de Forms]**.
   1. En el cuadro de diálogo Servicio de configuración de Forms adaptable, active **[!UICONTROL Hacer únicos los nombres de archivo]**. De forma predeterminada, está desactivado.

* Para permitir que los usuarios adjunten un PDF mediante el explorador Safari, asegúrese de que **aplicación/pdf** se agrega a la propiedad Tipos de archivo compatibles del componente Archivo adjunto. Forms adaptable creado con versiones anteriores [!DNL AEM Forms] la versión puede contener **.pdf** en lugar de **aplicación/pdf** en la propiedad Tipos de archivo compatibles.

>[!NOTE]
>
>Los componentes de Formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL). Por ejemplo, hebreo.