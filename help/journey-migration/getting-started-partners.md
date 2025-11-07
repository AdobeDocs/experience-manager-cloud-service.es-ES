---
title: Guía de migración de Experience Manager as a Cloud Service para socios
description: Guía de migración de Experience Manager as a Cloud Service para socios
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 18%

---

# Guía de migración de Adobe Experience Manager as a Cloud Service para socios {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migración a AEM as a Cloud Service"
>abstract="Describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager a Experience Manager as a Cloud Service y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=es" text="¿Qué hay de nuevo y diferente?"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=es" text="Introducción a AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service ofrece una arquitectura actualizada para Experience Manager. Esta base se basa en una infraestructura basada en contenedores, un desarrollo impulsado por API y un proceso de DevOps guiado. Esto permite a los especialistas en marketing y a los desarrolladores adelantarse a la curva en las innovaciones de la administración de experiencias del cliente.

Cloud Service aúna las abundantes funciones y extensibilidad integradas de Adobe Experience Manager con la agilidad de la moderna arquitectura nativa de la nube, lo que permite a las marcas satisfacer la demanda de los consumidores, que evoluciona constantemente.

Esta página describe el enfoque por fases recomendado para realizar la transición de clientes de implementaciones anteriores de Experience Manager a as a Cloud Service de Experience Manager. La nueva plataforma diseñada específicamente le ayuda a ofrecer experiencias conectadas y continuas.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Consulte el diagrama siguiente para obtener una representación general del recorrido de migración.

![Representación general del recorrido de migración](/help/journey-migration/assets/migration-process.png)

## Introducción a Adobe Experience Manager as a Cloud Service {#getting-started}

