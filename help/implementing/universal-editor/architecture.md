---
title: Arquitectura de editor universal
description: Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---


# Arquitectura de editor universal {#architecture}

Obtenga información sobre la arquitectura del Editor universal y cómo fluyen los datos entre sus servicios y capas.

## Componentes de arquitectura {#building-blocks}

El editor universal consta de cuatro componentes básicos que interactúan para permitir que los autores de contenido editen cualquier aspecto de cualquier contenido en cualquier implementación con el fin de ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.

1. [Editores](#editors)
1. [Aplicación remota](#remote-app)
1. [Capa de API](#api-layer)
1. [Capa de persistencia](#persistence-layer)

Este documento describe cada uno de estos componentes básicos y cómo intercambian datos.

![Arquitectura del editor universal](assets/architecture.png)

>[!TIP]
>
>Si desea ver el Editor universal y su arquitectura en acción, consulte el documento [Introducción al Editor universal en AEM](getting-started.md) para obtener información sobre cómo acceder al editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.

### Editores {#editors}

* **Editor universal** - El Editor universal utiliza un DOM instrumentado para permitir la edición in situ del contenido. Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los metadatos necesarios. Consulte el documento [Introducción al Editor universal en AEM](getting-started.md) para ver un ejemplo de la instrumentación en AEM.
* **Carril de propiedades** - Algunas propiedades de los componentes no se pueden editar en contexto, por ejemplo, el tiempo de rotación de un carrusel o la pestaña de acordeón que siempre se abrirá o cerrará. Para permitir la edición de dicha información de componentes, se proporciona un editor basado en formularios en el carril lateral del editor.

### Aplicación remota {#remote-app}

Para que una aplicación se pueda editar en contexto dentro del Editor universal, se debe instrumentar el DOM. La aplicación remota debe representar ciertos atributos en el DOM. Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los metadatos necesarios. Consulte el documento [Introducción al Editor universal en AEM](getting-started.md) para ver un ejemplo de la instrumentación en AEM.

El editor universal se esfuerza por conseguir un SDK mínimo, por lo que la instrumentación es responsabilidad de la implementación de la aplicación remota.

### Capa de API {#api-layer}

* **Datos de contenido** - Para el editor universal, no es importante ni los sistemas de origen de los datos de contenido ni la forma en que se consumen. Solo es importante definir y proporcionar los atributos necesarios utilizando datos editables en contexto.
* **Datos persistentes** - Para cada dato editable hay un identificador URN. Este URN se utiliza para enrutar la persistencia al sistema y recurso correctos.

### Capa de persistencia {#persistence-layer}

* **Modelo de fragmento de contenido** : para admitir el carril para editar las propiedades del fragmento de contenido, el editor de fragmentos de contenido y los editores basados en formularios, se requieren modelos por componente y fragmento de contenido.
* **Contenido** - El contenido se puede almacenar en cualquier parte, como en AEM, Magento, etc.

![Capa de persistencia](assets/persistence-layer.png)

## Servicio de editor universal y envío del sistema back-end {#service}

El editor universal envía todos los cambios de contenido a un servicio centralizado denominado Servicio de editor universal. Este servicio, que se ejecuta en Adobe I/O Runtime, carga los complementos disponibles en el Registro de extensiones en función del URN proporcionado. El complemento es responsable de comunicarse con el servidor y devolver una respuesta unificada.

![Servicio de editor universal](assets/universal-editor-service.png)

## Canalizaciones de renderización {#rendering-pipelines}

### Procesamiento del lado del servidor {#server-side}

![Renderización del lado del servidor](assets/server-side.png)

### Generación estática del sitio {#static-generation}

![Generación estática del sitio](assets/static-generation.png)

### Renderización del lado del cliente {#client-side}

![Renderización del lado del cliente](assets/client-side.png)

## Recursos adicionales {#additional-resources}

Para obtener más información sobre el Editor universal, consulte estos documentos.

* [Introducción al Editor universal](introduction.md) : Descubra cómo el Editor universal permite editar cualquier aspecto de cualquier contenido en cualquier implementación para ofrecer experiencias excepcionales, aumentar la velocidad de contenido y proporcionar una experiencia de desarrollador de última generación.
* [Creación de contenido con el editor universal](authoring.md) : Aprenda lo fácil e intuitivo que es para los autores de contenido crear contenido con el Editor universal.
* [Publicación de contenido con el Editor universal](publishing.md) : Descubra cómo el Editor visual universal publica contenido y cómo sus aplicaciones pueden gestionar el contenido publicado.
* [Introducción al Editor universal en AEM](getting-started.md) : Obtenga información sobre cómo acceder al Editor universal y cómo instrumentar la primera aplicación de AEM para utilizarla.
* [Atributos y tipos](attributes-types.md) : Obtenga información sobre los atributos y tipos de datos que requiere el Editor universal.
* [Autenticación del editor universal](authentication.md) - Obtenga información sobre cómo se autentica el editor universal.
