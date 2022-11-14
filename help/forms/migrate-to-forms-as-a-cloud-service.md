---
title: Migrar desde AEM 6.5 Forms y AEM 6.4 Forms a un entorno de  [!DNL AEM Forms]  as a Cloud Service
description: Migrar desde un entorno local de  [!DNL AEM Forms]  a un entorno de  [!DNL AEM Forms]  as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 8e28cff5b964005278858b6c8dd8a0f5f8156eaa
workflow-type: ht
source-wordcount: '1218'
ht-degree: 100%

---

# Migrar a [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Puede migrar su formulario adaptable, temáticas, plantillas y configuraciones de nube desde <!-- AEM 6.3 Forms--> AEM 6.4 Forms en OSGi y AEM 6.5 Forms en OSGi a [!DNL AEM] as a Cloud Service. Antes de migrar estos recursos, utilice la utilidad de migración para convertir el formato utilizado en las versiones anteriores al formato utilizado en [!DNL AEM] as a Cloud Service. Al ejecutar la utilidad de migración, se actualizan los siguientes recursos:

* Componentes personalizados para formularios adaptables
* Plantillas y temáticas de formularios adaptables
* Configuraciones de nube
* Los scripts del editor de código se convierten en funciones reutilizables y se aplican a reglas visuales.

## Consideraciones {#consideration}

* El servicio ayuda a migrar contenido solo de [!DNL AEM Forms] a entornos OSGi. No es compatible migrar contenido desde [!DNL AEM Forms] en JEE a un entorno de Cloud Service.

* (Solo para AEM 6.3 Forms o un entorno de versión anterior actualizado a AEM 6.4 Forms o AEM 6.5 Forms) Los formularios adaptables basados en plantillas y temáticas predeterminadas disponibles en AEM 6.3 Forms o en versiones anteriores no son compatibles con [!DNL AEM Forms] as a Cloud Service.

## Requisitos previos {#prerequisites}

