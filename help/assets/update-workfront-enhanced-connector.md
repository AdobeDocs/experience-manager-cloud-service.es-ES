---
title: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
description: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Actualización [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] le permite actualizar [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la más reciente.

>[!TIP]
>
>¿Está buscando la documentación de actualización de [!DNL Workfront for Experience Manager enhanced connector] para AEM 6.5? Haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Para actualizar [!DNL Workfront for Experience Manager enhanced connector] a la última versión:

1. Descargue la versión más reciente del conector mejorado de [Distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acceda](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) y clone su repositorio de AEM as a Cloud Service desde Cloud Manager.

1. Abra el repositorio clonado de Experience Manager as a Cloud Service mediante un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la carpeta `resources` no existe, créela.

1. Actualice la versión mejorada del conector en el elemento principal `pom.xml`.

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
   >Asegúrese de agregar `<scope>` y `<systemPath>` a las dependencias en el paso 5 y el paso 6.

1. Actualizar `pom.xml` incrustaciones. Agregue los paquetes de [!DNL Workfront for Experience Manager enhanced connector] a la sección `embeddeds` de `pom.xml` de todo su subproyecto. Incorporar las actualizaciones en todos los módulos `pom.xml`.

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

1. [Elimine las dependencias de los puntos de distribución Hoodoo](remove-external-dependencies.md), si los hubiera.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización para [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
