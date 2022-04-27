---
title: Identificación del contenido para traducir
description: Descubra cómo las reglas de traducción identifican el contenido que necesita traducción.
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: 0c75a367861c9e4c77ee537322fa49330c70db85
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 1%

---

# Identificación del contenido para traducir {#identifying-content-to-translate}

Las reglas de traducción identifican el contenido que se debe traducir para páginas, componentes y recursos que se incluyen en proyectos de traducción o que se excluyen de ellos. Cuando se traduce una página o un recurso, AEM extrae este contenido para que se pueda enviar al servicio de traducción.

>[!TIP]
>
>Si es nuevo en traducir contenido, consulte nuestra [Recorrido de traducción de sitios,](/help/journey-sites/translation/overview.md) que es una ruta guiada a través de la traducción del contenido de AEM Sites mediante las poderosas herramientas de traducción de AEM, ideal para aquellos que no tengan experiencia de traducción ni AEM.

## Fragmentos de contenido y reglas de traducción {#content-fragments}

Las reglas de traducción descritas en este documento solo se aplican a los fragmentos de contenido si la variable **Habilitar campos del modelo de contenido para su traducción** no se ha activado en la [nivel de configuración del marco de integración de traducción.](integration-framework.md#assets-configuration-properties)

Si la variable **Habilitar campos del modelo de contenido para su traducción** está activa, AEM usará la opción **Translatable** campo en [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md#properties) para determinar si el campo se va a traducir y crea automáticamente reglas de traducción según corresponda. Esta opción reemplaza las reglas de traducción que haya creado y no requiere intervención ni pasos adicionales.

Si desea utilizar reglas de traducción para traducir los fragmentos de contenido, la variable **Habilitar campos del modelo de contenido para su traducción** en la configuración del marco de integración de traducción debe estar desactivada y debe seguir los pasos descritos a continuación para crear las reglas.

## Información general {#overview}

Las páginas y los recursos se representan como nodos en el repositorio JCR. El contenido extraído es uno o más valores de propiedad de los nodos. Las reglas de traducción identifican las propiedades que contienen el contenido que se va a extraer.

Las reglas de traducción se expresan en formato XML y se almacenan en estas posibles ubicaciones:

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

El archivo se aplica a todos los proyectos de traducción.

Las reglas incluyen la siguiente información:

* La ruta del nodo al que se aplica la regla
   * La regla también se aplica a los descendientes del nodo.
* Nombres de las propiedades del nodo que contienen el contenido que se va a traducir
   * La propiedad puede ser específica para un tipo de recurso específico o para todos los tipos de recurso.

Por ejemplo, puede crear una regla que traduzca el contenido que los autores añaden a todos los componentes de texto de sus páginas. La regla puede identificar la variable `/content` y `text` para la variable `core/wcm/components/text/v2/text` componente.

Hay un [consola](#translation-rules-ui) que se ha añadido para configurar reglas de traducción. Las definiciones de la IU rellenarán el archivo por usted.

Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](overview.md).

>[!NOTE]
>
>AEM admite la asignación individual entre tipos de recursos y atributos de referencia para la traducción del contenido al que se hace referencia en una página.

## Sintaxis de reglas para páginas, componentes y recursos {#rule-syntax-for-pages-components-and-assets}

Una regla es `node` elemento con uno o más elementos secundarios `property` elementos y cero o más elementos secundarios `node` elementos:

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

Cada uno de estos `node` tiene las siguientes características:

* La variable `path` contiene la ruta al nodo raíz de la rama a la que se aplican las reglas.
* Niño `property` los elementos identifican las propiedades del nodo que se deben traducir para todos los tipos de recursos:
   * La variable `name` contiene el nombre de la propiedad.
   * La opción `translate` el atributo es igual a `false` si la propiedad no está traducida. De forma predeterminada, el valor es `true`. Este atributo es útil cuando se anulan reglas anteriores.
* Niño `node` los elementos identifican las propiedades del nodo que se deben traducir para tipos de recursos específicos:
   * La variable `resourceType` contiene la ruta que se resuelve en el componente que implementa el tipo de recurso.
   * Niño `property` identifique la propiedad node que desea traducir. Utilice este nodo del mismo modo que el nodo secundario `property` elementos para reglas de nodo.

La siguiente regla de ejemplo causa el contenido de todas las `text` propiedades que se van a traducir para todas las páginas debajo de la variable `/content` nodo . La regla es efectiva para cualquier componente que almacene contenido en un `text` , como el componente de texto.

```xml
<node path="/content">
          <property name="text"/>
</node>
```

El siguiente ejemplo traduce el contenido de todas las `text` y traduce también otras propiedades del componente de imagen. Si otros componentes tienen propiedades con el mismo nombre, la regla no se les aplica.

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## Sintaxis de reglas para extraer recursos de páginas  {#rule-syntax-for-extracting-assets-from-pages}

Utilice la siguiente sintaxis de regla para incluir recursos incrustados en componentes o a los que se hace referencia desde ellos:

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

Cada `assetNode` tiene las siguientes características:

* One `resourceType` que es igual a la ruta que se resuelve en el componente
* One `assetReferenceAttribute` atributo igual al nombre de la propiedad que almacena el binario de recursos (para recursos incrustados) o la ruta al recurso al que se hace referencia

El siguiente ejemplo extrae imágenes del componente de imagen:

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## Reglas de anulación {#overriding-rules}

La variable `translation_rules.xml` consta de `nodelist` elemento con varios elementos secundarios `node` elementos. AEM lee la lista de nodos de arriba a abajo. Cuando varias reglas se dirigen al mismo nodo, se utiliza la regla que se encuentra más abajo en el archivo. Por ejemplo, las siguientes reglas causan todo el contenido en `text` propiedades que se van a traducir excepto para `/content/mysite/en` rama de páginas:

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## Filtrado de propiedades {#filtering-properties}

Puede filtrar nodos que tengan una propiedad específica utilizando una `filter` elemento.

Por ejemplo, las siguientes reglas causan todo el contenido en `text` propiedades que desea traducir excepto para los nodos que tienen la propiedad `draft` configure como `true`.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## Interfaz de usuario de reglas de traducción {#translation-rules-ui}

También hay una consola disponible para configurar las reglas de traducción.

Para acceder a él:

1. Vaya a **Herramientas** y luego **General**.

1. Select **Configuración de traducción**.

En la interfaz de usuario de las reglas de traducción puede:

1. **Agregar contexto**, que le permite añadir una ruta.

   ![Agregar contexto de traducción](../assets/add-translation-context.png)

1. Utilice el navegador de rutas para seleccionar el contexto necesario y toque o haga clic en el **Confirmar** para guardar.

   ![Seleccionar contexto](../assets/select-context.png)

1. A continuación, debe seleccionar el contexto y hacer clic en **Editar**. Se abrirá el Editor de reglas de traducción.

   ![Editor de reglas de traducción](../assets/translation-rules-editor.png)

Hay cuatro atributos que puede cambiar mediante la interfaz de usuario:

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  es aplicable en los filtros de nodo y es true de forma predeterminada. Comprueba si el nodo (o sus antecesores) contiene esa propiedad con el valor de propiedad especificado en el filtro. Si es false, solo comprueba en el nodo actual.

Por ejemplo, los nodos secundarios se agregan a un trabajo de traducción incluso cuando el nodo principal tiene la propiedad `draftOnly` se establece en true para marcar el contenido de borrador. Aquí `isDeep` entra en juego y comprueba si los nodos principales tienen propiedad `draftOnly` como true y excluye esos nodos secundarios.

En el editor, puede marcar o desmarcar **Es profundo** en el **Filtros** pestaña .

![Filtrar reglas](../assets/translation-rules-editor-filters.png)

Este es un ejemplo del XML resultante cuando **Es profundo** está desmarcada en la interfaz de usuario:

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### heredar {#inherit}

**`inherit`** es aplicable a las propiedades. De forma predeterminada, todas las propiedades se heredan, pero si desea que el elemento secundario no herede alguna propiedad, puede marcar esta propiedad como falsa para que se aplique únicamente a ese nodo específico.

En la interfaz de usuario, puede marcar o desmarcar **Heredar** en el **Propiedades** pestaña .

### traducir {#translate}

**`translate`** se utiliza simplemente para especificar si se desea traducir o no una propiedad.

En la interfaz de usuario, puede marcar o desmarcar **Traducir** en el **Propiedades** pestaña .

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** se utiliza para propiedades que no tienen texto, sino códigos de idioma, por ejemplo `jcr:language`. El usuario no traduce texto sino la configuración regional del idioma de origen a destino. Estas propiedades no se envían para su traducción.

En la interfaz de usuario, puede marcar o desmarcar **Traducir** en el **Propiedades** para modificar este valor, pero para las propiedades específicas que tienen códigos de idioma como valor.

Para ayudar a aclarar la diferencia entre `updateDestinationLanguage` y `translate`, aquí hay un ejemplo sencillo de contexto con solo dos reglas:

![ejemplo updateDestinationLanguage](../assets/translation-rules-updatedestinationlanguage.png)

El resultado en el xml tendrá este aspecto:

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## Edición manual del archivo de reglas {#editing-the-rules-file-manually}

La variable `translation_rules.xml` que se instala con AEM contiene un conjunto predeterminado de reglas de traducción. Puede editar el archivo para satisfacer los requisitos de sus proyectos de traducción. Por ejemplo, puede agregar reglas para que se traduzca el contenido de los componentes personalizados.

Si edita la variable `translation_rules.xml` mantenga una copia de seguridad en un paquete de contenido. La reinstalación de ciertos paquetes de AEM puede reemplazar al actual `translation_rules.xml` con el original. Para restaurar las reglas en esta situación, puede instalar el paquete que contiene la copia de seguridad.

>[!NOTE]
>
>Después de crear el paquete de contenido, reconstruya el paquete cada vez que edite el archivo.

## Ejemplo de archivo de reglas de traducción {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
