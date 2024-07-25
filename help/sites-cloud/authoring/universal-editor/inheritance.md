---
title: Herencia de contenido en el editor universal
description: Descubra cómo el Editor universal admite la herencia de contenido para la administración de varios sitios y los lanzamientos para admitir la reutilización y localización de contenido.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---


# Herencia de contenido en el editor universal {#inheritance}

Descubra cómo el Editor universal admite la herencia de contenido para la administración de varios sitios y los lanzamientos para admitir la reutilización y localización de contenido.

## Caso práctico {#use-case}

AEM Para muchos usuarios de la aplicación, crear una página es solo el comienzo de la creación de una página. Para escalar el contenido de forma eficaz, normalmente se realizan los siguientes pasos después de la creación de la página:

1. **Traduzca la página** usando copias de idioma y flujos de trabajo de traducción.
1. **Localice la página** usando Multi Site Management para desplegar la página traducida en diferentes mercados.
1. **Crear nuevas versiones** utilizando Lanzamientos para preparar futuras iteraciones de la página y aplicar esos cambios.

Estos pasos pueden acelerar la velocidad del contenido y garantizar su coherencia. El editor universal admite la herencia de contenido, que es el mecanismo en el que se basan estos pasos.

## Herencia {#what-is-inheritance}

La herencia es el mecanismo por el que el contenido se puede vincular de modo que, al cambiar uno, se cambia automáticamente el otro. Los componentes heredados pueden ser el producto de distintos escenarios, como por ejemplo:

* [Administración de varios sitios (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)

MSM y los lanzamientos son herramientas potentes que le ayudan a reutilizar el contenido. Las páginas se pueden copiar desde una fuente central (el modelo) para permitir a los autores realizar cambios específicos del contexto de esas copias, mientras que el resto del contenido permanece heredado del modelo. Esto resulta extremadamente útil a la hora de localizar sitios.

Para modificar parte del contenido de las copias, los autores rompen la herencia en los componentes afectados para garantizar que sus cambios locales no se sobrescriban cuando las copias se sincronizan desde el modelo.

## Herencia de contenido y editor universal {#universal-editor}

Cuando una página forma parte de MSM o de un lanzamiento y el contenido se edita con el editor universal, el editor desactiva automáticamente la herencia de todos los cambios realizados por los autores en esa página, lo que garantiza que el contenido modificado se conserva cuando las actualizaciones se sincronizan desde el modelo.

El autor no necesita hacer clic en un botón ni realizar ningún otro paso para deshabilitar la herencia antes de realizar modificaciones locales. Tan pronto como se realiza un cambio, la herencia se cancela implícitamente. Esto contrasta con el [Editor de páginas.](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)

## Limitaciones {#limitations}

* Los autores no pueden revertir la herencia para componentes únicos.
   * La herencia solo se puede revertir para toda la página a través de la [Consola de información general de Live Copy](/help/sites-cloud/administering/msm/live-copy-overview.md) o la [Consola de inicios.](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Los autores no tienen comentarios visuales para ver qué componentes tienen deshabilitada la herencia y cuáles aún la conservan.
* Actualmente, estas características están limitadas a los componentes de las páginas y aún no se aplican a [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md), a pesar de que también tienen capacidades de MSM y Launch.