* [Habilite la opción Formularios: inscripción digital](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=es#editing-program) para su programa de Forms Cloud Service y [ejecute la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es).

   ![Resultado del simulacro](assets/enable-add-on.png)

* En un entorno de Cloud Service, la utilidad de migración funciona junto con la herramienta de asignación de usuarios y la herramienta de transferencia de contenido. La utilidad de migración hace que los recursos de [!DNL AEM Forms] sean compatibles con Cloud Service y la herramienta de transferencia de contenido migra el contenido de su entorno de [!DNL AEM Forms] a un entorno de [!DNL AEM] as a Cloud Service. Antes de usar la utilidad de migración, conozca el proceso de [mover a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=es). El proceso posee dos herramientas:
   * [Herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=es#cloud-migration): La herramienta de asignación de usuarios le ayuda a asignar sus usuarios con las cuentas de usuario de Adobe IMS correspondientes.
   * [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration): La herramienta de transferencia de contenido le ayuda a preparar y transferir contenido de un entorno existente a un entorno de Cloud Service.
* Cuentas con privilegios de administrador en [!DNL AEM Forms] as a Cloud Service y su entorno local de [!DNL AEM Forms].
* Descargue e instale el Analizador de prácticas recomendadas, la herramienta de transferencia de contenido y la utilidad de migración de [!DNL AEM Forms] del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html)

* Ejecute el [Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es#cloud-migration) y corrija el problema del que se ha informado.

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## Migrar recursos de [!DNL AEM Forms]  {#use-the-migration-utility}

Realice los siguientes pasos para lograr que sus recursos de [!DNL AEM Forms] sean compatibles con Cloud Service y transferirlos a un entorno de [!DNL AEM] as a Cloud Service.

1. Cree un [clon](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/td-p/363487?profile.language=es) de su entorno de [!DNL AEM Forms].

   Utilice siempre el entorno clonado para ejecutar la herramienta de transferencia de contenido y la utilidad de migración. La herramienta de transferencia de contenido y la utilidad de migración realizan algunos cambios en el contenido y los recursos. Por lo tanto, no ejecute la herramienta de transferencia de contenido ni la utilidad de migración en un entorno de producción.

1. Inicie sesión en su entorno clonado con privilegios administrativos.

1. Ejecute la [herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=es#cloud-migration) para asignar los usuarios con las cuentas de usuario de Adobe IMS correspondientes. Necesita que las cuentas de usuario de Adobe IMS inicien sesión en una instancia de [!DNL AEM Forms] as a Cloud Service.

1. Descargue e instale la [herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration) y la utilidad de migración de [!DNL AEM Forms] as a Cloud Service desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) en el entorno clonado. Puede utilizar el administrador de paquetes de AEM para instalar la herramienta y la utilidad.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Migración de contenido]**.

1. Abra la tarjeta **[!UICONTROL Preparar formularios para la migración]**. El explorador muestra cinco opciones:
   * **[!UICONTROL Migración de recursos de AEM Forms]**
   * **[!UICONTROL Migración de componentes personalizados de formularios adaptables]**
   * **[!UICONTROL Migración de plantillas de formularios adaptables]**
   * **[!UICONTROL Migración de configuraciones en la nube de AEM Forms]**
   * **[!UICONTROL Migración de scripts del editor de código]**

1. Utilice la opción una tras otra para lograr que sus recursos de [!DNL AEM Forms] sean compatibles con [!DNL AEM] as a Cloud Service:

   1. Pulse **[!UICONTROL Migración de recursos de AEM Forms]** y, en la siguiente pantalla, pulse **[!UICONTROL Iniciar migración]**. Hace que sus formularios adaptables y temáticas en su entorno de [!DNL AEM Forms] sean compatibles con [!DNL AEM] as a Cloud Service.

   1. Pulse **[!UICONTROL Migración de componentes personalizados de formularios adaptables]** y, en la página Migración de componentes personalizados, pulse **[!UICONTROL Iniciar migración]**. Hace que cualquier componente personalizado desarrollado para formularios adaptables y superposiciones de componentes en su entorno de [!DNL AEM Forms] sea compatible con [!DNL AEM] as a Cloud Service.

   1. Pulse **[!UICONTROL Migración de plantillas de formularios adaptables]** y, en la página Migración de componentes personalizados, pulse **[!UICONTROL Iniciar migración]**. Hace que las plantillas de formulario adaptable en /apps o /conf y las que se crean con el editor de plantillas de AEM sean compatibles con [!DNL AEM] as a Cloud Service.

   1. Pulse **[!UICONTROL Migración de configuraciones en la nube de AEM Forms]** y, a continuación, en la página Migración de configuración, pulse **[!UICONTROL Iniciar migración]**. Actualiza y mueve los siguientes servicios en la nube a una nueva ubicación:

      * Servicio en la nube de modelo de datos de formulario
      * Servicio en la nube de Google reCAPTCHA
      * Servicio de nube de [!DNL Adobe Sign]
      * Servicio en la nube de Adobe Fonts
   1. Pulse **[!UICONTROL Migración de scripts del editor de código]**, especifique una ubicación para guardar funciones reutilizables y pulse **[!UICONTROL Iniciar migración].

   Cloud Service no es compatible con scripts del editor de reglas. La herramienta **[!UICONTROL Migración de scripts del editor de código]** convierte todos los scripts de regla en su entorno en funciones reutilizables y aplica las funciones reutilizables al editor visual en la ubicación apropiada. Estas funciones reutilizables se guardan en forma de bibliotecas de cliente y le ayudan a mantener intacta la funcionalidad existente. La herramienta aplica automáticamente las funciones reutilizables generadas a los formularios adaptables correspondientes.

   Utilice el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es#contentmanagement) para exportar las funciones reutilizables (bibliotecas de cliente) a un paquete.

1. [Implemente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es#deploying-content-packages-via-cloud-manager-and-package-manager) el paquete de funciones reutilizables (bibliotecas de cliente), [código personalizado, componentes y configuraciones](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=es#cloud-manager), bibliotecas específicas locales personalizadas para su entorno de [!DNL AEM] as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Ejecute la [herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration). Al especificar los parámetros en la pantalla **[!UICONTROL Crear conjunto de migración]**, especifique la ruta de los formularios adaptables, temáticas, plantillas, modelos de datos de formulario, servicios en la nube, componentes personalizados y otros recursos específicos de AEM Forms a la opción **[!UICONTROL Rutas que se deben incluir]**. Añade los recursos especificados de [!DNL AEM Forms] al conjunto de migración.

## Rutas de varios recursos específicos de AEM Forms

* **Formularios adaptables**: Puede encontrar formularios adaptables en `/content/dam/formsanddocuments/` y en /content/forms/af. Por ejemplo, para un formulario adaptable titulado “WKND Registration”, añada las rutas `/content/dam/formsanddocuments/wknd-registration` y `/content/forms/af/wknd-registration`.
* **Modelo de datos de formulario**: Puede encontrar todos los modelos de datos de formulario en `/content/dam/formsanddocuments-fdm`. Por ejemplo, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Bibliotecas de cliente**: La ruta predeterminada de las bibliotecas de cliente es `/etc/clientlibs/fd/theme`.

* **Plantillas de formulario adaptable**: La ruta predeterminada de las plantillas es `/conf/<template folder>`. Por ejemplo, para una plantilla titulada “basic”, añada la ruta `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temáticas de formularios adaptables y bibliotecas de cliente**: La ruta predeterminada de las temáticas es ` /content/dam/formsanddocuments-themes/` y la ruta predeterminada de las bibliotecas de cliente es `/etc/clientlibs/fd/theme`. Por ejemplo, para una plantilla titulada “WKND Theme”, añada la ruta ` /content/dam/formsanddocuments-themes/wkndtheme` y las bibliotecas de cliente para la temática en `/etc/clientlibs/reference-themes/wkndtheme-3-0`. También puede tener temáticas y bibliotecas de cliente en otras rutas personalizadas.

* **Configuraciones de nube**: Puede encontrar configuraciones de nube en `/conf/`. Por ejemplo, la configuración de nube del modelo de datos de formulario se encuentra en `/conf/global/settings/cloudconfigs/fdm`.

* **Modelo de flujo de trabajo**: Puede encontrar modelos de flujo de trabajo de AEM en `/conf/global/settings/workflow/models/`. Por ejemplo, para un modelo de flujo de trabajo llamado “WKND Registration”, añada la ruta `/conf/global/settings/workflow/models/wknd-registration`

Puede agregar las rutas de carpeta de nivel superior que se enumeran a continuación o las rutas de carpeta específicas, tal como se describe a continuación. Le permite migrar ciertos recursos y todos los recursos y formularios a la vez.

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

Para migrar modelos de flujo de trabajo de AEM, especifique las siguientes rutas:

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
