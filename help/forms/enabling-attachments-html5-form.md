---
title: Activar archivos adjuntos en un formulario HTML5
description: De forma predeterminada, la compatibilidad con los archivos adjuntos de los formularios HTML5 está deshabilitada.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: HTML5 Forms,Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 92%

---

# Activar archivos adjuntos en un formulario HTML5 {#enabling-attachments-for-an-html-form}

<span class="preview">: la funcionalidad HTML5 Forms se ofrece como parte del programa de acceso anticipado. Para solicitar acceso, envíe un correo electrónico con el ID de correo electrónico oficial (de trabajo) a aem-forms-ea@adobe.com.
</span>

Puede cargar, previsualizar y enviar archivos adjuntos con formularios HTML5. De forma predeterminada, la compatibilidad con los archivos adjuntos está deshabilitada. Para habilitar la compatibilidad de datos adjuntos, haga lo siguiente:

1. Cree un [perfil personalizado](/help/forms/custom-profile.md) con una propiedad de cadena multiselección`mfAttachmentOptions`. Cada cadena de la propiedad `mfAttachmentOptions` debe tener un formato `property=value` para configurar las opciones del widget de archivos adjuntos. `property` y `value` pueden tener cualquiera de los siguientes valores:

   | Propiedad | Valor |
   |--- |---|
   | multiSelect | true o false (true de forma predeterminada) |
   | fileSizeLimit | Número en MB (2 MB de forma predeterminada). Por ejemplo, 5. |
   | buttonText | Texto del botón de la ventana emergente (“Adjuntar” de forma predeterminada) |
   | aceptar | lista separada por comas de los tipos de archivo que se van a aceptar (&quot;audio/&ast;, video/&ast;, image/&ast;, text/&ast;, .pdf&quot; de manera predeterminada) |

   Por ejemplo:

   ![configurar opciones](assets/mfAttachmentOptions.png)

   Si es necesario, también puede especificar más opciones personalizadas para la propiedad `mfAttachmentOptions`.

   >[!NOTE]
   >
   >En Microsoft Internet Explorer 9, los usuarios pueden adjuntar archivos que superen el límite especificado. Es un problema conocido.

1. Utilice el [editor de metadatos](/help/forms/manage-form-metadata.md) para seleccionar el perfil personalizado que ha creado anteriormente para los formularios HTML5.
1. Procese la plantilla de formulario con un perfil personalizado y el icono de archivos adjuntos aparecerá en la barra de herramientas de formularios.

   >[!NOTE]
   >
   >De forma predeterminada, el portal de formularios proporciona un perfil personalizado con la capacidad Borradores y archivos adjuntos habilitada. Para obtener más información sobre el perfil **Guardar como borrador**, consulte [Guardar formularios HTML5 como borrador](/help/forms/saving-html5-form-draft.md).

1. Haga clic en el icono de datos adjuntos y aparecerá un cuadro de diálogo de selección de datos adjuntos. Examine y seleccione el archivo adjunto y haga clic en **Adjuntar**.

   >[!NOTE]
   >
   >Para obtener una vista previa de un archivo adjunto, haga clic en su nombre.

   >[!NOTE]
   >
   >La opción de vista previa del archivo no está disponible para usuarios anónimos.

## Formato de envío de datos adjuntos {#attachment-submission-format}

Cuando los archivos adjuntos están habilitados, el formulario HTML5 envía datos de varias partes. Los datos de envío de varias partes tienen dos partes **dataXml** y **archivos adjuntos**.

>[!NOTE]
>
>Para la compatibilidad con versiones anteriores, si la opción `mfAllowAttachments` está desactivada, los formularios HTML5 no enviarán los datos de varias partes. Envía xml de datos simples en el formato **application/xml**.

Si el indicador mfAllowAttachments está activado, el [servicio enviar servicio proxy](/help/forms/service-proxy.md) también publicará datos de varias partes con dataXml y archivos adjuntos.
