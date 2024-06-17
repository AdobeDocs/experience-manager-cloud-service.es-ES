---
title: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
description: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Actualizar [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] permite actualizar el [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la última.

>[!TIP]
>
>¿Está buscando [!DNL Workfront for Experience Manager enhanced connector] AEM ¿desea actualizar la documentación de 6.5? Clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Para actualizar el [!DNL Workfront for Experience Manager enhanced connector] a la versión más reciente:

1. Descargue la última versión del conector mejorado desde [Distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) AEM y clone el repositorio as a Cloud Service de la desde Cloud Manager.

1. Abra el repositorio as a Cloud Service del Experience Manager clonado mediante un IDE de su elección.

1. Coloque el archivo zip del conector mejorado descargado en el paso 1 en la siguiente ruta:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Si la variable `resources` no existe, cree la carpeta.

1. Actualizar la versión mejorada del conector en el elemento principal `pom.xml`.

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
   >Asegúrese de añadir `<scope>` y `<systemPath>` a las dependencias en los pasos 5 y 6.

1. Actualizar `pom.xml` incrusta. Añada el [!DNL Workfront for Experience Manager enhanced connector] paquetes para `embeddeds` de la sección `pom.xml` de todos los subproyectos. Incorporar las actualizaciones en todos los módulos `pom.xml`.

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

1. [Elimine las dependencias de los puntos de distribución de Hoodoo](remove-external-dependencies.md), si procede.

1. Inserte los cambios en el repositorio.

1. Ejecute la canalización en [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
