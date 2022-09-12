---
title: Solución de problemas de instalación y configuración
seo-title: Troubleshooting installation and configuration
description: Solución de problemas de instalación y configuración
seo-description: Troubleshooting installation and configuration
contentOwner: khsingh
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configuración {#installation-and-configuration}

Puede encontrar algunos de los siguientes problemas al configurar un entorno de Cloud Service:

## La opción Forms no está disponible

La variable **[!UICONTROL Forms]** no está disponible en la **[!UICONTROL Navegación]** página.

![La opción Forms no está disponible](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

Para habilitar la variable **[!UICONTROL Forms]** opción:

1. Inicie sesión en el [Cloud Manager](https://experience.adobe.com/)
1. Busque el programa y haga clic en el botón ![La opción Forms no está disponible](assets/Smock_Edit_18_N.svg) icono. Se abre la página Editar programa del programa.
1. Abra el **[!UICONTROL Soluciones y complementos]** pestaña .
1. Seleccione el **[!UICONTROL Forms]** y haga clic en **[!UICONTROL Guardar]**.

   ![Seleccione la opción Forms](assets/installation-configuration-select-forms-option.png)
1. [Crear](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) y [run](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) canalizaciones tanto de producción como de no producción.

Una vez construida e implementada la canalización, la variable **[!UICONTROL Forms]** en la **[!UICONTROL Navegación]** página.

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## La canalización de compilación falla {#build-pipeline-fails}

Los usuarios no pueden ejecutar la canalización de compilación. La canalización falla después de ejecutarse durante algún tiempo.

Para resolver el problema, abra Cloud Manager, seleccione la opción **[!UICONTROL Actualizar]** para su entorno y ejecute la canalización.
