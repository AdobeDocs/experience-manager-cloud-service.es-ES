---
title: Configuración de reglas de traducción
description: Aprenda a definir reglas de traducción para identificar el contenido que se va a localizar.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Configurar reglas de traducción {#configure-translation-rules}

Aprenda a definir reglas de traducción para identificar el contenido que se va a localizar.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de localización AEM sin encabezado, [Configure translation connector](configure-connector.md) ha aprendido a instalar y configurar el conector de traducción y ahora debe:

* Comprender los parámetros importantes del marco de integración de traducción en AEM.
* Puede configurar su propia conexión con el servicio de traducción.

Ahora que el conector está configurado, este artículo le explica el siguiente paso para identificar qué contenido debe traducir.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar AEM reglas de traducción para identificar el contenido de la traducción. Después de leer este documento, debe:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

## Reglas de traducción {#translation-rules}

Las reglas de traducción identifican el contenido que se incluye en los proyectos de traducción o que se excluye de ellos. Cuando se traduce el contenido, AEM extrae el contenido en función de estas reglas para que se pueda enviar al servicio de traducción mediante el conector que ya ha configurado.

Las reglas de traducción incluyen la siguiente información:

* Ruta del contenido al que se aplica la regla
   * La regla también se aplica a los descendientes del contenido
* Nombres de las propiedades que contienen el contenido que se va a traducir
   * La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso

Debido a que los modelos de fragmento de contenido son exclusivos de su propio proyecto, es vital configurar reglas de traducción para AEM sepa qué elementos de los modelos de contenido traducir.

## Creación de reglas de traducción {#creating-rules}

Se pueden crear varias reglas para admitir requisitos de traducción complejos. Por ejemplo, un proyecto en el que esté trabajando requiere que se traduzcan todos los campos del modelo, pero en otro solo los campos de descripción deben traducirse mientras los títulos no se hayan traducido.

Las reglas de traducción están diseñadas para manejar estos escenarios. Sin embargo, en este ejemplo ilustraremos cómo crear reglas centrándose en una configuración simple y única.

Hay una consola **Configuración de traducción** disponible para configurar las reglas de traducción. Para acceder a él:

1. Vaya a **Tools** -> **General**.
1. Toque o haga clic en **Configuración de traducción**.

En la interfaz de usuario de **Configuración de traducción** hay varias opciones disponibles para las reglas de traducción. Aquí resaltaremos los pasos más necesarios y típicos necesarios para una configuración de localización básica y sin encabezado.

1. Toque o haga clic en **Agregar contexto**, que le permite agregar una ruta. Esta es la ruta del contenido que se verá afectado por la regla.
   ![Añadir contexto](assets/add-translation-context.png)
1. Utilice el navegador de rutas para seleccionar la ruta requerida y toque o haga clic en el botón **Confirm** para guardar. Recuerde que los fragmentos de contenido, que contienen contenido sin encabezado, generalmente se encuentran en `/content/dam/<your-project>`.
   ![Seleccione la ruta](assets/select-context.png)
1. AEM guarda la configuración.
1. Debe seleccionar el contexto que acaba de crear y, a continuación, tocar o hacer clic en **Editar**. Se abrirá el **Editor de reglas de traducción** para configurar las propiedades.
   ![Editor de reglas de traducción](assets/translation-rules-editor.png)
1. De forma predeterminada, todas las configuraciones se heredan de la ruta principal, en este caso `/content/dam`. Anule la selección de la opción **Heredar de`/content/dam`** para añadir campos adicionales a la configuración.
1. Una vez desmarcada, en la sección **General** de la lista, añada los nombres de propiedad que [identificó anteriormente como campos de traducción.](getting-started.md#content-models)
   1. Introduzca el nombre de la propiedad en el campo **New Property**.
   1. Las opciones **Translate** e **Inherit** se comprueban automáticamente.
   1. Toque o haga clic en **Agregar**.
   1. Repita estos pasos para todos los campos que necesite traducir.
   1. Toque o haga clic en **Guardar**.
      ![Agregar propiedad](assets/add-property.png)

Ya ha configurado las reglas de traducción.

## Uso avanzado {#advanced-usage}

Hay varias propiedades adicionales que se pueden configurar como parte de las reglas de traducción. Además, puede especificar las reglas manualmente como XML, lo que permite una mayor especificidad y flexibilidad.

Estas funciones generalmente no son necesarias para empezar a localizar el contenido sin encabezado, pero puede leer más sobre ellas en la sección [Recursos adicionales](#additional-resources) si le interesa.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de localización sin encabezado, debe:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

Aproveche este conocimiento y continúe con su recorrido de localización AEM sin encabezado revisando el documento [Translate content](translate-content.md), donde aprenderá cómo funcionan juntos sus conectores y reglas para traducir contenido sin encabezado.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de localización sin encabezado revisando el documento [Traducir contenido,](translate-content.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no es necesario que continúen en el recorrido sin encabezado.

* [Identificación del contenido para la traducción](/help/sites-cloud/administering/translation/rules.md) : obtenga información sobre cómo las reglas de traducción identifican el contenido que debe traducirse.
