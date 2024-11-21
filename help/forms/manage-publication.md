---
title: ¿Cómo publicar o cancelar la publicación de formularios en instancias de vista previa o publicación?
description: AEM Obtenga información sobre cómo publicar o cancelar la publicación de formularios desde el entorno de autor de la para previsualizar o publicar instancias. AEM Tanto si está probando los formularios en un entorno de ensayo como si los está implementando en directo para los usuarios finales, proporciona herramientas optimizadas para administrar este proceso de forma eficaz.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, manage publication, , AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: 242dcbc5bb541dfac601454fb75dec3bdff1ea64
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---


# &#x200B;Administrar publicación en Experience Manager Forms

Como administrador de Adobe Experience Manager Forms, puede publicar formularios de su instancia de autor en Experience Manager Forms. Puede programar la publicación de un formulario o una carpeta en una fecha u hora posterior. Una vez publicados, los usuarios pueden acceder a los formularios y rellenarlos.

Puede publicar o cancelar la publicación de un formulario mediante las opciones Publish o Administrar publicación disponibles en la interfaz de Experience Manager Forms. Si realiza las modificaciones posteriores a los formularios o carpetas originales en Experience Manager Forms, los cambios no se reflejarán en la instancia de publicación hasta que vuelva a publicar desde Experience Manager Forms. Garantiza que los cambios en curso no estén disponibles en la instancia de publicación. En la instancia de publicación solo están disponibles los cambios publicados por un administrador.

## Formularios Publish que utilizan la opción Publish

La opción de publicación permite publicar inmediatamente un formulario. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desee publicar. Haga clic en la opción Publish en la barra de herramientas, observe todos los recursos de referencia que se publicarían con el formulario y haga clic en Publish.

Captura de pantalla de un equipo

Descripción generada automáticamente

## Publish o Cancelar la publicación de formularios mediante Administrar publicación


Administrar publicación permite publicar o cancelar la publicación del contenido desde y hacia el destino seleccionado, agregar contenido a la lista de publicaciones desde la carpeta formularios y documentos, seleccionar referencias para publicar y programar la publicación a una fecha u hora posterior.


En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desee publicar. Haga clic en la opción Administrar publicación en la barra de herramientas.


Captura de pantalla de un equipo

Descripción generada automáticamente



Las siguientes opciones están disponibles en la interfaz Administrar publicación:

* Acciones

   * Publish: formularios de Publish al destino seleccionado.
   * Cancelar publicación: cancelar la publicación de formularios desde el destino

* Destino

   * Publish: instancia de Publish Forms a Experience Manager Forms AEM () Publish.
   * Vista previa: la instancia de vista previa de Publish Forms a Experience Manager Forms AEM ().

* Programación

   * Ahora: formularios Publish inmediatamente
   * Más tarde: formularios de Publish basados en la fecha u hora de activación



Para continuar, haz clic en **Siguiente**. En la pestaña Ámbito, utilice las opciones Agregar contenido para agregar más contenido para la publicación. Por ejemplo, puede agregar más archivos de Forms o de documento de registro.

### Añadir contenido

La publicación en Experience Manager Forms permite añadir más contenido (formularios, recursos y carpetas) a la lista de publicaciones. Puede agregar más formularios, recursos o carpetas a la lista desde la carpeta formsanddocuments. Pero no puede agregar recursos de varias carpetas a la vez.

Captura de pantalla de un equipo

Descripción generada automáticamente

Haga clic en el botón **Agregar contenido** para agregar más contenido. Puede agregar varios recursos desde una carpeta o agregar varias carpetas a la vez. Pero no puede agregar recursos de varias carpetas a la vez.

Para configurar las referencias para que se publiquen o no para un formulario u otros recursos, seleccione el formulario o el recurso y haga clic en Referencias publicadas.

Captura de pantalla de un equipo

Descripción generada automáticamente

En el cuadro de diálogo Referencias publicadas, anule la selección de los recursos que planea no publicar y haga clic en listo.


Captura de pantalla de un equipo

Descripción generada automáticamente


## Publish o cancelar la publicación de un formulario más tarde


Además de permitirle publicar o cancelar la publicación de formularios en una fecha y hora posteriores, la opción Publicar o cancelar la publicación más tarde también permite configurar un flujo de trabajo. Los formularios se publican o no se completan una vez finalizado el flujo de trabajo. Para programar la publicación o cancelación de la publicación de un formulario:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea programar para la publicación.
1. Haga clic en la opción Administrar publicación en la barra de herramientas.
1. Haga clic en Publish o en Cancelar la publicación de la acción y, a continuación, seleccione el destino en el que desea publicar o cancelar la publicación del contenido.

   * Vista previa: utilice la opción Vista previa para publicar o cancelar la publicación en un entorno de vista previa de Experience Manager Forms. Los entornos de vista previa de Experience Manager Forms se utilizan para realizar pruebas en formularios de desarrollo.
   * Publish: utilice la opción Experience Manager Forms Publish para enviar el formulario al entorno de publicación de Experience Manager Forms después de que el formulario esté listo para utilizarse en un entorno de producción.


1. Seleccione Más tarde en Programación.

1. Seleccione una Fecha de activación y especifique la fecha y la hora. Haga clic en Siguiente.

   Captura de pantalla de un equipo

   Descripción generada automáticamente

1. En la pestaña Scope, agregue contenido (si es necesario). Haga clic en Siguiente.

   Captura de pantalla de un equipo

   Descripción generada automáticamente

1, (Opcional) En la pestaña Flujos de trabajo, especifique un título para el flujo de trabajo. Haga clic en Publish más tarde.

Captura de pantalla de un equipo

Descripción generada automáticamente

## Determinar el estado de publicación

Existen varias formas de determinar el estado de publicación:

* Inicie sesión en la instancia de destino para verificar los formularios publicados y otros recursos (según la fecha u hora programadas).

* Utilice la vista de cronología para determinar el estado de la publicación.

* Utilice el menú de información de página del editor de Forms adaptable.