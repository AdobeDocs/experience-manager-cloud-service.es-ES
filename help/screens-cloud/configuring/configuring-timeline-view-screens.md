---
title: Configuración de la vista Cronología para AEM Screens
description: En esta página se describe cómo configurar una vista de cronología en Pantallas as a Cloud Service.
source-git-commit: 30317d006142b3fbfc1b62fab5b4e28cb1b7dbb7
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 7%

---

# Configuración de la vista Cronología para AEM Screens {#configuring-timelineview-screens}

## Introducción {#introduction}

En esta sección se describe cómo crear una vista de línea de tiempo para AEM Screens.

AEM proporciona un conjunto de funciones que permiten a varias personas de grupos de una organización colaborar en la creación, administración y uso del canal.
La cronología, ubicada en la barra izquierda, describe los canales, la ubicación o el ciclo de vida de cualquier carpeta de pantalla en orden temporal para transmitir lo que le ha sucedido a lo largo de su vida útil. Esto se puede filtrar por tipo.
El raíl de cronología proporciona las siguientes funciones además de los registros de ciclo de vida.

![Aplicar perfil a la carpeta](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![Aplicar perfil a la carpeta](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

Para crear una vista de línea de tiempo para AEM Screens, complete los siguientes pasos:

1. Añadir un comentario
1. Guardar una versión
1. Iniciar un flujo de trabajo

La siguiente sección describe estos pasos en detalle.

### Agregar un comentario {#addcomment}

Los comentarios disponibles a través de la cronología permiten a los usuarios crear un registro centralizado e histórico para las discusiones que tienen lugar sobre el canal, la ubicación o cualquier carpeta de la pantalla.
AEM Los comentarios proporcionan una buena manera consolidada para que los usuarios de la discutan una manera que puede persistir, permitiendo que otros entiendan las decisiones clave.

1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Añada el comentario deseado y pulse Intro

![Agregar un comentario](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

La información de la cronología se actualiza para indicar que se ha añadido el comentario.

![Agregar un comentario](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### Guardar una versión {#saveversion}

El control de versiones crea una &quot;captura de pantalla&quot; de un canal en un momento específico. Con las versiones, se pueden realizar las siguientes operaciones:
* Cree una versión de un canal.
* Restaurar un canal a una versión anterior; por ejemplo:
   * para deshacer un cambio realizado en la página.
* Comparar la versión actual de un canal con una versión anterior:
   * para resaltar diferencias en el contenido del canal.


#### Crear una nueva versión {#createnewversion}

1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Haga clic en el botón (tres puntos) junto al campo de comentarios en la parte inferior.

   ![Agregar un comentario](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. Seleccione Guardar como versión
1. Introduzca una Etiqueta y un Comentario si es necesario

   ![Agregar un comentario](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. Confirme la nueva versión con Crear. La información de la cronología se actualiza para indicar la nueva versión.

#### Revertir a una versión {#revertversion}

Para revertir la página seleccionada a una versión anterior:
1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Seleccione Mostrar todo o Versiones en el menú desplegable de filtros. Se muestran las versiones de canal del canal seleccionado
1. Seleccione la versión a la que desea revertir. Se muestran las opciones posibles:

   ![Agregar un comentario](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. Seleccione Revertir a esta versión. La versión seleccionada se restaura y la información de la cronología se actualiza

#### Previsualizar una versión {#previewversion}

Puede obtener una vista previa de una versión específica:
1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Seleccione Mostrar todo o Versiones en el menú desplegable de filtros. Se muestran las versiones de canal del canal seleccionado
1. Seleccione la versión que desee previsualizar. Se muestran las opciones posibles:

   ![Previsualizar versión](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. Seleccione Previsualizar. El canal se muestra en una nueva pestaña.

#### Comparar una versión con la versión actual {#compareversion}

Puede comparar una versión específica con la versión actual:
1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Seleccione Mostrar todo o Versiones en el menú desplegable de filtros. Se muestran las versiones de canal del canal seleccionado
1. Seleccione la versión que desea comparar. Se muestran las opciones posibles:

   ![Comparar versión](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. Seleccione Comparar con actual. La ventana emergente se abre para mostrar las diferencias

### Iniciar un flujo de trabajo {#workflowstart}

Durante la creación, puede invocar flujos de trabajo para realizar acciones en los canales; también es posible aplicar más de un flujo de trabajo.
A la hora de aplicar el flujo de trabajo, se especifica la siguiente información:
* Flujo de trabajo que se va a aplicar
* De forma opcional, un título que ayude a identificar la instancia de flujo de trabajo en la bandeja de entrada de un usuario
* La carga útil del flujo de trabajo

#### Inicio del flujo de trabajo

1. Vaya al canal para el que desea agregar un comentario
1. Seleccione el canal
1. Abrir la columna Cronología
1. Haga clic en el botón (tres puntos) junto al campo de comentarios en la parte inferior

   ![Iniciar flujo de trabajo](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. Seleccione Iniciar flujo de trabajo
1. Se abrirá el asistente Crear flujo de trabajo para especificar los detalles del flujo de trabajo
1. Seleccione Modelo de flujo de trabajo de la lista desplegable e introduzca el título del flujo de trabajo

   ![Iniciar flujo de trabajo](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. Continúe haciendo clic en Siguiente
1. En el paso Ámbito, puede
* Añadir contenido para añadir recursos adicionales al flujo de trabajo
* Incluir elementos secundarios para especificar que en el flujo de trabajo se incluirán los elementos secundarios de ese recurso
* Remove Selection para eliminar ese recurso del flujo de trabajo

  ![Iniciar flujo de trabajo](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. Use Crear para cerrar el asistente y crear la instancia de flujo de trabajo
1. Es posible que deba realizar algunas acciones adicionales para completar el flujo de trabajo según el modelo de flujo de trabajo seleccionado

![Iniciar flujo de trabajo](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
