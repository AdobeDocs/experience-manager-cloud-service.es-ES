---
title: Funciones en desuso y eliminadas
description: Notas de versión específicas de las funciones en desuso y eliminadas de  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: b64c8f16976988d04840f1006afe4f7c9b28c705
workflow-type: tm+mt
source-wordcount: '2488'
ht-degree: 98%

---

# Funciones y API obsoletas y eliminadas {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funciones en desuso y eliminadas en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service tiene un modelo de implementación nativo de la nube. Algunas funciones y características se han reemplazado con homólogos nativos de la nube y esta pestaña muestra esas funciones."

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas más modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores. Además, como [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] proporciona un modelo de implementación nativo de la nube, ciertas funciones y características se han reemplazado con homólogos nativos de la nube.

Para comunicar la eliminación o el reemplazo inminente de las capacidades de [!DNL Experience Manager], se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Las funciones en desuso siguen estando disponibles, pero no se siguen actualizando.
1. Las funciones anunciadas como obsoletas se eliminan en la siguiente versión principal, como pronto. Se anuncia la auténtica fecha límite para la eliminación.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

## Funciones en desuso {#deprecated-features}

Esta sección enumera las funciones que se han marcado como en desuso en [!DNL Experience Manager] as a [!DNL Cloud Service]. Normalmente, las funciones que se quieren eliminar en una versión futura se establecen en primer lugar como en desuso, con una alternativa.

Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Capacidades | Función en desuso | Reemplazo |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | [API de uso de JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [API de uso de Java](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | Propiedades de Fragmentos de experiencias para **Estado de los medios sociales**. | La función se eliminará próximamente. |
| [!DNL Sites] | Fragmentos de contenido simples basados en plantillas. | [Fragmentos de contenido estructurados basados en modelos](/help/assets/content-fragments/content-fragments-models.md) ahora. |
| [!DNL Assets] | `DAM Asset Update` flujo de trabajo para procesar imágenes grabadas. | Ahora, el consumo de recursos utiliza [los microservicios](/help/assets/asset-microservices-overview.md) de recursos. |
| [!DNL Assets] | Cargar recursos directamente en [!DNL Experience Manager].  Consulte [API de carga de recursos en desuso](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilice la [carga binaria directa](/help/assets/add-assets.md). Para obtener más información técnica, consulte [API de carga directa](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | No se admiten [determinados pasos](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) en el flujo de trabajo `DAM Asset Update`, incluida la llamada a herramientas de línea de comandos como [!DNL ImageMagick]. | [Los microservicios de recursos](/help/assets/asset-microservices-overview.md) sustituyen a muchos flujos de trabajo. Para el procesamiento personalizado, utilice [flujos de trabajo posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | FFmpeg transcodificar vídeos. | Para la generación de miniaturas de FFmpeg, use los [microservicios de Asset](/help/assets/asset-microservices-overview.md). Para la transcodificación FFmpeg, utilice [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | IU de replicación de árbol en la pestaña Distribuir del agente de replicación (eliminación después del 30 de septiembre de 2021) | Enfoques [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Ni la pestaña Distribuir de la pantalla del administrador del agente de replicación ni la API de replicación pueden utilizarse para replicar paquetes de contenido de más de 10 MB.  En su lugar, utilice [Administrar publicación](/help/operations/replication.md#manage-publication) o [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Las integraciones que utilizan credenciales generadas a partir de proyectos de Adobe Developer Console perderán gradualmente la compatibilidad con las credenciales de la cuenta de servicio (JWT). No se pueden crear nuevas credenciales de cuenta de servicio (JWT) enAdobe Developer Console a partir del 1 de mayo de 2024, aunque las credenciales de cuenta de servicio (JWT) existentes se pueden seguir utilizando para integraciones ya configuradas hasta el 1 de enero de 2025, momento en el que las credenciales de cuenta de servicio (JWT) existentes dejarán de funcionar y los clientes deberán migrar a las credenciales de servidor a servidor de OAuth. [Más información](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrar](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) a las credenciales de servidor a servidor de OAuth. |

## Funciones eliminadas {#removed-features}

En esta sección se enumeran las funciones que se han eliminado de [!DNL Experience Manager] con [!DNL Experience Manager] as a [!DNL Cloud Service].

| Área | Funcionalidad | Reemplazo | Fecha de eliminación objetivo |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaz de usuario | La IU clásica se elimina de la interfaz de usuario del producto. Hay algunos cuadros de diálogo de IU clásica disponibles para algunas funciones seleccionadas, como Verificador de vínculos, Depuración de versiones y algunas configuraciones de Cloud Service. Próximas [actualizaciones de productos](/help/release-notes/home.md) pueden eliminar aún más la disponibilidad de la IU clásica. | IU estándar | Eliminado |
| [!DNL Dynamic Media] | Las integraciones anteriores con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=es#integration) y el [modo híbrido de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=es#dynamic) no están disponibles en [!DNL Experience Manager] as a [!DNL Cloud Service]. | Utilice [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) proporcionado con [!DNL Experience Manager] as a [!DNL Cloud Service]. | Eliminado |
| [!DNL Sites] | Portal Director y componentes Portlet | Estas funciones quedaron obsoletas en [!DNL Experience Manager] 6.4 y ahora se han eliminado de [!DNL Experience Manager]. | Eliminado |
| [!DNL Sites] | Importador de diseños | Esta capacidad se ha eliminado porque no se puede acceder a las secciones inmutables del repositorio de [!DNL Experience Manager] durante la ejecución. | Eliminado |
| [!DNL Assets] | El uso compartido de [!DNL Assets] con el servicio principal de Experience Cloud Assets y Creative Cloud Services no está disponible. | Para la integración con [!DNL Adobe Creative Cloud], utilice [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html). | Eliminado |
| [!DNL Foundation] | Compatibilidad con fuentes de datos de Apache Sling (paquete OSGi org.apache.sling.datasource) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con plantillas de scripts JST (paquete OSGi org.apache.sling.scripting.jst) | N/D | Eliminado |
| [!DNL Foundation] | Compatibilidad con la pizarra Apache Felix Http | Pizarra Http OSGi | Marzo de 2022 |
| [!DNL Foundation] | Compatibilidad con com.adobe.granite.oauth.server | Integración de IMS de Adobe | Marzo de 2023 |
| [!DNL Foundation] | Compatibilidad con la función org.apache.sling.serviceusermapping para [obtener el id de usuario del servicio](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | N/D | 30/08/24 |


## API DE AEM {#aem-apis}

A continuación se incluye una lista detallada de las API de AEM en desuso y su fecha prevista de eliminación. Se espera que los clientes eliminen las API antes de la fecha prevista de eliminación de su código. Cualquier uso de la API más allá de la fecha de eliminación generará errores en el SDK/entorno de desarrollo local y en el proceso de compilación de Cloud Manager.

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
    <td>Uso de las interfaces Auth Core/Auth Core SPI de Sling como alternativa. <a href="#org.apache.sling.commons.auth">Consulte las notas de eliminación a continuación.</a></td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Uso de la API Discovery de Sling como alternativa</td>
    <td>2015</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>3/1/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>3/5/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>La implementación de Apache Johnzon de <a href="https://johnzon.apache.org/index.html">javax.json</a> se recomienda y debe utilizarse. </td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Los administradores de persistencia personalizados no son compatibles con AEM as a Cloud Service.</td>
    <td>4/30/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 está en modo de mantenimiento. Debe utilizarse Commons Lang 3 en su lugar.</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 está en modo de mantenimiento. Debe utilizarse Commons Collections 4 en su lugar.</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Se recomienda utilizar la API Apache Felix HealthCheck en su lugar</td>
    <td>4/30/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>La consola web de Felix no es compatible con entornos de la nube</td>
    <td>4/30/21</td>
    <td>7/30/21</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Los paquetes Eclipse Jetty y Felix Http Jetty ya no se admiten. <a href="#org.eclipse.jetty">Consulte las notas de eliminación a continuación.</a></td>
    <td>5/27/21</td>
    <td>8/26/21</td>
  </tr>
  <tr> <td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread
</td>
    <td>Los paquetes Eclipse Jetty y Felix Http Jetty ya no se admiten.</td>
    <td>5/27/21</td>
    <td>8/26/21</td>
  </tr>  
  <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>El uso de esta API no se admite en AEM as a Cloud Service. <a href="#com.mongodb">Consulte las notas de eliminación a continuación.</a></td>
    <td>5/27/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Las API Apache Felix metatype y SCR están en desuso.  Utilice en su lugar las API OSGi metatype y Declarative Service.</td>
    <td>5/27/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>Las clases de implementación de registros no son compatibles con AEM as a Cloud Service.</td>
    <td>7/4/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte las notas de eliminación a continuación.</a></td>
    <td>7/29/21</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017.</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>API heredada AEM 6.x.</td>
    <td>4/8/19</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Esta API no se admite en Cloud Service.</td>
    <td>9/30/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Las clases de utilidad relacionadas con Apache Xerces se eliminan en las versiones posteriores, lo que provoca un cambio de versión importante. Como estas utilidades son de uso interno en Filevault, la API está quedando en desuso en la superficie de la API pública.</td>
    <td>9/1/21</td>
    <td>eliminado</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>API heredada de AEM 6.x. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulte las notas de eliminación a continuación.</a></td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>La pizarra Apache Felix Http ya no es compatible. Migre su código a la pizarra Http OSGi. <a href="#org.apache.felix.http.whiteboard">Consulte las notas de eliminación a continuación.</a></td>
    <td>1/27/2022</td>
    <td>03/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Esta API está en desuso. Migre su código a las API XML proporcionadas por el JDK.</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>Esta API de inicio de sesión interna no es compatible con AEM as a Cloud Service.</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>Esta API interna de log4j no es compatible con AEM as a Cloud Service.</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 ha llegado al fin de su vida útil en 2015 y ya no es compatible.</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>Esta API de inicio de sesión interna no es compatible con AEM as a Cloud Service.</td>
    <td>1/27/2022</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>Se requiere la actualización de Handlebars de 4.0.5 a 4.3.0 debido a una vulnerabilidad de seguridad. Este paquete ya no está presente en los controladores actualizados.</td>
    <td>5/5/2022</td>
    <td>8/5/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Esta API ya no es compatible. En su lugar, utilice org.apache.sling.api.resource.ResourceResolverFactory.</td>
    <td>9/29/2022</td>
    <td>11/24/2022</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Esta API está obsoleta. En su lugar, utilice los generadores de Apache Sling.</td>
    <td>10/31/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>Esta API no es compatible con AEM as a Cloud Service.</td>
    <td>15/5/2023</td>
    <td>15/6/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Las bibliotecas principales de Google Guava están en desuso.</td>
    <td>15/5/2023</td>
    <td>15/6/2023</td>
  </tr>
  <tr>
    <td>org.slf4j.event    </td>
    <td>Esta API slf4j interna no es compatible con AEM as a Cloud Service.</td>
    <td>11/4/2022</td>
    <td>30/8/2024</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>El uso de esta API no se admite en AEM as a Cloud Service.</td>
    <td>17/5/2024</td>
    <td>30/6/2024</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>En su lugar, utilice org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>30/6/2024</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>En su lugar, utilice org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>30/6/2024</td>
  </tr>  
  <tr>
    <td>com.drew.*</td>
    <td>La extracción de metadatos de imágenes y vídeos debe realizarse mediante Asset Compute en Cloud Service, o mediante Apache POI o Apache Tika.</td>
    <td>17/9/2024</td>
    <td>17/12/2024</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td></td>
    <td>23/9/2024</td>
    <td>23/12/2024</td>
  </tr>       
</tbody>
</table>
</details>

### Eliminación de `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

Si usa `org.apache.sling.commons.auth` o `org.apache.sling.commons.auth.spi`, el uso se puede reemplazar migrando el código a `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`. Si está usando una versión antigua de [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), asegúrese de actualizarla a la versión más reciente.

Lista de acciones:
* Actualizar ACS AEM Commons a la versión más reciente
* Migrar de `org.apache.sling.commons.auth` o `org.apache.sling.commons.auth.spi` a `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`.

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
   * org.mongodb:mongo-java-driver:3.12.7

### Uso de `org.apache.abdera*` y `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

Reemplazar el uso de cualquier paquete de `org.apache.abdera` y `org.apache.sling.atom.taglib` con una biblioteca de terceros que proporcione una funcionalidad similar o con su propio código.

Lista de acciones:
* Reemplazar el uso de paquetes de `org.apache.abdera` y `org.apache.sling.atom.taglib` por otras bibliotecas de terceros o código propio.

### Uso de `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

Reemplazar el uso de `org.apache.felix.http.whiteboard` con la [pizarra Http OSGi](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html). La API oficial de OSGi tiene capacidades similares y su reemplazo la mayoría de las veces solo requiere cambiar las propiedades de registro del servicio.

Lista de acciones:
* Reemplazar el uso de `org.apache.felix.http.whiteboard` con la [pizarra Http OSGi](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

## Configuración OSGi {#osgi-configuration}

Las dos listas siguientes reflejan la superficie de configuración de AEM as a Cloud Service de OSGi, describiendo lo que los clientes pueden configurar.

1. Una lista de configuraciones de OSGi que el código de cliente no debe configurar
1. Una lista de configuraciones de OSGi cuyas propiedades pueden configurarse, pero deben cumplir las reglas de validación indicadas. Estas reglas incluyen si la declaración de la propiedad es obligatoria, su tipo y, en algunos casos, su intervalo permitido de valores.

Si la configuración de OSGI no aparece en la lista, puede configurarse mediante el código de cliente.

Estas reglas se validan durante el proceso de compilación de Cloud Manager.  Con el tiempo se pueden añadir reglas adicionales y la fecha de aplicación esperada se indica en la tabla. Se espera que los clientes cumplan estas reglas en la fecha objetivo de aplicación. Si no se respetan las reglas después de la fecha de eliminación, se generarán errores en el proceso de generación de Cloud Manager. Los proyectos de Maven deben incluir [el complemento Maven AEM as a Cloud Service SDK Build Analyzer](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es) para marcar los errores de configuración de OSGI durante el desarrollo local del SDK.

Puede encontrar información adicional sobre la configuración de OSGI en [esta ubicación](/help/implementing/deploying/configuring-osgi.md).

Configuraciones de +++OSGi que no se pueden modificar.
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Fecha de anuncio: 25/8/2021, fecha de aplicación: 26/11/2021)
+++

Las configuraciones de +++OSGi están sujetas a reglas de validación de compilación.
* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * Tipo: entero
   * Intervalo requerido: 2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * Tipo: doble
* `org.apache.felix.eventadmin.Timeout`
   * Tipo: entero
* `org.apache.felix.eventadmin.RequireTopic`
   * Tipo: booleano
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * Requerido
   * Tipo: matriz de cadenas
   * Intervalo requerido: debe incluir al menos todos los `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * Tipo: matriz de cadenas
* **`org.apache.felix.http`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: entero
   * `org.apache.felix.http.session.timeout`
      * Tipo: entero
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: entero
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: entero
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: entero
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: cadena
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: entero
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: entero
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: entero
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: cadena
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: matriz de cadenas
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: matriz de cadenas
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: matriz de cadenas
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: entero
      * Intervalo requerido: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Requerido
      * Tipo: matriz de cadenas
      * Intervalo requerido: debe incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Fecha de anuncio: 30/4/2021, fecha de aplicación: 31/7/2021)
   * `smtp.host`
      * Tipo: cadena
   * `smtp.port`
      * Tipo: entero
      * Intervalo requerido: 465, 587 o 25
   * `smtp.user`
      * Tipo: cadena
   * `smtp.password`
      * Tipo: cadena
   * `from.address`
      * Tipo: cadena
   * `smtp.ssl`
      * Tipo: cadena
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Fecha de anuncio: 16/11/21, Fecha de aplicación: 2/16/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumeración
      * Intervalo requerido: INFO, DEPURACIÓN o TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: cadena
   * `org.apache.sling.commons.log.file`
      * Tipo: cadena
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano
+++

