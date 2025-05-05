---
title: ¿Cómo se puede migrar de AEM 6.5 Forms a AEM Forms as a Cloud Service?
description: Introducción al Recorrido de migración a AEM as a Cloud Service | Adobe Experience Manager. Migración desde un  [!DNL AEM Forms] (entornos On-Premise y AMS) a un entorno de  [!DNL AEM Forms] as a Cloud Service.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1380'
ht-degree: 100%

---

# Migración desde un [!DNL AEM Forms] (entornos On-Premise y AMS) a [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Puede migrar o actualizar sus formularios adaptables, temáticas, plantillas y configuraciones de nube desde <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms en OSGi hasta [!DNL AEM] as a Cloud Service. Antes de migrar estos recursos, emplee la utilidad de migración para convertir el formato utilizado en las versiones anteriores al formato utilizado en [!DNL AEM] as a Cloud Service.
Empecemos con el recorrido de migración a AEM as a Cloud Service | Adobe Experience Manager. Al ejecutar la utilidad de migración, se actualizan los siguientes recursos:

* Componentes personalizados para formularios adaptables
* Plantillas y temáticas de formularios adaptables
* Configuraciones de nube
* Los scripts del editor de código se convierten en funciones reutilizables y se aplican a reglas visuales.

## Consideraciones para migrar a Forms as a Cloud Service {#consideration}

Para migrar de AEM 6.5 Forms a AEM Cloud Service, es importante tener en cuenta los siguientes puntos:

* El servicio ayuda a migrar contenido solo de [!DNL AEM Forms] a entornos OSGi. No es compatible migrar contenido desde [!DNL AEM Forms] en JEE a un entorno de Cloud Service.

