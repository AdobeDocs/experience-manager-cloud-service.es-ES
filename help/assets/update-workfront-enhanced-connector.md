---
title: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
description: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Actualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] le permite actualizar el [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la más reciente.

>[!TIP]
>
>¿Está buscando [!DNL Workfront for Experience Manager enhanced connector] actualizar documentación para AEM 6.5? Haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Para actualizar el [!DNL Workfront for Experience Manager enhanced connector] a la versión más reciente:

1. Descargue la versión más reciente del conector mejorado desde [Distribución del software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) y clone su repositorio as a Cloud Service AEM desde Cloud Manager.

1. Abra el repositorio as a Cloud Service del Experience Manager clonado utilizando un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la variable `resources` carpeta no existe, cree la carpeta.

1. Actualizar la versión del conector mejorado en parent `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. Actualice la dependencia en `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >Asegúrese de agregar `<scope>` y `<systemPath>` a las dependencias de los pasos 5 y 6.

1. Actualizar `pom.xml` incrustaciones. Agregue la variable [!DNL Workfront for Experience Manager enhanced connector] paquetes a `embeddeds` de la sección `pom.xml` de todo el subproyecto. Incorporar las actualizaciones en todos los módulos `pom.xml`.

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

1. [Eliminar las dependencias de los puntos de distribución de Hoodoo](remove-external-dependencies.md), si existe.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización a [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
