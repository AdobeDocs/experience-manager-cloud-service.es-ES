---
title: AEM Copia de seguridad y restauración en as a Cloud Service
description: AEM Copia de seguridad y restauración en as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 17%

---


# AEM Copia de seguridad y restauración en as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Copia de seguridad y restauración"
>abstract="AEM as a Cloud Service puede restaurar la aplicación completa (código y contenido) de un cliente de horas específicas y predeterminadas de los últimos siete días, sustituyendo lo que estaba en producción. Esta función solo debe usarse cuando hay problemas graves con el código o el contenido. Se pierden los datos recientes entre el momento de la copia de seguridad restaurada y el presente. El ensayo también se restaurará a la versión antigua."

AEM En caso de que se dañe el contenido o los datos, los as a Cloud Service pueden restaurar la aplicación completa (código y contenido) de un cliente a tiempos específicos y predeterminados en los últimos siete días, sustituyendo lo que había en producción.
Si la implementación de un cliente, lo que significa que el código de la aplicación implementado está dañado o dañado, es preferible corregirlo y pasar a una nueva versión en lugar de restaurarlo desde la copia de seguridad. La copia de seguridad se realiza de una manera que no afecta al rendimiento en tiempo de ejecución de una aplicación.

>[!CAUTION]
>
>Esta función solo debe usarse cuando hay problemas graves con el código o el contenido. Se pierden los datos recientes entre el momento de la copia de seguridad restaurada y el presente. El ensayo también se restaura a la versión antigua.

## Usos {#how-to-use}

Los clientes deben presentar un ticket de asistencia, en el que se describa el problema que se está experimentando. Esto llevará a que el equipo de soporte del Adobe investigue si es necesario realizar una restauración.

AEM Compatibilidad con as a Cloud Service:

* Copia de seguridad y restauración para entornos de ensayo, producción y desarrollo.
* Recuperación en 24 horas, lo que significa que el sistema se puede restaurar en cualquier punto de las últimas 24 horas.
* Restaure a partir de una marca de tiempo específica definida por el Adobe que se haya tomado dos veces al día durante los últimos 7 días.  Se conserva cualquier mensaje de replicación (eliminaciones, actualizaciones, creaciones).

En todos los casos, la versión de código personalizado es la que se toma de la última implementación correcta antes del punto de restauración.

El objetivo de tiempo de recuperación (RTO) puede variar, pero como guía general, la secuencia de recuperación tarda entre 60 y 90 minutos de media en función de varios factores, como el tamaño del repositorio. Los entornos de vista previa y los editores de varias regiones pueden ampliar el objetivo de tiempo de restauración.

AEM Después de una restauración, la versión de la se actualiza a la más reciente.

>[!CAUTION]
>
>Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.

## Copia de seguridad fuera del sitio {#offsite-backup}

Aunque las copias de seguridad regulares cubren el riesgo de eliminaciones accidentales o fallos técnicos en AEM Cloud Services, también deben cubrirse los riesgos que pueden surgir del fallo de una región. Además de la disponibilidad, el riesgo más bueno en estas interrupciones de la región de datos es principalmente la pérdida de datos.
AEM El as a Cloud Service AEM AEM cubre este riesgo como estándar para todos los entornos de producción de la copiando continuamente todo el contenido de la en una región remota y poniéndolo a disposición para recuperarlo durante un periodo de 3 meses. Llamamos a esta capacidad Copia de seguridad fuera del sitio.
AEM La restauración de AEM Cloud Services para entornos de ensayo y producción la realiza ingeniería de fiabilidad del servicio de la aplicación en caso de interrupciones en la región de datos.
