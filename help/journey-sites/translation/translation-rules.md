---
title: Configuración de las reglas de traducción
description: Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.
index: true
hide: false
hidefromtoc: false
exl-id: 831009b8-8e09-4b0f-b0fd-4e21221c1455
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 86%

---

# Configuración de las reglas de traducción {#configure-translation-rules}

Aprenda a definir reglas de traducción para identificar el contenido que se va a traducir.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de traducción de AEM Sites, [Configuración del conector de traducción](configure-connector.md) ha aprendido a instalar y configurar el conector de traducción y ahora debe hacer lo siguiente:

* Comprender los parámetros importantes del marco de trabajo de integración de traducción en AEM.
* Puede configurar su propia conexión con el servicio de traducción.

Ahora que el conector está configurado, este artículo le explica el siguiente paso para identificar qué contenido debe traducir.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo utilizar las reglas de traducción de AEM para identificar el contenido de la traducción. Después de leer este documento, debería poder hacer lo siguiente:

* Comprender lo que hacen las reglas de traducción.
* Poder definir sus propias reglas de traducción.

## Reglas de traducción {#translation-rules}

Las páginas de AEM Sites pueden contener mucha información. Según las necesidades del proyecto, es probable que no toda la información de una página deba traducirse.

Las reglas de traducción identifican el contenido que se incluye en los proyectos de traducción o que se excluye de ellos. Cuando se traduce contenido, AEM lo extrae o saca en función de estas reglas. De este modo, solo el contenido que debe traducirse se envía al servicio de traducción.

Las reglas de traducción incluyen la siguiente información:

* Ruta del contenido al que se aplica la regla
   * La regla también se aplica a los descendientes del contenido
* Nombres de las propiedades que contienen el contenido que se va a traducir
   * La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso

AEM crea automáticamente reglas de traducción para las páginas de sitios, pero como los requisitos de cada proyecto son diferentes, es importante que sepa cómo revisar y adaptar las reglas según sea necesario para su proyecto.

## Creación de reglas de traducción {#creating-rules}

Se pueden crear varias reglas para admitir requisitos de traducción complejos. Por ejemplo, un proyecto en el que esté trabajando requiere que se traduzca toda la información de la página, pero en otra página solo las descripciones deben traducirse mientras los títulos no estén traducidos.

Las reglas de traducción están diseñadas para manejar estos escenarios. Sin embargo, en este ejemplo ilustramos cómo crear reglas centrándose en una configuración simple y única.

Hay una consola de **Configuración de traducción** disponible para configurar las reglas de traducción.

Para acceder a ella:

1. Vaya a **Herramientas** > **General**.
1. Seleccione **Configuración de traducción**.

AEM crea automáticamente reglas de traducción para todo el contenido. Para ver estas reglas, haga lo siguiente:

1. Seleccione el `/content` contexto.
1. En la barra de herramientas, seleccione **Editar**.
1. El Editor de reglas de traducción se abre con las reglas que AEM crea automáticamente para la ruta `/content`.

   ![Editor de reglas de traducción](assets/translation-rules-editor.png)

1. Las propiedades de página que se traducen se encuentran en la sección **General** de la lista. Puede agregar o actualizar nombres de propiedades existentes que desee incluir explícitamente en la traducción.
   1. En el **Nueva propiedad** , introduzca el nombre de la propiedad. Las opciones **Traducir** y **Heredar** se marcan automáticamente.
   1. Seleccionar **Añadir**.
   1. Repita estos pasos para todos los campos que debe traducir.
   1. Seleccione **Guardar**.

Ya ha configurado las reglas de traducción.

>[!NOTE]
>
>AEM crea automáticamente las reglas de traducción. Para una configuración de traducción sencilla o para probar un flujo de trabajo de traducción, no es necesario crear nuevas reglas ni modificar las reglas creadas automáticamente existentes. Los detalles de estos pasos se presentan para explicar cómo funcionan las reglas y dar contexto a cómo AEM procesa las traducciones.

>[!TIP]
>
>También es posible crear reglas solo para una ruta o proyecto concreto tocando o haciendo clic en el botón **Agregar contexto** en la consola Configuración de traducción. Esto está fuera del ámbito de este recorrido.

## Uso avanzado {#advanced-usage}

Hay varias propiedades adicionales que se pueden configurar como parte de las reglas de traducción. Además, puede especificar las reglas manualmente como XML, lo que permite una mayor especificidad y flexibilidad.

Estas funciones generalmente no son necesarias para empezar a localizar el contenido. De igual manera, puede leer más sobre ellas en la sección [Recursos adicionales](#additional-resources).

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de traducción de AEM Sites, debe:

* Comprender lo que hacen las reglas de traducción.
* Poder definir sus propias reglas de traducción.

Aproveche este conocimiento y continúe con su recorrido de traducción de AEM Sites revisando el documento a continuación [Traducir contenido](translate-content.md) donde aprenderá cómo funcionan juntos el conector y las reglas para traducir contenido.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de traducción al revisar el documento [Traducción de contenido,](translate-content.md) los siguientes son algunos recursos opcionales que profundizan ciertos conceptos mencionados en este documento, pero que no son necesarios para continuar el recorrido.

* [Identificación del contenido para traducir](/help/sites-cloud/administering/translation/rules.md): aprenda cómo las reglas de traducción identifican el contenido que necesita traducirse.
