---
title: ¿Cómo se concede acceso al Editor de reglas para seleccionar grupos de usuarios?
description: Existen diferentes tipos de usuarios con diversas habilidades que trabajan con Adaptive Forms. Obtenga información sobre cómo limitar el acceso al editor de reglas a los usuarios en función de su función o función.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---


# Conceder acceso al editor de reglas a determinados grupos de usuarios {#grant-rule-editor-access-to-select-user-groups}

## Información general {#overview}

Existen diferentes tipos de usuarios con diversas habilidades que trabajan con Adaptive Forms. Aunque los usuarios expertos pueden tener los conocimientos adecuados para trabajar con secuencias de comandos y reglas complejas, puede haber usuarios de nivel básico que solo deben trabajar con el diseño y las propiedades básicas de Forms adaptable.

[!DNL Experience Manager Forms] le permite limitar el acceso al editor de reglas a los usuarios en función de su función o función. En los ajustes del servicio de configuración de Forms adaptable, puede especificar la variable [grupos de usuarios](forms-groups-privileges-tasks.md) que pueden ver y acceder al editor de reglas.

## Especificar grupos de usuarios que pueden acceder al editor de reglas {#specify-user-groups-that-can-access-rule-editor}

1. Iniciar sesión en [!DNL Experience Manager Forms] como administrador.
1. En la instancia de autor, haga clic en ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Herramientas ![martillo](assets/hammer-icon.svg) > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. La consola web se abre en una nueva ventana.

   ![1-2](assets/1-2.png)

1. En [!UICONTROL Consola web] Ventana, localizar y hacer clic **[!UICONTROL Servicio de configuración de formularios adaptables]**. **[!UICONTROL Servicio de configuración de formularios adaptables]** se abre. No cambie ningún valor y haga clic en **[!UICONTROL Guardar]**.

   Crea un archivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` en el repositorio CRX.

1. Inicie sesión en CRXDE como administrador. Abrir archivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` para editar.
1. Utilice la siguiente propiedad para especificar el nombre de un grupo que puede acceder al editor de reglas (por ejemplo, RuleEditorsUserGroup) y haga clic en **[!UICONTROL Guardar todo]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar el acceso para varios grupos, especifique una lista de valores separados por comas:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crear usuario](assets/create_user_new.png)

   Ahora, cuando un usuario no forma parte del grupo de usuarios especificado (aquí    `RuleEditorsUserGroup`) toca un campo, el icono Editar regla ( ![edit-rules1](assets/edit-rules1.png)) no está disponible en la barra de herramientas Componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de herramientas de componentes visible para un usuario con acceso al editor de reglas:

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de herramientas de componentes visible para el usuario sin acceso al editor de reglas

   Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y seguridad](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

