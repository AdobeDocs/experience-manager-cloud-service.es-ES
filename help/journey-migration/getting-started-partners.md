---
title: Guía de migración de Experience Manager as a Cloud Service para socios
description: Guía de migración de Experience Manager as a Cloud Service para socios
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 14%

---

# Guía de migración a Adobe Experience Manager as a Cloud Service para socios {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migración a AEM as a cloud Service"
>abstract="Describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager hasta el as a Cloud Service de Experience Manager y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html" text="¿Qué hay de nuevo y diferente?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html" text="Introducción a AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service ofrece una base rediseñada para el Experience Manager, basada en una infraestructura basada en contenedores, un desarrollo basado en API y un proceso guiado de DevOps, lo que permite a los especialistas en marketing y a los desarrolladores mantenerse siempre a la vanguardia en las innovaciones de la administración de experiencias del cliente.

Cloud Service aúna abundantes prestaciones y extensibilidad integradas de Adobe Experience Manager con la agilidad de la arquitectura nativa de la nube moderna, lo que permite a las marcas satisfacer la demanda del consumidor en constante evolución.

Este paginador único describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager hasta as a Cloud Service de Experience Manager y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas en esta plataforma moderna y diseñada para la administración de experiencias.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Consulte el diagrama siguiente para ver una representación general del recorrido de migración.

![imagen](/help/journey-migration/assets/migration-process.png)

## Introducción a Adobe Experience Manager as a Cloud Service {#getting-started}