* (Solo para versiones anteriores a AEM 6.5 Forms) Los formularios adaptables basados en plantillas y temáticas predeterminadas disponibles en AEM 6.3 Forms o en versiones anteriores no son compatibles con [!DNL AEM Forms] as a Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service incluye algunos cambios importantes en las funciones existentes en comparación con los entornos de Adobe Experience Manager 6.5 Forms (On-Premise y Adobe Managed Services). Antes de continuar con la migración al servicio, [obtenga información acerca de estos cambios importantes](notable-changes.md) y las [diferencias de nivel de funcionalidad](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=es#viewing-report) para decidir migrar según las funciones que requiera su organización.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=es#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Requisitos previos {#prerequisites}

Para garantizar una transición sin problemas de AEM Forms 6.5 a un entorno de AEM as a Cloud Service, es importante tener en cuenta los siguientes requisitos previos:

* Habilite la opción [Formularios: inscripción digital](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=es#editing-program) para su programa de Forms Cloud Service y [ejecute la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=es).

  ![Resultado del ensayo](assets/enable-add-on.png)

* En un entorno de Cloud Service, la utilidad de migración funciona junto con la herramienta de transferencia de contenido. La utilidad de migración hace que los recursos de [!DNL AEM Forms] sean compatibles con Cloud Service y la herramienta de transferencia de contenido migra el contenido de su entorno de [!DNL AEM Forms] a un entorno de [!DNL AEM] as a Cloud Service. Antes de usar la utilidad de migración, conozca el proceso de [mover a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=es). El proceso utiliza la siguiente herramienta:
   * [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration): la herramienta de transferencia de contenido le ayuda a preparar y transferir contenido de un entorno existente a un entorno de Cloud Service. Ayuda a los usuarios a realizar actualizaciones fácilmente de AEM Forms al entorno de la nube.
* Las cuentas con privilegios de administrador en [!DNL AEM Forms] as a Cloud Service y su entorno local de [!DNL AEM Forms].
* Descargue e instale el Analizador de prácticas recomendadas, la herramienta de transferencia de contenido y la utilidad de migración de [!DNL AEM Forms] del [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html).

* Ejecute el [Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es#cloud-migration) y corrija el problema del que se ha informado. Para ver los posibles problemas relacionados con la migración de Adobe Experience Manager Forms a Adobe Experience Manager Forms as a Cloud Service, consulte [Detección de patrones de AEM para Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=es#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migración de recursos de [!DNL AEM 6.5 Forms] a AEM Cloud Service {#use-the-migration-utility}

Realice los siguientes pasos para lograr que sus recursos de [!DNL AEM Forms] sean compatibles con Cloud Service y transferirlos a un entorno de [!DNL AEM] as a Cloud Service.

1. Cree un [clon](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/td-p/363487?profile.language=es) de su entorno de [!DNL AEM Forms].

   >[!NOTE]
   >
   > Cuando migre de 6.5 a Cloud Service, es recomendable utilizar el entorno clonado para ejecutar la herramienta de transferencia de contenido y la utilidad de migración. La herramienta de transferencia de contenido y la utilidad de migración realizan algunos cambios en el contenido y los recursos. Por lo tanto, no ejecute la herramienta de transferencia de contenido ni la utilidad de migración en un entorno de producción.

1. Inicie sesión en su entorno clonado con privilegios administrativos.

1. Descargue e instale la [herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration) y la utilidad de migración de [!DNL AEM Forms] as a Cloud Service desde el [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) en el entorno clonado. Puede utilizar el administrador de paquetes de AEM para instalar la herramienta y la utilidad.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Migración de contenido]**.

1. Abra la tarjeta **[!UICONTROL Preparar formularios para la migración]**. El explorador muestra cinco opciones:
   * **[!UICONTROL Migración de recursos de AEM Forms]**
   * **[!UICONTROL Migración de componentes personalizados de formularios adaptables]**
   * **[!UICONTROL Migración de plantillas de formularios adaptables]**
   * **[!UICONTROL Migración de configuraciones en la nube de AEM Forms]**
   * **[!UICONTROL Migración de scripts del editor de código]**

1. Utilice la opción una tras otra para lograr que sus recursos de [!DNL AEM Forms] sean compatibles con [!DNL AEM] as a Cloud Service:

   1. Seleccione **[!UICONTROL Migración de recursos de AEM Forms]** y, en la siguiente pantalla, seleccione **[!UICONTROL Iniciar migración]**. Hace que sus formularios adaptables y temáticas en su entorno de [!DNL AEM Forms] sean compatibles con [!DNL AEM] as a Cloud Service.

   1. Seleccione **[!UICONTROL Migración de componentes personalizados de formularios adaptables]** y, en la página Migración de componentes personalizados, seleccione **[!UICONTROL Iniciar migración]**. Hace que cualquier componente personalizado desarrollado para formularios adaptables y superposiciones de componentes en su entorno de [!DNL AEM Forms] sea compatible con [!DNL AEM] as a Cloud Service.

   1. Seleccione **[!UICONTROL Migración de plantillas de formularios adaptables]** y, en la página Migración de componentes personalizados, seleccione **[!UICONTROL Iniciar migración]**. Hace que las plantillas de formularios adaptables en `/apps` o `/conf` y las que se crean con el editor de plantillas de AEM sean compatibles con [!DNL AEM] as a Cloud Service.

   1. Seleccione **[!UICONTROL Migración de configuraciones en la nube de AEM Forms]** y, a continuación, en la página Migración de configuración, seleccione **[!UICONTROL Iniciar migración]**. Actualiza y mueve los siguientes servicios en la nube a una nueva ubicación:

      * Servicio en la nube de modelo de datos de formulario
      * Servicio en la nube de Google reCAPTCHA
      * Servicio de nube de [!DNL Adobe Sign]
      * Servicio en la nube de Adobe Fonts

   1. Seleccione **[!UICONTROL Migración de scripts del editor de código]**, especifique una ubicación para guardar funciones reutilizables y seleccione **[!UICONTROL Iniciar migración].

   Cloud Service no es compatible con scripts del editor de reglas. La herramienta **[!UICONTROL Migración de scripts del editor de código]** convierte todos los scripts de regla en su entorno en funciones reutilizables y aplica las funciones reutilizables al editor visual en la ubicación apropiada. Estas funciones reutilizables se guardan en forma de bibliotecas de cliente y le ayudan a mantener intacta la funcionalidad existente. La herramienta aplica automáticamente las funciones reutilizables generadas a los formularios adaptables correspondientes.

   La migración de AEM Forms a Cloud Service, utilice el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es#contentmanagement) para exportar las funciones reutilizables (bibliotecas de cliente) a un paquete.

1. [Implemente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es#deploying-content-packages-via-cloud-manager-and-package-manager) el paquete de funciones reutilizables (bibliotecas de cliente), [código personalizado, componentes y configuraciones](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=es#cloud-manager), bibliotecas específicas locales personalizadas para su entorno de [!DNL AEM] as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es&#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Ejecute la [herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=es#cloud-migration). Cuando especifique los parámetros en la pantalla **[!UICONTROL Crear conjunto de migración]**, indique la ruta de los formularios adaptables, temáticas, plantillas, modelo de datos de formulario, servicios en la nube, componentes personalizados y otros recursos específicos de AEM Forms correspondientes a la opción **[!UICONTROL Rutas a incluir]**. Añade los recursos especificados de [!DNL AEM Forms] al conjunto de migración.

## Rutas de varios recursos específicos de AEM Forms

Cuando migre de AEM Forms 6.5 al servicio en la nube, puede localizar los recursos específicos de AEM Forms en los siguientes lugares:

* **Formularios adaptables**: puede encontrar formularios adaptables en `/content/dam/formsanddocuments/` y en `/content/forms/af`. Por ejemplo, para un formulario adaptable titulado “WKND Registration”, añada las rutas `/content/dam/formsanddocuments/wknd-registration` y `/content/forms/af/wknd-registration`.
* **Modelo de datos de formulario**: puede encontrar todo el modelo de datos de formulario (FDM) en `/content/dam/formsanddocuments-fdm`. Por ejemplo, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Bibliotecas de cliente**: La ruta predeterminada de las bibliotecas de cliente es `/etc/clientlibs/fd/theme`.

* **Plantillas de formulario adaptable**: La ruta predeterminada de las plantillas es `/conf/<template folder>`. Por ejemplo, para una plantilla titulada “basic”, añada la ruta `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temáticas de formularios adaptables y bibliotecas de cliente**: La ruta predeterminada de las temáticas es ` /content/dam/formsanddocuments-themes/` y la ruta predeterminada de las bibliotecas de cliente es `/etc/clientlibs/fd/theme`. Por ejemplo, para una plantilla titulada “WKND Theme”, añada la ruta ` /content/dam/formsanddocuments-themes/wkndtheme` y las bibliotecas de cliente para la temática en `/etc/clientlibs/reference-themes/wkndtheme-3-0`. También puede tener temáticas y bibliotecas de cliente en otras rutas personalizadas.

* **Configuraciones de nube**: Puede encontrar configuraciones de nube en `/conf/`. Por ejemplo, la configuración del modelo de datos de formulario (FDM) se encuentra en `/conf/global/settings/cloudconfigs/fdm`.

* **Modelo de flujo de trabajo**: Puede encontrar modelos de flujo de trabajo de AEM en `/conf/global/settings/workflow/models/`. Por ejemplo, para un modelo de flujo de trabajo llamado “WKND Registration”, añada la ruta `/conf/global/settings/workflow/models/wknd-registration`

Puede agregar las rutas de carpeta de nivel superior que se enumeran a continuación o las rutas de carpeta específicas, tal como se describe a continuación. Esto permite migrar un recurso determinado y todos los recursos y formularios a la vez, al actualizar a Cloud Service desde Forms 6.5.

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

Cuando migre modelos de flujo de trabajo de AEM Forms 6.5 a Cloud Service, especifique las siguientes rutas:

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## Ver siguiente

* [Cambios importantes para los usuarios de Adobe Experience Manager 6.5 Forms existentes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html?lang=es)
* [Introducción a AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/formssetup-configure-migrate/setup-forms-cloud-service.html?lang=es)
* [Creación de su primer formulario adaptable en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=es)

## Información adicional

La utilidad de migración le ayuda a migrar formularios adaptables en función de los componentes de base. Además, Forms as a Cloud Service es compatible con los componentes principales de los formularios adaptables. Por lo tanto, puede hacer lo siguiente:

* [Crear formularios adaptables independientes basados en los componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Creación de un formulario adaptable basado en componentes principales directamente en una página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Para obtener más información sobre AEM Forms as a Cloud Service, consulte lo siguiente:

* [Introducción a AEM Forms Cloud Service](/help/forms/home.md)
* [Innovaciones en AEM Forms Cloud Service](/help/forms/latest-innovations.md)