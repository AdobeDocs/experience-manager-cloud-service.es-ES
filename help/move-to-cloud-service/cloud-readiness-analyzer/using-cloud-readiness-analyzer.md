---
title: Uso del analizador de preparación para la nube
description: Uso del analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: 1739f81d4894f3e04cc4119f344a3bea5bd042d8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

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

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Una vez que haga clic en el Analizador **de preparación para** la nube, la herramienta inicio la generación del informe y, a los pocos minutos, el informe de resumen estará disponible en la instancia de AEM.

   >[!NOTE]
   >Tendrá que desplazarse hacia abajo por la página para vista del informe completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### Visualización de los resultados en el informe Resumen {#viewing-the-results}

>[!IMPORTANT]
>Los informes generados a partir del analizador de preparación para la nube se basan en los detectores de patrones. Consulte Detectores [de patrones](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) para obtener más detalles.

Una vez que se desplace hacia abajo por la página para realizar la vista del informe de resumen completo, podrá ver la siguiente información para cada una de las categorías resaltadas en el informe:

1. **Nivel de importancia**

   En la tabla siguiente se describe el significado de los distintos niveles de importancia del detector de patrones y del analizador de preparación para la nube.

   | Nivel de importancia | Descripción |
   |--- |--- |
   | INFORMACIÓN/0 | Esta conclusión se proporciona con fines informativos. |
   | CONSEJO/1 | Este hallazgo es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
   | PRINCIPAL/2 | Es probable que este hallazgo sea un problema de actualización que se debe abordar. |
   | CRÍTICO/3 | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |

1. **Descripción** La descripción proporciona información sobre la categoría notificada.

1. **Dirección URL** de la documentación La dirección URL de la documentación le permite realizar la vista de la documentación técnica del tipo asociado.

1. **Mensaje** Descripción de la búsqueda en un solo mensaje.

### Visualización de los resultados en formato CSV {#viewing-the-results-csv}

El informe de resumen está disponible en la interfaz de usuario de AEM. Puede descargar el informe completo en un formato de valores separados por comas (CSV) que sea útil durante el proceso de refactorización.

Siga los pasos a continuación para generar un formato CSV del informe de resumen:

1. 
   1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

1. Una vez que el informe esté disponible, haga clic en **CSV** para descargar el informe de resumen completo en formato de valores separados por comas (CSV), como se muestra en la figura siguiente.

![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### Visualización del informe en instancias de AEM 6.1 {#aem-instances-report}

Siga los pasos a continuación para descargar el informe CSV de Adobe Experience Manager (AEM) 6.1:

1. Vaya a **Adobe Experience Manager Web ConsoleConfiguración** mediante `https://serveraddress:serverport/system/console/configMgr`.

1. Seleccione la ficha **Estado** y busque Detector **de** patrones en la lista desplegable, como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Puede descargar el informe de resumen en una carpeta zip o en formato JSON.


