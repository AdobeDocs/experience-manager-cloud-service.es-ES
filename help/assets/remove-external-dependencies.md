---
title: Eliminación de dependencias externas para instalaciones existentes
description: Eliminación de dependencias externas para instalaciones existentes
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 17%

---

# Eliminación de dependencias externas para instalaciones existentes {#remove-external-depedencies}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Adobe recomienda ejecutar los pasos de configuración para las instalaciones de conectores mejoradas existentes para Workfront a fin de eliminar las dependencias de los puntos de distribución de Hoodoo.

>[!NOTE]
>
>Ejecute los pasos de configuración solo si ha instalado el conector mejorado para Workfront antes de marzo de 2022. No existen dependencias en los puntos de distribución de Hoodoo para las nuevas instalaciones de conectores mejoradas para Workfront a partir de marzo de 2022.

Para eliminar las dependencias externas:

1. Quite la siguiente configuración del repositorio Hoodoo del elemento principal `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Quite la siguiente configuración de servidor del archivo `settings.xml`, disponible en `./cloudmanager/maven/settings.xml`:

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

1. Ejecute los [nuevos pasos de instalación](workfront-connector-install.md).
