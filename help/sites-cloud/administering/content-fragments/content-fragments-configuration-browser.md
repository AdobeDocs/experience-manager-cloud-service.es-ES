---
title: 'Fragmentos de contenido: explorador de configuración'
description: Obtenga información sobre cómo habilitar la funcionalidad Fragmento de contenido y GraphQL AEM en el Explorador de configuración para utilizar las funciones de envío sin encabezado de la aplicación de la configuración de la aplicación para utilizar las funciones de envío sin encabezado de la aplicación.
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 1fc57dacbf811070664d5f5aaa591dd705516fa8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 34%

---

# Fragmentos de contenido: explorador de configuración{#content-fragments-configuration-browser}

Obtenga información sobre cómo habilitar una funcionalidad de fragmento de contenido específica en el Explorador de configuración.

## Habilitación de la funcionalidad de fragmento de contenido para la instancia {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de contenido, debe usar la variable **Explorador de configuración** para habilitar:

* **Modelos de fragmentos de contenido**: obligatorio
* **Consultas persistentes de GraphQL**: opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmentos de contenido**:
>
>* el **Crear** La opción no está disponible para crear modelos.
>* no puede [seleccione la configuración de Sites para crear el punto final relacionado](/help/headless/graphql-api/graphql-endpoint.md).

Para habilitar la funcionalidad de fragmento de contenido, debe hacer lo siguiente:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el Explorador de configuración
* Aplicar la configuración a la carpeta de Assets

### Habilitación de la funcionalidad de fragmento de contenido en el Explorador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Para usar ciertos [Funcionalidad de fragmento de contenido](#creating-a-content-fragment-model), usted **debe** habilite primero estas opciones a través de **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfiguraciones](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (una configuración anidada en otra configuración) son totalmente compatibles para su uso con fragmentos de contenido, modelos de fragmentos de contenido y consultas de GraphQL.
>
>Solo tenga en cuenta lo siguiente:
>
>
>* Después de crear modelos en una subconfiguración, NO es posible mover o copiar el modelo a otra subconfiguración.
>
>* Un extremo de GraphQL se basa (aún) en una configuración principal (raíz).
>
>* Las consultas persistentes se guardan (aún) de forma relevante para la configuración principal (raíz).


1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Use **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. El **Nombre** se convierte en el nombre de nodo del repositorio.
      * Se genera automáticamente en función del título y se ajusta según [AEM Convenciones de nomenclatura de.](/help/implementing/developing/introduction/naming-conventions.md)
      * Puede ajustarlo si es necesario.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmentos de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)

1. Seleccione **Crear** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta {#apply-the-configuration-to-your-folder}

Cuando la configuración **global** está habilitado para la funcionalidad de fragmento de contenido, se aplica a cualquier carpeta de recursos, accesible a través de **Assets** consola.

Para utilizar otras configuraciones (es decir, excluidas las globales) con una carpeta de Assets comparable, debe definir la conexión. Esta conexión se realiza seleccionando la opción **Configuración** en el **Cloud Services** de la pestaña **Propiedades de carpeta** de la carpeta adecuada.

![Aplicar configuración](assets/cfm-conf-02.png)
