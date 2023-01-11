---
title: AEM as a Cloud Service en Unified Shell
description: AEM as a Cloud Service en Unified Shell
exl-id: ea739307-dc99-4621-a239-dbe60ab6b52e
source-git-commit: aeb8244b4da17a0675b86a69727807abf45ca84a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 68%

---

# AEM as a Cloud Service en Unified Shell {#aem-as-a-cloud-service-on-unified-shell}

## Información general {#overview}

AEM as a Cloud Service (servicio de autor) está integrado con Unified Shell para mejorar la experiencia del usuario y unificarla con todas las demás aplicaciones de Experience Cloud. El impacto de esta integración se puede ver en el encabezado superior de la aplicación, como se muestra a continuación.

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
>El shell unificado solo se puede deshabilitar mediante una cuenta con privilegios administrativos.

1. Vaya a **Herramientas → Cloud Services**.

   Un usuario administrador verá la tarjeta de configuración de Unified Shell como se muestra a continuación:

   ![imagen](/help/overview/assets/unifiedshell2.png)

1. Haga clic en **Configuración de Unified Shell**. A continuación, anule la selección de la casilla de verificación que aparece a continuación para deshabilitar Unified Shell:

   ![imagen](/help/overview/assets/unifiedshell3.png)

## Cambio a tema oscuro {#changing-to-dark-theme}

Para cambiar al tema oscuro, haga clic en su icono de perfil. Se mostrará una ventana emergente como se muestra a continuación. Puede utilizar el conmutador para cambiar a un tema oscuro para el Unified Shell.

>[!INFO]
>
>El tema oscuro se aplica solo a Unified Shell (la barra superior).

![imagen](/help/overview/assets/unifiedshell4.png)

## Identificación del entorno as a Cloud Service AEM {#identify-aemaacs-environment}

AEM as a Cloud Service proporciona tres tipos de entornos: Producción, fase y desarrollo. Consulte [Tipos de entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en) para obtener más información. Con esta integración con Unified Shell, el tipo de entorno en el que el usuario ha iniciado sesión en el servicio Autor se muestra en el encabezado superior mediante una etiqueta como se muestra a continuación.

![imagen](/help/overview/assets/unifiedshell_header_label.png)

## Acceso a la bandeja de entrada AEM {#accessing-the-aem-inbox}

Se puede acceder a la Bandeja de entrada AEM haciendo clic en el icono de campana del shell unificado.

>[!INFO]
>
> El número indicado en el icono de campana incluye notificaciones sin leer en todas las soluciones de esa organización de IMS y tareas enumeradas en la bandeja de entrada de AEM.

![imagen](/help/overview/assets/unifiedshell5.png)

Haga clic en el botón Bandeja de entrada en la ventana emergente para ir a la Bandeja de entrada AEM:

![imagen](/help/overview/assets/unifiedshell6.png)
