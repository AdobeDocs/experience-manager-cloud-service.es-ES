---
title: Integrar ArchiveSign con un formulario adaptable
description: Aprenda a utilizar ArchiveSign con un formulario adaptable para recopilar firmas electrónicas.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Uso de ArchiveSign con un formulario adaptable {#integrate-aem-forms-with-DocuSign}

ArchiveSign es una solución destacada de firma electrónica. Puede utilizarlo para firmar un acuerdo por correo electrónico. Puede integrar ArchiveSign con un formulario adaptable. Le ayuda a enviar un formulario adaptable para firmas electrónicas a varios destinatarios. El uso de firmas electrónicas le ayuda a:

- Cierre las ofertas de cualquier dispositivo con procesos de propuesta, presupuesto y contrato totalmente automatizados.
- Finalice los procesos de Recursos Humanos más rápido y ofrezca a sus empleados las experiencias digitales.
- Reduzca los tiempos de ciclo de contrato e incorpore a sus proveedores más rápido.

AEM Forms as a Cloud Service proporciona un [acción de envío personalizada para Sign](#deploy-custom-submit-action). La acción de envío le ayuda a enviar los formularios adaptables para las firmas electrónicas mediante las API de Sign.

| También puede utilizar la solución de firma electrónica de Adobe, Adobe Sign, para firmar por correo electrónico un formulario adaptable. AEM Forms tiene una integración mucho más profunda con Adobe Sign y proporciona controles mucho más precisos, como firma secuencial y paralela, varios métodos de autenticación, experiencia de firma en formularios y mucho más. Para obtener más información, consulte [Uso de Adobe Sign en un formulario adaptable](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Requisitos previos {#prerequisites}

Se requieren las siguientes opciones para integrar ArchiveSign con AEM Forms:

- Un.000.000.000 [cuenta de desarrollador](https://developers.docusign.com/platform/account/)
- Una aplicación DATSign
- Credenciales (ID de cliente y Secreto de cliente) de la aplicación de API ArchiveSign.
- [Acción de envío personalizado y servicio en la nube para Sign](https://github.com/adobe/aem-forms-docusign-sample)
- (solo para el entorno de desarrollo local) [Configurar documento de registro](setup-local-development-environment.md#docker-microservices).

## Configurar la acción de envío personalizada y el servicio en la nube para Sign00 {#deploy-custom-submit-action}

AEM Forms as a Cloud Service proporciona una acción de envío personalizada para Sign. La acción de envío le ayuda a enviar los formularios adaptables para las firmas electrónicas mediante las API de Sign. El código para la acción de envío personalizado está disponible en [AEM Forms muestra un repositorio de Git público](https://github.com/adobe/aem-forms-docusign-sample). Puede implementar el código tal como está en su entorno de AEM Forms o personalizarlo según los requisitos de su organización.

Realice los siguientes pasos para configurar la acción de envío personalizado y el Cloud Service de DAT predeterminados:

1. [Clonar el proyecto as a Cloud Service de AEM Forms](setup-local-development-environment.md#forms-cloud-service-local-development-environment) o crear un [!DNL Experience Manager Forms] como [!DNL Cloud Service] proyecto basado en [AEM Tipo de archivo 27](https://github.com/adobe/aem-project-archetype) o posterior. Para crear un [!DNL Experience Manager Forms] como [!DNL Cloud Service] proyecto basado en AEM tipo de archivo:
   </br> Abra el símbolo del sistema y ejecute el siguiente comando para crear un [!DNL Experience Manager Forms] Proyecto as a Cloud Service:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Además, cambie `appTitle`, `appId`y `groupId`, en el comando anterior para reflejar su entorno.

1. Clonar el [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) repositorio. Este repositorio contiene una acción de envío personalizada para los detalles de ArchivoSign y configuración para conectarse con el servidor de ArchivoSign.

1. Abra el proyecto as a Cloud Service de AEM Forms creado en el paso 1 para editarlo en IDE de su elección.

1. Abra el `[AEM Forms as a Cloud Service project]\pom.xml` para editarlo y realice los cambios siguientes:

   1. Agregue el siguiente texto al final del `<properties>` etiqueta:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Agregue el siguiente texto al final del `<repositories>` etiqueta:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Si no hay `<repositories>` , cree la etiqueta debajo de la etiqueta `<properties>` etiqueta.

   1. Agregue el siguiente texto al final del `<dependencyManagement>` etiqueta:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Siga estos pasos en la sección `all/pom.xml` archivo disponible en la carpeta del proyecto de Cloud Service:

   1. Agregue el siguiente texto al final del `<embeddeds>` etiqueta:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Agregue el siguiente texto al final del `<dependencies>` etiqueta:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Abra el símbolo del sistema y vaya a `aem-forms-samples\forms-integration-docusign` (clonado en el paso 3) y ejecute el siguiente comando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` hace referencia al nombre de la carpeta creada en el paso 1 de este procedimiento.

1. Implemente el proyecto en el entorno de desarrollo local. Puede utilizar el siguiente comando para implementar en el entorno de desarrollo local

   `mvn -PautoInstallPackage clean install`

   Después de ejecutar estos pasos, puede ver una nueva acción de envío personalizada [Enviar con firmas electrónicas de ArchiveSign](#enabledocusign) disponible en la lista de opciones de envío para un formulario adaptable y un [Configuración del servicio en la nube ArchiveSign](#configure-docusign-with-aem-forms) en su entorno de desarrollo local.

1. Compilar y [Implemente el código en su [!DNL AEM Forms] Entorno as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrar [!DNL DocuSign] con [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para integrar [!DNL DocuSign] con [!DNL AEM Forms] en las instancias de Autor.

1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL ArchivoSign]** y seleccione una carpeta para alojar la configuración.

1. En la página de configuraciones, pulse **[!UICONTROL Crear]** para crear [!DNL DocuSign] en AEM Forms.
1. En el **[!UICONTROL General]** de la pestaña **[!UICONTROL Crear la configuración de ArchiveSign]** página, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un **[!UICONTROL Título]**.

1. Copie la dirección URL de la ventana actual del explorador en un bloc de notas. La dirección URL es necesaria para configurar [!DNL DocuSign] aplicación con [!DNL AEM Forms] en un paso posterior.

1. Configure las opciones de OAuth para la variable [!DNL DocuSign] aplicación:

   1. Abra una ventana del explorador e inicie sesión en [!DNL DocuSign] [cuenta de desarrollador](https://admindemo.docusign.com/apps-and-keys).
   1. Abra la aplicación configurada para [!DNL AEM Forms].
   1. En el **[!UICONTROL URI de redirección]** , añada la URL copiada en el paso anterior y haga clic en **[!UICONTROL Guardar]**.
   1. Tenga en cuenta las claves de integración y secreto.

   Para obtener información paso a paso sobre cómo configurar las opciones de OAuth para un [!DNL DocuSign] y obtenga las claves, consulte [Configuración de oAuth para la aplicación](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) documentación para desarrolladores.

1. Vuelva a la **[!UICONTROL Crear la configuración de ArchiveSign]** página. En el **[!UICONTROL Configuración]** , la pestaña **[!UICONTROL URL de OAuth]** menciona la siguiente dirección URL predeterminada:

   `https://account-d.docusign.com/oauth/auth`

1. Especifique la variable **[!UICONTROL ID de cliente]** (Clave de integración de ArchiveSign) y **[!UICONTROL Secreto del cliente]** (Clave secreta de ArchiveSign).

1. Toque **[!UICONTROL Conectarse a ArchiveSign]**. Cuando se le soliciten credenciales, proporcione el nombre de usuario y la contraseña de la cuenta utilizada al crear [!DNL DocuSign] aplicación. Cuando se le pida que confirme el acceso para `your developer account`, haga clic en **[!UICONTROL Permitir acceso]**. Si las credenciales son correctas, aparecerá un mensaje de éxito.

1. Toque **[!UICONTROL Crear]** para crear la variable [!DNL DocuSign] configuración.

1. Seleccione la configuración y haga clic en **[!UICONTROL Publicación]**, seleccione la configuración y haga clic en **[!UICONTROL Publicación]**. Duplica la configuración en los entornos de publicación correspondientes.

1. Repita todos los pasos anteriores en las instancias de desarrollador, etapa y producción (la que se quede) para completar la configuración [!DNL DocuSign] con [!DNL AEM Forms] para su entorno.

Ahora, el entorno de AEM Forms está configurado para utilizar ArchiveSign. Asegúrese de agregar el contenedor de configuración utilizado para el Cloud Service a todos los Forms adaptables habilitados para [!DNL DocuSign]. Puede especificar un contenedor de configuración desde las propiedades de un formulario adaptable.

### Uso [!DNL DocuSign] en un formulario adaptable {#enabledocusign}

Puede habilitar [!DNL DocuSign] para un formulario adaptable existente o crear un [!DNL DocuSign] formulario adaptable activado. Elija una de las siguientes opciones:

- [Cree un [!DNL DocuSign] formulario adaptable habilitado](#create-an-adaptive-form-for-docusign)
- [Habilitar [!DNL DocuSign] para un formulario adaptable existente](#editafsign).

#### Creación de un formulario adaptable para ArchiveSign {#create-an-adaptive-form-for-docusign}

Para crear un formulario adaptable habilitado para firmar:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
1. Toque **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparece una lista de plantillas. Seleccione una plantilla y pulse **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Básico]** pestaña:

   1. Especifique la variable **[!UICONTROL Nombre]** y **[!UICONTROL Título]** para el formulario adaptable.

   1. Seleccione el [contenedor de configuración](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) created while [integrar [!DNL DocuSign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   El contenedor de configuración contiene el [!DNL DocuSign] Cloud Services configurados para su entorno. Estos servicios están disponibles para su selección en el editor de formularios adaptables.

1. En el **[!UICONTROL Modelo de formulario]** , seleccione una de las siguientes opciones:

   - Si tiene una plantilla de formulario personalizada y necesita un documento de registro basado en la plantilla de formulario, seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla Documento de registro]** y seleccione una plantilla Documento de registro. Cuando se utiliza la opción , los documentos enviados para firmar solo muestran los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   - Si no tiene una plantilla de formulario personalizada, seleccione la **[!UICONTROL Generar documento de registro]** . Cuando se utiliza la opción , el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Crear.]** Se crea un formulario adaptable con firma habilitada. Puede añadir [!DNL DocuSign] al formulario y envíelo para su firma.
1. Abra el formulario adaptable en modo de edición. En el **[!UICONTROL Contenido]** , toque la pestaña **[!UICONTROL Contenedor de formulario]** y toque ![Configurar](assets/configure-icon.svg).

1. En el **[!UICONTROL Envío]** , seleccione **[!UICONTROL Enviar con firmas electrónicas de ArchiveSign]** de la variable **[!UICONTROL Enviar acción]** lista desplegable.

1. En el **[!UICONTROL Configuración de la acción]** sección, toque **[!UICONTROL Agregar]** para añadir un destinatario y especificar la dirección de correo electrónico del destinatario. Toque **[!UICONTROL Agregar]** para añadir más destinatarios.

1. Especifique el asunto del mensaje de correo electrónico en la **[!UICONTROL Asunto del correo electrónico]** campo . Select **Incluir archivos adjuntos** para incluir archivos adjuntos en el mensaje de correo electrónico.

1. Toque ![Guardar](assets/save_icon.svg) para guardar las propiedades.

#### Habilitar [!DNL DocuSign] para un formulario adaptable {#editafsign}

Para usar [!DNL DocuSign] en un formulario adaptable existente:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
1. Seleccione el formulario adaptable y pulse **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Básico]** , seleccione [contenedor de configuración](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al integrar [!DNL DocuSign] con [!DNL AEM Forms].
1. En el **[!UICONTROL Modelo de formulario]** , seleccione una de las siguientes opciones:

   - Si tiene una plantilla de formulario personalizada y necesita un documento de registro basado en la plantilla de formulario, seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla Documento de registro]** y seleccione una plantilla Documento de registro. Cuando se utiliza la opción , los documentos enviados para firmar solo muestran los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   - Si no tiene una plantilla de formulario personalizada, seleccione la **[!UICONTROL Generar documento de registro]** . Cuando se utiliza la opción , el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Toque **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL DocuSign]. Ahora, puede agregar su [!DNL DocuSign] al formulario y envíelo para su firma.

1. Abra el formulario adaptable en modo de edición. En el **[!UICONTROL Contenido]** , toque la pestaña **[!UICONTROL Contenedor de formulario]** y toque ![Configurar](assets/configure-icon.svg).

1. En el **[!UICONTROL Envío]** , seleccione **[!UICONTROL Enviar con firmas electrónicas de ArchiveSign]** de la variable **[!UICONTROL Enviar acción]** lista desplegable.

1. En el **[!UICONTROL Configuración de la acción]** sección, toque **[!UICONTROL Agregar]** para añadir un destinatario y especificar la dirección de correo electrónico del destinatario. Toque **[!UICONTROL Agregar]** para añadir más destinatarios.

1. Especifique el asunto del mensaje de correo electrónico en la **[!UICONTROL Asunto del correo electrónico]** campo . Select **Incluir archivos adjuntos** para incluir archivos adjuntos en el mensaje de correo electrónico.

1. Toque ![Guardar](assets/save_icon.svg) para guardar las propiedades.
