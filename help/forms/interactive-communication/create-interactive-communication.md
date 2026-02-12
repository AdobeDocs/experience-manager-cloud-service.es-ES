---
title: Crear una comunicación interactiva
description: Crear comunicaciones personalizadas basadas en datos. Explore las funciones clave, los pasos de incorporación y los casos de uso reales con guías y tutoriales.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: c23145c9-078d-4b03-a8f4-2d835cdd1592
source-git-commit: 98465743f73f38e2a766657dda8c9ff18ecea856
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 11%

---


# Crear una comunicación interactiva

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

Interactive Communications le permite crear, administrar y entregar comunicaciones personalizadas e interactivas, incluido el servicio de atención al cliente, la facturación, los documentos de incorporación, las cartas de oferta, las actualizaciones de cuenta y más. Está diseñado para admitir cualquier escenario en el que el contenido dinámico y específico del usuario mejore la experiencia de comunicación entre industrias.

Imagine que necesita enviar un extracto bancario, una póliza de seguro o una factura de servicios públicos a miles de clientes. Cada una tiene el mismo diseño, pero con datos personalizados. La comunicación interactiva (CI) lo hace posible de forma eficaz.

![Buscar documento CI](/help/forms/interactive-communication/assets/introduction.png)

La producción manual de estos documentos puede llevar mucho tiempo y, a menudo, genera incoherencias, especialmente cuando se requieren la personalización y la integración de datos. Con el editor de comunicaciones interactivas, los usuarios pueden agilizar el proceso de creación de comunicaciones interactivas.

## Requisitos previos

* [Asegúrese de que el autor sea miembro del grupo forms-users](/help/forms/setup-forms-cloud-service.md#configure-users)

## Crear una comunicación interactiva

Elija entre diferentes escenarios para crear una comunicación interactiva, en función del nivel de reutilización e integración de datos necesaria:

+++ Crear una comunicación interactiva en blanco

La creación de una comunicación interactiva en blanco le permite empezar desde cero, lo que resulta ideal cuando desea tener un control total sobre el diseño, la estructura y la lógica.
Pasos a seguir:

1. Abra **Adobe Experience Manager (AEM) Forms as a Cloud Service**.
1. Vaya a **Forms > Forms y documentos**.
1. Haga clic en **Crear > Comunicación interactiva**.

   ![Buscar documento CI](/help/forms/interactive-communication/assets/comm.png)

1. En la pantalla de creación, deje en blanco el campo **Plantilla**.

   ![Buscar documento CI](/help/forms/interactive-communication/assets/create-ic-document.png)

1. Complete otros detalles como Título, Nombre, Autor, etc.
1. Haga clic en **Crear** para ingresar a la interfaz de usuario del editor de comunicaciones interactivas y comenzar a diseñar.
1. Se abre el Editor IC, donde puede empezar a diseñar la comunicación.
+++

+++ Crear una comunicación interactiva basada en plantillas

El uso de una plantilla ayuda a acelerar el diseño al reutilizar elementos de diseño coherentes, como encabezados, pies de página, logotipos o formato estándar.
Las plantillas garantizan la coherencia de la marca y ahorran tiempo para los tipos de comunicación más utilizados. Siga estos pasos:

1. Abra la instancia de AEM Forms as a Cloud Service.
1. Vaya a **Forms > Forms y documentos**, haga clic en **Crear > Comunicación interactiva**.
1. En el formulario de creación, **seleccione** una plantilla habilitada del selector de plantillas.
1. Complete otros detalles como Título, Nombre, Autor, etc.
1. Haga clic en **Crear** para diseñar la comunicación con la estructura de plantillas seleccionada.
1. Se abre el Editor IC, donde puede empezar a diseñar la comunicación.
+++

+++ Crear una comunicación interactiva con interacción de datos

Las comunicaciones interactivas con datos personalizan automáticamente el contenido mediante datos back-end.
Ideal para extractos, facturas o avisos donde la estructura permanece constante, pero los datos varían según el destinatario. Pasos a seguir:

1. Abra la instancia de AEM Forms as a Cloud Service.
1. Vaya a **Forms > Forms y documentos**, haga clic en **Crear > Comunicación interactiva**.
1. En el campo **Modelo de datos de formulario**, vincule el **FDM (Modelo de datos de formulario)** predefinido.
1. Complete otros detalles como Título, Nombre, Autor, etc.
1. Use **Modelo de datos** dentro del editor para enlazar campos a datos dinámicos (por ejemplo: nombre del cliente, saldo, número de cuenta).
1. Use **Áreas de contenido, subformularios** y **Fragmentos** para estructurar y repetir datos donde sea necesario.
1. Obtenga una vista previa con **PDF Preview** y finalice la comunicación para la entrega.
1. Se abre el Editor IC, donde puede empezar a diseñar la comunicación.

![Buscar documento CI](/help/forms/interactive-communication/assets/ic-ui.png)
+++

Comience a crear comunicaciones interactivas para optimizar los flujos de trabajo y ofrecer experiencias impactantes y específicas para el usuario.

## Próximos pasos

[Crear una plantilla de comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication-template.md)
[Crear un fragmento de comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication-fragment.md)