| ¿Qué es diferente? | Información general sobre la arquitectura |
|--------------------------|--------------------------|
| <ul><li>[Arquitectura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Actualizaciones automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)</li><li>[Microservicios de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Binarios de acceso directo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[Separación de código y contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Replicación como servicio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=en)</li><li>[Consola de administración, pertenencia a grupos/usuarios y ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[Introducción a AEM Arquitectura](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Pila de entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Nivel de Author](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Nivel de publicación](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[La red de distribución de contenido (CDN)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es) via [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[Servicio de asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service: arquitectura del tiempo de ejecución](/help/overview/assets/concepts-03.png "AEM as a Cloud Service: arquitectura del tiempo de ejecución")

<br>

## Recorrido para desarrolladores en Adobe Experience Manager as a Cloud Service {#developer-journey}

### Desarrollo de

Los fundamentos del desarrollo de código son similares en Adobe Experience Manager as a Cloud Service en comparación con las soluciones de Adobe Experience Manager On Premise y Managed Services.

Los desarrolladores escriben código y lo prueban localmente, que luego se inserta en entornos remotos de Adobe Experience Manager as a Cloud Service.

Consulte los recursos de autoayuda sobre la implementación para el Experience Manager as a Cloud Service para aprender a personalizar la implementación as a Cloud Service del Experience Manager.

| Configuración de desarrollo local | Cosas que hay que saber antes de empezar |
|-----------|------------|
| <ol><li>Consulte [SDK de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) documentación para obtener más información.</li><li>Watch [Instalación del SDK de Dispatcher](https://video.tv.adobe.com/v/30601) para comprender cómo instalar el SDK de Dispatcher</li><li>Watch [Configuración del SDK de Dispatcher](https://video.tv.adobe.com/v/30602) para comprender cómo configurar el SDK de Dispatcher</li><li>Consulte [Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) documentación para obtener más información</li><li>Configuración del acceso al Experience Manager [recorrido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Aspectos básicos del desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Directrices de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[Explicación de la estructura del proyecto del Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)</li><li>[Modelo de base digital](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[Superposiciones](/help/implementing/developing/introduction/overlays.md)</li><li>[Referencia de API as a Cloud Service del Experience Manager](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Consulte el tutorial sobre cómo [Desarrollo e implementación de WKND en el SDK del Experience Manager local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Implementación

Los desarrolladores escriben el código y lo prueban localmente, para a continuación insertarlo en entornos de AEM as a Cloud Service remotos.

Se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Este es ahora el único mecanismo para implementar código en entornos de AEM as a Cloud Service.

Consulte los recursos de autoayuda sobre cómo configurar e implementar en AEM entornos as a Cloud Service.

1. [Configuración de canalizaciones de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * Canalización de producción
   * Canalizaciones de calidad de código y no producción
2. [Implementar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [Comprender los resultados de la prueba](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **Acceso a registros**
   * [a través de la interfaz de usuario de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [a través de i/o cli de Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operaciones y mantenimiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [Configuración de OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [Copia de seguridad y restauración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> Consulte el tutorial sobre cómo [Implementar WKND en el Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Ayuda y recursos

1. [Consejos y sugerencias para la depuración](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (Solo disponible en los entornos SDK local y Experience Manager Cloud Dev)
4. [Registros y registro](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Registros de CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (build-unit-testing, code-scan, build-image, deploy)
   * [Registros del Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registros de SDK locales (en host:port/crx-quickstart/logs)

>[!NOTE]
> Para obtener más ayuda, es posible que desee:
>1. [Póngase en contacto con el equipo de asistencia al Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Migración a Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Migración a Adobe Experience Manager as a Cloud Service"
>abstract="Este paginador único describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager hasta as a Cloud Service de Experience Manager y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas en esta plataforma moderna y diseñada para la administración de experiencias."

**Experience Manager as a Cloud Service proporciona una base tecnológica escalable, segura y ágil para Experience Manager Sites y Assets, lo que permite a los especialistas en marketing y TI centrarse en ofrecer experiencias impactantes a escala.**

Con el as a Cloud Service Experience Manager, sus equipos pueden centrarse en la innovación en lugar de planificar las actualizaciones de productos. Las nuevas funciones del producto se prueban a fondo y se entregan a sus equipos sin interrupciones para que siempre tengan acceso a la aplicación más avanzada.

El viaje de transición a Cloud Service incluye tres fases: Planificación, Ejecución y Publicación de Go-live.
Para una transición exitosa y sin problemas, se debe asegurar una planificación adecuada y atenerse a las prácticas recomendadas descritas en esta guía.

En la figura siguiente se muestra una representación de alto nivel del recorrido de transición recomendado al Cloud Service.

![imagen](/help/journey-migration/assets/home-img1.png)

<br>

### Planificación

Antes de comenzar el recorrido de transición a Cloud Service, debe familiarizarse con el Experience Manager as a Cloud Service, revisar los cambios importantes que se le han realizado y también las funciones que se han sustituido o dejado de utilizar.

<table>
<tr>
<td>Descubrimiento y evaluación de proyectos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=es">Cambios importantes en el Experience Manager as a Cloud Service</a> para comprender las diferencias importantes entre Adobe Experience Manager as a Cloud Service y Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">Funciones obsoletas</a> para obtener más información sobre las funciones y capacidades que se han marcado como obsoletas.</li><li>[Solo para migraciones de Cloud Service] Evaluación de la preparación del Cloud Service : Ejecute el <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Analizador de prácticas recomendadas (BPA)</a> en el entorno de origen </li><li>Lleve a cabo una evaluación de los cambios más importantes y las funciones obsoletas en el Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Revisión</td>
<td><ul><li>En función del descubrimiento, realice ejercicios de estimación de esfuerzo y asignación de recursos</li></ul></td>
</tr>
<tr>
<td>Medida</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Establecimiento de KPI de proyecto</a>, criterios de éxito y cronologías del proyecto</li></ul></td>
</tr>
</table>

>[!NOTE]
>El informe de Best Practices Analyzer acelera el proceso de estimación del tiempo y el costo necesarios para realizar la transición a AEM as a Cloud Service al proporcionar información que de otra manera tendría que recopilarse y evaluarse manualmente.


<br>

### Ejecución

Antes de iniciar la fase de ejecución de un proyecto, debe estar integrado en Cloud Service. También debe familiarizarse con Cloud Manager. Este es el mecanismo para implementar el código de proyecto en una instancia de Experience Manager Cloud Service.

Cloud Manager permite a las organizaciones administrar su Experience Manager en la nube. Incluye una integración continua y un envío continuo ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en)) que permite a los equipos de TI y a los socios de implementación acelerar la entrega de personalizaciones o actualizaciones sin comprometer el rendimiento o la seguridad.

#### Migración de contenido

1. [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) : se utiliza para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de AEM Cloud Service de destino.
2. [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) : se utiliza para importar y exportar contenido mutable del repositorio.


#### Refactorizar/Optimizar

| Introducción | Revisar y refactorizar código | Revisión de Dispatcher |
|---|---|---|
| <ul><li>[Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Configuración de Dispatcher local](https://video.tv.adobe.com/v/30602/)</li><li>[Compile su código con el SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Revisar AEM directrices para desarrolladores](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>Tareas en segundo plano y trabajos de larga duración</li><li>Programadores de Sling</li><li>Uso del flujo de entrada y más</li></ul></li></ul> | <ul><li>Ejecute el [Analizador de prácticas recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) en el entorno de origen.[**Solo migración**]<ul><li>Consideraciones sobre la estructura del proyecto (basadas en [Tipo de archivo de la nube](https://github.com/adobe/aem-project-archetype))<ul><li>Separación de código y contenido (mutable vs. inmutable)</li><li>[Definiciones de índice personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[Modos de ejecución personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>Revisar y ejecutar los cambios necesarios</li><li>[Implementación](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) it en el SDK local</li><li>Realizar pruebas de humo mediante AEM SDK</li></ul> | <ul><li>Consulte [Configuraciones de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) para refactorización</li><li>Uso [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) cuando proceda. [**Solo migración**]</li><li>Las pruebas se pueden realizar utilizando [SDK de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clientes de Assets : Revisar y refactorizar flujos de trabajo de recursos mediante [Migración de Asset Cloud](https://github.com/adobe/aem-cloud-migration) herramientas


#### Implementación/Go-Live

1. [Implementar en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) git
2. Ejecute el código de cliente mediante la variable [Canalización de calidad de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [Implementar en entorno de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Solo migración**] Transferencia de contenido mediante paquetes o [Herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Realizar ciclos de prueba recomendados (humo, control de calidad y más)
6. Enviar a la canalización de producción de Cloud Manager
7. Validación de prueba de humo
8. Go-Live

<br>

### Publicar Go-Live

En la fase de Publicar Go-live, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

>[!TIP]
> Las herramientas están disponibles para solucionar problemas AEM entorno as a Cloud Service
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [Administración de registros](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)


<br>

### Herramientas y recursos

| Evaluación | Refactorización | Modernización del Experience Manager | Migración de contenido |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Complemento de experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[Plantillas estáticas a plantillas editables.](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Diseño de las configuraciones para directivas.](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componentes básicos a principales](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[De IU clásica a IU táctil.](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es)</li><li>[el administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es#contentmanagement)</li></ul> |

>[!NOTE]
> Para obtener más ayuda, es posible que desee:
>1. [Póngase en contacto con el equipo de asistencia al Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

