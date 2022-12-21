---
title: Copia de seguridad y restauración en AEM as a Cloud Service
description: Copia de seguridad y restauración en AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 12e747ff73e9416775a3f26040ac7e15c21505ec
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 3%

---


# Copia de seguridad y restauración en AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Copia de seguridad y restauración"
>abstract="AEM as a Cloud Service puede restaurar la aplicación completa (código y contenido) de un cliente a tiempos específicos y predeterminados en los últimos siete días, sustituyendo lo que estaba en producción. Esta función solo debe usarse cuando haya problemas graves con el código o el contenido. Se perderán los datos recientes entre el momento de la copia de seguridad restaurada y el presente. El ensayo también se restaurará a la versión antigua."

En caso de que se dañen los datos o el contenido, AEM as a Cloud Service puede restaurar la aplicación completa (código y contenido) de un cliente a tiempos específicos y predeterminados en los últimos siete días, sustituyendo lo que estaba en producción.
Si la implementación de un cliente, es decir, el código de aplicación implementado está dañado o está dañado, es preferible corregirlo y avanzar a una nueva versión en lugar de restaurarlo desde la copia de seguridad. La copia de seguridad se realiza de una manera que no afecta al rendimiento en tiempo de ejecución de una aplicación.

>[!CAUTION]
>
>Esta función solo debe usarse cuando haya problemas graves con el código o el contenido. Se perderán los datos recientes entre el momento de la copia de seguridad restaurada y el presente. El ensayo también se restaurará a la versión antigua.

## Usos {#how-to-use}

Los clientes deben presentar un ticket de asistencia que describa el problema que se está experimentando. Esto llevará a una investigación por parte del soporte de Adobe que determinará si es necesario un restore.

AEM admite as a Cloud Service:

* Backup y restore para entornos de etapa, producción y desarrollo.
* 24 horas de recuperación, lo que significa que el sistema puede ser restaurado a cualquier punto en las últimas 24 horas.
* Restaure desde una marca de tiempo específica definida por Adobe que se tome dos veces al día durante los últimos 7 días.  Se conservará cualquier mensaje de replicación (elimina, actualiza, crea).

En todos los casos, la versión del código personalizado se tomará de la última implementación correcta antes del punto de restauración.

El objetivo de tiempo de recuperación (RTO) puede variar, pero como guía general, la secuencia de recuperación tarda entre 60 y 90 minutos en promedio según varios factores, como el tamaño del repositorio.

Después de una restauración, la versión AEM se actualizará a la más reciente.

>[!CAUTION]
>
>Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.

## Copia de seguridad fuera del sitio {#offsite-backup}

Mientras que las copias de seguridad regulares cubren el riesgo de eliminaciones accidentales o fallos técnicos en AEM Cloud Services, también se deben cubrir los riesgos que pueden surgir de la falla de una región. Además de la disponibilidad, el riesgo bueno de que se produzcan interrupciones en esas regiones de datos es principalmente una pérdida de datos.
AEM as a Cloud Service cubre este riesgo como estándar para todos los entornos de producción AEM copiando continuamente todo el contenido AEM en una región remota y poniéndolo a disposición para su recuperación durante un período de 3 meses. Llamamos a esta capacidad Copia de seguridad fuera del sitio.
La restauración de AEM Cloud Services para entornos de fase y producción corre a cargo de AEM Service Fiabilidad Engineering en caso de interrupciones en la región de datos.
