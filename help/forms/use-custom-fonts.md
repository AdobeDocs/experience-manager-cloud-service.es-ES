---
title: 'Usar fuentes personalizadas '
description: 'Usar fuentes personalizadas '
source-git-commit: 10fe582edc8ffc93ea3f8564a64259882bba1d6f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Usar fuentes personalizadas

**La documentación de Cloud Service Communications está en versión beta**

Puede utilizar Comunicaciones as a Cloud Service de Forms para combinar una plantilla XDP, un documento de PDF basado en XDP o un formulario de Acrobat (AcroForm) con datos XML para generar documentos de PDF. Puede utilizar las fuentes incluidas en las fuentes Cloud Service o personalizadas (fuentes aprobadas por la organización) para procesar los documentos PDF generados. Puede utilizar el proyecto de desarrollo de Cloud Service para agregar fuentes personalizadas al entorno de Cloud Service.

## Comportamiento de los documentos del PDF

Puede [incrustar una fuente](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) a un documento de PDF. Cuando se incrusta una fuente, el documento PDF aparecerá (se verá) idéntico en todas las plataformas. Utilizó fuentes incrustadas para garantizar un aspecto y una apariencia coherentes. Cuando una fuente no está incrustada, la renderización de la fuente depende de la configuración de renderización del cliente del visor del PDF. Si la fuente está disponible en el equipo cliente, el PDF utiliza la fuente especificada; de lo contrario, el PDF se procesa con una fuente de reserva.

## Añada fuentes personalizadas al entorno as a Cloud Service de Forms.

Para agregar fuentes personalizadas al entorno del Cloud Service:

1. Configure y abra el proyecto de desarrollo local. Puede utilizar cualquier IDE de su elección.
1. En la estructura de carpetas de nivel superior del proyecto, cree una carpeta para guardar fuentes personalizadas y agregar fuentes personalizadas a la carpeta. Por ejemplo, fonts/src/main/resources
   ![Carpeta Fuentes](assets/fonts.png)

1. Abra el archivo pom.xml de nivel superior del proyecto de desarrollo.
1. Agregar `<Font-Archive-Version>` entrada de manifiesto al archivo .pom y establecer el valor de la versión en 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
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

1. Compruebe el código actualizado y [ejecutar la canalización](/help/implementing/cloud-manager/deploy-code.md) para implementar las fuentes en el entorno del Cloud Service.
