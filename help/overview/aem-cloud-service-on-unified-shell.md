---
title: AEM as a Cloud Service en Unified Shell
description: Obtenga información acerca de las ventajas de AEM as a Cloud Service en Unified Shell
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
feature: Release Information
role: Admin
source-git-commit: 55cf6a10c2cb4c62aa8f89fac7f9d1fb4c012d26
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 95%

---

# AEM as a Cloud Service en Unified Shell {#aem-as-a-cloud-service-on-unified-shell}

## Información general {#overview}

AEM as a Cloud Service (Servicio de Autor) está integrado con Unified Shell para mejorar la experiencia del usuario y unificarla con todas las demás aplicaciones de Experience Cloud. El impacto de esta integración se puede ver en el encabezado superior de la aplicación, como se muestra a continuación.

![imagen](/help/overview/assets/unifiedshell_header.png)

Los beneficios de esto son los siguientes:

* Inicio de sesión único en todas las aplicaciones de Experience Cloud
* Fácil cambio entre organizaciones o cambio a una aplicación diferente
* Ayuda del producto mejorada
* Botón de comentarios fácil dentro del producto para informar sobre problemas o compartir ideas con Adobe
* Acceso a anuncios y notificaciones de productos globales, además de notificaciones específicas de AEM as a Cloud Service

## Desactivación de Unified Shell {#disabling-unified-shell}

De forma predeterminada, AEM as a Cloud Service tiene habilitado el shell unificado. Sin embargo, en caso de que el encabezado superior se haya personalizado, se recomienda deshabilitar el shell unificado para evitar problemas con las personalizaciones. Para deshabilitar el shell unificado, siga los pasos a continuación:

>[!NOTE]
>Unified Shell solo se puede deshabilitar con una cuenta con privilegios administrativos.

1. Haga clic en **Herramientas > Cloud Services**.

   Un usuario administrador verá la tarjeta de configuración de Unified Shell como se muestra a continuación:

   ![imagen](/help/overview/assets/unifiedshell2.png)

1. Haga clic en **Configuración de Unified Shell**. A continuación, anule la selección de la casilla de verificación que aparece a continuación para deshabilitar Unified Shell:

   ![imagen](/help/overview/assets/unifiedshell3.png)

>[!NOTE]
>
>Unified Shell también se puede deshabilitar desde el código del proyecto. AEM Consulte [Estructura de la interfaz de usuario de la: Unified Shell](/help/implementing/developing/introduction/ui-structure.md#unified-shell).

## Cambio a tema oscuro {#changing-to-dark-theme}

Para cambiar al tema oscuro, haga clic en su icono de perfil. Esta acción muestra una ventana emergente como se muestra a continuación. Puede utilizar el conmutador para cambiar a un tema oscuro para el Unified Shell.

>[!INFO]
>
>El tema oscuro se aplica solo a Unified Shell (la barra superior).

![imagen](/help/overview/assets/unifiedshell4.png)

## Identificación del entorno de AEM as a Cloud Service {#identify-aemaacs-environment}

AEM as a Cloud Service proporciona tres tipos de entornos: producción, ensayo y desarrollo. Consulte [Tipos de entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=es) para obtener más información. Con esta integración con Unified Shell, el tipo de entorno en el que el usuario ha iniciado sesión en el servicio de creación se muestra en el encabezado superior con una etiqueta, como se muestra a continuación.

![imagen](/help/overview/assets/unifiedshell_header_label.png)

## Acceso a la bandeja de entrada AEM {#accessing-the-aem-inbox}

Se puede acceder a la Bandeja de entrada AEM haciendo clic en el icono de campana del shell unificado.

>[!INFO]
>
> El número indicado en el icono de campana incluye notificaciones sin leer en todas las soluciones de esa organización de IMS y tareas enumeradas en la bandeja de entrada de AEM.

![imagen](/help/overview/assets/unifiedshell5.png)

Haga clic en el botón Bandeja de entrada en la ventana emergente para poder ir a la Bandeja de entrada AEM:

![imagen](/help/overview/assets/unifiedshell6.png)

