---
title: Ampliación de las opciones y funciones de búsqueda en Recursos Adobe Experience Manager
description: Amplíe las capacidades de búsqueda de Recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Ampliar búsqueda de recursos {#extend-assets-search}

Puede ampliar las capacidades de búsqueda de recursos de Adobe Experience Manager (AEM). De forma predeterminada, Recursos AEM busca recursos por cadenas.

La búsqueda se realiza a través de la interfaz de QueryBuilder para que la búsqueda se pueda personalizar con varios predicados. Puede superponer el conjunto predeterminado de predicados en el siguiente directorio: `/apps/dam/content/search/searchpanel/facets`.

También puede añadir fichas adicionales al panel de administración de Recursos AEM.

## Superposición {#overlay}

Para superponer los predicados preconfigurados, copie el `facets` nodo de `/libs/dam/content/search/searchpanel` a `/apps/dam/content/search/searchpanel/` o especifique otra `facetURL` propiedad en la configuración del panel de búsqueda (el valor predeterminado es a `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

>[!NOTE]
>
>De forma predeterminada, la estructura de directorio en `/apps` no existe y debe crearse. Asegúrese de que los tipos de nodo coincidan con los de `/libs`.

### Agregar fichas {#add-tabs}

Puede agregar fichas de búsqueda adicionales configurándolas en el administrador de AEM Assets. Para crear fichas adicionales:

1. Cree la estructura de carpetas `/apps/wcm/core/content/damadmin/tabs,`si aún no existe, copie el `tabs` nodo `/libs/wcm/core/content/damadmin` y péguelo.
1. Cree y configure la segunda ficha como desee.

   >[!NOTE]
   >
   >Cuando cree un segundo `siteadminsearchpanel`, asegúrese de establecer una `id` propiedad para evitar conflictos de formularios.

### Crear predicados personalizados {#create-custom-predicates}

Recursos AEM incluye un conjunto de predicados predefinidos que se pueden utilizar para personalizar una página de uso compartido de recursos.
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

La creación de predicados personalizados requiere conocimientos básicos sobre el marco [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)utilidades.

Se recomienda copiar un predicado existente y ajustarlo. Los predicados de muestra se encuentran en **/libs/cq/search/components/predicates**.

#### Ejemplo: Generar un predicado de propiedades simple {#example-build-a-simple-property-predicate}

Para generar un predicado de propiedad:

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo **/apps/geometrixx/components/titlepredicate**.
1. Agregar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Añada `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Para que el componente esté disponible, debe poder editarlo. Para que un componente se pueda editar, en CRXDE, agregue un nodo **cq:editConfig** de tipo principal **cq:EditConfig**. Para poder eliminar párrafos, agregue una propiedad de varios valores **cq:actions** con un único valor de **ELIMINAR**.
1. Vaya al navegador y, en la página de muestra (por ejemplo, **press.html**), cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos de predicado (por ejemplo, **izquierda**).

1. En el modo **Editar** , el nuevo componente ahora está disponible en la barra de tareas (que se encuentra en el grupo **Buscar** ). Inserte el componente en la columna **Predicados** y escriba una palabra de búsqueda, por ejemplo, **Diamante** y haga clic en la lupa para iniciar la búsqueda.

   >[!NOTE]
   >
   >Al buscar, asegúrese de escribir el término exactamente, incluyendo el caso correcto.

#### Ejemplo: Crear un predicado de grupo simple {#example-build-a-simple-group-predicate}

Para crear un predicado de grupo:

1. Cree una carpeta de componentes en el directorio de proyectos, por ejemplo **/apps/geometrixx/components/picspredicate.**
1. Agregar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Agregar **titlepredicate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Para que el componente esté disponible, debe poder editarlo. Para que un componente se pueda editar, en CRXDE, agregue un nodo **cq:editConfig** de tipo principal **cq:EditConfig**. Para poder eliminar párrafos, agregue una propiedad de varios valores **cq:actions** con un único valor de **ELIMINAR**.
1. Vaya al navegador y, en la página de muestra (por ejemplo, **press.html**), cambie al modo de diseño y habilite el nuevo componente para el sistema de párrafos de predicado (por ejemplo, **izquierda**).
1. En el modo **Editar** , el nuevo componente ahora está disponible en la barra de tareas (que se encuentra en el grupo **Buscar** ). Inserte el componente en la columna **Predicados** .

### Widgets de predicado instalados {#installed-predicate-widgets}

Los siguientes predicados están disponibles como utilidades preconfiguradas de ExtJS.

#### FulltextPredicate {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Cadena</td>
   <td>Nombre del predicado. Predeterminado en 'fulltext'</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Función</td>
   <td>Llamada de retorno para activar la búsqueda en el evento 'keyup'. Valor predeterminado de 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
 </tbody>
</table>

#### PropertyPredicate {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Cadena</td>
   <td>Nombre del predicado. El valor predeterminado es "propiedad"</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Cadena </td>
   <td>Nombre de la propiedad JCR. Predeterminado en 'jcr:title'</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>Cadena<br /> </td>
   <td>Valor predeterminado predefinido.<br /> </td>
  </tr>
 </tbody>
</table>

#### PathPredicate {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Cadena</td>
   <td>Nombre del predicado. Predeterminado en 'path'</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Cadena </td>
   <td>Ruta raíz del predicado. Predeterminado en '/content/dam'</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>Cadena</td>
   <td>Predeterminado en 'folder'</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>Booleano</td>
   <td>Marca para mostrar la casilla de verificación 'buscar en subcarpetas'. La opción predeterminada es true.</td>
  </tr>
 </tbody>
</table>

#### DatePredicate {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Cadena</td>
   <td>Nombre del predicado. Valores predeterminados de 'daterange'</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>Cadena</td>
   <td>Nombre de la propiedad JCR. Predeterminado en 'jcr:content/jcr:lastModified'</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>Cadena </td>
   <td>Valor predeterminado predefinido </td>
  </tr>
 </tbody>
</table>

#### OptionsPredicate {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>el título </td>
   <td>Cadena </td>
   <td>Agrega un título superior adicional </td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Cadena</td>
   <td>Nombre del predicado. Valores predeterminados de 'daterange'</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>Cadena</td>
   <td>Nombre de la propiedad JCR. Predeterminado en 'jcr:content/metadata/cq:tags'</td>
  </tr>
  <tr>
   <td>contraer</td>
   <td>Cadena</td>
   <td>Contraer nivel. Predeterminado en 'level1'</td>
  </tr>
  <tr>
   <td>desencadenadorBúsqueda</td>
   <td>Booleano </td>
   <td>Marca para activar la búsqueda al marcar. Predeterminado en false</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Función</td>
   <td>Llamada de retorno para activar la búsqueda. Valores predeterminados de 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td>Número</td>
   <td>Tiempo de espera antes de que se active searchCallback. Valores predeterminados de 800 ms</td>
  </tr>
 </tbody>
</table>
