---
title: 'Fragmentos de contenido: navegador de configuración'
description: Obtenga información sobre cómo habilitar ciertas funciones de fragmento de contenido en el navegador de configuración.
translation-type: tm+mt
source-git-commit: da8fcf1288482d406657876b5d4c00b413461b21
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 18%

---


# Fragmentos de contenido - Navegador de configuración{#content-fragments-configuration-browser}

>[!CAUTION]
>
>El Envío API de GraphQL de AEM para fragmentos de contenido está disponible bajo petición.
>
>Póngase en contacto con [Soporte técnico de Adobe](https://experienceleague.adobe.com/?lang=en&amp;support-solution=General#support) para habilitar la API para su AEM como programa de Cloud Service.

## Habilitar la funcionalidad de fragmento de contenido para su instancia {#enable-content-fragment-functionality-instance}

Antes de utilizar fragmentos de contenido, debe utilizar el **Navegador de configuración** para habilitar:

* **Modelos**  de fragmento de contenido: obligatorio
* **Consultas**  persistentes de GraphQL: opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmento de contenido**, la opción **Crear** no estará disponible para crear nuevos modelos.

Para habilitar la funcionalidad de fragmento de contenido, debe:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el navegador de configuración
* Aplicar la configuración a la carpeta Assets

### Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Para [utilizar cierta funcionalidad de fragmento de contenido](#creating-a-content-fragment-model) **primero debe** habilitarlos mediante el **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte también [Navegador de configuración:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Las subconfiguraciones (una configuración anidada en una configuración) no son compatibles para su uso con fragmentos de contenido.

1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Utilice **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmento de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)


1. Seleccione **Crear** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitada para la funcionalidad de fragmento de contenido, se aplica a cualquier carpeta de recursos.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

![Aplicar configuración](assets/cfm-conf-02.png)