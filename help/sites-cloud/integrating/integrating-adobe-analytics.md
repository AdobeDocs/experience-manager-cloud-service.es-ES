---
title: Integración con Adobe Analytics
description: 'Integración con Adobe Analytics '
translation-type: tm+mt
source-git-commit: f2ed74afd2df43e31ff1002cd42a60f372d0b769
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---


# Integración con Adobe Analytics{#integrating-with-adobe-analytics}

La integración de Adobe Analytics y AEM como Cloud Service le permite rastrear la actividad de su página web. La integración requiere:

* uso de la IU táctil para crear una configuración de Analytics en AEM como Cloud Service.
* agregar y configurar Adobe Analytics como una extensión en [Adobe Launch].(https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html).

En comparación con las versiones anteriores de AEM, la configuración de Analytics no ofrece soporte técnico como Cloud Service en AEM. En su lugar, ahora se realiza a través de Adobe Launch, que es la herramienta de facto para instrumentar un sitio AEM con las capacidades de Analytics (bibliotecas JS). En Inicio de Adobe, se crea una propiedad en la que se puede configurar la extensión Adobe Analytics y se crean reglas para enviar datos a Adobe Analytics. Inicio de Adobe ha reemplazado la tarea de análisis proporcionada por sitecatalyst.

>[!NOTE]
>
>Adobe Experience Manager como cliente Cloud Service que no tiene una cuenta Analytics existente, puede solicitar acceso a Analytics Foundation Pack para Experience Cloud. Este paquete de Foundation proporciona un uso limitado por volumen de Analytics.

## Creación de la configuración de Analytics {#analytics-configuration}

1. Vaya a **Herramientas** → **Cloud Service**.
2. Seleccione Configuraciones **de Adobe Analytics**.
   ![Ventana](assets/analytics_screen1.png "de Analytics WindowAnalytics")
3. Seleccione el botón **Crear** .
4. Complete los detalles (véase más abajo) y haga clic en **Connect**.

### Parámetros de configuración {#configuration-parameters}

Los campos de configuración presentes en la ventana Configuración de Adobe Analytics son:

![Parámetros](assets/properties_field1.png "de configuración Parámetros de configuración")

| Propiedad | Descripción |
|---|---|
| Empresa | Compañía de inicio de sesión de Adobe Analytics |
| Nombre de usuario | Usuario de la API de Adobe Analytics |
| Contraseña | Contraseña de Adobe Analytics utilizada para la autenticación |
| Centro de datos | Centro de datos de Adobe Analytics con el que está asociada su cuenta (servidor, por ejemplo, San José, Londres) |
| Segmento | Opción para utilizar un segmento de Analytics definido en el grupo de sistemas de informes actual. Los informes de Analytics se filtrarán según el segmento. Consulte [esta página](https://docs.adobe.com/content/help/en/analytics/components/segmentation/seg-overview.html) para obtener más detalles. |
| Grupos de informes | Repositorio en el que se envían datos y se extraen informes. Un grupo de informes define el sistema de informes completo e independiente en un sitio web, conjunto de sitios web o subconjunto de páginas de sitios web elegidos. Puede realizar la vista de los informes recuperados desde un único grupo de informes y puede editar este campo en una configuración en cualquier momento según sus necesidades. |

### Añadir una configuración en un sitio {#add-configuration}

Para aplicar una configuración de IU táctil a un sitio, vaya a: **Sitios** → **Seleccione cualquier página** del sitio → **Propiedades** → **Avanzadas** → **Configuración** → seleccione el inquilino de configuración.

## Integración de Adobe Analytics en sitios AEM mediante Adobe Launch

Adobe Analytics se puede agregar como extensión en la propiedad Launch. Se pueden definir reglas para realizar asignaciones y realizar una llamada posterior a Adobe Analytics:

* Vea [este vídeo](https://docs.adobe.com/content/help/en/analytics-learn/tutorials/implementation/via-adobe-launch/basic-configuration-of-the-analytics-launch-extension.html) para aprender a configurar la extensión de Analytics en Launch para un sitio básico.

* Consulte [esta página](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html) para obtener más información sobre cómo crear reglas y enviar datos a Adobe Analytics.

>[!NOTE]
>
>Los marcos existentes (heredados) siguen funcionando, pero no se pueden configurar en la IU táctil. Es aconsejable volver a compilar las configuraciones de asignación de variables en Launch.

>[!NOTE]
>
>La configuración de IMS (cuentas técnicas) para Launch está preconfigurada en AEM como Cloud Service. Los usuarios no tienen que crear esta configuración.
