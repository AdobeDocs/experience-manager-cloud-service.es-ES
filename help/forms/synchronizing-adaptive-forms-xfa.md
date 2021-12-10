---
title: Sincronización de Forms adaptable con plantillas de formulario XFA
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: Sincronización de Forms adaptable con archivos XFA/XDP.
seo-description: Synchronizing Adaptive Forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# Sincronización de Forms adaptable con plantillas de formulario XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introducción {#introduction}

Puede crear un formulario adaptable basado en una plantilla de formulario XFA ( `*.XDP` ). Esta reutilización le permite preservar su inversión en formularios XFA existentes. Para obtener información sobre cómo utilizar una plantilla de formulario XFA para crear un formulario adaptable, [Creación de un formulario adaptable basado en una plantilla](creating-adaptive-form.md).

Puede reutilizar campos del archivo XDP en el formulario adaptable. Estos campos se denominan campos enlazados. Las propiedades de los campos enlazados (como secuencias de comandos, etiquetas y formato de visualización) se copian del archivo XDP. También puede optar por anular el valor de algunas de estas propiedades.

[!DNL AEM Forms] proporciona una forma de ayudarle a mantener los campos de Adaptive Forms sincronizados con cualquier cambio que se realice posteriormente en los campos correspondientes del archivo XDP. Este artículo explica cómo habilitar esta sincronización.

![Puede arrastrar campos de un formulario XFA a un formulario adaptable](assets/drag-drop-xfa.gif.gif)

En el [!DNL AEM Forms] entorno de creación, puede arrastrar campos de un formulario XFA (izquierda) a un formulario adaptable (derecha)

## Requisitos previos {#prerequisites}

Para utilizar la información de este artículo, se recomienda estar familiarizado con las siguientes áreas:

* [Creación de un formulario adaptable](creating-adaptive-form.md)

* XFA (XML Forms Architecture)

