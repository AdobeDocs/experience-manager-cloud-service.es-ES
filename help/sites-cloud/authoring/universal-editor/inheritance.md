---
title: Herencia de contenido en el editor universal
description: Descubra cómo el Editor universal admite la herencia de contenido para la administración de varios sitios y los lanzamientos para admitir la reutilización y localización de contenido.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 20f57e2b1b502f48f54e8a03d35a231d0c905739
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 3%

---

# Herencia de contenido en el editor universal {#inheritance}

Descubra cómo el Editor universal admite la herencia de contenido para la administración de varios sitios y los lanzamientos para admitir la reutilización y localización de contenido.

>[!NOTE]
>
>Esta función solo está disponible para el contenido almacenado en el repositorio de AEM.

## Caso práctico {#use-case}

Para muchos usuarios de AEM, crear una página es solo el principio. Para escalar el contenido de forma eficaz, normalmente se realizan los siguientes pasos después de la creación de la página:

1. **Traduzca la página** usando copias de idioma y flujos de trabajo de traducción.
1. **Localice la página** usando Multi Site Management para desplegar la página traducida en diferentes mercados.
1. **Crear nuevas versiones** utilizando Lanzamientos para preparar futuras iteraciones de la página y aplicar esos cambios.

Estos pasos pueden acelerar la velocidad del contenido y garantizar su coherencia. El editor universal admite la herencia de contenido, que es el mecanismo en el que se basan las copias de idioma, la administración de varios sitios y los lanzamientos.

## Herencia {#what-is-inheritance}

La herencia es el mecanismo por el que el contenido se puede vincular de modo que, al cambiar uno, se cambia automáticamente el otro.

MSM y los lanzamientos son herramientas útiles para ayudarle a reutilizar el contenido mediante la herencia. Las páginas se pueden copiar desde una fuente central (el modelo) para permitir a los autores realizar cambios específicos del contexto de esas copias, mientras que el resto del contenido permanece heredado del modelo. Esto resulta extremadamente útil a la hora de localizar sitios.

Para modificar parte del contenido de las copias, los autores rompen la herencia en los componentes afectados para garantizar que sus cambios locales no se sobrescriban cuando las copias se sincronizan desde el modelo.

## Herencia de contenido y editor universal {#universal-editor}

Cuando una página forma parte de MSM o de un lanzamiento y el contenido se edita con el editor universal, el editor desactiva automáticamente la herencia de todos los cambios realizados por los autores en esa página, lo que garantiza que el contenido modificado se conserva cuando las actualizaciones se sincronizan desde el modelo.

El autor no necesita hacer clic en un botón ni realizar ningún otro paso para deshabilitar la herencia antes de realizar modificaciones locales. Tan pronto como se realiza un cambio, la herencia se cancela implícitamente. Este flujo de trabajo contrasta con [Editor de páginas](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components).

La herencia se puede revertir para toda la página mediante el:

* [Consola de información general de Live Copy](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [Consola de lanzamiento](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Usando el botón **Restablecer** en la ficha **Live Copy** de la [ventana de propiedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md).

El editor universal no afecta al mecanismo subyacente de herencia. Para obtener más información sobre cómo funciona la herencia, consulte la siguiente documentación.

* [Administración de varios sitios (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)

### Extensión de AEM Multi-Site-Management (MSM) {#msm-extension}

Si está instalada, la extensión **AEM Multi-Site-Management (MSM) Extension** muestra el estado de herencia actual del componente seleccionado, así como le permite interrumpir o restablecer la herencia en el nivel de componente.

Consulte la [documentación de creación para obtener más información.](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)

## Limitaciones {#limitations}

* Para revertir la herencia de componentes únicos, debe habilitarse la extensión **AEM Multi-Site-Management (MSM)**.
* Para que los comentarios visuales vean qué componentes tienen deshabilitada la herencia y cuáles la conservan, debe habilitarse la extensión de administración de varios sitios de AEM **MSM (Multi-Site-Management)**.
* Actualmente, estas características están limitadas a los componentes de las páginas y aún no se aplican a [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md), a pesar de que también tienen capacidades de MSM y Launch.
