---
title: Restauración de contenido en AEM as a Cloud Service
description: Obtenga información sobre cómo restaurar el contenido as a Cloud Service AEM desde la copia de seguridad mediante Cloud Manager.
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 09049213eaf92830dc0e0d4c0885017c69a5d56e
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 0%

---


# Restauración de contenido en AEM as a Cloud Service {#content-restore}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Copia de seguridad y restauración"
>abstract="Obtenga información sobre cómo restaurar el contenido as a Cloud Service AEM desde la copia de seguridad mediante Cloud Manager."

Obtenga información sobre cómo restaurar el contenido as a Cloud Service AEM desde la copia de seguridad mediante Cloud Manager.

## Información general {#overview}

El proceso de restauración de autoservicio de Cloud Manager copia datos de los backups del sistema de Adobe y los restaura a su entorno original. Se realiza una restauración para devolver datos que se han perdido, dañado o eliminado accidentalmente a su condición original.

El proceso de restauración solo afecta al contenido, dejando el código y la versión de AEM sin cambios. Puede iniciar una operación de restauración de entornos individuales en cualquier momento.

Cloud Manager ofrece dos tipos de copias de seguridad desde las que puede restaurar contenido.

* **Punto en el tiempo (PIT):** Este tipo restaura los backups del sistema desde las últimas 24 horas desde el momento actual.
* **Última semana:** Este tipo se restaura de las copias de seguridad del sistema en los últimos siete días, excluyendo las 24 horas anteriores.

En ambos casos, la versión del código personalizado y AEM versión permanecen sin cambios.

>[!TIP]
>
>También es posible restaurar backups [mediante la API pública.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)

## Restricciones     {#limitations}

El uso del mecanismo de restauración de autoservicio está sujeto a las siguientes limitaciones.

* Las operaciones de restauración están limitadas a siete días, lo que significa que no es posible restaurar una instantánea a partir de siete días.
* Se permiten un máximo de diez restauraciones exitosas en todos los entornos de un programa por mes del calendario.
* Después de la creación del entorno, tardan seis horas en crearse la primera instantánea de backup. Hasta que se cree esta instantánea, no se puede realizar ninguna restauración en el entorno.
* Una operación de restauración no se iniciará si hay una pila completa o una canalización de configuración de nivel web que se esté ejecutando para el entorno.
* No se puede iniciar una restauración si ya se está ejecutando otra restauración en el mismo entorno.
* En casos excepcionales, debido al límite de copias de seguridad de 24 horas/siete días, es posible que la copia de seguridad seleccionada no esté disponible debido a un retraso entre el momento en que se seleccionó y el momento en que se inició la restauración.
* Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.

## Restauración de contenido {#restoring-content}

En primer lugar, determine el lapso de tiempo del contenido que desea restaurar. A continuación, para restaurar el contenido de su entorno desde una copia de seguridad, realice estos pasos.

>[!NOTE]
>
>Un usuario con la variable **Propietario empresarial** o **Administrador de implementación** para iniciar una operación de restauración, debe iniciar sesión en la función .

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea iniciar una restauración.

1. En el **Información general del programa** en la **Entornos** , haga clic en el botón de puntos suspensivos situado junto al entorno para el que desea iniciar una restauración y seleccione **Restaurar contenido**.

   ![Opción Restaurar](assets/backup-option.png)

   * También puede navegar directamente al **Restaurar contenido** de la página de detalles del entorno de un entorno específico.

1. En el **Restaurar contenido** en la página de detalles del entorno, seleccione primero el lapso de tiempo de la restauración en la sección **Tiempo para restaurar** lista desplegable.

   1. Si selecciona **Últimas 24 horas** el vecino **Tiempo** permite especificar el tiempo exacto dentro de las últimas 24 horas que se va a restaurar.

      ![Últimas 24 horas](assets/backup-time.png)

   1. Si selecciona **La semana pasada** el vecino **Día** permite seleccionar una fecha en los últimos siete días, excluidas las 24 horas anteriores.

      ![Última semana](assets/backup-date.png)

