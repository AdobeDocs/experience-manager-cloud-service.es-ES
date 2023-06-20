---
title: Configuración del entorno de la cuenta
description: AEM le permite configurar su cuenta y ciertos aspectos del entorno de creación
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 73%

---

# Configuración del entorno de la cuenta   {#configuring-your-account-environment}

AEM le permite configurar su cuenta y ciertos aspectos del entorno de creación.

Mediante la opción [Usuario](#user-settings) del [encabezado](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header) y el cuadro de diálogo [Mis preferencias](#my-preferences) asociado, puede modificar las opciones de usuario.

Para comenzar, acceda a la opción [Usuario](#user-settings) en el encabezado.

## Configuración de usuario {#user-settings}

El **Usuario** El cuadro de diálogo de configuración le permite acceder a:

* Suplantar como
   * Con la función Suplantar como, un usuario puede trabajar en nombre de otro usuario. <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* Perfil
   * Ofrece un práctico vínculo a la configuración de usuario<!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->.
* [Mis preferencias](#my-preferences)
   * Especifique las distintas preferencias exclusivas al usuario 

![Configuración de usuario](/help/sites-cloud/authoring/assets/user-settings.png)

### Mis preferencias {#my-preferences}

Puede acceder al cuadro de diálogo **Preferencias** a través de la opción [Usuario](#user-settings) en el encabezado.

Cada usuario puede establecer determinadas propiedades para sí mismo. 

![Mis preferencias](/help/sites-cloud/authoring/assets/user-preferences.png)

* **Idioma**

  Define el idioma que se utilizará para la interfaz de usuario del entorno de creación. Seleccione el idioma en la lista disponible.

* **Gestión de ventanas**

  Define el comportamiento para abrir ventanas. Seleccione:

   * **Varias ventanas** (Predeterminado)

      * Las páginas se abren en una nueva ventana.

   * **Ventana única**

      * Las páginas se abren en la ventana actual.

* **Mostrar las acciones del escritorio para Assets**

  AEM Esta opción requiere que utilice la aplicación de escritorio de la.

* **Color de anotación**

  Define el color predeterminado que se utiliza para realizar anotaciones.

   * Haga clic en el bloque de colores para abrir el selector de muestras y seleccionar un color.
   * Como alternativa, introduzca el código hexadecimal del color deseado en el campo. 

* **Presentación de fecha relativa**

  Para mejorar la legibilidad, AEM procesará las fechas dentro de los últimos siete días como fechas relativas (por ejemplo, hace tres días) y las fechas más antiguas como fechas exactas (por ejemplo, el 20 de marzo de 2017).

  Esta opción define el modo en que se muestran las fechas del sistema. Las opciones disponibles son las siguientes:

   * **Mostrar siempre la fecha exacta**: se muestra siempre la fecha exacta (nunca una fecha relativa).
   * **1 día**: se muestra la fecha relativa para las fechas dentro de un día; de lo contrario, se muestra una fecha exacta. 
   * **7 días (valor predeterminado)**: se muestra la fecha relativa para las fechas dentro de siete días; de lo contrario, se muestra una fecha exacta. 
   * **1 mes**: se muestra la fecha relativa para las fechas dentro de un mes; de lo contrario, se muestra una fecha exacta. 
   * **1 año**: se muestra la fecha relativa para las fechas dentro de un año; de lo contrario se muestra una fecha exacta. 
   * **Mostrar siempre la fecha relativa**: las fechas exactas nunca se muestran, y solo se muestran fechas relativas.

* **Habilitar métodos abreviados**

  AEM admite varios métodos abreviados del teclado para mejorar la eficiencia de la creación de contenido.

   * [Métodos abreviados del teclado para editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [Métodos abreviados del teclado para las consolas](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

  Esta opción habilita los métodos abreviados de teclado. De forma predeterminada están habilitadas, pero se pueden deshabilitar, por ejemplo, si un usuario tiene ciertos requisitos de accesibilidad.

* **Activar la página principal de los recursos**

  Esta opción solo está disponible si el administrador del sistema ha habilitado la experiencia de la página principal de los recursos para toda la organización.

* **Configuración de Stock**

  Esta opción permite especificar la configuración preferida de Adobe Stock y solo estará disponible si el administrador del sistema ha activado [Integración de Adobe Stock](/help/assets/aem-assets-adobe-stock.md).
