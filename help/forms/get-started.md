---
title: Introducción a los formularios HTML5
description: Para empezar, implemente el paquete de complementos de AEM Forms e importe los formularios HTML5 existentes en AEM.
content-type: reference
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 1496d7517d586c99c5f1001fff13d88275e91d09
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 67%

---

# Introducción a los formularios HTML5 {#getting-started-with-html-forms}

<span class="preview">: la funcionalidad de Forms HTML5 se ofrece como parte del programa de acceso anticipado. Para solicitar acceso, envíe un correo electrónico desde su dirección oficial (de trabajo) a aem-forms-ea@adobe.com.
</span>

Los formularios HTML5 ofrecen numerosas funciones compatibles con dispositivos móviles. Esto le permite ampliar sus soluciones y flujos de trabajo actuales a tabletas o smartphones con exploradores HTML5. Ofrece, entre otras, las siguientes funcionalidades se encuentran:

* **Renderización basada en HTML5 de las plantillas de formulario XFA:** además de los formularios PDF normales, ahora puede procesar formularios existentes basados en XFA en formato HTML5. Esto le permite ampliar su plataforma de cliente a dispositivos móviles (iPad de Apple, tabletas Android, smartphones, etc.) compatibles con HTML5 y que no admiten Adobe Reader con los formularios XFA. Para obtener más información sobre la capacidad de procesamiento basada en HTML5, consulte [Introducción a los formularios HTML5](/help/forms/introductionhtml5.md).

* **Administración de formularios:** asimismo, AEM incluye nuevas funcionalidades para simplificar el proceso de organización y administración de formularios. Puede activar, desactivar, publicar y obtener una vista previa de los formularios.<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## Configurar el entorno para los formularios HTML5 {#installing-html-forms}

Para habilitar los envíos de formularios y el procesamiento adecuado de HTML5 Forms, realice los siguientes pasos:

* **Agregar filtros de Dispatcher:** Actualice su archivo `src/conf.dispatcher.d/filters/filters.any` para permitir las solicitudes necesarias para HTML5 Forms. Añada las siguientes reglas de filtro:

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **Agregue un paquete para el envío:** En su proyecto, agregue un paquete en la carpeta `src/main/content/jcr_root/content` para admitir la funcionalidad de envío de formularios.

* **Importar HTML5 Forms:** Importe formularios de su sistema de archivos local a AEM Forms.