1. Una vez seleccionada una fecha o especificada una hora, la variable **Copias de seguridad disponibles** a continuación se muestra una lista de las copias de seguridad disponibles que se pueden restaurar

   ![Copias de seguridad disponibles](assets/backup-available.png)

1. Busque la copia de seguridad que desea restaurar mediante el icono de información para ver información sobre la versión del código y la versión de AEM que se incluye en la copia de seguridad y tenga en cuenta las implicaciones de una restauración cuando [seleccionando la copia de seguridad.](#choosing-the-right-backup)

   ![Información de copia de seguridad](assets/backup-info.png)

   * Tenga en cuenta que la marca de tiempo mostrada para las opciones de restauración se basa en la zona horaria del equipo del usuario.

1. Haga clic en el **Restaurar** en el extremo derecho de la fila que representa la copia de seguridad que desea restaurar para iniciar el proceso de restauración.

1. Consulte los detalles sobre la **Restaurar contenido** antes de confirmar la solicitud haciendo clic en **Restaurar**.

   ![Confirmar restauración](assets/backup-restore.png)

El proceso de copia de seguridad se inicia y puede ver su estado en la **[Restaurar actividad](#restore-activity)** tabla. El tiempo necesario para completar una operación de restauración depende del tamaño y el perfil del contenido que se está restaurando.

Cuando la restauración se complete correctamente, el entorno:

* Ejecute el mismo código y AEM versión que en el momento de iniciar la operación de restauración.
* Tener el mismo contenido que estaba disponible en la marca de tiempo de la instantánea elegida, con los índices reconstruidos para coincidir con el código actual.

## Elección de la copia de seguridad correcta {#choosing-backup}

Restaura solo el contenido de restauración en AEM. Por este motivo, debe tener en cuenta cuidadosamente los cambios que se hayan realizado en el código entre el punto de restauración deseado y el momento actual revisando el historial de confirmación entre su ID de confirmación actual y el que se está restaurando.

Hay varios escenarios.

* El código personalizado en el entorno y la restauración se encuentran en el mismo repositorio y en la misma rama.
* El código personalizado en el entorno y la restauración se encuentran en el mismo repositorio pero en una rama diferente con una confirmación común.
* El código personalizado del entorno y la restauración se encuentran en diferentes repositorios.
   * En este caso, no se mostrará un ID de confirmación.
   * Se recomienda clonar ambos repositorios y utilizar una herramienta de diferenciación para comparar las ramas.

Además, tenga en cuenta que una restauración puede causar que los entornos de producción y ensayo no estén sincronizados. Usted es responsable de las consecuencias de restaurar contenido.

## Restaurar actividad {#restore-activity}

La variable **Restaurar actividad** muestra el estado de las diez solicitudes de restauración más recientes, incluidas las operaciones de restauración activas.

![Restaurar actividad](assets/backup-activity.png)

Al hacer clic en el icono de información para una copia de seguridad, puede descargar registros para esa copia de seguridad, así como inspeccionar los detalles del código, incluidas las diferencias entre la instantánea y los datos en el momento en que se inició la restauración.

## Copia de seguridad fuera del sitio {#offsite-backup}

Las copias de seguridad regulares cubren el riesgo de eliminaciones accidentales o fallos técnicos en AEM Cloud Services, pero pueden surgir riesgos adicionales debido a la falla de una región. Además de la disponibilidad, el riesgo bueno en esas interrupciones regionales es la pérdida de datos.

AEM as a Cloud Service mitiga este riesgo para todos los entornos de producción AEM copiando continuamente todo AEM contenido en una región remota y poniéndolo a disposición para su recuperación durante un período de tres meses. Esta capacidad se denomina copia de seguridad fuera del sitio.

La restauración de AEM Cloud Services para entornos de ensayo y producción a partir de copias de seguridad fuera del sitio la realiza AEM Service Fiabilidad Engineering en caso de interrupciones en la región de datos.
