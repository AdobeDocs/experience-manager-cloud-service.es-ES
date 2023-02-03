---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 68f84de83873029f7cd16cb9ed70f916170cb566
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] instala el conector mejorado. Antes de realizar la instalación, revise el soporte de plataforma y otros [requisitos previos para el conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto ocurre, es posible que se requiera a los clientes que pasen del uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones anteriores y personalizadas. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones de instalación del conector mejorado](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socios para conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información acerca del examen, consulte [Guía de examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Antes de instalar el conector, siga estos pasos previos a la instalación:

1. [Configuración del cortafuegos](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Para conocer el clúster IP en [!DNL Workfront], vaya a [!UICONTROL Configuración] > [!UICONTROL Sistema] > [!UICONTROL Información del cliente].

1. En Dispatcher, permita encabezados HTTP con el nombre `authorization`, `username`y `apikey`. Permitir `GET`, `POST`y `PUT` solicitudes a `/bin/workfront-tools`.

1. Asegúrese de que las rutas siguientes no existan en [!DNL Experience Manager] repositorio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Esta instalación requiere conocimientos para configurar un proyecto Maven en [!DNL Experience Manager] como [!DNL Cloud Service]. Utilice los siguientes recursos para comprender cómo incluir un paquete de terceros en su proyecto de Maven:

   * [Incluir paquete de terceros en el proyecto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implementar con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es).

Para instalar el complemento en [!DNL Experience Manager] como [!DNL Cloud Service], siga estos pasos:

1. Descargue el conector mejorado desde [Distribución del software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) y clone su repositorio as a Cloud Service AEM desde Cloud Manager.

1. Abra el repositorio as a Cloud Service AEM clonado con un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la variable `resources` carpeta no existe, cree la carpeta.


1. Agregar `pom.xml` dependencias:

   1. Añadir una dependencia en parent `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >Asegúrese de actualizar el número de versión del conector mejorado antes de copiar la dependencia al primario `pom.xml`.

   1. Añadir una dependencia en `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Agregar `pom.xml` incrustaciones. Agregue la variable [!DNL Workfront for Experience Manager enhanced connector] paquetes a `embeddeds` de la sección `pom.xml` de todo el subproyecto. Lo necesita incrustado en el módulo todo `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   El objetivo de la sección integrada se establece en `/apps/<path-to-project-install-folder>/install`. Esta ruta JCR `/apps/<path-to-project-install-folder>` debe incluirse en las reglas de filtro del `all/src/main/content/META-INF/vault/filter.xml` archivo. Las reglas de filtro para el repositorio generalmente se derivan del nombre del programa. Utilice el nombre de la carpeta como destino en las reglas existentes.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización a [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para crear una configuración de usuario del sistema, cree `wf-workfront-users` en [!DNL Experience Manager] Grupo de usuarios y asignar el permiso `jcr:all` a `/content/dam`. Un usuario del sistema `workfront-tools` se crea automáticamente y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] que utilizan el conector mejorado se añaden automáticamente como parte de este grupo.

Para obtener información sobre cómo actualizar la variable [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la más reciente, haga clic en [here](update-workfront-enhanced-connector.md).

## Configurar la conexión entre [!DNL Experience Manager] como [!DNL Cloud Service] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con [!DNL Workfront], siga estos pasos:

1. En [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Select `workfront-tools` en el panel izquierdo y seleccione **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el **[!UICONTROL Conexión de Workfront]** , proporcione los detalles requeridos del [!DNL Workfront] implementación y seleccione **[!UICONTROL Conectarse a Workfront]** . Una vez que se haya conectado correctamente, la variable [!DNL Workfront] la integración personalizada de documento se crea automáticamente en la variable [!DNL Workfront] entorno.

   ![Connect [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Vaya a la **[!UICONTROL Avanzadas]** y seleccione la opción **[!UICONTROL ¿Está as a Cloud Service el servidor AEM]**.
