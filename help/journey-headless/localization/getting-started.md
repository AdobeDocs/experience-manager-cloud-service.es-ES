---
title: Introducción a AEM localización sin encabezado
description: Obtenga información sobre cómo organizar el contenido sin encabezado y cómo funcionan AEM herramientas de localización.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Introducción a la localización sin encabezado de AEM {#getting-started}

Obtenga información sobre cómo organizar el contenido sin encabezado y cómo funcionan AEM herramientas de localización.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de localización AEM sin encabezado, [Obtenga información sobre el contenido sin encabezado y cómo localizar en AEM](learn-about.md) ha aprendido la teoría básica de lo que es un CMS sin encabezado y ahora debería:

* Comprender los conceptos básicos de la entrega de contenido sin encabezado.
* Familiarícese con cómo AEM admite la localización y la eliminación de encabezados.

Este artículo se basa en estos fundamentos para que entienda cómo AEM almacena y administra contenido sin objetivos y cómo puede utilizar AEM herramientas de localización para traducir ese contenido.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo empezar a localizar contenido sin encabezado en AEM. Después de leer, debe:

* Comprenda la importancia de la estructura de contenido para la localización.
* Comprenda cómo AEM almacena contenido sin encabezado.
* Familiarícese con AEM herramientas de localización.

## Requisitos y requisitos previos {#requirements-prerequisites}

Antes de empezar a localizar el contenido AEM sin encabezado, existen varios requisitos.

### Conocimiento {#knowledge}

* Experiencia en la localización de contenido para un CMS
* Experiencia utilizando las funciones básicas de un CMS a gran escala
* Tener un conocimiento práctico de AEM manipulación básica
* Comprensión del servicio de traducción que utiliza
* Tenga una comprensión básica del contenido que está traduciendo

>[!TIP]
>
>Si no está familiarizado con el uso de un CMS de gran escala como AEM, considere revisar la documentación de [Basic Handling](/help/sites-cloud/authoring/getting-started/basic-handling.md) antes de continuar. La documentación de Gestión básica no forma parte del recorrido, por lo que debe volver a esta página cuando haya terminado.

### Herramientas {#tools}

* Acceso a espacio aislado para probar la traducción del contenido
* Credenciales para conectarse al servicio de traducción preferido
* Ser miembro del grupo `project-administrators` en AEM

## La estructura es clave {#content-structure}

AEM contenido, ya sea páginas web tradicionales o sin encabezado, está impulsado por su estructura. AEM impone pocos requisitos a la estructura de contenido, pero tener en cuenta la jerarquía de contenido como parte de la planificación del proyecto puede hacer que la localización sea mucho más sencilla.

>[!TIP]
>
>Planifique la traducción y localización al principio del proyecto sin encabezado. Trabaje en estrecha colaboración con el director del proyecto y los arquitectos de contenido desde el principio.
>
>Puede ser necesario un &quot;administrador de proyectos de internacionalización&quot; como persona independiente, cuya responsabilidad es definir qué contenido debe traducirse y qué no, y qué contenido traducido pueden modificar los productores de contenido regionales o locales.

Cree un plan sobre la localización de contenido que necesitará.

* ¿Solo necesita idiomas diferentes o también un idioma para adoptar los detalles regionales?
* ¿Necesita contenido multimedia enriquecido como imágenes o vídeos para que sea diferente en diferentes configuraciones regionales?

## Cómo AEM Almacena Contenido Sin Cabeza {#headless-content-in-aem}

Para el especialista en localización, no es importante comprender en profundidad cómo AEM gestiona el contenido sin encabezado. Sin embargo, familiarizarse con los conceptos básicos y la terminología será muy útil, ya que más adelante utilizará AEM herramientas de localización. Lo más importante es que debe comprender su propio contenido y cómo está estructurado para localizarlo de forma eficaz.

### Modelos de contenido {#content-models}

Para que el contenido sin encabezado se envíe de forma coherente entre canales, regiones e idiomas, el contenido debe estar muy estructurado. AEM usa modelos de contenido para aplicar esta estructura. Considere los modelos de contenido como una especie de plantilla o patrón para crear contenido sin encabezado. Dado que cada proyecto tiene sus propias necesidades, cada proyecto define sus propios modelos de fragmento de contenido. AEM no tiene requisitos ni estructura fijos para estos modelos.

El arquitecto de contenido trabaja al principio del proyecto para definir esta estructura. Como se ha recomendado anteriormente, como especialista en localización, debe trabajar en estrecha colaboración con el arquitecto de contenido para comprender y organizar el contenido.

Dado que los modelos de contenido definen la estructura del contenido, debe saber qué campos de los modelos deben traducirse. Normalmente, se trabaja con el arquitecto de contenido para definir esto. Para examinar los campos de los modelos de contenido, siga los pasos a continuación.

1. Vaya a **Herramientas** -> **Recursos** -> **Modelos de fragmento de contenido**.
1. Los modelos de fragmento de contenido generalmente se almacenan en una estructura de carpetas. Toque o haga clic en la carpeta de su proyecto.
1. Se muestran los modelos. Toque o haga clic en el modelo para ver los detalles.
   ![Modelos de fragmento de contenido](assets/content-fragment-models.png)
1. Se abre el **Editor del modelo de fragmento de contenido**.
   1. La columna izquierda contiene los campos del modelo. Esta columna nos interesa.
   1. La columna derecha contiene los campos que se pueden agregar al modelo. Esta columna se puede ignorar.
      ![Editor del modelo de fragmento de contenido](assets/content-fragment-model-editor.png)
1. Toque o haga clic en uno de los campos del modelo. AEM marca y los detalles de ese campo se muestran en la columna derecha.
   ![Detalles del Editor del modelo de fragmento de contenido](assets/content-fragment-model-editor-detail.png)

Tome nota del campo **Nombre de propiedad** para todos los campos que deben traducirse. Necesitará esta información para el siguiente paso del recorrido.

### Fragmentos de contenido {#content-fragments}

Los autores de contenido utilizan los modelos de contenido para crear el contenido sin encabezado real. Los autores de contenido seleccionan en qué modelo basar su contenido y luego crean fragmentos de contenido. Los fragmentos de contenido son instancias de los modelos y representan el contenido real que se va a entregar sin problemas.

Si los modelos de contenido son los patrones para el contenido, los fragmentos de contenido son el contenido real basado en esos patrones.

Los fragmentos de contenido se administran como recursos en AEM como parte de la administración de recursos digitales (DAM). Esto es importante, ya que todos se ubicarán bajo la ruta `/content/dam`.

## Estructura de contenido recomendada {#recommended-structure}

Como se recomendó anteriormente, trabaje con su arquitecto de contenido para determinar la estructura de contenido adecuada para su propio proyecto. Sin embargo, lo siguiente es una estructura probada, simple e intuitiva que es bastante efectiva.

Defina una carpeta base para su proyecto en `/content/dam`.

```text
/content/dam/<your-project>
```

El idioma en el que se crea el contenido se denomina raíz del idioma. En nuestro ejemplo es inglés y debería estar por debajo de este camino.

```text
/content/dam/<your-project>/en
```

Todo el contenido del proyecto que puede ser necesario localizar en caso de que se coloque en el idioma maestro.

```text
/content/dam/<your-project>/en/<your-project-content>
```

Las ubicaciones deben crearse como carpetas del mismo nivel a lo largo de la raíz del idioma. Por ejemplo, el alemán tendría la siguiente ruta.

```text
/content/dam/<your-project>/de
```

La estructura final puede tener un aspecto similar al siguiente.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

## Herramientas de localización de AEM {#localization-tools}

Ahora que comprende qué son los fragmentos de contenido y la importancia de la estructura de contenido, podemos ver cómo localizar este contenido. Las herramientas de localización en AEM son bastante poderosas, pero son fáciles de entender a un alto nivel.

* **Conector de traducción** : el conector es el vínculo entre AEM y el servicio de traducción que utiliza.
* **Reglas de traducción** : las reglas definen qué contenido bajo rutas específicas se debe traducir.
* **Proyectos de traducción** : los proyectos de traducción reúnen contenido que debe tratarse como un esfuerzo de traducción único y rastrean el progreso de la traducción, interconectándose con el conector para transmitir el contenido que se va a traducir y recibir de nuevo del servicio de traducción.

Por lo general, solo necesita configurar el conector una vez para la instancia y las reglas por proyecto sin encabezado. A continuación, utilice proyectos de traducción para localizar su contenido y mantener sus traducciones actualizadas de forma continua.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de localización sin encabezado, debe:

* Comprenda la importancia de la estructura de contenido para la localización.
* Comprenda cómo AEM almacena contenido sin encabezado.
* Familiarícese con AEM herramientas de localización.

Aproveche este conocimiento y continúe con su recorrido de localización AEM sin encabezado revisando el documento [Configure el conector de traducción](configure-connector.md) donde aprenderá a conectar AEM a un servicio de traducción.|

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de localización sin encabezado revisando el documento [Configure the translation connector](configure-connector.md), los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido sin encabezado.

* [AEM Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) : Descubra los conceptos básicos de la IU de AEM para poder desplazarse cómodamente y realizar tareas esenciales como encontrar su contenido.
* [Identificación del contenido para la traducción](/help/sites-cloud/administering/translation/rules.md) : obtenga información sobre cómo las reglas de traducción identifican el contenido que debe traducirse.
* [Configuración del marco de integración de traducción](/help/sites-cloud/administering/translation/integration-framework.md) : Aprenda a configurar el marco de integración de traducción para integrarlo con servicios de traducción de terceros.
* [Administración de proyectos de traducción](/help/sites-cloud/administering/translation/managing-projects.md) : Aprenda a crear y administrar proyectos de traducción automática y humana en AEM.
