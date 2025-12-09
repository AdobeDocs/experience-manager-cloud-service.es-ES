---
title: Vista previa de PDF en el Editor de comunicaciones interactivas con diferentes opciones de datos
description: Vista previa de PDF en el Editor de comunicaciones interactivas con diferentes opciones de datos para obtener una vista previa de las comunicaciones interactivas de tres formas diferentes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 14%

---


# Vista previa de PDF en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

La función de vista previa de PDF permite a los usuarios obtener una vista previa de las comunicaciones interactivas de tres formas diferentes: sin datos, con datos locales basados en JSON o con datos de muestra del modelo de datos configurado.

## Principales ventajas

- Previsualice las comunicaciones interactivas con datos de ejemplo para visualizar cómo aparecerán los datos activos cuando se combinen con la comunicación.

- Cargar archivos de datos JSON locales para generar previsualizaciones impulsadas por datos sin configuración back-end.

- Utilice modelos de datos de formulario (FDM) conectados para simular la integración de datos en tiempo real con datos de ejemplo durante el diseño.

- Cambie fácilmente entre las opciones de datos (sin datos, datos locales, FDM) para validar el diseño, la estructura y la personalización.

## Vista previa de PDF en el Editor de comunicaciones interactivas con diferentes opciones de datos

Obtenga una vista previa de las comunicaciones interactivas sin datos, datos locales ni datos de muestra del modelo de datos configurado para realizar pruebas y validaciones flexibles.

+++&#x200B;1. Vista previa sin datos.

1.1. Abra la comunicación interactiva en el editor de CI.

1.2. Use la opción Vista previa de PDF y seleccione la opción **Sin datos** para ver una comunicación sin datos.

![Buscar documento CI](/help/forms/interactive-communication/assets/nodata.png)

+++

+++&#x200B;2. Vista previa con datos JSON locales

2.1. Prepare un archivo JSON estructurado. Como referencia, puede copiar los datos de ejemplo del esquema JSON [(FDM)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model) utilizado para la comunicación.

2.2. En el Editor IC, vaya a **Vista previa de PDF** > Uso de datos locales.

2.3. Seleccione y cargue su archivo JSON para obtener una vista previa de PDF con los datos proporcionados.

![Buscar documento CI](/help/forms/interactive-communication/assets/localdata.png)

+++

+++&#x200B;3. Vista previa con el modelo de datos 

3.1. Seleccione **Uso del modelo de datos** para usar datos de ejemplo de un modelo de datos de formulario (FDM) ya configurado de la CI.

3.2. La vista previa rellena automáticamente los datos de los campos de modelo. Asegúrese de que los datos de ejemplo se guarden en FDM la primera vez que los utilice; de lo contrario, la vista previa puede mostrarse como sin datos.

![Buscar documento CI](/help/forms/interactive-communication/assets/datamodel.png)

+++

