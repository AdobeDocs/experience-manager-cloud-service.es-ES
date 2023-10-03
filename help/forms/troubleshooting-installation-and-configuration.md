---
title: Resolución de problemas de instalación y configuración
description: Resolución de problemas de instalación y configuración del entorno as a Cloud Service de AEM Forms.
contentOwner: khsingh
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 95%

---

# Configuración {#installation-and-configuration}

Puede encontrar algunos de los siguientes problemas al configurar un entorno de Cloud Service:

## La opción Forms no está disponible

La opción **[!UICONTROL Forms]** no está disponible en la página **[!UICONTROL Navegación]**.

![La opción Forms no está disponible](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

Para habilitar la opción **[!UICONTROL Forms]**:

1. Inicie sesión en [Cloud Manager](https://experience.adobe.com/).
1. Busque el programa y haga clic en el icono ![La opción Forms no está disponible](assets/Smock_Edit_18_N.svg). Se abre la página Editar programa del programa.
1. Abra la pestaña **[!UICONTROL Soluciones y complementos]**.
1. Seleccione la opción **[!UICONTROL Forms]** y haga clic en **[!UICONTROL Guardar]**.

   ![Selección de la opción Forms](assets/installation-configuration-select-forms-option.png)
1. [Cree](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=es#how-to-use) y [ejecute](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es) canalizaciones de producción y de no producción.

Una vez construida e implementada la canalización, la opción **[!UICONTROL Forms]** en la página **[!UICONTROL Navegación]**.

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## Se produce un error en la canalización de compilación {#build-pipeline-fails}

Los usuarios no pueden ejecutar la canalización de compilación. Se produce un error en la canalización después de ejecutarse durante algún tiempo.

Para resolver el problema, abra Cloud Manager, seleccione la opción **[!UICONTROL Actualizar]** correspondiente a su entorno y ejecute la canalización.
