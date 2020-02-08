---
title: Repositorio de código fuente - Servicios de nube
description: Repositorio de código fuente - Servicios de nube
translation-type: tm+mt
source-git-commit: 6f323f33663f83043eb8a15fe00e6ed872c3cac1

---


# Repositorio de códigos de origen {#source-code-repository}

El programa Cloud Manager se aprovisionará automáticamente con su propio repositorio Git.

Para que un usuario pueda acceder al repositorio de Git de Cloud Manager, los usuarios deberán utilizar un cliente Git con una herramienta de línea de comandos, un cliente Git visual independiente o el IDE del usuario como Eclipse, IntelliJ o NetBeans.

Una vez configurado un cliente Git, puede administrar el repositorio git desde la interfaz de usuario de Cloud Manager. Para obtener más información sobre cómo administrar Git mediante la interfaz de usuario del Administrador de nube, consulte [Acceso a Git](/help/implementing/cloud-manager/accessing-git.md).

Para comenzar a desarrollar la aplicación de AEM Cloud, se debe realizar una copia local del código de la aplicación desprotegiéndolo del repositorio de Cloud Manager en una ubicación de su equipo local en la que desee crear su repositorio.

```java
$ git clone {URL}
```

> [!NOTE]
> Un usuario puede extraer una copia de su código y realizar cambios en el repositorio de código local. Cuando esté listo, el usuario puede volver a transferir los cambios de código al repositorio de código remoto en Cloud Manager.
