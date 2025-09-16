---
title: Cómo integrar DocuSign con un formulario adaptable
description: Aprenda a utilizar DocuSign con un formulario adaptable para recopilar firmas electrónicas.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 99%

---

# Usar DocuSign con un formulario adaptable {#integrate-aem-forms-with-DocuSign}

DocuSign es una solución destacada de firma electrónica. Puede utilizarla para firmar un acuerdo electrónicamente. Puede integrar DocuSign con un formulario adaptable. Le ayuda a enviar un formulario adaptable para firmas electrónicas a varios destinatarios. El uso de firmas electrónicas le ayuda a lo siguiente:

- Cerrar acuerdos desde cualquier dispositivo con procesos de propuesta, presupuesto y contrato totalmente automatizados.
- Finalizar los procesos de Recursos Humanos más rápido y ofrecer a sus empleados las experiencias digitales.
- Reducir los tiempos de ciclo de contrato e incorporar a sus proveedores más rápido.

AEM Forms as a Cloud Service ofrece una [acción de envío personalizada para DocuSign](#deploy-custom-submit-action). La acción de envío le ayuda a enviar los formularios adaptables para las firmas electrónicas mediante las API de DocuSign.

| También puede utilizar la solución de firma electrónica de Adobe, Adobe Sign, para firmar electrónicamente un formulario adaptable. AEM Forms posee una integración mucho más profunda con Adobe Sign y ofrece controles mucho más precisos, como firma secuencial y paralela, varios métodos de autenticación, experiencia de firma en formularios y mucho más. Para obtener más información, consulte [Usar Adobe Sign en un formulario adaptable](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Requisitos previos {#prerequisites}

Se requiere lo siguiente para integrar DocuSign con AEM Forms:

- Una [cuenta de desarrollador](https://developers.docusign.com/platform/account/) de DocuSign
- Una aplicación de DocuSign
- Credenciales (ID del cliente y secreto del cliente) de la aplicación del API de DocuSign.
- [Acción de envío personalizada y servicio en la nube para DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (solo para el entorno de desarrollo local) [Configuración del documento de registro](setup-local-development-environment.md#docker-microservices).

## Configurar la acción de envío personalizada y servicio en la nube para DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service ofrece una acción de envío personalizada para DocuSign. La acción de envío le ayuda a enviar los formularios adaptables para las firmas electrónicas mediante las API de DocuSign. El código para la acción de envío personalizada está disponible en el [repositorio GIT público de muestras de AEM Forms](https://github.com/adobe/aem-forms-docusign-sample). Puede implementar el código tal como figura en su entorno de AEM Forms o personalizarlo según los requisitos de su organización.

Realice los siguientes pasos para configurar la acción de envío personalizada y el servicio en la nube de DocuSign predeterminados:

1. [Clone su proyecto de AEM Forms as a Cloud Service](setup-local-development-environment.md#forms-cloud-service-local-development-environment) o cree un [!DNL Experience Manager Forms] como proyecto de [!DNL Cloud Service] basado en el [tipo de archivo 27 de AEM](https://github.com/adobe/aem-project-archetype) o posterior. Para crear un [!DNL Experience Manager Forms] como proyecto de [!DNL Cloud Service] basado en un tipo de archivo de AEM:
   </br> Abra la solicitud de comando y ejecute el siguiente comando para crear un proyecto de [!DNL Experience Manager Forms] as a Cloud Service:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Además, cambie `appTitle`, `appId`y `groupId`, en el comando anterior para reflejar su entorno.

1. Clone el repositorio [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample). Este repositorio contiene una acción de envío personalizada para los detalles de DocuSign y configuración para conectarse con el servidor de DocuSign.

1. Abra el proyecto de AEM Forms as a Cloud Service creado en el paso 1 para editarlo en el IDE de su elección.

1. Abra el archivo `[AEM Forms as a Cloud Service project]\pom.xml` para editarlo y realice los cambios siguientes:

   1. Añada el siguiente texto al final de la etiqueta `<properties>`:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Añada el siguiente texto al final de la etiqueta `<repositories>`:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Si no hay etiqueta `<repositories>`, cree la etiqueta tras la etiqueta `<properties>`.

   1. Añada el siguiente texto al final de la etiqueta `<dependencyManagement>`:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Siga estos pasos en el archivo `all/pom.xml` disponible en la carpeta del proyecto de Cloud Service:

   1. Añada el siguiente texto al final de la etiqueta `<embeddeds>`:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Añada el siguiente texto al final de la etiqueta `<dependencies>`:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Abra la solicitud de comando y vaya a `aem-forms-samples\forms-integration-docusign` (clonado en el paso 3) y ejecute el siguiente comando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` hace referencia al nombre de la carpeta creada en el paso 1 de este procedimiento.

1. Implemente el proyecto en su entorno de desarrollo local. Puede utilizar el siguiente comando para implementarlo en su entorno de desarrollo local

   `mvn -PautoInstallPackage clean install`

   Tras ejecutar estos pasos, puede ver una nueva acción de envío personalizada [Enviar con firmas electrónicas de DocuSign](#enabledocusign) disponible en la lista de opciones de envío para un formulario adaptable y una [configuración del servicio en la nube DocuSign](#configure-docusign-with-aem-forms) en su entorno de desarrollo local.

1. Compile e [implemente el código en su entorno de  [!DNL AEM Forms]  as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=es#customer-releases).

## Integrar [!DNL DocuSign] con [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para integrar [!DNL DocuSign] con [!DNL AEM Forms] en las instancias de autor.

1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** y seleccione una carpeta para hospedar la configuración.

1. En la página de configuraciones, seleccione **[!UICONTROL Crear]** para crear una configuración de [!DNL DocuSign] en AEM Forms.
1. En la pestaña **[!UICONTROL General]** de la página **[!UICONTROL Crear la configuración de DocuSign]**, especifique un **[!UICONTROL Nombre]** para la configuración y seleccione **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un **[!UICONTROL Título]**.

1. Copie la URL de la ventana actual del explorador en un bloc de notas. La URL es necesaria para configurar la aplicación [!DNL DocuSign] con [!DNL AEM Forms] en un paso posterior.

1. Configure OAuth para la aplicación [!DNL DocuSign]:

   1. Abra una ventana del explorador e inicie sesión en su [cuenta de desarrollador](https://admindemo.docusign.com/apps-and-keys) de [!DNL DocuSign].
   1. Abra la aplicación configurada para [!DNL AEM Forms].
   1. En el cuadro **[!UICONTROL URI de redireccionamiento]**, añada la URL copiada en el paso anterior y haga clic en **[!UICONTROL Guardar]**.
   1. Tenga en cuenta la integración y las claves secretas.

   Para obtener información paso a paso sobre cómo configurar OAuth para una aplicación [!DNL DocuSign] y obtener las claves, consulte la documentación para desarrolladores [Configurar OAuth para la aplicación](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys).

1. Vuelva a la página **[!UICONTROL Crear la configuración de DocuSign]**. En la pestaña **[!UICONTROL Configuración]**, el campo **[!UICONTROL URL de OAuth]** menciona la siguiente URL predeterminada:

   `https://account-d.docusign.com/oauth/auth`

1. Especifique el **[!UICONTROL ID del cliente]** (clave de integración de DocuSign) y el **[!UICONTROL secreto del cliente]** (clave secreta de DocuSign).

1. Seleccione **[!UICONTROL Conectarse a DocuSign]**. Cuando se le soliciten credenciales, indique el nombre de usuario y la contraseña de la cuenta utilizada al crear la aplicación [!DNL DocuSign]. Cuando se le pida que confirme el acceso para `your developer account`, haga clic en **[!UICONTROL Permitir acceso]**. Si las credenciales son correctas, aparecerá un mensaje de éxito.

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de [!DNL DocuSign].

1. Seleccione la configuración y haga clic en **[!UICONTROL Publicar]**, seleccione la configuración y haga clic en **[!UICONTROL Publicar]**. Esto replicará la configuración en los entornos de publicación correspondientes.

1. Repita todos los pasos anteriores en las instancias de desarrollador, fase y producción (cualquiera de las restantes) para completar la configuración de [!DNL DocuSign] con [!DNL AEM Forms] para su entorno.

Ahora, su entorno de AEM Forms está configurado para utilizar DocuSign. Asegúrese de agregar el contenedor de configuración utilizado para Cloud Service a todos los formularios adaptables habilitados para [!DNL DocuSign]. Puede especificar un contenedor de configuración desde las propiedades de un formulario adaptable.

### Utilizar [!DNL DocuSign] en un formulario adaptable {#enabledocusign}

Puede habilitar [!DNL DocuSign] para un formulario adaptable existente o crear un formulario adaptable con [!DNL DocuSign] habilitado. Elija una de las acciones siguientes:

- [Crear un formulario adaptable con [!DNL DocuSign] habilitado](#create-an-adaptive-form-for-docusign)
- [Habilitar  [!DNL DocuSign]  para un formulario adaptable existente](#editafsign).

#### Crear un formulario adaptable para DocuSign {#create-an-adaptive-form-for-docusign}

Para crear un formulario adaptable habilitado para firmar:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione **[!UICONTROL Crear]** y seleccione **[!UICONTROL Formulario adaptable]**. Aparece una lista de plantillas. Seleccione una plantilla y seleccione **[!UICONTROL Siguiente]**.
1. En la pestaña **[!UICONTROL Básico]**:

   1. Especifique el **[!UICONTROL Nombre]** y el **[!UICONTROL Título]** para el formulario adaptable.

   1. Seleccione el [contenedor de configuración](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al [integrarse [!DNL DocuSign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   El contenedor de configuración contiene [!DNL DocuSign] Cloud Service configurado para su entorno. Estos servicios están disponibles para su selección en el creador de formularios adaptables.

1. En la pestaña **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   - Si tiene una plantilla de formulario personalizada y necesita un documento de registro basado en la plantilla de formulario, seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla de documento de registro]** y elija una plantilla de documento de registro. Cuando se utiliza la opción, los documentos enviados para firmar solo muestran los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   - Si no cuenta con una plantilla de formulario personalizada, seleccione la opción **[!UICONTROL Generar documento de registro]**. Cuando se utiliza la opción, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Seleccione **[!UICONTROL Crear]**. Se crea un formulario adaptable con firma habilitada. Puede agregar campos de [!DNL DocuSign] al formulario y enviarlo para su firma.
1. Abra el formulario adaptable en modo de edición. En la pestaña **[!UICONTROL Contenido]**, seleccione **[!UICONTROL Contenedor del formulario]** y seleccione ![Configurar](assets/configure-icon.svg).

1. En la sección **[!UICONTROL Envío]**, seleccione **[!UICONTROL Enviar con firmas electrónicas de DocuSign]** de la lista desplegable **[!UICONTROL Enviar acción]**.

1. En la sección **[!UICONTROL Configuración de la acción]**, seleccione **[!UICONTROL Añadir]** para agregar un destinatario y especificar la dirección de correo electrónico del destinatario. Seleccione **[!UICONTROL Añadir]** para agregar más destinatarios.

1. Especifique el asunto del mensaje de correo electrónico en el campo **[!UICONTROL Asunto del correo electrónico]**. Seleccione **Incluir archivos adjuntos** para incluir archivos adjuntos en el mensaje de correo electrónico.

1. Seleccione ![Guardar](assets/save_icon.svg) para guardar las propiedades.

#### Habilitar [!DNL DocuSign] para un formulario adaptable {#editafsign}

Para usar [!DNL DocuSign] en un formulario adaptable existente:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario adaptable y seleccione **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Básico]**, seleccione el [contenedor de configuración](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creado al integrarse [!DNL DocuSign] con [!DNL AEM Forms].
1. En la pestaña **[!UICONTROL Modelo de formulario]**, seleccione una de las siguientes opciones:

   - Si tiene una plantilla de formulario personalizada y necesita un documento de registro basado en la plantilla de formulario, seleccione la opción **[!UICONTROL Asociar plantilla de formulario como la plantilla de documento de registro]** y elija una plantilla de documento de registro. Cuando se utiliza la opción, los documentos enviados para firmar solo muestran los campos basados en la plantilla de formulario asociada. No muestra todos los campos del formulario adaptable.

   - Si no cuenta con una plantilla de formulario personalizada, seleccione la opción **[!UICONTROL Generar documento de registro]**. Cuando se utiliza la opción, el documento enviado para firmar muestra todos los campos del formulario adaptable.

1. Seleccione **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL DocuSign]. Ahora, puede agregar campos de [!DNL DocuSign] al formulario y enviarlo para su firma.

1. Abra el formulario adaptable en modo de edición. En la pestaña **[!UICONTROL Contenido]**, seleccione **[!UICONTROL Contenedor del formulario]** y seleccione ![Configurar](assets/configure-icon.svg).

1. En la sección **[!UICONTROL Envío]**, seleccione **[!UICONTROL Enviar con firmas electrónicas de DocuSign]** de la lista desplegable **[!UICONTROL Enviar acción]**.

1. En la sección **[!UICONTROL Configuración de la acción]**, seleccione **[!UICONTROL Añadir]** para agregar un destinatario y especificar la dirección de correo electrónico del destinatario. Seleccione **[!UICONTROL Añadir]** para agregar más destinatarios.

1. Especifique el asunto del mensaje de correo electrónico en el campo **[!UICONTROL Asunto del correo electrónico]**. Seleccione **Incluir archivos adjuntos** para incluir archivos adjuntos en el mensaje de correo electrónico.

1. Seleccione ![Guardar](assets/save_icon.svg) para guardar las propiedades.
