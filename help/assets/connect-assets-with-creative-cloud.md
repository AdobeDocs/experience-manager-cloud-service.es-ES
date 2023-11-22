---
title: Conectar AEM Assets a Creative Cloud
description: Obtenga información sobre cómo configurar y conectar AEM Assets a Creative Cloud. Conéctese a un derecho de Creative Cloud que esté aprovisionado para una organización IMS diferente para utilizar fácilmente las integraciones de Creative Cloud más recientes en AEM Assets, incluidas las bibliotecas Express y de Creative Cloud.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
source-git-commit: 237b4a8e01af74dbaac0ba1715b5fa95c931be7c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Conectar AEM Assets a Creative Cloud  {#cross-org-entitlements}

Experience Manager Assets tiene la capacidad de conectarse a un derecho de Creative Cloud que se proporciona a una organización IMS diferente para utilizar fácilmente las integraciones de Creative Cloud más recientes en AEM Assets, incluidas las bibliotecas Express y de Creative Cloud.

Si los productos de Creative Cloud y AEM Assets se aprovisionan para organizaciones IMS independientes, puede conectarse a una organización de Creative Cloud diferente para poder ejecutar flujos de trabajo integrados entre las dos soluciones.

## Requisitos previos {#prerequisites}

* Derechos de administrador en Experience Manager Assets

* Derecho activo al Creative Cloud para el mismo ID de usuario utilizado en el Creative Cloud y el Experience Manager. Los derechos sobre los ID personales y federados con la misma dirección de correo electrónico se tratan como ID de usuario diferentes.

## Conexión a una nueva organización de Creative Cloud {#connect-to-creative-cloud-org}

Para conectarse a una nueva organización de Creative Cloud, ejecute los siguientes pasos:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Creative Cloud]**.

1. Seleccione la nueva organización de Creative Cloud mediante el **[!UICONTROL Seleccionar nuevo ID de organización de Creative Cloud]** lista desplegable. La lista muestra todas las organizaciones a las que tiene acceso. Seleccione la organización con derechos de Creative Cloud activos.

1. Clic **[!UICONTROL Cambio de organizaciones]** para cambiar a la nueva organización.

   ![Derechos entre Organizaciones](assets/cross-org-entitlements.png)

## Restricciones {#limitations}

* Puede conectar AEM Assets a una organización Creative Cloud a la vez. No se admite la conexión a varias organizaciones de Creative Cloud a la vez.

* La organización de Creative Cloud a la que se conecta en AEM Assets se aplica a todos los usuarios de su organización.
