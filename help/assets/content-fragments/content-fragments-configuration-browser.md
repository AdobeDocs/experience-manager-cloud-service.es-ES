---
title: 'Fragmentos de contenido: navegador de configuración (Recursos - Fragmentos de contenido)'
description: Obtenga información sobre cómo habilitar la funcionalidad Fragmento de contenido en el navegador de configuración.
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 34574fdc7f246499bd238fef388671d2287e62bc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 84%

---

# Fragmentos de contenido: explorador de configuración{#content-fragments-configuration-browser}

Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.

## Habilitación de la funcionalidad de fragmento de contenido para la instancia {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de contenido, debe usar el **Explorador de configuración** para habilitar lo siguiente:

* **Modelos de fragmentos de contenido**: obligatorio
* **Consultas persistentes de GraphQL**: opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmentos de contenido**:
>
>* la opción **Crear** no estará disponible para crear nuevos modelos.
>* no podrá [seleccionar la configuración de Sites para crear el punto de conexión relacionado](/help/headless/graphql-api/graphql-endpoint.md).


Para habilitar la funcionalidad de fragmento de contenido, debe hacer lo siguiente:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el Explorador de configuración
* Aplicar la configuración a la carpeta de Assets

### Habilitación de la funcionalidad de fragmento de contenido en el Explorador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar ciertas funcionalidades de fragmentos de contenido](#creating-a-content-fragment-model), primero **debe** activarlas a través del **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte también [Explorador de configuración:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfiguraciones](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (una configuración anidada en otra configuración) es totalmente compatible para su uso con fragmentos de contenido, modelos de fragmentos de contenido y consultas de GraphQL.
>
>Solo tenga en cuenta lo siguiente:
>
>
>* Después de crear modelos en una subconfiguración, NO es posible mover o copiar el modelo a otra subconfiguración.
>
>* Un extremo de GraphQL (aún) se basará en una configuración principal (raíz).
>
>* Las consultas persistentes se guardarán (aún) de forma relevante para la configuración principal (raíz).



1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Use **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. El **Nombre** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Puede ajustarlo si es necesario.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmentos de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)


1. Seleccione **Crear** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicación de la configuración a la carpeta Recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitado para la funcionalidad de fragmentos de contenido y se aplica a cualquier carpeta de recursos.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

![Aplicar configuración](assets/cfm-conf-02.png)
