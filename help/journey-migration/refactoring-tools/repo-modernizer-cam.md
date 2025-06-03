---
title: Modernizador de repositorios (CAM)
description: Aprenda a reestructurar los paquetes de proyectos existentes y a hacerlos compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.
feature: Migration
role: Admin
source-git-commit: 317ee65786d48d7b92d95c7c6b8782f617d6e346
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 4%

---


# Modernizador de repositorios (CAM) {#repo-modernizer-cam}

Repository Modernizer es una utilidad desarrollada para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para que sean compatibles con la estructura de proyectos definida para Adobe Experience Manager as a Cloud Service.

## Introducción {#introduction}

Adobe Experience Manager as a Cloud Service ofrece muchas nuevas funciones y posibilidades para sus proyectos de AEM. Con todo, se requieren algunos cambios en los proyectos de Adobe Experience Manager Maven para que sean compatibles con AEM Cloud Service. En un nivel superior, AEM requiere una separación de **content** y **code** en subpaquetes discretos para respetar la división entre contenido mutable e inmutable. Consulte [Estructura del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es) para obtener más información sobre la nueva estructura del proyecto AEM para Cloud Service.

El Modernizador de repositorio crea una estructura de proyecto de AEM Cloud Service compatible mediante la creación de la siguiente estructura de implementación:

- El paquete `ui.apps` se implementa en `/apps` y contiene todo el código

- El paquete `ui.content` se implementa en áreas en tiempo de ejecución modificables (por ejemplo, `/content`, `/conf`, `/home` o cualquier elemento que no sea `/apps`) y contiene todo el contenido y la configuración.

- El paquete `all` es un paquete contenedor que contiene los subpaquetes `ui.apps` y `ui.content`.

