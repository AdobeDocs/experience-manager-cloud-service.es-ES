---
title: Guía de migración de Experience Manager as a Cloud Service para socios
description: Guía de migración de Experience Manager as a Cloud Service para socios
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 22%

---

# Guía de migración de Adobe Experience Manager as a Cloud Service para socios {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migración a AEM as a Cloud Service"
>abstract="Describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager a Experience Manager as a Cloud Service y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=es" text="¿Qué hay de nuevo y diferente?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=es" text="Introducción a AEM as a Cloud Service."

Adobe Experience Manager AEM () as a Cloud Service ofrece una base rediseñada para Experience Manager, basada en una infraestructura basada en contenedores, un desarrollo impulsado por API y un proceso de DevOps guiado, lo que permite a los especialistas en marketing y a los desarrolladores mantenerse siempre a la vanguardia en las innovaciones de la administración de experiencias del cliente.

Cloud Service aúna las abundantes funciones y extensibilidad integradas de Adobe Experience Manager con la agilidad de la moderna arquitectura nativa de la nube que permite a las marcas satisfacer la demanda de los consumidores, que evoluciona constantemente.

Este breve informe describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager a Experience Manager as a Cloud Service y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas en esta plataforma moderna y diseñada para la administración de experiencias

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Consulte el diagrama siguiente para obtener una representación general del recorrido de migración.

![imagen](/help/journey-migration/assets/migration-process.png)

## Introducción a Adobe Experience Manager as a Cloud Service {#getting-started}

