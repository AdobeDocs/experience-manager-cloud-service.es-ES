---
title: Uso del analizador de preparación para la nube
description: Uso del analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Uso del analizador de preparación para la nube {#using-cloud-readiness-analyzer}

## Consideraciones importantes sobre el uso del analizador de preparación para la nube {#imp-considerations}

Siga la sección siguiente para comprender las consideraciones importantes al ejecutar el analizador de preparación para la nube (CRA):

* CRA es compatible con las instancias de AEM de origen con la versión 6.1 o superior
* CRA puede ejecutarse en cualquier entorno (preferiblemente *entorno de etapa* )

   >[!NOTE]
   >Para aumentar la tasa de detección y evitar cualquier desaceleración en instancias críticas del negocio, se recomienda ejecutar CRA en los entornos de ensayo del autor de origen que estén lo más cerca posible de los de producción en las áreas de personalización, configuración, contenido y aplicaciones de usuario. También puede ejecutarse en un clon del entorno *Publicar* .

## Disponibilidad {#availability}

El analizador de preparación para la nube se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue el analizador de preparación para la nube del portal de distribución de software *pendiente*.

## Ejecución del analizador de preparación para la nube {#running-tool}

Siga esta sección para obtener información sobre cómo ejecutar el analizador de preparación para la nube:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

### Visualización de los resultados {#viewing-the-results}

>[!IMPORTANT]
>Los informes generados a partir del analizador de preparación para la nube se basan en los detectores de patrones. Consulte Detectores [de patrones](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) para obtener más detalles.

Existen dos formas de vista del resultado desde el analizador de preparación para la nube:

1. **Uso del informe organizado**

   >[!NOTE]
   >El informe organizado está disponible en AEM versión 6.3 y posterior.

   O bien,

1. **Visualización del resultado del CRA**

   Siga los pasos que se describen a continuación para vista del resultado del analizador de preparación para la nube:

   >[!NOTE]
   >Los pasos a continuación se aplican a AEM versión 6.1 y posterior.

   1. Vaya a **AEM Web Console** mediante `https://serveraddress:serverport/system/console/configMgr`.

   1. Seleccione **Estado - Detector** de patrones como se muestra en la figura siguiente.

#### Visualización del informe en instancias de AEM 6.1 {#aem-instances-report}

Puede descargar el informe csv para AEM 6.1. Esto está pendiente.

#### Explicación de los niveles de importancia en el informe {#importance-levels}

En la tabla siguiente se describe el significado de los distintos niveles de importancia del detector de patrones y del analizador de preparación para la nube.

| Nivel de importancia | Descripción |
|--- |--- |
| INFORMACIÓN/0 | Esta conclusión se proporciona con fines informativos. |
| CONSEJO/1 | Este hallazgo es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL/2 | Es probable que este hallazgo sea un problema de actualización que se debe abordar. |
| CRÍTICO/3 | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |