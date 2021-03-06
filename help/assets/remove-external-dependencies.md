---
title: Eliminar dependencias externas para instalaciones existentes
description: Eliminar dependencias externas para instalaciones existentes
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Eliminar dependencias externas para instalaciones existentes {#remove-external-depedencies}

Adobe recomienda ejecutar los pasos de configuración para las instalaciones de conectores mejorados existentes para Workfront a fin de eliminar las dependencias de los puntos de distribución de Hoodoo.

>[!NOTE]
>
>Ejecute los pasos de configuración solo si ha instalado el conector mejorado para Workfront antes de marzo de 2022. No hay dependencias en los puntos de distribución de Hoodoo para las nuevas instalaciones de conectores mejoradas para Workfront a partir de marzo de 2022.

Para eliminar las dependencias externas:

1. Elimine la siguiente configuración del repositorio de Hoodoo del primario `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Elimine la siguiente configuración del servidor de la sección `settings.xml` archivo, disponible en `./cloudmanager/maven/settings.xml`:

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

1. Ejecute el [nuevos pasos de instalación](workfront-connector-install.md).
