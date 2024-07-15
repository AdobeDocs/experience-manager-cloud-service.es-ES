---
title: Arquitectura del editor universal
description: Obtenga información sobre la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.
exl-id: e6f40743-0f21-4fb6-bf23-76426ee174be
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 83%

---


# Arquitectura del editor universal {#architecture}

Obtenga información sobre la arquitectura del editor universal y cómo fluyen los datos entre sus servicios y capas.

## Bloques de creación de arquitectura {#building-blocks}

El editor universal consta de cuatro bloques de creación básicos que interactúan para permitir que los autores de contenido editen los aspectos del contenido en cualquier implementación con el fin de ofrecer experiencias excepcionales, aumentar la velocidad del contenido y proporcionar una experiencia de desarrollador de última generación.

1. [Editores](#editors)
1. [Aplicación remota](#remote-app)
1. [Capa de la API](#api-layer)
1. [Capa de persistencia](#persistence-layer)

Este documento describe cada uno de estos bloques de creación básicos y cómo intercambian datos.

![Arquitectura del editor universal](assets/architecture.png)

>[!TIP]
>
>AEM AEM Para ver el editor universal y su arquitectura en acción, consulta [Introducción al editor universal en el editor universal](getting-started.md) para obtener información sobre cómo obtener acceso al editor universal y cómo empezar a instrumentar tu primera aplicación de la para que la uses.

### Editores {#editors}

* **Editor universal**: el editor universal utiliza un DOM instrumentado para permitir la edición in situ del contenido. Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los metadatos necesarios. Consulte el documento [Introducción al editor universal en AEM](getting-started.md) para ver un ejemplo de la instrumentación en AEM.
* **Carril de propiedades**: algunas propiedades de los componentes no se pueden editar en contexto; por ejemplo, el tiempo de rotación de un carrusel o qué pestaña de acordeón se debe abrir o cerrar siempre. Para permitir la edición de dicha información de componentes, se proporciona un editor basado en formularios en el carril lateral.

### Aplicación remota {#remote-app}

Para que una aplicación se pueda editar en contexto dentro del editor universal, se debe instrumentar el DOM. La aplicación remota debe representar ciertos atributos en el DOM. Consulte el documento [Atributos y tipos](attributes-types.md) para obtener más información sobre los metadatos necesarios. Consulte el documento [Introducción al editor universal en AEM](getting-started.md) para ver un ejemplo de la instrumentación en AEM.

El editor universal se esfuerza por conseguir un SDK mínimo, por lo que la instrumentación es responsabilidad de la implementación de la aplicación remota.

### Capa de la API {#api-layer}

* **Datos de contenido**: para el editor universal, no es importante ni los sistemas de origen de los datos de contenido ni la forma en que se consumen. Solo es importante definir y proporcionar los atributos necesarios utilizando datos editables en contexto.
* **Datos persistentes**: para cada dato editable hay un identificador URN. Este URN se utiliza para enrutar la persistencia al sistema y recurso correctos.

### Capa de persistencia {#persistence-layer}

* **Modelo de fragmento de contenido**: para admitir el carril para editar las propiedades del Fragmento de contenido, el editor de Fragmentos de contenido y los editores basados en formularios, se requieren modelos por componente y por fragmento de contenido.
* AEM **Contenido**: el contenido se puede almacenar en cualquier lugar, como en el sitio de trabajo, el Magento, el, etc.

![Capa de persistencia](assets/persistence-layer.png)

## Servicio de editor universal y envío del sistema back-end {#service}

El editor universal envía todos los cambios de contenido a un servicio centralizado denominado Servicio del editor universal. Este servicio, que se ejecuta en Adobe I/O Runtime, carga los complementos disponibles en el Registro de extensiones en función del URN proporcionado. El complemento es responsable de comunicarse con el back-end y devolver una respuesta unificada.

![Servicio del editor universal](assets/universal-editor-service.png)

## Canalizaciones de renderización {#rendering-pipelines}

### Procesamiento del lado del servidor {#server-side}

![Procesamiento del lado del servidor](assets/server-side.png)

### Generación estática del sitio {#static-generation}

![Generación estática del sitio](assets/static-generation.png)

### Renderización del lado del cliente {#client-side}

![Renderización del lado del cliente](assets/client-side.png)
