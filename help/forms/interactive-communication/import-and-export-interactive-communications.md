---
title: Importar y exportar comunicaciones interactivas
description: Importar y exportar comunicaciones interactivas permite a los usuarios migrar, reutilizar y administrar las comunicaciones entre entornos sin problemas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 15%

---


# Importar y exportar comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

La funcionalidad de importación y exportación de la comunicación interactiva (IC) permite a los usuarios migrar, reutilizar y administrar sin problemas las comunicaciones entre entornos. Permite exportar una comunicación interactiva (CI) junto con sus fragmentos y modelos de datos asociados de un entorno e importarla en otro, lo que garantiza la coherencia y reduce la duplicación de esfuerzos durante la implementación.

## Principales ventajas

- Simplifica la migración de las CI entre entornos.
- Conserva fragmentos, modelos de datos y dependencias.
- Reduce el esfuerzo por recrear CI en todos los proyectos.

## Importar y exportar comunicaciones interactivas

Cree una comunicación interactiva (CI) en un entorno y reutilícela en otro exportándola e importándola siguiendo estos pasos:

+++&#x200B;1. Cómo exportar la comunicación interactiva

1.1. Seleccione una [comunicación interactiva creada](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/create-interactive-communication) (CI).
1.2. Haga clic en la opción **Descargar** para exportarla como archivo ZIP.
1.3. El archivo ZIP descargado incluye la CI junto con su **plantilla**, **fragmentos** y **modelo de datos** seleccionados.

![Buscar documento CI](/help/forms/interactive-communication/assets/downloadic.png)
+++

+++&#x200B;2. Cómo importar la comunicación interactiva

2.1. Vaya al entorno de destino.
2.2. Vaya a **Forms > Forms y Documentos > Crear > Cargar archivo**.
2.3. Cargue el archivo ZIP para **importar** la CI.

![Buscar documento CI](/help/forms/interactive-communication/assets/uploadfile.png)

2.4. Después de la carga, aparece la CI junto con sus fragmentos y modelos de datos asociados.

![Buscar documento CI](/help/forms/interactive-communication/assets/importfragment.png)
+++

+++&#x200B;3. Importar y exportar fragmento

3.1. Para exportar, seleccione el fragmento necesario de **Forms > Forms and Documents** y, a continuación, haga clic en **Descargar** para exportarlo como archivo ZIP.

3.2. Para importar, vaya al entorno de destino, vaya a Forms > Forms y Documentos > Crear > **Carga de archivos** y cargue el archivo ZIP exportado.

Esto permite reutilizar fácilmente los fragmentos en diferentes entornos, lo que garantiza la coherencia del diseño y reduce la duplicación de esfuerzos.
+++
