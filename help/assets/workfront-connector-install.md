---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: d75d9ac16f64b6770fcf35d58474c47c52b1585b
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] como [!DNL Cloud Service] instala el conector mejorado. Antes de realizar la instalación, revise el soporte de plataforma y otros [requisitos previos para el conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>El Adobe requiere la implementación y la configuración del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hace que este conector sea redundante; si esto ocurre, es posible que se requiera a los clientes que pasen del uso de este conector.

Antes de instalar el conector, siga estos pasos previos a la instalación:

1. [Configuración del cortafuegos](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Para conocer el clúster IP en [!DNL Workfront], vaya a [!UICONTROL Configuración] > [!UICONTROL Sistema] > [!UICONTROL Información del cliente].

1. En Dispatcher, permita encabezados HTTP con el nombre `authorization`, `username`y `apikey`. Permitir `GET`, `POST`y `PUT` solicitudes a `/bin/workfront-tools`.

1. Asegúrese de que las rutas siguientes no existan en [!DNL Experience Manager] repositorio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Esta instalación requiere conocimientos para configurar un proyecto Maven en [!DNL Experience Manager] como [!DNL Cloud Service]. Utilice los siguientes recursos para comprender cómo incluir un paquete de terceros en su proyecto de Maven:

   * [Incluir paquete de terceros en el proyecto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implementar con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Para instalar el complemento en [!DNL Experience Manager] como [!DNL Cloud Service], siga estos pasos:

1. Agregar `pom.xml` dependencias:

   1. Añadir una dependencia en parent `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. Añadir una dependencia en todos los módulos [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. Agregar `pom.xml` autenticación.

   1. Incluya la siguiente configuración del repositorio en pom.xml dentro del perfil adobe-public, de modo que las dependencias del conector (arriba) se puedan resolver en el momento de la compilación (tanto localmente como mediante Cloud Manager). Las credenciales para el acceso al repositorio se proporcionarán al adquirir una licencia. Las credenciales deberán agregarse al archivo settings.xml en la sección de servidores.

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. Crear un archivo con el nombre `./cloudmanager/maven/settings.xml` en la raíz del proyecto. Para admitir un repositorio Maven protegido por contraseña, consulte [configuración del proyecto](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). Además, un ejemplo `settings.xml` para referencia. Por último, actualice la `settings.xml` para compilar localmente.

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. Para crear una configuración de usuario del sistema, cree `wf-workfront-users` en [!DNL Experience Manager] Grupo de usuarios y asignar el permiso `jcr:all` a `/content/dam`. Un usuario del sistema `workfront-tools` se crea automáticamente y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] que utilizan el conector mejorado se añaden automáticamente como parte de este grupo.

## Configurar la conexión entre [!DNL Experience Manager] como [!DNL Cloud Service] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con [!DNL Workfront], siga estos pasos:

1. En [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Select `workfront-tools` en el panel izquierdo y seleccione **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el **[!UICONTROL Conexión de Workfront]** , proporcione los detalles requeridos del [!DNL Workfront] implementación y seleccione **[!UICONTROL Conectarse a Workfront]** . Una vez que se haya conectado correctamente, la variable [!DNL Workfront] la integración personalizada de documento se crea automáticamente en la variable [!DNL Workfront] entorno.

   ![Connect [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Vaya a la **[!UICONTROL Avanzadas]** y seleccione la opción **[!UICONTROL ¿Está as a Cloud Service el servidor AEM]**.
