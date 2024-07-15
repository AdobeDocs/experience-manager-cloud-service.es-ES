---
title: Programas y tipos de programas
description: Obtenga información sobre la jerarquía de Cloud Manager y cómo encajan los distintos tipos de programas en su estructura y cómo difieren.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 91%

---


# Programas y tipos de programas {#understanding-programs}

Cloud Manager se basa en una jerarquía de entidades. Los detalles de esto no son esenciales para su trabajo diario en Cloud Manager, pero una descripción general de él le ayudará a comprender los programas y a configurar los suyos propios.

![Jerarquía de Cloud Manager](assets/program-types1.png)

* **INQUILINO**: Esta es la parte superior de la jerarquía. Cada cliente está aprovisionado con un inquilino.
* **PROGRAMAS**: Cada inquilino tiene uno o más programas, [que a menudo reflejan las soluciones con licencia del cliente.](introduction-production-programs.md)
* **ENTORNOS**: Cada programa tiene múltiples entornos, como producción para contenido en directo, uno para ensayo y otro para desarrollo.
   * Cada programa puede tener un solo entorno de producción, pero varios entornos que no sean de producción.
* **REPOSITORIO**: Los programas tienen repositorios de Git donde el código de la aplicación y del front-end se mantiene para los entornos.
* **HERRAMIENTAS Y FLUJOS DE TRABAJO**: Las canalizaciones administran la implementación de código desde los repositorios a los entornos, mientras que otras herramientas permiten el acceso a los registros, la monitorización y la administración del entorno.

Un ejemplo suele ser útil para contextualizar esta jerarquía.

* Las empresas de viajes y aventura de WKND pueden ser un **inquilino** que se centra en medios relacionados con viajes.
* El inquilino de empresas de viajes y aventura de WKND puede tener dos **programas**: un programa de Sites para la revista de WKND y uno de Assets para los medios de WKND.
* Los programas de revista de WKND y de medios de WKND tendrían **entornos** de desarrollo, ensayo y producción.

## Repositorio de códigos de origen {#source-code-repository}

Un programa de Cloud Manager vendrá aprovisionado automáticamente con su propio repositorio de Git.

Para acceder al repositorio de Git de Cloud Manager, los usuarios deben utilizar un cliente de Git con una herramienta de línea de comandos, un cliente de Git visual independiente o el IDE que el usuario elija, como Eclipse, IntelliJ o NetBeans.

Una vez configurado el cliente de Git, puede administrar el repositorio Git desde la interfaz de usuario de Cloud Manager. Para obtener más información sobre cómo administrar Git mediante la interfaz de usuario de Cloud Manager, consulte [Acceso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

Para comenzar a desarrollar la aplicación de AEM Cloud, se debe realizar una copia local del código de la aplicación desprotegiéndolo del repositorio de Cloud Manager a una ubicación de su equipo local.

```java
$ git clone {URL}
```

Por lo tanto, el flujo de trabajo es un flujo de trabajo de Git estándar.

1. Un usuario clona una copia local del repositorio de Git.
1. El usuario realiza cambios en el repositorio de código local.
1. Cuando está listo, el usuario vuelve a enviar los cambios al repositorio remoto de Git.

La única diferencia es que el repositorio remoto de Git forma parte de Cloud Manager, que es transparente para el desarrollador.

## Tipos de programas {#program-types}

Un usuario puede crear un programa de **producción** o un programa de **espacio aislado**.

* Un **programa de producción** se crea para habilitar el tráfico en directo para el sitio.
   * Consulte [Introducción a los programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obtener más información.
* Un **programa de zona protegida** normalmente se crea para servir los propósitos de formación, ejecución de demostraciones, habilitación, POC o documentación.
   * Una zona protegida no está diseñada para transportar tráfico en directo y tiene restricciones que un programa de producción no.
   * Incluye Sites y Assets y se entrega rellenado automáticamente con una rama de Git que incluye código de muestra, un entorno de desarrollo y una canalización que no es de producción.
   * Consulte [Introducción a los programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obtener más información.