Para utilizar los recursos que proporciona el ejemplo en el artículo , descargue el paquete de muestra como se explica en la siguiente sección, [Paquete de muestra](synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Paquete de muestra {#sample-package}

El artículo utiliza un ejemplo para demostrar cómo sincronizar el formulario adaptable con una plantilla de formulario XFA actualizada. Los recursos utilizados en el ejemplo están disponibles en un paquete que se puede descargar de la [Descargas](synchronizing-adaptive-forms-xfa.md#p-downloads-p) en este artículo.

Después de cargar el paquete, puede ver estos recursos en la [!DNL AEM Forms] IU.

Instale el paquete utilizando el administrador de paquetes: `https://<server>:<port>/crx/packmgr/index.jsp`

El paquete contiene los siguientes activos:

1. `sample-form.xdp`: La plantilla de formulario XFA utilizada como ejemplo

1. `sample-xfa-af`: El formulario adaptable basado en el archivo ejemplo-form.xdp. Sin embargo, este formulario adaptable no incluye ningún campo. En el siguiente paso, añadiremos contenido a este formulario adaptable.

### Añadir contenido al formulario adaptable {#add-content-to-adaptive-form-br}

1. Vaya a https://&lt;server>:&lt;port>/aem/forms.html. Introduzca sus credenciales si se le solicita.
1. Abra el ejemplo af-xfa para editarlo en modo de autor.
1. En el navegador de contenido de la barra lateral, seleccione la ficha Objetos del modelo de datos. Arrastre NumericField1 y TextField1 al formulario adaptable.
1. Cambiar el título del campo numérico1 de **Campo numérico** a **Campo numérico AF.**

>[!NOTE]
>
>En los pasos anteriores, se sobrescribió una propiedad de un campo en el archivo XDP. Por lo tanto, esta propiedad no se sincroniza si la propiedad correspondiente del archivo XDP se modifica más adelante.

## Detección de cambios en el archivo XDP {#detecting-changes-in-xdp-file}

Siempre que haya algún cambio en un archivo XDP o en un fragmento, la variable [!DNL AEM Forms] La interfaz de usuario marca todos los Forms adaptables basados en el archivo XDP o en el fragmento.

Después de actualizar un archivo XDP, debe cargarlo de nuevo en la [!DNL AEM Forms] IU para marcar los cambios.

Por ejemplo, vamos a actualizar el `sample-form.xdp` mediante los siguientes pasos:

1. Vaya a `https://<server>:<port>/projects.html.` Introduzca sus credenciales si se le solicita.
1. Haga clic en la ficha Forms de la izquierda.
1. Descargue el `sample-form.xdp` en el equipo local. El archivo XDP se descarga como un `.zip` , que se puede extraer utilizando cualquier utilidad de descompresión de archivos.

1. Abra el `sample-form.xdp` y cambie el título del campo TextField1 de **Campo de texto** a **Mi campo de texto**.

1. Cargue el `sample-form.xdp` volver a entrar en el [!DNL AEM Forms] IU.

Si se actualiza un archivo XDP, verá un icono en el editor cuando edite el Forms adaptable basado en el archivo XDP. Este icono indica que el formulario adaptable no está sincronizado con el archivo XDP. En la siguiente imagen, vea el icono que hay junto en la barra lateral.

![Icono para mostrar que el formulario adaptable no está sincronizado con el archivo XDP](assets/sync-af-xfa.png)

## Sincronización de Forms adaptable con el archivo XDP más reciente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Cuando se abre un formulario adaptable que no está sincronizado con el archivo XDP para la creación la próxima vez, se muestra el siguiente mensaje: **Se ha actualizado la plantilla de esquema/formulario del formulario adaptable. `Click Here` para volver a basarlo en la nueva versión.**

Al hacer clic en el mensaje, se sincronizan los campos del formulario adaptable con los campos correspondientes del archivo XDP.

Para el ejemplo utilizado en este artículo, abra `sample-xfa-af` en modo de creación. El mensaje se muestra hacia la parte inferior del formulario adaptable.

![Mensaje que le solicita que sincronice el formulario adaptable con el archivo XDP](assets/sync-af-xfa-1.png)

### Actualización de las propiedades {#updating-the-properties}

Todas las propiedades que se copiaron del archivo XDP al formulario adaptable se actualizan, a excepción de las propiedades que el autor anuló explícitamente en el formulario adaptable (del cuadro de diálogo de componentes). La lista de propiedades que se han actualizado está disponible en los registros del servidor.

Para actualizar las propiedades en el formulario adaptable de ejemplo, haga clic en el vínculo (etiquetado `"Click Here"`) en el mensaje. El título de TextField1 cambia de **Campo de texto** a **Mi campo de texto**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>La etiqueta Campo numérico AF no se ha modificado porque se ha anulado esta propiedad del cuadro de diálogo de propiedades del componente, tal como se describe en [Añadir contenido a Forms adaptable](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Adición de nuevos campos del archivo XDP al formulario adaptable   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Todos los campos que se agreguen posteriormente al archivo XDP original aparecen en la ficha Jerarquía del formulario y puede arrastrar los nuevos campos al formulario adaptable.

No es necesario hacer clic en el vínculo del mensaje de error para actualizar los campos en la ficha Jerarquía del formulario.

### Campos eliminados en el archivo XDP {#deleted-fields-in-xdp-file}

Si un campo que se copió anteriormente en un formulario adaptable se elimina de un archivo XDP, se muestra un mensaje de error en el modo de creación indicando que el campo no existe en el archivo XDP. En estos casos, elimine manualmente el campo del formulario adaptable o borre la variable `bindRef` en el cuadro de diálogo del componente.

Los siguientes pasos ilustran este flujo de uso para los recursos en el ejemplo utilizado en este artículo:

1. Actualice el `sample-form.xdp` y elimine NumericField1.
1. Cargue el `sample-form.xdp` en el [!DNL AEM Forms] IU
1. Abra el `sample-xfa-af` Formulario adaptable para la creación. Se muestra el siguiente mensaje de error: Se ha actualizado la plantilla de esquema/formulario del formulario adaptable. `Click Here` para volver a basarlo en la nueva versión.

1. Haga clic en el vínculo (con la etiqueta &quot; `Click Here`&quot;) en el mensaje. Se muestra un mensaje de error indicando que el campo ya no existe en el archivo XDP.

![Error que se ve al eliminar un elemento del archivo XDP](assets/no-element-xdp.png)

El campo que se ha eliminado también se marca con un icono para indicar un error en el campo.

![Icono de error en el campo](assets/error-field.png)

>[!NOTE]
>
>Los campos del formulario adaptable que tienen un enlace incorrecto (un enlace no válido) `bindRef` en el cuadro de diálogo de edición) también se consideran campos eliminados. Si el autor no corrige estos errores y publica el formulario adaptable, el campo se trata como un campo de formulario adaptable normal sin enlazar y se incluye en la sección sin enlazar del archivo XML de salida.

## Descargas {#downloads}

Paquete de contenido, por ejemplo, en este artículo

[Obtener archivo](assets/sample-xfa-af-sync-1.0.zip)
