---
title: API obsoletas
description: Notas de la versión específicas de las API obsoletas y eliminadas en [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
exl-id: fbd8c60a-3e2b-4696-aaba-f4db97923184
source-git-commit: ac72c6f668e36b0904459f4448dd3bf889a8a69e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 8%

---

# API obsoletas {#deprecated-apis}

A continuación se ofrece una lista exhaustiva de las API de AEM obsoletas y su fecha de eliminación prevista. Se espera que los clientes eliminen las API antes de la fecha de eliminación objetivo de su código. Cualquier uso de la API pasado la fecha de eliminación generará errores en el SDK/entorno de desarrollo local y en el proceso de creación de Cloud Manager.


<table>
<thead>
  <tr>
    <th>Paquete/Clase</th>
    <th>Comentarios</th>
    <th>Fecha de finalización del soporte</th>
    <th>Fecha de eliminación del objetivo</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>Usar las interfaces de Sling Auth Core / Auth Core SPI como alternativa</td>
    <td>2015</td>
    <td>30/7/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>30/7/21</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Usar la API de Discovery de Sling como alternativa</td>
    <td>2015</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.sling.settings</td>
    <td>AEM como Cloud Service no admite modos de ejecución ni acceso al sistema de archivos durante la ejecución. </td>
    <td>5/10/20</td>
    <td>Finales de 2021</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>1/3/21</td>
    <td>1/6/21</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>5/3/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>Se recomienda la implementación de Apache Johnzon de <a href="https://johnzon.apache.org/index.html">javax.json</a>, que debe usarse. </td>
    <td>30/4/21</td>
    <td>31/12/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Los administradores de persistencia personalizados no son compatibles con AEM como Cloud Service.</td>
    <td>30/4/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 está en modo de mantenimiento. Commons Lang 3 debería usarse en su lugar.</td>
    <td>30/4/21</td>
    <td>31/12/21</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Las colecciones Commons 3 están en modo de mantenimiento. Colecciones Commons 4 deberían usarse en su lugar.</td>
    <td>30/4/21</td>
    <td>31/12/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Se recomienda utilizar la API HealthCheck de Apache Felix en su lugar</td>
    <td>30/4/21</td>
    <td>eliminado</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>La consola web Felix no es compatible con los entornos de Cloud</td>
    <td>30/4/21</td>
    <td>30/7/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml<br>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.client.util</td>
    <td>Los paquetes Eclipse Jetty y Felix Http Jetty ya no son compatibles.</td>
    <td>27/5/21</td>
    <td>26/8/21</td>
  </tr>
  <tr>
    <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>El uso de esta API no es compatible en AEM como Cloud Service.</td>
    <td>27/5/21</td>
    <td>30/7/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info</td>
    <td>El tipo de método Apache Felix y las API de SCR están en desuso.  En su lugar, utilice el tipo de método OSGi y las API de servicio declarativas.</td>
    <td>27/5/21</td>
    <td>26/8/21</td>
  </tr>
  <tr>
    <td>oorg.slf4j.impl</td>
    <td>Las clases de implementación de registros no son compatibles con AEM como Cloud Service.</td>
    <td>4/7/21</td>
    <td>26/8/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017.</td>
    <td>29/7/21</td>
    <td>29/9/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Esta API está en desuso, ya que Apache Abdera es un proyecto retirado desde 2017.</td>
    <td>8/4/19</td>
    <td>29/9/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter</td>
    <td>API AEM 6.x heredada.</td>
    <td>8/4/19</td>
    <td>29/9/21</td>
  </tr>
</tbody>
</table>
