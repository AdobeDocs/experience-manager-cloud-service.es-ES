---
title: Configurar reglas de traducción
description: Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.
index: true
hide: false
hidefromtoc: false
source-git-commit: 08127d72c84d6f47f5058ef631dc3128114f1953
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Configurar reglas de traducción {#configure-translation-rules}

Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción de AEM Sites, [Configure translation connector](configure-connector.md) ha aprendido a instalar y configurar el conector de traducción y ahora debe:

* Comprender los parámetros importantes del marco de integración de traducción en AEM.
* Puede configurar su propia conexión con el servicio de traducción.

Ahora que el conector está configurado, este artículo le explica el siguiente paso para identificar qué contenido debe traducir.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar AEM reglas de traducción para identificar el contenido de la traducción. Después de leer este documento, debe:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

## Reglas de traducción {#translation-rules}

Las páginas de AEM Sites pueden contener mucha información. Según las necesidades del proyecto, es probable que no toda la información de una página deba traducirse.

Las reglas de traducción identifican el contenido que se incluye en los proyectos de traducción o que se excluye de ellos. Cuando se traduce el contenido, AEM extrae o cosecha el contenido en función de estas reglas. De este modo, solo el contenido que debe traducirse se envía al servicio de traducción.

Las reglas de traducción incluyen la siguiente información:

* Ruta del contenido al que se aplica la regla
   * La regla también se aplica a los descendientes del contenido
* Nombres de las propiedades que contienen el contenido que se va a traducir
   * La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso

AEM crea automáticamente reglas de traducción para las páginas de sitios, pero como los requisitos de cada proyecto son diferentes, es importante que sepa cómo revisar y adaptar las reglas según sea necesario para su proyecto.

## Creación de reglas de traducción {#creating-rules}

Se pueden crear varias reglas para admitir requisitos de traducción complejos. Por ejemplo, un proyecto en el que esté trabajando requiere que se traduzca toda la información de la página, pero en otra página solo las descripciones deben traducirse mientras los títulos no estén traducidos.

Las reglas de traducción están diseñadas para manejar estos escenarios. Sin embargo, en este ejemplo ilustramos cómo crear reglas centrándose en una configuración simple y única.

Hay una consola **Configuración de traducción** disponible para configurar las reglas de traducción.

Para acceder a él:

1. Vaya a **Tools** -> **General**.
1. Toque o haga clic en **Configuración de traducción**.

AEM crea automáticamente reglas de traducción para todo el contenido. Para ver estas reglas:

1. Seleccione el contexto `/content` y, a continuación, la opción **Editar** en la barra de herramientas.
1. El Editor de reglas de traducción se abre con las reglas que AEM creadas automáticamente para la ruta `/content`.

   ![Editor de reglas de traducción](assets/translation-rules-editor.png)

1. Las propiedades de página que se traducirán se encuentran en la sección **General** de la lista. Puede agregar o actualizar nombres de propiedades existentes que desee incluir explícitamente en la traducción.
   1. Introduzca el nombre de la propiedad en el campo **New Property**.
   1. Las opciones **Translate** e **Inherit** se comprueban automáticamente.
   1. Toque o haga clic en **Agregar**.
   1. Repita estos pasos para todos los campos que debe traducir.
   1. Toque o haga clic en **Guardar**.

Ya ha configurado las reglas de traducción.

>[!NOTE]
>
>AEM crea automáticamente reglas de traducción. Para una sencilla configuración de traducción o para probar un flujo de trabajo de traducción, no es necesario crear nuevas reglas ni modificar las reglas creadas automáticamente existentes. Los detalles de estos pasos se presentan para explicar cómo funcionan las reglas y dar contexto a cómo procesan AEM traducciones.

>[!TIP]
>
>También es posible crear reglas solo para una ruta o proyecto concreto tocando o haciendo clic en el botón **Agregar contexto** de la consola Configuración de traducción. Esto está fuera del ámbito de este recorrido.

## Uso avanzado {#advanced-usage}

Hay varias propiedades adicionales que se pueden configurar como parte de las reglas de traducción. Además, puede especificar las reglas manualmente como XML, lo que permite una mayor especificidad y flexibilidad.

Estas funciones generalmente no son necesarias para empezar a localizar el contenido, pero puede leer más sobre ellas en la sección [Recursos adicionales](#additional-resources) si le interesa.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción de AEM Sites, debe:

* Comprender lo que hacen las reglas de traducción.
* Puede definir sus propias reglas de traducción.

Aproveche este conocimiento y continúe con su recorrido de traducción de AEM Sites revisando el documento [Traducir contenido](translate-content.md), donde aprenderá cómo funcionan juntos sus conectores y reglas para traducir contenido.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción revisando el documento [Traducir contenido,](translate-content.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no es necesario que continúen en el recorrido.

* [Identificación del contenido para la traducción](/help/sites-cloud/administering/translation/rules.md) : obtenga información sobre cómo las reglas de traducción identifican el contenido que debe traducirse.
