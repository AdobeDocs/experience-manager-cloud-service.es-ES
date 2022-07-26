---
title: 'Fragmentos de contenido: navegador de configuración'
description: Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 23%

---

# Fragmentos de contenido: navegador de configuración{#content-fragments-configuration-browser}

Aprenda a habilitar ciertas funciones de fragmento de contenido en el navegador de configuración para aprovechar AEM potentes funciones de envío sin periféricos.

## Habilitación de la funcionalidad de fragmento de contenido para la instancia {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de contenido, debe usar la variable **Explorador de configuración** para habilitar:

* **Modelos de fragmento de contenido** - obligatorio
* **Consultas persistentes de GraphQL** - opcional

>[!CAUTION]
>
>Si no habilita **Modelos de fragmento de contenido**:
>
>* el **Crear** no estará disponible para crear nuevos modelos.
>* no podrá [seleccione la configuración Sitios para crear el punto final relacionado](/help/headless/graphql-api/graphql-endpoint.md).


Para habilitar la funcionalidad de fragmento de contenido, debe:

* Habilitar el uso de la funcionalidad de fragmento de contenido mediante el navegador de configuración
* Aplique la configuración a la carpeta Assets

### Habilitar la funcionalidad de fragmento de contenido en el navegador de configuración {#enable-content-fragment-functionality-in-configuration-browser}

Hasta [usar ciertas funciones de fragmento de contenido](#creating-a-content-fragment-model) you **must** primero, actívelos a través de la variable **Explorador de configuración**:

>[!NOTE]
>
>Para obtener más información, consulte también [Explorador de configuración:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfiguraciones](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (una configuración anidada en otra configuración) es totalmente compatible para su uso con fragmentos de contenido, modelos de fragmentos de contenido y consultas de GraphQL.
>
>Sólo para tener en cuenta que:
>
>
>* Después de crear modelos en una subconfiguración, NO es posible mover o copiar el modelo a otra subconfiguración.
>
>* Un extremo de GraphQL (aún) se basará en una configuración principal (raíz).
>
>* Las consultas persistentes se guardarán (aún) de forma relevante para la configuración principal (raíz).



1. Vaya a **Herramientas**, **General**, luego abra el **Explorador de configuración**.

1. Uso **Crear** para abrir el cuadro de diálogo, donde:

   1. Especifique un **Título**.
   1. El **Nombre** se convertirá en el nombre de nodo en el repositorio.
      * Se generará automáticamente en función del título y se ajustará según las [convenciones de nomenclatura de AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Puede ajustarlo si es necesario.
   1. Para habilitar su uso, seleccione
      * **Modelos de fragmentos de contenido**
      * **Consultas persistentes de GraphQL**

      ![Definir configuración](assets/cfm-conf-01.png)


1. Select **Crear** para guardar la definición.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar la configuración a la carpeta de recursos {#apply-the-configuration-to-your-assets-folder}

Cuando la configuración **global** está habilitado para la funcionalidad de fragmentos de contenido y se aplica a cualquier carpeta de recursos.

Para utilizar otras configuraciones (es decir, excluyendo global) con una carpeta de Assets comparable, debe definir la conexión. Para ello, seleccione la **configuración** adecuada en la pestaña **Cloud Services** de las **Propiedades de carpeta** de la carpeta correspondiente.

![Aplicar configuración](assets/cfm-conf-02.png)
