---
title: Uso del analizador de preparación para la nube
description: Uso del analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Uso del analizador de preparación para la nube {#using-cloud-readiness-analyzer}

## Consideraciones importantes sobre el uso del analizador de preparación para la nube {#imp-considerations}

Siga la sección siguiente para comprender las consideraciones importantes al ejecutar el analizador de preparación para la nube (CRA):

* CRA es compatible con las instancias de AEM de origen con la versión 6.1 o posterior.
* CRA se puede ejecutar en cualquier entorno. Sin embargo, para aumentar la tasa de detección y evitar cualquier ralentización de las instancias críticas del negocio, se recomienda ejecutarlo en los entornos de ensayo del autor de origen que estén lo más cerca posible de los de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. También puede ejecutarse en un clon del entorno Publicar.

## Disponibilidad {#availability}

El analizador de preparación para la nube (CRA) se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue el analizador de preparación para la nube (CRA) de pendiente.

## Ejecución del analizador de preparación para la nube {#running-tool}

Siga esta sección para obtener información sobre cómo ejecutar el analizador de preparación para la nube:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

### Visualización de los resultados {#viewing-the-results}

Existen dos maneras de vista de la salida de la CRA:

1. Uso del informe organizado (disponible en AEM versión 6.3 y posterior)Consulte Planificación y estado de Documentos de CRA para describir los niveles de importancia en el informe

Para la vista de la salida de CRA (se puede utilizar con AEM versión 6.1 y posterior):

1. Vaya a la consola web de AEM navegando hasta.

1. Seleccione Estado - Analizador de preparación para la nube, como se muestra en la imagen siguiente.