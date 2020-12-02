---
title: Backup y Restore en AEM como Cloud Service
description: 'Backup y Restore en AEM como Cloud Service '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Backup y Restore en AEM como Cloud Service

Si se produce corrupción de contenido o datos, AEM como Cloud Service puede restaurar la aplicación completa de un cliente (código y contenido) a tiempos específicos predeterminados en los últimos siete días, reemplazando lo que estaba en producción.
Si la implementación de un cliente, lo que significa que el código de la aplicación implementado está dañado o dañado, es preferible corregirlo y avanzar a una nueva versión en lugar de restaurarlo desde el backup. La copia de seguridad se realiza de una manera que no afecta al rendimiento en tiempo de ejecución de una aplicación.

>[!CAUTION]
>
>Esta función solo debe usarse cuando haya problemas graves con el código o el contenido. Se perderán los datos recientes entre el tiempo de la copia de seguridad restaurada y el presente. El ensayo también se restaurará a la versión anterior.

## Usos

Los clientes deben presentar un ticket de asistencia técnica en el que se describa el problema que se está experimentando. Esto conducirá a una investigación por parte del personal de apoyo al Adobe, quien determinará si es necesaria una restauración.

AEM como Cloud Service admite:

* 24 horas de recuperación de tiempo, lo que significa que el sistema puede restaurarse en cualquier momento en las últimas 24 horas.
* Restaure desde una marca de tiempo específica definida por Adobes una vez al día durante los últimos 7 días.  Se conservarán todos los mensajes de replicación (eliminaciones, actualizaciones, creaciones).

En todos los casos, la versión del código personalizado será la tomada desde la última implementación correcta antes del punto de restauración.

El objetivo de tiempo de recuperación (RTO) variará según el tamaño del repositorio, pero como guía general una vez que comience la secuencia de restauración, debe tardar unos 30 minutos.

Después de una restauración, la versión AEM se actualizará a la más reciente.

**Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.**
