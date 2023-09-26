---
title: Configuración del entorno de la cuenta
description: Adobe Experience Manager AEM () permite configurar la cuenta y ciertos elementos del entorno de creación.
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 60%

---

# Configuración del entorno de la cuenta   {#configuring-your-account-environment}

Adobe Experience Manager AEM () permite configurar la cuenta y ciertos elementos del entorno de creación.

Mediante la opción [Usuario](#user-settings) del [encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header) y el cuadro de diálogo [Mis preferencias](#my-preferences) asociado, puede modificar las opciones de usuario.

Para comenzar, acceda a la opción [Usuario](#user-settings) en el encabezado.

## Configuración de usuario {#user-settings}

El cuadro de diálogo de configuración **Usuario** le da acceso a lo siguiente:

* Suplantar como
   * Con la función Suplantar como, un usuario puede trabajar en nombre de otro usuario. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Perfil
   * Ofrece un práctico vínculo a la configuración del usuario <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [Mis preferencias](#my-preferences)
   * Especifique las distintas preferencias exclusivas al usuario 

![Configuración de usuario](/help/sites-cloud/authoring/assets/user-settings.png)

### Mis preferencias {#my-preferences}

El **Mis preferencias** se accede al cuadro de diálogo a través del [Usuario](#user-settings) en el encabezado.

Cada usuario puede establecer sus propias propiedades preferidas.

![Mis preferencias](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Idioma**

  Se trata del idioma que se utiliza para la IU del entorno de creación. Seleccione el idioma requerido de la lista disponible.

* **Gestión de ventanas**

  Esta opción permite definir el comportamiento o la apertura de las ventanas. Seleccione:

   * **Varias ventanas** (predeterminado)

      * Las páginas se abren en una nueva ventana.

   * **Ventana única**

      * Las páginas se abren en la ventana actual.

* **Mostrar las acciones del escritorio para Assets**

  AEM Esta opción requiere que utilice la aplicación de escritorio de la aplicación de.

* **Color de anotación**

  Define el color predeterminado que se utiliza para realizar anotaciones.

   * Haga clic en el bloque de colores para poder abrir el selector de muestras y seleccionar un color.
   * Como alternativa, introduzca el código hexadecimal del color deseado en el campo. 

* **Presentación de fecha relativa**

  AEM Para mejorar la legibilidad, la función procesa las fechas dentro de los últimos siete días como fechas relativas (por ejemplo, hace tres días) y las fechas más antiguas como fechas exactas (por ejemplo, el 20 de marzo de 2017).

  Esta opción define el modo en que se muestran las fechas del sistema. Las opciones disponibles son las siguientes:

   * **Mostrar siempre la fecha exacta**: se muestra siempre la fecha exacta (nunca una fecha relativa).
   * **1 día**: se muestra la fecha relativa para las fechas dentro de un día; de lo contrario, se muestra una fecha exacta. 
   * **7 días (valor predeterminado)**: se muestra la fecha relativa para las fechas dentro de siete días; de lo contrario, se muestra una fecha exacta. 
   * **1 mes**: se muestra la fecha relativa para las fechas dentro de un mes; de lo contrario, se muestra una fecha exacta. 
   * **1 año**: se muestra la fecha relativa para las fechas dentro de un año; de lo contrario se muestra una fecha exacta. 
   * **Mostrar siempre la fecha relativa**: las fechas exactas nunca se muestran, y solo se muestran fechas relativas.

* **Habilitar métodos abreviados**

  AEM La creación de formularios es compatible con varios métodos abreviados de teclado que hacen que la creación sea más eficaz.

   * [Métodos abreviados del teclado para editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [Métodos abreviados del teclado para las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

  Esta opción habilita los métodos abreviados de teclado. De forma predeterminada, están habilitadas, pero se pueden deshabilitar, por ejemplo, si un usuario tiene ciertos requisitos de accesibilidad.

* **Activar la página principal de los recursos**

  Esta opción solo está disponible si el administrador del sistema ha habilitado la experiencia de la página principal de los recursos para toda la organización.

* **Configuración de Stock**

  Esta opción le permite especificar la configuración preferida de Adobe Stock y solo está disponible si el administrador del sistema ha activado [Integración de Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
