---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 2%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] instala el conector mejorado. Antes de realizar la instalación, revise la compatibilidad con la plataforma y otros [requisitos previos del conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* El Adobe requiere la implementación y la configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con el Adobe.
>
>* El Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones de instalación del conector mejorado](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener más información sobre el examen, consulte [Guía del examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Antes de instalar el conector, siga estos pasos previos a la instalación:

1. [Configuración del cortafuegos](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Para conocer el clúster IP en [!DNL Workfront], vaya a [!UICONTROL Configurar] > [!UICONTROL Sistema] > [!UICONTROL Información del cliente].

1. En el despachante, permita los encabezados HTTP llamados `authorization`, `username`, y `apikey`. Permitir `GET`, `POST`, y `PUT` solicitudes a `/bin/workfront-tools`.

1. Asegúrese de que las siguientes rutas no existan en [!DNL Experience Manager] repositorio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Esta instalación requiere conocimientos para establecer un proyecto Maven en [!DNL Experience Manager] as a [!DNL Cloud Service]. Utilice los siguientes recursos para comprender cómo incluir un paquete de terceros en su proyecto Maven:

   * [Incluir paquetes de terceros en el proyecto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implementación con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es).

Para instalar el complemento en [!DNL Experience Manager] as a [!DNL Cloud Service], siga estos pasos:

1. Descargue el conector mejorado desde [Distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) AEM y clone el repositorio as a Cloud Service de la desde Cloud Manager.

1. AEM Abra el repositorio as a Cloud Service clonado de mediante un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la variable `resources` no existe, cree la carpeta.


1. Añadir `pom.xml` dependencias:

   1. Agregar una dependencia en el elemento principal `pom.xml`.

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
      >Asegúrese de actualizar el número de versión del conector mejorado antes de copiar la dependencia en el elemento principal `pom.xml`.

   1. Adición de una dependencia en `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Añadir `pom.xml` incrusta. Añada el [!DNL Workfront for Experience Manager enhanced connector] paquetes para `embeddeds` de la sección `pom.xml` de todos los subproyectos. Lo necesita incrustado en el módulo de todo `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   El destino de la sección incrustada se establece en `/apps/<path-to-project-install-folder>/install`. Esta ruta JCR `/apps/<path-to-project-install-folder>` debe incluirse en las reglas de filtro de la `all/src/main/content/META-INF/vault/filter.xml` archivo. Las reglas de filtrado para el repositorio generalmente se derivan del nombre del programa. Utilice el nombre de la carpeta como destino en las reglas existentes.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización en [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para crear una configuración de usuario del sistema, cree `wf-workfront-users` in [!DNL Experience Manager] Grupo de usuarios y asignar el permiso `jcr:all` hasta `/content/dam`. Un usuario del sistema `workfront-tools` se crea automáticamente y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] los usuarios que utilizan el conector mejorado se añaden automáticamente como parte de este grupo.

Para obtener información sobre cómo actualizar la [!DNL Workfront for Experience Manager enhanced connector] desde una versión anterior a la versión más reciente, haga clic en [aquí](update-workfront-enhanced-connector.md).

## Configuración de la conexión entre [!DNL Experience Manager] as a [!DNL Cloud Service] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con [!DNL Workfront], siga estos pasos:

1. Entrada [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Seleccionar `workfront-tools` en el panel izquierdo y seleccione **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el **[!UICONTROL Conexión de Workfront]** diálogo, proporcione los detalles necesarios de su [!DNL Workfront] implementación y seleccione **[!UICONTROL Conectar con Workfront]** opción. Una vez que se haya conectado correctamente, la [!DNL Workfront] la integración personalizada de documentos se crea automáticamente en [!DNL Workfront] entorno.

   ![Connect [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Vaya a **[!UICONTROL Avanzadas]** y seleccione la opción **[!UICONTROL AEM ¿Está as a Cloud Service el servidor]**.
