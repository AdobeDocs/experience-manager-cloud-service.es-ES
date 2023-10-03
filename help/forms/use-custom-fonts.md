---
title: ¿Cómo se utilizan las fuentes personalizadas en AEM Forms?
description: Aprenda a añadir fuentes personalizadas a un entorno as a Cloud Service de Forms.
exl-id: 88214d36-fb97-4d46-a9fe-71dbc7826eb1
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 95%

---

# Usar fuentes personalizadas

**La documentación de Comunicaciones de Cloud Service está en versión beta**

Puede utilizar Comunicaciones de Forms as a Cloud Service para combinar una plantilla XDP, un documento PDF basado en XDP o un formulario de Acrobat (AcroForm) con datos XML para generar documentos PDF. También puede utilizar Comunicaciones para combinar, reorganizar y aumentar documentos PDF y XDP y obtener información sobre documentos PDF.

Junto con las operaciones mencionadas anteriormente, puede utilizar las fuentes incluidas en Cloud Service o fuentes personalizadas (fuentes aprobadas por la organización) para representar los documentos PDF generados. Puede utilizar el proyecto de desarrollo de Cloud Service para agregar fuentes personalizadas al entorno de Cloud Service.

## Comportamiento de los documentos PDF

Puede [incrustar una fuente](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions) en un documento PDF. Cuando se incrusta una fuente, el documento PDF tiene la misma apariencia (aspecto) en todas las plataformas. Se utilizan fuentes incrustadas para garantizar una apariencia uniforme. Cuando una fuente no está incrustada, la representación de la fuente depende de la configuración de representación de los clientes de visor de PDF, como Acrobat o Acrobat Reader. Si la fuente está disponible en el equipo cliente, el PDF utiliza la fuente especificada; de lo contrario, el PDF se representa con una fuente de reserva predeterminada.

## Añadir fuentes personalizadas al entorno de Forms as a Cloud Service {#custom-fonts-cloud-service}

Para agregar fuentes personalizadas al entorno de Cloud Service:

1. Configure y abra el [proyecto de desarrollo local](setup-local-development-environment.md). Puede utilizar cualquier IDE de su elección.
1. En la estructura de carpetas de nivel superior del proyecto, cree una carpeta (módulo) para guardar fuentes personalizadas y agregue fuentes personalizadas a la carpeta; por ejemplo, fonts/src/main/resources.
   ![Carpeta Fuentes](assets/fonts.png)

1. Abra el archivo pom.xml del módulo de fuentes del proyecto de desarrollo.
1. Agregue el complemento jar al archivo pom:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```

1. Agregue el archivo de entrada de manifiesto .pom `<Font-Archive-Version>` y establezca el valor de la versión en 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. Añada la carpeta de fuentes a `<modules>` en el archivo pom. Por ejemplo:

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

   La carpeta de fuentes contiene todas las fuentes personalizadas.

1. Compruebe el código actualizado y [ejecute la canalización](/help/implementing/cloud-manager/deploy-code.md) para implementar las fuentes en el entorno de Cloud Service.

1. (Opcional) Abra el símbolo del sistema, vaya a la carpeta local del proyecto y ejecute el siguiente comando. El comando empaqueta las fuentes en un archivo .jar junto con información relevante. Puede utilizar el archivo .jar para agregar fuentes personalizadas al entorno de desarrollo local de Forms Cloud Service.

   ```shell
   mvn clean install
   ```

## Añadir fuentes personalizadas al entorno de desarrollo local de Forms Cloud Service {#custom-fonts-cloud-service-sdk}

1. Inicie el entorno de desarrollo local.
1. Vaya a la carpeta `<aem install directory>/crx-quickstart/install`.
1. Coloque el archivo `<jar file contaning custom fonts and relevant deployment code>.jar` en la carpeta de instalación. Si no tiene el archivo .jar, realice los pasos que se indican en la sección [Añadir fuentes personalizadas al entorno de Forms as a Cloud Service](#custom-fonts-cloud-service) para generar el archivo.
1. Ejecute el [entorno de SDK basado en Docker](setup-local-development-environment.md#docker-microservices).


   >[!NOTE]
   >
   >Siempre que implemente un archivo .jar de fuentes personalizadas actualizado en el entorno de desarrollo local, reinicie el entorno de SDK basado en Docker.
