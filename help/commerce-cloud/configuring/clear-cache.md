---
title: Componente y GraphQL Borrar caché
description: Obtenga información sobre cómo habilitar y comprobar la función de borrar caché en AEM CIF.
feature: Commerce Integration Framework
role: Admin
source-git-commit: 63a3a40cc19a83ce51a74899434c73f0ff4f318c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 2%

---


# Componente y GraphQL Borrar caché {#clear-cache}

Este documento proporciona una guía completa sobre la activación y verificación de la función clear-cache en AEM CIF.

## Habilitar la función Borrar caché en la configuración de CIF {#enable-clear-cache}

De forma predeterminada, la función de borrado de caché está desactivada en la configuración de CIF. Para habilitarlo, debe agregar lo siguiente a sus proyectos correspondientes:

* Habilite el servlet `/bin/cif/invalidate-cache`, que le ayuda a activar la API de borrar caché con sus solicitudes correspondientes agregando la configuración `com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json` en su proyecto como se muestra [aquí](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json).
  >[!NOTE]
  >
  > La configuración solo debe habilitarse para las instancias de autor.
* Habilite la escucha para borrar la caché de cada instancia de AEM (publicación y autor) agregando la configuración `com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json` en su proyecto como se muestra [aquí](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json).
   * La configuración debe habilitarse tanto para instancias de autor como de publicación.
   * Habilitar la caché de Dispatcher (opcional): puede habilitar la configuración Borrar caché de Dispatcher estableciendo la propiedad `enableDispatcherCacheInvalidation` en true en la configuración anterior. Esto proporciona funcionalidad para borrar la caché de Dispatcher.

  >[!NOTE]
  >
  > Esto solo funciona con instancias de publicación.
  > * Además, asegúrese de proporcionar el patrón correspondiente que se adapte a su producto, categoría y página de CMS debe añadirse al archivo de configuración anterior para eliminarlo de la caché de Dispatcher.
* Para mejorar el rendimiento de las consultas SQL para encontrar la página correspondiente relacionada con el producto y la categoría, agregue el índice correspondiente en el proyecto (recomendado). Para obtener más información, consulte [cifCacheInvalidationSupport/]&#x200B;(vínculo https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml).

## Verificación de la función Borrar caché {#verify-clear-cache}

Para comprobar que todo está configurado correctamente:

* Almacene en déclencheur el servlet correspondiente en la instancia de autor AEM, por ejemplo [http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache), y debería obtener una respuesta HTTP 200.
* Compruebe que se ha creado un nodo en la siguiente ruta de acceso en instancias de autor: `/var/cif/cacheinvalidation`. El nombre del nodo sigue este patrón: `cmd_{{timestamp}}`.
* Compruebe que se ha creado el mismo nodo en cada instancia de publicación.

Ahora, para comprobar si las cachés se están borrando correctamente:
1. Navegue hasta las páginas PLP y PDP correspondientes.
2. Actualice el nombre de un producto o categoría en el motor de comercio. Los cambios no se reflejan en AEM inmediatamente en función de las configuraciones de caché.
3. Almacene en déclencheur la API de servlet como se muestra aquí:

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ••••••' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

Si todo va bien, los nuevos cambios se reflejan en cada instancia. Si los cambios no se reflejan para la instancia de publicación, compruebe en la ventana privada las páginas PLP y PDP correspondientes.

>[!NOTE]
>
> Las instancias de publicación pueden tener varios niveles de capas de caché. La función solo es responsable de borrar la caché de la memoria interna de AEM y de Dispatcher.

## Borrar API de invalidación de caché {#clear-cache-api}

Esta es la API que debe almacenar en déclencheur siempre que desee borrar la caché de los datos relacionados con el comercio de AEM.

Tipo de solicitud: `POST`

### Encabezados

| Parámetro | Valor | Obligatorio/Obligatorio | Comentar |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | Requerido |  |
| `Authorization` | Credenciales de usuario del autor correspondiente (tipo de autenticación: autenticación básica) | Requerido | Añada el nombre de usuario y la contraseña correspondientes. |


### Carga útil

La siguiente tabla muestra los atributos existentes que la función proporciona de forma predeterminada. Estas propiedades de `InvalidateType` deben proporcionarse en combinación con un atributo obligatorio (como `storePath`).

| `invalidateType` | Valor | Tipo (Matriz/Cadena/Booleano) | ¿Borrará esto la caché de Dispatcher? | Comentar |
|------------------------------|-------------------|---|---|---|
| `productSkus` | Sku del producto, que debe invalidarse de la caché. | Matriz | Sí | Borre la caché de la memoria interna mediante el siguiente patrón:<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>Borre la caché de la página PDP de los SKU correspondientes</li><li>Borrar caché de la página de categorías correspondiente en la que existe(según la respuesta de graphql de commerce)</li><li>Borre la caché en función de la siguiente consulta:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | Uid de categoría: que debe invalidarse de la caché. | Matriz | Sí | Borre la caché de la memoria interna mediante el siguiente patrón:<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>Borre la memoria caché de las páginas de categorías para los datos correspondientes (incluida su página de categoría secundaria)</li><li>Borrar todas las páginas de PDP que tengan las categorías correspondientes</li><li>Borre la caché en función de la siguiente consulta:</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | Si necesita borrar los datos de respuesta de GraphQL basados en el patrón regex, utilice esta opción. | Matriz | No | |
| `cacheNames` | Estos valores se definen en la correspondiente fábrica de configuración del cliente de CIF GraphQL > Configuración de GraphQL de StorePath correspondiente > Configuraciones de caché de GraphQL | Matriz | No | |
| `invalidateAll` | Verdadero o falso | Booleano | Sí | |

Esta tabla muestra la propiedad obligatoria que debe pasarse en cada llamada de API:

| Propiedad | Valor | Tipo (Matriz/Cadena/Booleano) | ¿Borrará esto la caché de Dispatcher? | Comentar |
|------------------------------|-------------------|---|---|---|
| `storePath` | Valor correspondiente de la ruta de acceso del sitio desde el que debe eliminarse la caché (Ejemplo: `/content/venia/us/en` como referencia con un proyecto de venia). | Cadena | Sí | Esto se debe administrar con la combinación de `invalidateType.` |


### Ejemplo de solicitud de API

```
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## Extensibilidad {#clear-cache-extensibility}

Esta función no solo ofrece su funcionalidad principal, sino que también ofrece extensibilidad, lo que permite a los desarrolladores desarrollarla y personalizarla según sea necesario.

### Ampliación del atributo existente {#existing-attribute}

En los casos en que sea necesario borrar la caché que actualmente no están cubiertos por la funcionalidad basada en atributos existente (como `categoryUids`), puede hacer referencia a [este archivo de referencia](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java) para agregar nuevos patrones y definir `invalidatePaths` adicionales que deben borrarse de la caché más allá de lo que administra la implementación actual.

### Añadir nuevo atributo personalizado {#new-custom-attribute}

Si, por ejemplo, no desea utilizar el atributo existente para borrar la caché, tiene la flexibilidad de crear su propio atributo y definir su funcionalidad correspondiente.

* Si solo necesita borrar la memoria caché de la memoria interna de AEM (la respuesta de graphql), debe seguir [esta referencia](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java).
* Si necesita borrar la caché de la memoria interna y de la caché de Dispatcher, debe seguir [esta referencia](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java).
  >[!NOTE]
  >
  > Puede omitir la caché de borrado interna devolviendo `null` para el método `getPatterns()`.
