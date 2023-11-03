---
title: Copia de seguridad y restauración en AEM as a Cloud Service
description: AEM as a Cloud Service Obtenga información acerca de Copia de seguridad y restauración en
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 27%

---


# Copia de seguridad y restauración en AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Copia de seguridad y restauración"
>abstract="AEM as a Cloud Service puede restaurar la aplicación completa (código y contenido) de un cliente de horas específicas y predeterminadas de los últimos siete días, sustituyendo lo que estaba en producción. Esta función solo debe usarse cuando hay problemas graves con el código o el contenido. Se perderán los datos recientes entre el momento de la copia de seguridad restaurada y el presente. La puesta en marcha también se restaurará a la versión antigua."

AEM En caso de que se dañe el contenido o los datos, los as a Cloud Service pueden restaurar la aplicación completa (código y contenido) de un cliente. Se restaura a tiempos específicos y predeterminados en los últimos siete días, reemplazando lo que estaba en producción.
Si la implementación de un cliente, lo que significa que el código de la aplicación implementado está dañado o dañado, es preferible corregirlo y pasar a una nueva versión en lugar de restaurarlo desde la copia de seguridad. La copia de seguridad se realiza de una manera que no afecta al rendimiento en tiempo de ejecución de una aplicación.

>[!CAUTION]
>
>Esta función solo debe usarse cuando hay problemas graves con el código o el contenido. Se perderán los datos recientes entre el momento de la copia de seguridad restaurada y el presente. La puesta en marcha también se restaurará a la versión antigua.

## Usos {#how-to-use}

Los clientes deben presentar un ticket de asistencia, en el que se describa el problema que se está experimentando. La incidencia de soporte técnico suele llevar a una investigación por parte del soporte técnico de Adobe, que puede determinar si es necesario realizar una restauración.

AEM Compatibilidad con as a Cloud Service:

* Copia de seguridad y restauración para entornos de ensayo, producción y desarrollo.
* Recuperación en 24 horas, lo que significa que el sistema se puede restaurar en cualquier punto de las últimas 24 horas.
* Restaure a partir de una marca de tiempo específica definida por el Adobe que se haya tomado dos veces al día durante los últimos siete días. Se conservará cualquier mensaje de replicación (eliminaciones, actualizaciones, creaciones).

En todos los casos, la versión de código personalizado es la que se toma de la última implementación correcta antes del punto de restauración.

El objetivo de tiempo de recuperación (RTO) puede variar, pero como guía general, la secuencia de recuperación tarda de 60 a 90 minutos en promedio según varios factores, como el tamaño del repositorio. Los entornos de vista previa y los editores de varias regiones pueden ampliar el objetivo de tiempo de restauración.

AEM Después de una restauración, la versión de la se actualiza a la más reciente.

>[!CAUTION]
>
>Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.

## Copia de seguridad fuera del sitio {#offsite-backup}

AEM Si bien los backups regulares cubren el riesgo de eliminaciones accidentales o fallos técnicos en los Cloud Service de la red, también deben cubrirse los riesgos que pueden surgir por el fallo de una región. Además de la disponibilidad, el mayor riesgo en estas interrupciones de la región de datos es principalmente la pérdida de datos.
AEM El as a Cloud Service AEM cubre este riesgo como estándar para todos los entornos de producción de la. AEM Copia continuamente todo el contenido de la en una región remota y lo pone a disposición para su recuperación durante tres meses. El Adobe llama a esta funcionalidad Copia de seguridad fuera del sitio.
AEM La restauración de los Cloud Service AEM de la para los entornos de ensayo y producción se realiza mediante ingeniería de fiabilidad del servicio de la unidad de servicio si se producen interrupciones en la región de datos.
