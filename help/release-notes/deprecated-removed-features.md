---
title: Funciones en desuso y eliminadas
description: Notas de versión específicas de las funciones en desuso y eliminadas de  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
mini-toc-levels: 1
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 90b1730522494cda0e777ecc0171703c2b2eff5b
workflow-type: tm+mt
source-wordcount: '3697'
ht-degree: 85%

---

# Funciones y API obsoletas y eliminadas {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funciones en desuso y eliminadas en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service tiene un modelo de implementación nativo de la nube. Esta pestaña resalta las funciones y capacidades reemplazadas por sus homólogos nativos de la nube."

Adobe revisa regularmente las funciones, incluidas las API y las configuraciones, para asegurarse de que cumplan los estándares de evolución en cuanto a rendimiento, seguridad y valor general de AEM as a Cloud Service. En función de estas evaluaciones, ciertas funciones pueden estar marcadas para su entrada en desuso. Cuando sea posible, Adobe proporcionará un reemplazo adecuado.

Cuando se anuncia un desuso, la función solo permanece disponible durante un período de tiempo limitado y los clientes deberán concluir todo uso antes de la fecha de eliminación especificada. Adobe proporciona un aviso y una guía razonables para facilitar una transición sin problemas.

Durante el plazo de tiempo hasta la entrada en desuso, Adobe recordará a los clientes las acciones que deben realizar para dejar de utilizar una función mediante notificaciones por correo electrónico, alertas del Centro de acciones o recordatorios en Cloud Manager.

>[!WARNING]
>
>En algunos casos, es posible que se requiera la eliminación de una función antes de implementar una nueva compilación de Cloud Manager o de actualizar a la versión más reciente de AEM as a Cloud Service.

