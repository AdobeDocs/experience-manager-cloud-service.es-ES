---
title: Envío de un conector de AEM
description: Envío de un conector de AEM
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
source-git-commit: eb6aa8741a07e14727b4e74df66b9643936e9231
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 11%

---

Envío de un conector de AEM
===========================

La información que se proporciona a continuación es útil para enviar Conectores AEM y debe leerse junto con los artículos sobre la [implementación](implement.md) y el [mantenimiento](maintain.md) de los conectores.

AEM conectores aparecen listados en el [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

En soluciones AEM anteriores, el Administrador de paquetes se utilizaba para instalar conectores en varias instancias de AEM. Sin embargo, con AEM como Cloud Service, los conectores se implementan durante el proceso CI/CD en Cloud Manager. Para que se implementen los conectores, es necesario hacer referencia a los conectores en el pom.xml del proyecto maven.

Existen varias opciones para incluir los paquetes en un proyecto:

1. Repositorio público del socio: un socio alojaría el paquete de contenido en un repositorio maven accesible públicamente
1. Repositorio protegido por contraseña de socio: un socio alojaría el paquete de contenido en un repositorio maven protegido por contraseña. Consulte repositorios maven protegidos por contraseña para obtener instrucciones.
1. Artefacto agrupado : en este caso, el paquete conector se incluye localmente en el proyecto maven del cliente.

Independientemente de dónde estén alojados, es necesario hacer referencia a los paquetes como dependencias en el archivo pom.xml, tal como lo proporciona el proveedor.

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

Si el socio de ISV aloja el conector en un repositorio maven accesible a Internet (como Cloud Manager accesible), el ISV debe proporcionar la configuración del repositorio en la que se puede colocar el pom.xml, de modo que las dependencias del conector (arriba) se puedan resolver en el momento de la compilación (tanto localmente como por Cloud Manager).

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

Si el socio de ISV decide distribuir el conector como archivos descargables, entonces el ISV debe proporcionar instrucciones sobre cómo se pueden implementar los archivos en un repositorio maven del sistema de archivos local que debe comprobarse en Git como parte del proyecto de AEM, de modo que Cloud Manager pueda resolver estas dependencias.
