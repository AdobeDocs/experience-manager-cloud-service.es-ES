---
title: Notas de la versión para Cloud Manager 2025.1.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2025.1.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f6c1aa32647bcabeb0781973f81b75c11edc6a5d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 19%

---

# Notas de la versión para Cloud Manager 2025.1.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.1.0 en AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.1.0 en AEM as a Cloud Service es el miércoles, 22 de enero de 2025.

La próxima versión planificada es el viernes, 13 de febrero de 2025.


## Novedades {#what-is-new}

* **Reglas de calidad del código - Actualización del servidor de SonarQube:** El paso de calidad del código de Cloud Manager empezará a utilizar SonarQube Server 9.9 con la versión 2025.2.0 de Cloud Manager, programada para el jueves 13 de febrero de 2025.

Para prepararse, las reglas actualizadas de SonarQube ya están disponibles en [Reglas de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

Puede &quot;comprobar antes&quot; las nuevas reglas configurando la siguiente variable de texto de canalización:

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

Además, establezca la siguiente variable para asegurarse de que el paso de calidad del código se ejecuta para la misma confirmación (normalmente se omite para el mismo `commitId`):

`CM_DISABLE_BUILD_REUSE` = `true`

![Página de configuración de variables](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe recomienda crear una nueva canalización de calidad de código de CI/CD, configurada en la misma rama que la canalización de producción principal. Establezca las variables apropiadas *antes* de la versión del 13 de febrero de 2025 para validar que las nuevas reglas aplicadas no introduzcan bloqueadores.

* **Compatibilidad con Java 17 y Java 21 Build:** Los clientes ahora pueden compilar con Java 17 o Java 21, obteniendo acceso a mejoras de rendimiento y nuevas características del lenguaje. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Cuando la versión de compilación se establece en Java 17 o Java 21, el tiempo de ejecución implementado es Java 21.

   * **Habilitación de características**
      * Esta función se habilitará para todos los clientes el jueves 13 de febrero de 2025, coincidiendo con el despliegue predeterminado de la nueva versión de SonarQube.
      * Los clientes pueden habilitarlo *inmediatamente* estableciendo las dos configuraciones de variables descritas anteriormente para actualizar la versión de SonarQube 9.9.

   * **Implementación de tiempo de ejecución de Java 21**
      * El tiempo de ejecución de Java 21 se implementa al crear con Java 17 o Java 21.
      * El despliegue gradual en todos los entornos de Cloud Manager comienza en febrero para los entornos de pruebas y desarrollo y se extiende a los entornos de producción en abril.
      * Los clientes que usen Java 11 y deseen adoptar el tiempo de ejecución de Java 21 *antes* pueden ponerse en contacto con el Adobe en [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* Se cambió el nombre de **&quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot;:** Como parte de las mejoras en la interfaz de usuario en AEM Cloud Manager, se cambió el nombre de la etiqueta &quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot; para mejorar la alineación de la terminología con la funcionalidad. <!-- CMGR-64738 -->

  Se cambió el nombre de ![ &quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot; en la interfaz de usuario](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
