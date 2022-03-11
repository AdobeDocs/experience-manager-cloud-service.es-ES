---
title: 'Repositorio de códigos de origen: Cloud Services'
description: 'Repositorio de códigos de origen: Cloud Services'
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Repositorio de códigos de origen {#source-code-repository}

El programa de Cloud Manager se aprovisionará automáticamente con su propio repositorio de Git.

Para que un usuario pueda acceder al repositorio de Git de Cloud Manager, los usuarios deberán utilizar un cliente Git con una herramienta de línea de comandos, un cliente Git visual independiente o el IDE del usuario, como Eclipse, IntelliJ o NetBeans.

Una vez configurado un cliente Git, puede administrar el repositorio de Git desde la interfaz de usuario de Cloud Manager. Para obtener información sobre cómo administrar Git mediante la interfaz de usuario de Cloud Manager, consulte [Acceso a Git](/help/implementing/cloud-manager/accessing-git.md).

Para comenzar a desarrollar la aplicación de AEM Cloud, se debe realizar una copia local del código de la aplicación comprobándolo desde el repositorio de Cloud Manager a una ubicación de su equipo local en la que deseen crear su repositorio.

```java
$ git clone {URL}
```

>[!NOTE]
>
>Un usuario puede extraer una copia de su código y realizar cambios en el repositorio de código local. Cuando esté listo, el usuario puede devolver los cambios de código al repositorio de código remoto en Cloud Manager.
