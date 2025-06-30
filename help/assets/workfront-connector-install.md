---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] instala el conector mejorado. Antes de instalar, revise la compatibilidad con la plataforma y otros [requisitos previos para el conector](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>A partir de junio de 2022, Adobe lanzó una nueva integración nativa para conectar Workfront con Adobe Experience Manager Assets as a Cloud Service. Esta integración se ha convertido en el método requerido para conectar estas dos soluciones. Cualquier nueva implementación futura del conector mejorado (1.9.8 y posterior) para conectar Workfront con AEM Assets as a Cloud Service está bloqueada. Para obtener más información sobre cómo configurar esta integración, consulte [Configuración de la integración de Experience Manager Assets as a Cloud Service](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones mejoradas de instalación del conector](workfront-connector-install.md).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Antes de instalar el conector, siga estos pasos previos a la instalación:

1. Si su programa de AEM as a Cloud Service ha configurado la red avanzada y ha habilitado la lista de IP permitidas, debe agregar las IP de Workfront a esta lista de permitidos para permitir que las suscripciones a eventos y varias llamadas a la API pasen a AEM.

   * [IP de clúster de Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Para conocer el clúster IP de [!DNL Workfront], vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Sistema]** > **[!UICONTROL Información del cliente]**.

   * [IP de API de suscripción a evento de Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)

   >[!IMPORTANT]
   >
   >* Si tiene Red avanzada configurada para su programa y utiliza la lista de IP permitidas, debido a una limitación con la arquitectura del conector mejorado de Workfront, también debe agregar la IP de salida del programa a la lista de permitidos en Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Para encontrar la IP del programa, abra una ventana de terminal y ejecute un comando, como:
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. Asegúrese de que las siguientes superposiciones no existan en el repositorio [!DNL Experience Manager]. Si tiene superposiciones preexistentes en estas rutas, debe eliminar las superposiciones o combinar el delta de cambios entre las dos:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Esta instalación requiere conocimientos para establecer un proyecto Maven en [!DNL Experience Manager] como [!DNL Cloud Service]. Utilice los siguientes recursos para comprender cómo incluir un paquete de terceros en su proyecto Maven:

   * [Incluya paquete de terceros en su proyecto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implementar con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Para instalar el complemento en [!DNL Experience Manager] como [!DNL Cloud Service], siga estos pasos:

1. Descargue el conector mejorado de [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Acceda](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) y clone su repositorio de AEM as a Cloud Service desde Cloud Manager.

1. Abra el repositorio de AEM as a Cloud Service clonado mediante un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la carpeta `resources` no existe, créela.


1. Agregar dependencias `pom.xml`:

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

   1. Agregar una dependencia en `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Agregar `pom.xml` incrustaciones. Agregue los paquetes de [!DNL Workfront for Experience Manager enhanced connector] a la sección `embeddeds` de `pom.xml` de todo su subproyecto. Lo necesita incrustado en todo el módulo `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   El destino de la sección incrustada se ha establecido en `/apps/<path-to-project-install-folder>/install`. Esta ruta JCR `/apps/<path-to-project-install-folder>` debe incluirse en las reglas de filtrado del archivo `all/src/main/content/META-INF/vault/filter.xml`. Las reglas de filtrado para el repositorio generalmente se derivan del nombre del programa. Utilice el nombre de la carpeta como destino en las reglas existentes.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización para [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para crear una configuración de usuario del sistema, cree `wf-workfront-users` en el grupo de usuarios [!DNL Experience Manager] y asigne el permiso `jcr:all` a `/content/dam`. Se crea automáticamente un usuario del sistema `workfront-tools` y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] que utilizan el conector mejorado se agregan automáticamente como parte de este grupo.

Para obtener información sobre cómo actualizar [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la versión más reciente, haga clic [aquí](update-workfront-enhanced-connector.md).

## Configure la conexión entre [!DNL Experience Manager] como [!DNL Cloud Service] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con [!DNL Workfront], siga estos pasos:

1. En [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Seleccione `workfront-tools` en el panel izquierdo y seleccione la opción **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el cuadro de diálogo **[!UICONTROL Conexión de Workfront]**, proporcione los detalles necesarios de su implementación de [!DNL Workfront] y seleccione la opción **[!UICONTROL Conectarse a Workfront]**. Una vez que se haya conectado correctamente, la integración personalizada del documento [!DNL Workfront] se creará automáticamente en el entorno [!DNL Workfront].

   ![Conectar [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Vaya a la ficha **[!UICONTROL Avanzado]** y seleccione la opción **[!UICONTROL Es el servidor AEM as a Cloud Service]**.
