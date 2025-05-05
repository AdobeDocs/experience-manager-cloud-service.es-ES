---
title: Envío de un conector de AEM
description: Aprenda a hacer referencia e implementar correctamente los conectores en Adobe Experience Manager AEM () as a Cloud Service.
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 32%

---

# Envío de un conector de AEM

La información que se proporciona a continuación es útil para enviar Conectores Adobe Experience Manager AEM () y se debe leer con artículos sobre [implementación](implement.md) y [mantenimiento de los conectores](maintain.md).

Los conectores de AEM aparecen en la lista de [Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

En soluciones anteriores de AEM, el [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) se utilizaba para instalar conectores en varias instancias de AEM. Sin embargo, con AEM as a Cloud Service, los conectores se implementan durante el proceso de CI/CD en Cloud Manager. Para que se implementen los conectores, se debe hacer referencia a los conectores en el pom.xml del proyecto de Maven.

Existen varias opciones para incluir los paquetes en un proyecto:

1. Repositorio público del partner: un partner alojaría el paquete de contenido en un repositorio Maven accesible públicamente
1. Repositorio protegido por contraseña del partner: un partner alojaría el paquete de contenido en un repositorio Maven protegido por contraseña. Consulte [repositorios Maven protegidos por contraseña](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html?lang=es#password-protected-maven-repositories) para obtener instrucciones.
1. Artefacto integrado: en este caso, el paquete de conector se incluye localmente en el proyecto Maven del cliente.

Independientemente de dónde estén alojados, se debe hacer referencia a los paquetes como dependencias en el archivo pom.xml, tal como lo proporciona el proveedor.

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

Si el partner de ISV aloja el conector en un repositorio Maven accesible por Internet (como accesible por Cloud Manager), el ISV debe proporcionar la configuración del repositorio en la que se puede colocar `pom.xml`. El motivo es que las dependencias del conector (arriba) se pueden resolver en el momento de la compilación, tanto localmente como por Cloud Manager.

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

Si el partner de ISV decide distribuir el conector como archivos descargables, el ISV debe proporcionar instrucciones. AEM La instrucción debe describir cómo se pueden implementar los archivos en un repositorio Maven del sistema de archivos local que debe registrarse en Git como parte del proyecto de. Esto garantiza que Cloud Manager pueda resolver estas dependencias.