>[!NOTE]
>
> La estructura del proyecto se basa en _tipo de archivo 48_ para los paquetes y sus `pom.xml/filter.xml files`. Consulte [Tipo de archivo 48](https://github.com/adobe/aem-project-archetype) para obtener más información.

El Modernizador de repositorio ahora también admite los siguientes tipos de proyectos:

- **MULTI_PROJECT**: representa un proyecto multimódulo sin POM principal común, Dispatcher y todos los módulos.
- **SINGLE_PROJECT**: representa un solo proyecto.
- **NESTED_PROJECT**: representa un proyecto multimódulo con un POM principal común, Dispatcher y todos los módulos.
- **PROYECTO_MONOLÍTICO**: representa un proyecto principal con uno o más subproyectos.

## Uso del Modernizador de repositorio {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

- El servicio de refactorización ahora invoca automáticamente el Modernizador de repositorio en la pestaña Trabajo de refactorización. Los clientes solo tienen que cargar su proyecto y almacenar en déclencheur el trabajo de refactorización; no se requiere ninguna configuración adicional.

## Referencia de código de error

Si encuentra un código de error mientras utiliza el Modernizador de repositorio, consulte la tabla siguiente para obtener detalles y acciones recomendadas.

| Código de error | Mensaje | Descripción | ¿Acción del usuario requerida? |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| RM-100 | Error al convertir el archivo de configuración OSGi {0} al formato .cfg.json. Valide el archivo de configuración existente antes de intentarlo de nuevo. | Este error se produce cuando hay un problema durante la transformación de un archivo de configuración OSGi al formato .cfg.json. | Sí |
| RM-101 | Error al intentar copiar contenido de: {0} | Este error se produce cuando se produce un error al intentar copiar contenido del origen especificado. | No |
| RM-102 | Error al intentar mover el archivo {0} de {1} a {2}. | Este error se produce cuando hay un problema al mover un archivo de una ubicación a otra. | No |
| RM-103 | La ruta especificada no se pudo resolver en un archivo válido: {0} | Este error se produce cuando el archivo no se encuentra en la ubicación determinada. | No |
| RM-104 | Error al repetir el contenido de {0}. | Este error se produce durante el recorrido de archivos o directorios, lo que indica un problema con el acceso o el procesamiento de contenido. | No |
| RM-105 | Error al intentar analizar el archivo XML: {0}. Valide el archivo XML antes de intentarlo de nuevo. | Este error se produce cuando se produce un error al analizar el archivo XML. | Sí |
| RM-106 | Error al escribir en el archivo XML: {0}. | Este error se produce cuando hay un problema al escribir en el archivo XML. | No |
| RM-107 | No se encontraron paquetes de contenido en el proyecto existente: {0}. Compruebe que se ha cargado el proyecto correcto. | Este error indica que no se encontraron paquetes de contenido en el proyecto existente. | Sí |
| RM-108 | No se encontró el archivo POM en la ruta de acceso esperada: {0}. Se espera que el archivo POM del proyecto o módulo se encuentre directamente dentro de su directorio como archivo secundario. | Este error se produce cuando el archivo POM no se encuentra en la ubicación esperada. | Sí |
| RM-109 | Error al intentar analizar el archivo pom.xml: {0}. Valide el archivo pom antes de intentarlo de nuevo. | Este error se produce cuando hay un problema al analizar el archivo pom.xml. | Sí |
| RM-110 | Error al escribir en el archivo pom.xml: {0}. | Este error se produce cuando hay un problema al escribir en el archivo pom. | No |
| RM-111 | Error al escribir en el archivo de informe. | Este error se produce cuando se produce un error durante el proceso de escritura en el archivo de informe. | No |
| RM-112 | No se pudo encontrar {0} en el archivo pom de estructura de repositorio en ({1}) | Este error se produce cuando la configuración esperada no se encuentra en la plantilla de tipo de archivo del proyecto de AEM. | No |
| RM-113 | Error al intentar copiar las plantillas de arquetipo del proyecto AEM en el destino. | Este error se produce cuando se produce un problema al copiar las plantillas de tipo de archivo del proyecto de AEM al destino. | No |
| RM-115 | Error al intentar conectar con Azure Blob Storage. | Este error se produce cuando hay un problema al conectar con Azure Blob Storage. | No |
| RM-116 | Error al intentar cargar el archivo: {0} al almacenamiento del blob de Azure. | Este error se produce cuando hay un problema al cargar un archivo en Azure Blob Storage. | No |
| RM-117 | Error al intentar descargar el archivo: {0} del almacenamiento del blob de Azure. | Este error se produce cuando hay un problema al descargar un archivo del almacenamiento del blob de Azure. | No |
| RM-118 | Error de E/S al administrar : {0}. | Este error se produce cuando hay un problema al leer o escribir en un archivo de proyecto. | No |
| RM-119 | Error de E/S al intentar archivar los resultados para cargar en Azure. | Este error se produce cuando hay un error al archivar los resultados generados por el proceso. | No |
| RM-120 | Error de E/S al intentar desarchivar el zip del proyecto proporcionado. Compruebe si el archivo zip del proyecto proporcionado es válido. | Este error se produce cuando se produce un error al anular el archivado del proyecto del cliente determinado. | Sí |
| RM-121 | Error al escribir en el archivo de configuración. | Este error se produce cuando se produce un error durante el proceso de escritura en el archivo de configuración. | No |
| RM-122 | Tipo de solicitud no compatible: {0}. | Este error se produce cuando el sistema no admite el tipo de solicitud. Compruebe el tipo de solicitud e inténtelo de nuevo. | No |

## Comprender las prioridades del informe Resultados

Al descargar el informe de resultados generado por la herramienta Modernizador de repositorio, a cada resultado se le asigna una **prioridad**. Estas prioridades le ayudan a comprender la urgencia y el impacto de cada problema:

| Prioridad | Descripción |
| -------- | ----------------------------------------------------------------------------------------------- |
| CRÍTICO | Se debe resolver para generar correctamente el proyecto. |
| ALTA | Debe resolverse para garantizar que la funcionalidad no se interrumpa en AEM. |
| NORMAL | Debe estar decidido a garantizar la sensatez y la integridad generales de la modernización. |
| BAJA | Para la verificación manual; estos hallazgos son informativos y pueden no requerir una acción inmediata. |

>[!NOTE]
> 
>Se recomienda abordar primero las conclusiones de mayor prioridad para garantizar un proceso de modernización e implementación sin problemas.
