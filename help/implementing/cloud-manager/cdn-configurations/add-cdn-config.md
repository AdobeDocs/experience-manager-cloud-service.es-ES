---
title: Añadir una configuración de CDN
description: Obtenga información acerca de cómo añadir una configuración de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e57a6ceb2482e61acabe928da0f539d26989985c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---


# Añadir una configuración de CDN {#add-cdn}

Debe completar la adición de una configuración de CDN para configurar un dominio con un SSL.

>
>
>En el caso de las CDN administradas por Adobe, al utilizar certificados DV, solo se permiten sitios con validación ACME.

**Para agregar una configuración de CDN:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en **Configuraciones de CDN**.

1. Cerca de la esquina superior derecha de la página Configuraciones de CDN, haga clic en **Agregar**.

   ![Cuadro de diálogo Configurar CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. En el cuadro de diálogo **Configurar CDN**, proporcione la información necesaria.

   * En la lista desplegable **Origen**, realice una de las siguientes acciones:
      * **Sitios:** Seleccione un sitio de Edge Delivery Services.
      * **Entornos:** Seleccione un entorno de Cloud Service.
         * **Nivel:** Seleccione un nivel web de **Publish** o **Vista previa** para el entorno seleccionado.
   * Seleccione su tipo de CDN: **CDN administrado por Adobe** o **Otro proveedor de CDN**.
   * Seleccione el dominio.
   * Seleccione el certificado SSL. Solo es necesario si ha seleccionado **CDN administrado por Adobe** como tipo de CDN.

1. Haga clic en **Guardar**.