| ¿Qué hay de diferente? | Información general sobre la arquitectura |
|--------------------------|--------------------------|
| <ul><li>[Arquitectura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=es)</li><li>[Actualizaciones automáticas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=es)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es)</li><li>[Microservicios de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=es)</li><li>[Binarios de acceso directo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=es)</li><li>[Separación de código y contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es)</li><li>[Replicación como servicio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=es)</li><li>[Admin Console, pertenencia a grupos/usuarios y ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es)</li></ul> | <ul><li>[Introducción a la arquitectura de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=es#underlying-technology)</li><li>[Pila de entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=es)</li><li>[Nivel de autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=es#underlying-technology)</li><li>[Publicar nivel](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=es#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=es) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=es) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es) mediante [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es)</li><li>[Servicio de Asset Compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=es)</li></ul> |

![AEM as a Cloud Service: arquitectura del tiempo de ejecución](/help/overview/assets/concepts-03.png "AEM as a Cloud Service: arquitectura del tiempo de ejecución")

<br>

## Recorrido de desarrollador en Adobe Experience Manager as a Cloud Service {#developer-journey}

### Desarrollo

Los aspectos básicos del desarrollo de código en Adobe Experience Manager as a Cloud Service son similares a los de las soluciones Adobe Experience Manager On Premise y Managed Services.

Los desarrolladores escriben código y lo prueban localmente y luego lo envían a entornos remotos de Adobe Experience Manager as a Cloud Service.

Consulte los recursos informativos sobre la implementación para Experience Manager as a Cloud Service para obtener información sobre cómo personalizar la implementación de Experience Manager as a Cloud Service.

| Configuración de desarrollo local | Cosas que hay que saber antes de empezar |
|-----------|------------|
| <ol><li>Revise la documentación de [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=es) para obtener más información.</li><li>Vea [Instalar Dispatcher SDK](https://video.tv.adobe.com/v/30601) para comprender cómo instalar Dispatcher SDK</li><li>Vea [Configurar Dispatcher SDK](https://video.tv.adobe.com/v/33692?captions=spa) para comprender cómo configurar Dispatcher SDK</li><li>Revise la documentación de [Configuración de desarrollo local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es#local-development-environment-set-up) para obtener más información</li><li>Configurando el acceso a Experience Manager [guía](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=es#accessing)</li></ol> | <ol><li>[Aspectos básicos del desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=es)</li><li>[Directrices de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es)</li><li>[Explicación de la estructura del proyecto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=es)</li><li>[Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)</li><li>[Modelo de Digital Foundation](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=es)</li><li>[Superposiciones](/help/implementing/developing/introduction/overlays.md)</li><li>[Referencia de la API de Experience Manager as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Ver tutorial sobre cómo [desarrollar e implementar WKND en Experience Manager SDK local](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Implementación

Los desarrolladores escriben código y lo prueban localmente y luego lo envían a entornos remotos de AEM as a Cloud Service.

Ahora se requiere Cloud Manager, que era una herramienta de entrega de contenido opcional para Managed Services. Es el único mecanismo para implementar código en entornos de AEM as a Cloud Service.

Consulte recursos informativos sobre cómo configurar e implementar en entornos de AEM as a Cloud Service.

1. [Configurar canalizaciones de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=es)

   * Canalización de producción
   * Canalizaciones de no producción y de solo calidad de código

1. [Implementar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es)
1. [Comprender los resultados de la prueba](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=es)
1. **Acceder a registros**

   * [mediante la interfaz de usuario de CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=es)
   * [a través de Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=es#debugging)

1. [Operaciones y mantenimiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=es)

   * [Configurando la configuración de OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=es)
   * [Copia de seguridad y restauración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=es)

>[!TIP]
> Ver tutorial sobre cómo [implementar WKND en Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es)

### Ayuda y recursos

1. [Sugerencias y trucos para la depuración](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=es#debugging-aem-as-a-cloud-service)
1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=es#debugging)
1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=es) (solo disponible en los entornos locales de desarrollo de SDK y Experience Manager Cloud)
1. [Registros y registros](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=es#debugging)

   * [Registros de CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=es#debugging) (build-unit-testing, digitalización de código, build-image, deploy)
   * [Registros de Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=es#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registros de SDK locales (en host:port/crx-quickstart/logs)

>[!NOTE]
>
> Para obtener ayuda adicional, es posible que desee:
>
>1. [Póngase en contacto con el equipo de soporte técnico de Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=es)
>1. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=es)

<br>

## Traslado a Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Traslado a Adobe Experience Manager as a Cloud Service"
>abstract="Este breve informe describe el enfoque por fases recomendado para los clientes de transición desde varias implementaciones de Experience Manager a Experience Manager as a Cloud Service y ayuda a los clientes existentes a ofrecer experiencias continuas y conectadas en esta plataforma moderna y diseñada para la administración de experiencias."

**Experience Manager as a Cloud Service proporciona una base tecnológica escalable, segura y ágil para Experience Manager Sites y Assets, lo que permite a los especialistas en marketing y TI centrarse en ofrecer experiencias impactantes a escala.**

Con Experience Manager as a Cloud Service, sus equipos pueden centrarse en la innovación en lugar de planificar las actualizaciones de los productos. Las nuevas funciones del producto se prueban a fondo y se entregan a sus equipos sin ninguna interrupción para que siempre tengan acceso a la aplicación más avanzada.

El recorrido de transición a Cloud Service consta de tres fases: Planificación, Ejecución y Publicación de Go-live.
Para una transición exitosa y sin problemas, se debe asegurar una planificación adecuada y atenerse a las prácticas recomendadas descritas en esta guía.

La figura siguiente muestra una representación de alto nivel del recorrido de transición recomendado para Cloud Service.

![Representación de alto nivel del recorrido de transición recomendado para Cloud Service](/help/journey-migration/assets/home-img1.png)

<br>

### Planificación

Antes de comenzar el recorrido de transición a Cloud Service, debe hacer lo siguiente:

* familiarícese con Experience Manager as a Cloud Service
* revise los cambios importantes que se le han realizado
* revise las funciones que se han sustituido o que están en desuso

<table>
<tr>
<td>Descubrimiento y evaluación de proyectos</td>
<td><ul><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=es">Cambios importantes en Experience Manager as a Cloud Service</a> para comprender las diferencias importantes entre Adobe Experience Manager as a Cloud Service y Experience Manager 6.x.</li><li>Consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=es">Características obsoletas</a> para obtener más información sobre las características y capacidades que se han marcado como obsoletas.</li><li>[Solo para migraciones de Cloud Service] Evaluación de la preparación de Cloud Service : ejecute el <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es">Analizador de prácticas recomendadas (BPA)</a> en el entorno de origen </li><li>Complete una evaluación de los cambios más importantes y las funciones obsoletas de Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Revisión</td>
<td><ul><li>En función del descubrimiento, realice ejercicios de estimación de esfuerzo y recursos</li></ul></td>
</tr>
<tr>
<td>Medida</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Establecer KPI de proyecto</a>, criterios de éxito y escalas de tiempo de proyecto</li></ul></td>
</tr>
</table>

>[!NOTE]
>El informe del Analizador de prácticas recomendadas acelera el proceso de estimación del tiempo y el coste necesarios para realizar la transición a AEM as a Cloud Service al proporcionar información que, de lo contrario, tendría que recopilarse y evaluarse manualmente.


<br>

### Ejecución

Antes de iniciar la fase de ejecución de un proyecto, debe estar integrado en Cloud Service. También debe familiarizarse con Cloud Manager. Este es el mecanismo para implementar el código de proyecto en una instancia de Experience Manager Cloud Service.

Cloud Manager permite a las organizaciones autoadministrar Experience Manager en la nube. Incluye un marco de trabajo de integración y entrega continuas ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=es)) que permite a los equipos de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

#### Migración de contenido

1. [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=es#migration) : utilizada para mover contenido existente de una instancia de AEM de origen (local o AMS) a la instancia de Cloud Service de AEM de destino.
1. [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es#package-manager) : se usa para importar y exportar contenido mutable del repositorio.


#### Refactorizar/optimizar

| Introducción | Revisar y refactorizar código | Revisión de Dispatcher |
|---|---|---|
| <ul><li>[Configuración de desarrolladores locales](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=es#local-development-environment-set-up)</li><li>[Configuración local de Dispatcher](https://video.tv.adobe.com/v/33692?captions=spa)</li><li>[Compile su código utilizando el JAR de la API de SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=es)</li><li>[Revisar las directrices de desarrollo de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es)<ul><li>Tareas de fondo y trabajos de larga duración</li><li>Planificadores de Sling</li><li>Uso del flujo de entrada y más</li></ul></li></ul> | <ul><li>Ejecute el [Analizador de prácticas recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es) en el entorno de origen.[**Solo migración**]<ul><li>Consideraciones sobre la estructura del proyecto (basadas en [arquetipo de nube](https://github.com/adobe/aem-project-archetype))<ul><li>Separación de código y contenido (mutable e inmutable)</li><li>[Definiciones de índice personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=es)</li><li>[Modos de ejecución personalizados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=es)</li></ul></li></ul></li><li>Revisar y ejecutar los cambios necesarios</li><li>[Implementarlo](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es) en SDK local</li><li>Realizar pruebas de humo a través de AEM SDK</li></ul> | <ul><li>Revise [configuraciones de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=es) para la refactorización</li><li>Utilice la herramienta [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=es) donde corresponda. [**Solo migración**]</li><li>Las pruebas se pueden realizar con [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=es#prerequisites)</li></ul> |

>[!TIP]
> Clientes de Assets: revise y refactorice los flujos de trabajo de Assets con las herramientas de [Migración de Asset Cloud](https://github.com/adobe/aem-cloud-migration)


#### Implementación/lanzamiento

1. [Implementar en Git de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=es)
2. Ejecutar código de cliente a través de [Cloud Manager Quality Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=es)
3. [Implementar en el entorno de desarrollo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=es#debugging)
4. **Solo migración** Transferencia de contenido mediante paquetes o [Herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Realizar ciclos de prueba recomendados (humo, control de calidad y más)
6. Enviar a la canalización de producción de Cloud Manager
7. Validación de prueba de humo
8. Go-Live

<br>

### Publicar Go-Live

En la fase de Publicar Go-live, se debe garantizar la limpieza de los archivos temporales, revisar las prácticas recomendadas para el desarrollo continuo y administrar los registros.

>[!TIP]
>
> Hay herramientas disponibles para solucionar problemas del entorno de AEM as a Cloud Service
>
>1. [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es)
>1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=es)
>1. [Administración de registros](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=es)

<br>

### Herramientas y recursos

| Evaluación | Refactorización | Modernización de Experience Manager | Migración de contenido |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es)</li></li> | <ul><li>[Complemento de experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=es)</li></ul> | <ul><li>[Plantillas estáticas a plantillas editables](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Diseñar configuraciones para directivas](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componentes básicos a componentes principales](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[IU clásica a IU táctil](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es)</li><li>[Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es#contentmanagement)</li></ul> |

>[!NOTE]
>
> Para obtener ayuda adicional, es posible que desee:
>
>1. [Póngase en contacto con el equipo de soporte técnico de Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=es)
>1. Explorar [Comunidades y foros de Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?profile.language=es)