| ¿Qué hay de diferente? | Información general sobre la arquitectura |
|--------------------------|--------------------------|
| <ul><li>[Arquitectura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Actualizaciones automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)</li><li>[Microservicios de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Binarios de acceso directo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Separación de código y contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es)</li><li>[Replicación como servicio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html)</li><li>[Admin Console, pertenencia a grupos/usuarios y ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[AEM Introducción a la arquitectura de la](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html#underlying-technology)</li><li>[Pila de entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Nivel de Author](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html#underlying-technology)</li><li>[Publicar nivel](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=es) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html) mediante [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[Servicio de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service: arquitectura del tiempo de ejecución](/help/overview/assets/concepts-03.png "AEM as a Cloud Service: arquitectura del tiempo de ejecución")

<br>

## Recorrido de desarrollador en Adobe Experience Manager as a Cloud Service {#developer-journey}

### Desarrollo de

Los aspectos básicos del desarrollo de código son similares en Adobe Experience Manager as a Cloud Service en comparación con las soluciones Adobe Experience Manager On Premise y Managed Services.

Los desarrolladores escriben código y lo prueban localmente, que luego se inserta en entornos remotos de Adobe Experience Manager as a Cloud Service.

Consulte los recursos informativos sobre la implementación para Experience Manager as a Cloud Service para obtener información sobre cómo personalizar la implementación as a Cloud Service de Experience Manager.

| Configuración de desarrollo local | Cosas que hay que saber antes de empezar |
|-----------|------------|
| <ol><li>Revisar [SDK de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html) para obtener más información.</li><li>Ver [Instalación del SDK de Dispatcher](https://video.tv.adobe.com/v/30601) para saber cómo instalar el SDK de Dispatcher</li><li>Ver [Configurar el SDK de Dispatcher](https://video.tv.adobe.com/v/30602) para saber cómo configurar el SDK de Dispatcher</li><li>Revisar [Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html#local-development-environment-set-up) documentación para obtener más información</li><li>Configuración del acceso al Experience Manager [recorrido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html#accessing)</li></ol> | <ol><li>[Aspectos básicos de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)</li><li>[Directrices de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)</li><li>[Explicación de la estructura del proyecto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es)</li><li>[Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)</li><li>[Modelo de Digital Foundation](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=es)</li><li>[Superposiciones](/help/implementing/developing/introduction/overlays.md)</li><li>[Referencia de API as a Cloud Service de Experience Manager](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Consulte el tutorial sobre cómo [Desarrollo e implementación de WKND en el SDK de Experience Manager local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Implementación

AEM Los desarrolladores escriben código y lo prueban localmente, que luego se inserta en entornos as a Cloud Service remotos de la.

Se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Este es ahora el único mecanismo para implementar código en entornos de AEM as a Cloud Service.

AEM Consulte recursos informativos sobre cómo configurar e implementar en entornos as a Cloud Service de la.

1. [Configurar canalizaciones de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html)
   * Canalización de producción
   * Canalizaciones de no producción y de solo calidad de código
2. [Implementar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)
3. [Comprender los resultados de la prueba](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html)
4. **Acceso a registros**
   * [mediante la IU de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=es)
   * [mediante cli de e/s de Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging)
5. [Operaciones y mantenimiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html)
   * [Configurar OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=es)
   * [Copia de seguridad y restauración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html)

>[!TIP]
> Consulte el tutorial sobre cómo [Implementar WKND en el Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Ayuda y recursos

1. [Sugerencias y trucos para la depuración](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html#debugging-aem-as-a-cloud-service)
2. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) (Solo disponible en los entornos locales de SDK y desarrollo de Experience Manager Cloud)
4. [Registros y registros](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging)
   * [Registros de CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html#debugging) (build-unit-testing, escaneo de código, build-image, deploy)
   * [Registros de Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registros de SDK locales (en host:port/crx-quickstart/logs)

>[!NOTE]
> Para obtener ayuda adicional, es posible que desee:
>1. [Póngase en contacto con el Equipo de soporte Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html)
>2. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

<br>

## Traslado a Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Traslado a Adobe Experience Manager as a Cloud Service"
>abstract="Este breve informe describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager a Experience Manager as a Cloud Service y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas en esta plataforma moderna y diseñada para la administración de experiencias"

**Experience Manager as a Cloud Service ofrece una base tecnológica escalable, segura y ágil para Experience Manager Sites y Assets, lo que permite a los especialistas en marketing y TI centrarse en ofrecer experiencias impactantes a escala.**

Con Experience Manager as a Cloud Service, sus equipos pueden centrarse en la innovación en lugar de planificar las actualizaciones de los productos. Las nuevas funciones del producto se prueban a fondo y se entregan a sus equipos sin ninguna interrupción para que siempre tengan acceso a la aplicación más avanzada.

El recorrido de transición a Cloud Service implica tres fases: Planificación, Ejecución y Publicación de Go-live.
Para una transición exitosa y sin problemas, se debe asegurar una planificación adecuada y atenerse a las prácticas recomendadas descritas en esta guía.

La figura siguiente muestra una representación de alto nivel del recorrido de transición recomendado para Cloud Service.

![imagen](/help/journey-migration/assets/home-img1.png)

<br>

### Planificación

Antes de comenzar la transición de recorrido a Cloud Service, debe familiarizarse con el as a Cloud Service de Experience Manager, revisar los cambios importantes que se le han realizado y también las funciones que se han sustituido o están en desuso.

<table>
<tr>
<td>Descubrimiento y evaluación de proyectos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=en">Cambios importantes en Experience Manager as a Cloud Service</a> para comprender las diferencias importantes entre Adobe Experience Manager as a Cloud Service y Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">Funciones obsoletas</a> para obtener más información sobre las funciones y capacidades que se han marcado como obsoletas.</li><li>[Solo para migraciones de Cloud Service] Evaluación de la preparación de los Cloud Service : ejecute el <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Analizador de prácticas recomendadas (BPA)</a> en el entorno de origen </li><li>Complete una evaluación de los cambios más importantes y las funciones obsoletas de Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Revisión</td>
<td><ul><li>En función del descubrimiento, realice ejercicios de estimación de esfuerzo y recursos</li></ul></td>
</tr>
<tr>
<td>Medida</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Establecer KPI de proyecto</a>, criterios de éxito y plazos del proyecto</li></ul></td>
</tr>
</table>

>[!NOTE]
>AEM El informe del Analizador de prácticas recomendadas acelera el proceso de estimación del tiempo y el coste necesarios para realizar la transición a la as a Cloud Service, al proporcionar información que, de lo contrario, tendría que recopilarse y evaluarse manualmente.


<br>

### Ejecución

Antes de iniciar la fase de ejecución de un proyecto, debe estar integrado en Cloud Service. También debe familiarizarse con Cloud Manager. Mecanismo para implementar el código de proyecto en una instancia de Experience Manager Cloud Service.

Cloud Manager permite a las organizaciones autoadministrar los Experience Manager en la nube. Incluye una integración y un envío continuos ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html)), que permite a los equipos de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

#### Migración de contenido

1. [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=es#migration) AEM : se utiliza para mover contenido existente de una instancia de origen de la aplicación (local o AMS) a la instancia de AEM Cloud Service de destino.
2. [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html#package-manager) : se utiliza para importar y exportar contenido mutable del repositorio.


#### Refactorizar/optimizar

| Introducción | Revisar y refactorizar código | Revisión de Dispatcher |
|---|---|---|
| <ul><li>[Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html#local-development-environment-set-up)</li><li>[Configuración local de Dispatcher](https://video.tv.adobe.com/v/30602/)</li><li>[Compile su código utilizando el jar de la API de SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)</li><li>[AEM Revisar directrices de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)<ul><li>Tareas de fondo y trabajos de larga duración</li><li>Planificadores de Sling</li><li>Uso del flujo de entrada y más</li></ul></li></ul> | <ul><li>Ejecute el [Analizador de prácticas recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es) en el entorno de origen.[**Solo migración**]<ul><li>Consideraciones sobre la estructuración del proyecto (basadas en [Arquetipo de nube](https://github.com/adobe/aem-project-archetype))<ul><li>Separación de código y contenido (mutable e inmutable)</li><li>[Definiciones de índice personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=es)</li><li>[Modos de ejecución personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)</li></ul></li></ul></li><li>Revisar y ejecutar los cambios necesarios</li><li>[Implementar](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) Implementación en el SDK local</li><li>AEM Realizar pruebas de humo mediante el SDK de</li></ul> | <ul><li>Revisar [Configuraciones de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para refactorización</li><li>Uso [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html) herramienta cuando proceda. [**Solo migración**]</li><li>Las pruebas se pueden realizar utilizando [SDK de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)</li></ul> |

>[!TIP]
> Clientes de Assets: revise y refactorice flujos de trabajo de Assets mediante [Migración de Asset Cloud](https://github.com/adobe/aem-cloud-migration) herramientas


#### Implementación/lanzamiento

1. [Implementar en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html) git
2. Ejecute el código de cliente a través de [Canalización de calidad de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html)
3. [Implementar en el entorno de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html#debugging)
4. [**Solo migración**] Transferencia de contenido mediante paquetes o [Herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Realizar ciclos de prueba recomendados (humo, control de calidad y más)
6. Enviar a la canalización de producción de Cloud Manager
7. Validación de prueba de humo
8. Go-Live

<br>

### Publicar Go-Live

En la fase de Publicar Go-live, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

>[!TIP]
> AEM Hay herramientas disponibles para solucionar problemas de entorno as a Cloud Service de la solución de problemas
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html)
>3. [Administración de registros](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=es)

<br>

### Herramientas y recursos

| Evaluación | Refactorización | Modernización del Experience Manager | Migración de contenido |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es)</li></li> | <ul><li>[Complemento de experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html)</li></ul> | <ul><li>[Plantillas estáticas a plantillas editables](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Diseñar configuraciones para directivas](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componentes básicos a principales](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[De IU clásica a IU táctil.](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es)</li><li>[Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html#contentmanagement)</li></ul> |

>[!NOTE]
> Para obtener ayuda adicional, es posible que desee:
>1. [Póngase en contacto con el Equipo de soporte Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html)
>2. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)
