---
title: Envío de un conector de AEM
description: Envío de un conector de AEM
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 11%

---


Envío de un conector de AEM
===========================

La información que se proporciona a continuación es útil para enviar Conectores AEM y debe leerse junto con los artículos sobre la [implementación](implement.md) y el [mantenimiento](maintain.md) de los conectores.

AEM Conectores se muestran en el [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

En soluciones AEM anteriores, el Administrador de paquetes se utilizó para instalar conectores en varias instancias de AEM. Sin embargo, con AEM como Cloud Service, los conectores se implementan durante el proceso de CI/CD en Cloud Manager. Para que se implementen los conectores, es necesario hacer referencia a los conectores en el archivo pom.xml del proyecto muven.

Existen varias opciones para incluir los paquetes en un proyecto:

1. Repositorio público del socio: un socio alojaría el paquete de contenido en un repositorio principal de acceso público
1. Repositorio protegido por contraseña de socio: un socio alojaría el paquete de contenido en un repositorio principal protegido por contraseña. Consulte [repositorios maestros protegidos con contraseña en](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories) para obtener instrucciones.
1. Artefacto agrupado: en este caso, el paquete de conector se incluye localmente en el proyecto mecanizado del cliente.

Independientemente del lugar en el que se alojen, es necesario hacer referencia a los paquetes como dependencias en pom.xml, tal como lo proporciona el proveedor.

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

Si el socio ISV aloja el conector en un repositorio accesible por Internet (como Cloud Manager accesible), el ISV debe proporcionar la configuración del repositorio donde se puede colocar el archivo pom.xml, de modo que las dependencias del conector (arriba) se puedan resolver en el momento de la creación (tanto localmente como por Cloud Manager).

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

Si el socio de ISV decide distribuir el conector como archivos descargables, el ISV debe proporcionar instrucciones sobre cómo se pueden implementar los archivos en un repositorio creado por el sistema de archivos local que se debe registrar en Git como parte del proyecto de AEM, para que Cloud Manager pueda resolver estas dependencias.