>[!IMPORTANT]
>  Varias [API obsoletas](#aem-apis) están planeando la eliminación el **26 de febrero de 2026**. Revise estas fechas e impactos clave:
>
> * **A partir del 26 de enero de 2026**: los correos electrónicos de notificación del Centro de acciones se envían **semanalmente por entorno** como recordatorio para eliminar el uso de estas API.
> * **26 de febrero de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **se pausarán** durante el paso **Calidad del código**. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular el problema para permitir que continúe la canalización.
> * **26 de marzo de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **fallarán** durante el paso de **Calidad del código**, **bloqueando implementaciones** de nuevo código hasta que se elimine el uso.
> * **30 de abril de 2026**: Es posible que los entornos que aún usan estas API **ya no reciban actualizaciones críticas de la versión de Adobe**.
>
> Para evitar bloques de implementación, elimine el uso de la API antes del 26 de marzo de 2026.

## Funcionalidad en desuso {#deprecated-features}

Se ha anunciado que la funcionalidad de la tabla siguiente ya no se utiliza, pero aún no se ha eliminado. El uso de la funcionalidad debe interrumpirse antes de la fecha de eliminación objetivo o se corre el riesgo de que se produzcan problemas relacionados con el rendimiento, la disponibilidad y la seguridad.

| Capacidades | Función en desuso | Reemplazo |
| ------------ | ------------------ | ----------- |
| Sites | [Compatibilidad con fragmentos de contenido en la API HTTP de Assets](/help/assets/content-fragments/assets-api-content-fragments.md) | [Envío de fragmentos de contenido con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)<br>junto con<br> [Fragmentos de contenido y OpenAPI de administración de modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md) |
| Sites | [Características de PWA](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | Ninguno |
| Sites | [Editor de SPA](/help/implementing/developing/hybrid/introduction.md) | Los editores preferidos para administrar el contenido sin encabezado en AEM son: <br> el [Editor universal](https://www.aem.live/docs/aem-authoring) para la edición visual.<br>- [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios. |
| [!DNL Sites] | [API de uso de JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [API de uso de Java](https://experienceleague.adobe.com/es/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. | Está previsto eliminar esta función en breve. |
| Sites | [Automatización de la configuración de Experience Cloud](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | Ninguno |
| [!DNL Sites] | Fragmentos de contenido simples basados en plantillas. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. |
| [!DNL Assets] | `DAM Asset Update` flujo de trabajo para procesar imágenes grabadas. | Ahora, la ingesta de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos. |
| [!DNL Assets] | Cargar recursos directamente en [!DNL Experience Manager]. Consulte [API de carga de recursos en desuso](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilice la [carga binaria directa](/help/assets/add-assets.md). Para obtener más información técnica, consulte [API de carga directa](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | No se admiten [determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) en el flujo de trabajo `DAM Asset Update`, incluida la llamada a herramientas de línea de comandos como [!DNL ImageMagick]. | [Los microservicios de recursos](/help/assets/asset-microservices-overview.md) sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | FFmpeg transcodificar vídeos. | Para la generación de miniaturas de FFmpeg, use los [microservicios de Asset](/help/assets/asset-microservices-overview.md). Para la transcodificación FFmpeg, utilice [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | IU de replicación del árbol en la pestaña de agentes de replicación &quot;Distribuir&quot; (eliminación después del 30 de septiembre de 2021) | Enfoques [Administrar publicación](/help/operations/replication.md#manage-publication) o [Paso de flujo de trabajo de activación de árbol](/help/operations/replication.md#tree-activation). |
| [!DNL Foundation] | La pestaña Distribuir de la pantalla del administrador del agente de replicación y la API de replicación no pueden replicar paquetes de contenido de más de 10 MB. | [Administrar publicación](/help/operations/replication.md#manage-publication) o [Paso de flujo de trabajo de activación de árbol](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | Las integraciones que utilizan credenciales generadas a partir de proyectos de Adobe Developer Console perderán gradualmente la compatibilidad con las credenciales de la cuenta de servicio (JWT). Desde el 1 de mayo de 2024, no se pueden crear nuevas credenciales de cuenta de servicio (JWT) en Adobe Developer Console. Las credenciales de la cuenta de servicio (JWT) existentes se pueden utilizar para las integraciones configuradas hasta el 1 de enero de 2025, después de lo cual dejan de funcionar y es necesario que los clientes migren a las credenciales de servidor a servidor de OAuth. [Más información](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrar](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview) a las credenciales de servidor a servidor de OAuth. |
| [!DNL Foundation] | Flujo de trabajo Publicar árbol de contenido y el paso de flujo de trabajo Publicar árbol de contenido relacionado, que se utilizaba para replicaciones de jerarquías de contenido. | Utilizar [Paso del flujo de trabajo de activación de árbol](/help/operations/replication.md#tree-activation), que es más eficaz. |
| [!DNL Foundation] | Usar YUI para comprimir o minimizar las bibliotecas de cliente de JavaScript. Adobe no tiene previsto actualizar ya más la biblioteca de YUI. | Adobe recomienda a los clientes cambiar a Google Closure Compiler (GCC) para su implementación. |

## Funcionalidad eliminada {#removed-features}

Esta sección enumera las funcionalidades que se han eliminado.

| Área | Característica | Reemplazo | Fecha de eliminación objetivo |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaz de usuario | La IU clásica se elimina de la interfaz de usuario del producto. Hay algunos cuadros de diálogo de IU clásica disponibles para algunas funciones seleccionadas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de Cloud Service. Próximas [actualizaciones de productos](/help/release-notes/home.md) pueden eliminar aún más la disponibilidad de la IU clásica. | IU estándar | Eliminado |
| [!DNL Dynamic Media] | Las integraciones anteriores con [Dynamic Media Classic](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) y el [modo híbrido de Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic) no están disponibles en [!DNL Experience Manager] as a [!DNL Cloud Service]. | Utilice [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) proporcionado con [!DNL Experience Manager] as a [!DNL Cloud Service]. | Eliminado |
| [!DNL Sites] | Portal Director y componentes Portlet | Estas funciones quedaron obsoletas en [!DNL Experience Manager] 6.4 y ahora se han eliminado de [!DNL Experience Manager]. | Eliminado |
| [!DNL Sites] | Importador de diseños | Esta capacidad se ha eliminado porque no se puede acceder a las secciones inmutables del repositorio de [!DNL Experience Manager] durante la ejecución. | Eliminado |
| [!DNL Assets] | [!DNL Assets]El uso compartido con los servicios de Assets Core Service y Creative Cloud no está disponible. | Para la integración con [!DNL Adobe Creative Cloud], utilice [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html). | Eliminado |
| [!DNL Foundation] | Compatibilidad con fuentes de datos de Apache Sling (paquete OSGi org.apache.sling.datasource) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con plantillas de scripts JST (paquete OSGi org.apache.sling.scripting.jst) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con la pizarra Apache Felix Http | Pizarra Http OSGi | Marzo de 2022 |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de IMS de Adobe | Marzo de 2023 |
| [!DNL Foundation] | Compatibilidad con la función org.apache.sling.serviceusermapping para [obtener el id de usuario del servicio](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | N/D | 30/08/24 |
| [!DNL Foundation] | El tiempo de ejecución de Java 11 ya no se utiliza y Adobe lo ha sustituido por el tiempo de ejecución de Java 21. Tenga en cuenta que se puede seguir creando código con Java 11 (Java 17 y 21 son las otras opciones) | Se aplica el tiempo de ejecución de Java 21. Para garantizar la compatibilidad, es esencial actualizar las versiones de la biblioteca tal como se describe en [Requisitos de tiempo de ejecución](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements) | 5 a 29 de marzo de 2025 |

## API obsoletas {#aem-apis}

Se ha anunciado que las API de la tabla siguiente (haga clic para ampliar y verlas) ya no se utilizan, pero aún no se han eliminado.  El uso de estas API debe interrumpirse antes de la fecha de eliminación objetivo o se corre el riesgo de que se produzcan problemas relacionados con el rendimiento, la disponibilidad y la seguridad. Algunas API hacen referencia a la sección Guía de eliminación de API que aparece a continuación.

>[!IMPORTANT]
> Se ha programado la eliminación de varias API el **26 de febrero de 2026**. Revise estas fechas e impactos clave:
>
> * **A partir del 26 de enero de 2026**: los correos electrónicos de notificación del Centro de acciones se envían **semanalmente por entorno** como recordatorio para eliminar el uso de estas API.
> * **26 de febrero de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **se pausarán** durante el paso **Calidad del código**. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular el problema para permitir que continúe la canalización.
> * **26 de marzo de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **fallarán** durante el paso de **Calidad del código**, **bloqueando implementaciones** de nuevo código hasta que se elimine el uso.
> * **30 de abril de 2026**: Es posible que los entornos que aún usan estas API **ya no reciban actualizaciones críticas de la versión de Adobe**.
>
> Para evitar bloques de implementación, elimine el uso de la API antes del 26 de marzo de 2026.


<details>
  <summary>Amplíe para ver la lista de API obsoletas.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Paquete/Clase</th>
    <th>Comentarios</th>
    <th>Fecha de desuso</th>
    <th>Fecha de eliminación objetivo</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>Use las interfaces Auth Core/Auth Core SPI de Sling como alternativa. <a href="#org.apache.sling.commons.auth">Consulte las notas de eliminación a continuación.</a></td>
    <td>2015</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>Los paquetes Eclipse Jetty y Felix Http Jetty ya no se admiten. <a href="#org.eclipse.jetty">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/5/2021</td>
    <td>26/2/2026</td>
  </tr>
 <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>El uso de esta API no se admite en AEM as a Cloud Service. <a href="#com.mongodb">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/5/2021</td>
    <td>26/2/2026</td>
  </tr>
   <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte las notas de eliminación a continuación.</a></td>
    <td>29/7/2021</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte las notas de eliminación a continuación.</a></td>
    <td>8/4/2019</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>La pizarra Apache Felix Http ya no es compatible. Migre su código a la pizarra Http OSGi. <a href="#org.apache.felix.http.whiteboard">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/1/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Esta API está obsoleta. Esta API está en desuso. Migre su código a las API de XML proporcionadas por el JDK.</td>
    <td>27/1/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service no admite esta API interna de registro. <a href="#ch.qos.logback">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/1/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service no admite esta API interna de log4j. <a href="#org.slf4j">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/1/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 ha llegado al fin de su vida útil en 2015 y ya no es compatible. <a href="#org.apache.log4j">Consulte las notas de eliminación a continuación.</a></td>
    <td>27/1/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>  <td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Las bibliotecas principales de Google Guava están en desuso en Cloud Service. <a href="#com.google.common">Consulte las notas de eliminación a continuación.</a></td>
    <td>15/5/2023</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>AEM as a Cloud Service no admite esta API interna de slf4j. <a href="#org.slf4j">Consulte las notas de eliminación a continuación.</a></td>
    <td>11/4/2022</td>
    <td>26/2/2026</td>
  </tr>
    <tr>
    <td>com.drew.*</td>
    <td>La extracción de metadatos de imágenes y vídeos debe realizarse mediante Asset Compute en Cloud Service, o mediante Apache POI o Apache Tika.</td>
    <td>17/9/2024</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td>Esta API es solo para uso interno.</td>
    <td>23/9/2024</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>Esta API es solo para uso interno.</td>
    <td>23/9/2024</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
<td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>La consola web de Felix no es compatible con entornos de nube. <a href="#org.apache.felix.webconsole">Consulte las notas de eliminación a continuación.</a></td>
    <td>30/4/2021</td>
    <td>26/2/2026</td>
  </tr>
<td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>El uso de esta API no se admite en AEM as a Cloud Service.</td>
    <td>31/10/2022</td>
    <td>26/2/2026</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>Por determinar</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>La implementación de Apache Johnzon de <a href="https://johnzon.apache.org/index.html">javax.json</a> se recomienda y debe utilizarse. </td>
    <td>30/4/2021</td>
    <td>Por determinar</td>
  </tr>
  <tr>
<td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 está en modo de mantenimiento. Debe utilizarse Commons Lang 3 en su lugar. <a href="#apache.commons">Consulte las notas de eliminación a continuación.</a></td>
    <td>30/4/2021</td>
    <td>Por determinar</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 está en modo de mantenimiento. Debe utilizarse Commons Collections 4 en su lugar. <a href="#apache.commons">Consulte las notas de eliminación a continuación.</a></td>
    <td>30/4/2021</td>
    <td>Por determinar</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Esta API está obsoleta. En su lugar, utilice los generadores de Apache Sling.</td>
    <td>31/10/2022</td>
    <td>Por determinar</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service no admite esta API.</td>
    <td>15/5/2023</td>
    <td>Por determinar</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>En su lugar, utilice org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>Por determinar</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>En su lugar, utilice org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>Por determinar</td>
  </tr>
  </tbody>
</table>
</details>

## API eliminadas {#removed-apis}

Esta sección enumera las API que ya no se utilizan y se han eliminado. Algunas API hacen referencia a la sección Guía de eliminación de API que aparece a continuación.

<details>
  <summary>Amplíe para ver la lista de API que se han quitado.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Paquete/Clase</th>
    <th>Comentarios</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Uso de la API Discovery de Sling como alternativa</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Los administradores de persistencia personalizados no son compatibles con AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Se recomienda utilizar la API Apache Felix HealthCheck en su lugar</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Los paquetes Eclipse Jetty y Felix Http Jetty ya no se admiten.</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Las API Apache Felix metatype y SCR están en desuso.  Utilice en su lugar las API OSGi metatype y Declarative Service.</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>Las clases de implementación de registros no son compatibles con AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>API heredada AEM 6.x.</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Esta API no se admite en Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Las clases de utilidad relacionadas con Apache Xerces se eliminan en las versiones posteriores, lo que provoca un cambio de versión importante. Como estas utilidades son de uso interno en Filevault, la API está quedando en desuso en la superficie de la API pública.</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>API heredada AEM 6.x. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte las notas de eliminación a continuación.</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service no admite esta API interna de registro.</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>Se requiere la actualización de Handlebars de 4.0.5 a 4.3.0 debido a una vulnerabilidad de seguridad. Este paquete ya no está presente en los controladores actualizados.</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Esta API ya no es compatible. En su lugar, utilice org.apache.sling.api.resource.ResourceResolverFactory.</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>El uso de esta API no se admite en AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>Esta API es solo para uso interno.</td>
  </tr>
</tbody>
</table>
</details>

## Guía de eliminación de API {#api-removal-guidance}

Esta sección presenta la guía de eliminación de API para las diversas API incluidas en las tablas anteriores.

Para identificar qué API de Java en desuso usa su código, integre el [complemento Maven de AEM as a Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) en su proyecto Maven y ejecútelo localmente. El informe enumera todos los usos de API obsoletos detectados e indica qué paquete OSGi hace referencia a cada API.

Aunque debe corregir todas las API obsoletas con el tiempo, dé prioridad a cualquier API enumerada en la tabla de API obsoletas con una fecha de eliminación objetivo del 26 de febrero de 2026 (o anterior). En el informe de AEM Analyzer, estas API pueden aparecer con una fecha de eliminación efectiva del 31/8/2025.

Después de actualizar el código, compruebe que no queda ningún uso obsoleto de la API en Cloud Manager comprobando los resultados del paso de calidad del código.

### Directrices generales

Si utiliza una biblioteca de terceros que actualmente requiere una API obsoleta, intente actualizar a una versión más reciente de esa biblioteca de terceros.

Si usa ACS AEM Commons, use al menos la versión 6.11.0 (se recomienda la versión más reciente) y asegúrese de [incluir la versión de Cloud Service](https://adobe-consulting-services.github.io/acs-aem-commons/pages/maven.html) especificando el clasificador `cloud` para el paquete de contenido.

Si la importación de una API obsoleta está marcada como `optional`, debe intentar eliminarla. Sin embargo, este uso opcional no bloqueará las implementaciones. Sin embargo, su implementación podría verse afectada, una vez que la importación opcional ya no se cumpla.

### Eliminación de `org.apache.sling.commons.auth*`  {#org.apache.sling.commons.auth}

Si usa `org.apache.sling.commons.auth` o `org.apache.sling.commons.auth.spi` o ambos, el uso se puede reemplazar migrando el código a `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:

* Actualizar ACS AEM Commons a la versión más reciente (6.11.0 como mínimo)
* Migrar de `org.apache.sling.commons.auth` o `org.apache.sling.commons.auth.spi` a `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`.

### Eliminación de `org.apache.felix.webconsole*` {#org.apache.felix.webconsole}

Si está usando paquetes de `org.apache.felix.webconsole*`, quite este código del proyecto. No se puede acceder a la consola web desde Cloud Service.

Lista de acciones:

* Quitar código utilizando paquetes de `org.apache.felix.webconsole*`

### Eliminación de `org.eclipse.jetty*` {#org.eclipse.jetty}

Si utiliza cualquier elemento del paquete `org.eclipse.jetty` o de uno de sus subpaquetes, es posible que desee migrar a otras bibliotecas de terceros cuya funcionalidad sea similar. Si la migración no es factible, añada los paquetes requeridos de la siguiente lista a su proyecto.

Lista de acciones:

* Reemplazar el uso de paquetes de `org.eclipse.jetty` con otras bibliotecas de terceros/código propio o 
* Seleccionar los paquetes necesarios de esta lista y añadirlos al proyecto:
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### Eliminación de `com.mongodb` {#com.mongodb}

Añadir la API del cliente Mongo al proyecto.

Lista de acciones:

* Añadir este paquete al proyecto
   * `org.mongodb:mongo-java-driver:3.12.7`

Es posible que desee elegir una versión diferente, según sus necesidades.

### Eliminación de `com.google.common*` {#com.google.common}

Elimine el uso de las bibliotecas principales de Google Guava o incluya una versión adecuada en su proyecto. En muchos casos, el uso de esta biblioteca se puede reemplazar con clases de colección de JDK o Apache Commons Collections4. Si no encuentra ningún reemplazo, incluya la versión más reciente de la biblioteca principal de Google Guave en su proyecto. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:

* Actualizar ACS AEM Commons a la versión más reciente (6.11.0 como mínimo)
* Reemplace el uso de la biblioteca principal de Google Guava con colecciones JDK o Apache Commons Collections4
* Si sigue siendo necesario, añada este paquete al proyecto (sustituya la versión por la más reciente disponible):
   * `com.google.guava:guava:33.4.8-jre`

### Eliminación de `Apache Commons Lang 2 and Apache Commons Collections 3` {#apache.commons}

Elimine el uso de las bibliotecas de Apache Commons no mantenidas y reemplace su uso por el de versiones compatibles. En la mayoría de los casos, esto simplemente requiere ajustar las importaciones de paquetes, solo en algunos casos se les ha cambiado el nombre a clases o métodos. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:

* Actualizar ACS AEM Commons a la versión más reciente (6.11.0 como mínimo)
* Reemplazar importaciones de `org.apache.commons.lang*` por `org.apache.commons.lang3`
* Reemplazar importaciones de `org.apache.commons.collections*` por `org.apache.commons.collecitons4`

### Uso de `org.apache.abdera*` y `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

Reemplazar el uso de cualquier paquete de `org.apache.abdera` y `org.apache.sling.atom.taglib` con una biblioteca de terceros que proporcione una funcionalidad similar o con su propio código.

Lista de acciones:

* Reemplazar el uso de paquetes de `org.apache.abdera` y `org.apache.sling.atom.taglib` por otras bibliotecas de terceros o código propio.

### Uso de `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

Reemplazar el uso de `org.apache.felix.http.whiteboard` con la [pizarra Http OSGi](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html). La API oficial de OSGi tiene capacidades similares y su reemplazo la mayoría de las veces solo requiere cambiar las propiedades de registro del servicio.

Lista de acciones:

* Reemplazar el uso de `org.apache.felix.http.whiteboard` con la [pizarra Http OSGi](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

### Uso de `ch.qos.logback*` {#ch.qos.logback}

Logback no es compatible en Cloud Service; elimine todo uso del mismo. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:

* Actualizar ACS AEM Commons a la versión más reciente (6.11.0 como mínimo)
* Quitar el código utilizando paquetes de `ch.qos.logback`

### Uso de `org.slf4j.event and org.slf4j.spi` {#org.slf4j}

Si está usando `org.slf4j.event` o `org.slf4j.spi`, elimine todo uso del mismo. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:

* Actualizar ACS AEM Commons a la versión más reciente (6.11.0 como mínimo)
* Quitar el código utilizando `org.slf4j.event` y `org.slf4j.spi`
* Si está usando el cliente Apache Kafka e incluye el paquete de envoltorio OSGi de Apache ServiceMix (`org.apache.servicemix.bundles.kafka-clients`), reemplácelo por el [Envoltorio para cliente Apache Kafka de AEM](https://repo.maven.apache.org/maven2/com/adobe/aem/osgi/com.adobe.aem.osgi.kafka-clients/4.0.0_1.0/). Esta es la misma versión que la de Apache ServiceMix con solo el uso de esos dos paquetes eliminados.

### Uso de `org.apache.log4j` {#org.apache.log4j}

Si usa `org.apache.log4j`, cambie a SLF4J (`org.slf4j`) o Log4J 2.x (`org.apache.logging.log4j`).

Lista de acciones:

* Reemplazar el uso de `org.apache.log4j` por el de `org.slf4j` (recomendado) o `org.apache.logging.log4j`

## Configuración OSGi {#osgi-configuration}

Las secciones siguientes reflejan la superficie de configuración de OSGi en AEM as a Cloud Service, e indican lo que los clientes pueden configurar.

1. El código de cliente no debe configurar las configuraciones de OSGi indicadas.
1. Una lista de configuraciones de OSGi cuyas propiedades pueden configurarse, pero deben cumplir las reglas de validación indicadas. Estas reglas incluyen si la declaración de la propiedad es obligatoria, su tipo y, en algunos casos, su intervalo permitido de valores.

El código de cliente puede configurar cualquier configuración de OSGi que no aparezca en la lista.

Estas reglas se validan durante el proceso de compilación de Cloud Manager. Con el tiempo se pueden añadir reglas adicionales y la fecha de aplicación esperada se indica en la tabla. Se espera que los clientes cumplan estas reglas en la fecha objetivo de aplicación. Si no se respetan las reglas después de la fecha de eliminación, se generarán errores en el proceso de generación de Cloud Manager. Los proyectos de Maven deben incluir [el complemento Maven AEM as a Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) para marcar los errores de configuración de OSGI durante el desarrollo local del SDK.

Puede encontrar información adicional sobre la configuración de OSGI en [esta ubicación](/help/implementing/deploying/configuring-osgi.md).

### Propiedades OSGi en desuso (pronto no se podrán modificar) {#deprecated-unmodifiable-osgi-properties}

Las propiedades para los siguientes PID de componentes de OSGi están en desuso y su uso debe haberse detenido ya en la fecha de aplicación.

| **ID de componente de OSGI** | **Propiedades no modificables** | **Desuso** | **Aplicación** |
|---|---|---|---|
| **`org.apache.sling.commons.log.LogManager`** | todo | 24/4/25 | 31/8/25 (configuración ignorada en junio) |
| **`org.apache.sling.commons.log.LogManager.factory.config`** | org.apache.sling.commons.log.file, org.apache.sling.commons.log.pattern | 24/4/25 | 31/8/25 (configuración ignorada en junio) |
| **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** | todo | 2024 | 31/8/25 |
| **`com.adobe.granite.toggle.impl.dev.DynamicToggleProviderImpl`** | todo | 3/6/25 | 31/8/25 |
| **`org.apache.http.proxyconfigurator`** | todo | 3/6/25 | 31/8/25 |

### Configuraciones de OSGi no modificables {#unmodifiable-osgi-properties}

Las propiedades de los siguientes PID de componentes OSGi no se pueden modificar, por lo que no deben configurarse.

| **ID de componente de OSGI** | **Propiedades no modificables** |
|---|---|
| **`com.day.cq.auth.impl.cug.CugSupportImpl`** |  |
| **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** | todo |
| **`com.adobe.granite.toggle.impl.ToggleRouterImpl`** | todo |
| **`org.apache.sling.engine.impl.log.RequestLoggerFilter`** | todo |
| **`org.apache.sling.feature.apiregions.impl`** | todo |
| **`org.apache.sling.jcr.resource.internal.helper.jcr.BinaryDownloadUriProvider`** | todo |
| **`com.adobe.cq.unifiedshell.impl.discovery.DiscoveryServlet`** | todo |
| **`com.adobe.cq.unifiedshell.impl.ui.FrameErrorHandler`** | todo |
| **`com.adobe.cq.unifiedshell.impl.config.UnifiedShellConfService`** | todo |
| **`com.adobe.cq.unifiedshell.impl.config.RepositoryIdentifier`** | todo |
| **`org.apache.sling.feature.apiregions.factory`** | todo |
| **`com.adobe.granite.toggle.monitor.systemproperty`** | todo |


### Futuras restricciones de propiedad de OSGi aplicadas {#future-restrictions-osgi-properties}

En el futuro, Adobe aplicará las siguientes restricciones a las propiedades de OSGi. Para los PID mencionados, solo se permite configurar las propiedades enumeradas.

| PID de componente de OSGi |   | Requerido | Tipo | Restricción (si es aplicable) |
|---|---|---|---|---|
| `com.day.cq.mailer.DefaultMailService` | `smtp.host` |   | cadena |   |
|   | `smtp.port` | Sí | integer | “465”, “587” o “25” |
|   | `smtp.user` |   | cadena |   |
|   | `smtp.password` |   | cadena |   |
|   | `from.address` |   | cadena |   |
|   | `smtp.ssl` |   | cadena |   |
|   | `smtp.starttls` |   | booleano |   |
|   | `smtp.requiretls` |   | booleano |   |
|   | `debug.email` |   | booleano |   |
|   | `oauth.flow` |   | booleano |   |
| `org.apache.sling.commons.log.LogManager.factory.config` | `org.apache.sling.commons.log.level` | Sí | cadena | “INFO”, “DEBUG” o “TRACE” |
|   | `org.apache.sling.commons.log.names` |   | matriz de cadenas |   |
|   | `org.apache.sling.commons.log.additiv` |   | booleano |   |
| `com.day.cq.commons.impl.ExternalizerImpl` | `externalizer.domains` | No | cadena[] |   |
|   | `externalizer.encodedpath` | No | booleano |   |
|   | `externalizer.host` | No | cadena |   |
|   | `externalizer.contextpath` | No | cadena |   |

### Restricciones de propiedad de OSGi {#restrictions-osgi-properties}

Los valores de estas propiedades de OSGi están restringidos a las reglas que se describen a continuación.

| PID de componente de OSGi |   | Requerido | Tipo | Restricción (si es aplicable) |
|---|---|---|---|---|
| `org.apache.felix.eventadmin.impl.EventAdmin` | `org.apache.felix.eventadmin.ThreadPoolSize` | Sí | integer | 2-100 |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | doble | -- |
|   | `org.apache.felix.eventadmin.AsyncToSyncThreadRatio` |   | integer | -- |
|   | `org.apache.felix.eventadmin.RequireTopic` |   | booleano | -- |
|   | `org.apache.felix.eventadmin.IgnoreTimeout` | Sí | matriz de cadenas | Debe incluir al menos todos los siguientes: `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*` |
|   | `org.apache.felix.eventadmin.IgnoreTopic` |   | matriz de cadenas | -- |
| `org.apache.felix.http` | `org.apache.felix.http.timeout` |   | integer |   |
|   | `org.apache.felix.http.session.timeout` |   | integer |   |
|   | `org.apache.felix.http.jetty.threadpool.max` |   | integer |   |
|   | `org.apache.felix.http.jetty.headerBufferSize` |   | integer |   |
|   | `org.apache.felix.http.jetty.requestBufferSize` |   | integer |   |
|   | `org.apache.felix.http.jetty.responseBufferSize` |   | integer |   |
|   | `org.apache.felix.http.jetty.maxFormSize` |   | integer |   |
|   | `org.apache.felix.https.jetty.session.cookie.httpOnly` |   | booleano |   |
|   | `org.apache.felix.https.jetty.session.cookie.secure` |   | booleano |   |
|   | `org.eclipse.jetty.servlet.SessionIdPathParameterName` |   | cadena |   |
|   | `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding` |   | booleano |   |
|   | `org.eclipse.jetty.servlet.SessionCookie` |   | cadena |   |
|   | `org.eclipse.jetty.servlet.SessionDomain` |   | cadena |   |
|   | `org.eclipse.jetty.servlet.SessionPath` |   | cadena |   |
|   | `org.eclipse.jetty.servlet.MaxAge` |   | integer |   |
|   | `org.eclipse.jetty.servlet.SessionScavengingInterval` |   | integer |   |
|   | `org.apache.felix.jetty.gziphandler.enable` |   | booleano |   |
|   | `org.apache.felix.jetty.gzip.minGzipSize` |   | integer |   |
|   | `org.apache.felix.jetty.gzip.compressionLevel` |   | integer |   |
|   | `org.apache.felix.jetty.gzip.inflateBufferSize` |   | integer |   |
|   | `org.apache.felix.jetty.gzip.syncFlush` |   | booleano |   |
|   | `org.apache.felix.jetty.gzip.excludedUserAgents` |   | cadena |   |
|   | `org.apache.felix.jetty.gzip.includedMethods` |   | matriz de cadenas |   |
|   | `org.apache.felix.jetty.gzip.excludedMethods` |   | matriz de cadenas |   |
|   | `org.apache.felix.jetty.gzip.includedPaths` |   | matriz de cadenas |   |
|   | `org.apache.felix.jetty.gzip.excludedPaths` |   | matriz de cadenas |   |
|   | `org.apache.felix.jetty.gzip.includedMimeTypes` |   | matriz de cadenas |   |
|   | `org.apache.felix.http.session.invalidate` |   | booleano |   |
|   | `org.apache.felix.http.session.container.attribute` |   | matriz de cadenas |   |
|   | `org.apache.felix.http.session.uniqueid` |   | booleano |   |
| `org.apache.sling.scripting.cache` | `org.apache.sling.scripting.cache.size` | Sí | integer | >= 2048 |
|   | `org.apache.sling.scripting.cache.additional_extensions` | Sí | matriz de cadenas | debe incluir “js” |
| `org.apache.sling.engine.impl.log.RequestLogger` | `request.log.output` | No | cadena |   |
|   | `request.log.outputtype` | No | cadena |   |
|   | `request.log.entry.format` | No | cadena |   |
|   | `request.log.exit.format` | No | cadena |   |
|   | `request.log.enabled` | No | cadena |   |
|   | `access.log.output` | No | cadena |   |
|   | `access.log.outputtype` | No | cadena |   |
|   | `access.log.enabled` | No | cadena |   |
| `org.apache.sling.servlets.resolver.SlingServletResolver` | `servletresolver.servletRoot` | No | cadena |   |
|   | `servletresolver.cacheSize` | No | integer |   |
|   | `servletresolver.paths` | No | cadena[] |   |
|   | `servletresolver.defaultExtensions` | No | cadena |   |
|   | `servletresolver.mountProviders` | No | booleano |   |
|   | `servletresolver.scriptUser` | No | cadena | en desuso, no utilizar |

## Actualización de Java Runtime a la versión 21 {#java-runtime-update-21}

Adobe Experience Manager as a Cloud Service ha realizado la transición al tiempo de ejecución de Java 21. Para garantizar la compatibilidad, es esencial actualizar las versiones de la biblioteca tal como se describe en [Requisitos de tiempo de ejecución](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

