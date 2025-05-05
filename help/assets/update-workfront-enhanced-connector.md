---
title: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
description: Actualizar [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---

# Actualización [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

[!UICONTROL Experience Manager Assets as a Cloud Service] le permite actualizar [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la más reciente.

>[!TIP]
>
>¿Está buscando la documentación de actualización de [!DNL Workfront for Experience Manager enhanced connector] para AEM 6.5? Haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=es##update-enhanced-connector-for-workfront).


Para actualizar [!DNL Workfront for Experience Manager enhanced connector] a la última versión:

1. Descargue la versión más reciente del conector mejorado de [Distribución de software de Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acceda](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=es) y clone su repositorio de AEM as a Cloud Service desde Cloud Manager.

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

1. Ejecute la canalización para [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es).
