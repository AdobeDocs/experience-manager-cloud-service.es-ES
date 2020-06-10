---
title: Uso del analizador de preparación para la nube
description: Uso del analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Uso del analizador de preparación para la nube {#using-cloud-readiness-analyzer}

## Consideraciones importantes sobre el uso del analizador de preparación para la nube {#imp-considerations}

Siga la sección siguiente para comprender las consideraciones importantes al ejecutar el analizador de preparación para la nube (CRA):

* CRA es compatible con las instancias de AEM de origen con la versión 6.1 o posterior.
* CRA se puede ejecutar en cualquier entorno.

   >[!NOTE]
   >Para aumentar la tasa de detección y evitar cualquier desaceleración en instancias críticas del negocio, se recomienda ejecutar CRA en los entornos de ensayo del autor de origen que estén lo más cerca posible de los de producción en las áreas de personalización, configuración, contenido y aplicaciones de usuario. También puede ejecutarse en un clon del entorno de publicación.

## Disponibilidad {#availability}

El analizador de preparación para la nube (CRA) se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue el analizador de preparación para la nube (CRA) de *pendiente*.

## Ejecución del analizador de preparación para la nube {#running-tool}

Siga esta sección para obtener información sobre cómo ejecutar el analizador de preparación para la nube:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

### Visualización de los resultados {#viewing-the-results}

Existen dos maneras de vista de la salida de la CRA:

1. Uso del informe organizado

   >[!NOTE]
   >El informe organizado está disponible en AEM versión 6.3 y posterior.

Consulte Planificación y estado del Documento de CRA para describir los niveles de importancia en el informe

1. Visualización del resultado del CRA (se puede utilizar con AEM versión 6.1 y posterior):

   1. Vaya a la consola web de AEM navegando hasta.

   1. Seleccione Estado - Analizador de preparación para la nube, como se muestra en la imagen siguiente.

#### Explicación de los niveles de importancia en el informe {#importance-levels}

En la tabla siguiente se describe el significado de los distintos niveles de importancia del detector de patrones y del analizador de preparación para la nube.

| Nivel de importancia | Descripción |
|--- |--- |
| INFORMACIÓN/0 | Esta conclusión se proporciona con fines informativos. |
| CONSEJO/1 | Este hallazgo es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL/2 | Es probable que este hallazgo sea un problema de actualización que se debe abordar. |
| CRÍTICO/3 | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |