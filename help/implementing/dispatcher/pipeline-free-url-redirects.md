---
title: Redirecciones de URL sin canalizaciones
description: Obtenga información sobre cómo declarar redireccionamientos 301 o 302 sin acceso a canalizaciones de Git o Cloud Manager.
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: 7a543c8fe63166ef34999f23ce9b05de8e8b0e9f
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Redirecciones de URL sin canalizaciones {#pipeline-free-redirects}

Por varias razones, las organizaciones reescriben las URL de una manera que causa un redirección 301 (o 302), lo que significa que el explorador se redirige a un Página diferente.

Los escenarios incluyen:

* Se ha eliminado una página de HTML, por lo que se lleva al usuario a una página de reemplazo (a veces la página principal) en lugar de ver un error de `404 Page Not Found`.
* Una página de HTML renombrada.
* Optimización de SEO.

AEM as a Cloud Service ofrece [varios enfoques](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) para implementar redirecciones del lado del servidor, pero la estrategia descrita en este artículo, redirecciones sin canalización, es una buena opción cuando:

* Las personas que mantienen las redirecciones son usuarios empresariales, que no tienen el acceso necesario para confirmar los cambios de archivo en el control de código fuente o la posibilidad de ejecutar una canalización de configuración de nivel web de Cloud Manager.
* El número de redirecciones va de unas pocas a decenas de miles.
* Desea la opción de una interfaz de usuario, ya sea creada como un proyecto personalizado o usando el [Administrador de mapas de redireccionamiento de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) o [Administrador de redireccionamiento de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html).

El núcleo de esta característica es la capacidad de AEM Apache/Dispatcher para cargar (o recargar) uno o más archivos de mapas de reescritura que se han colocado en una ubicación específica en el publicar repositorio (para que se pueda descargar desde AEM publicar). Es importante mencionar que la forma en que los archivos llegan allí está fuera del ámbito de esta característica, pero puede considerar uno de los siguientes métodos:

* Ingerir el mapa de reescritura como un recurso en la interfaz de usuario de autor y publicarlo.
* Instalando [ACS Commons Redirect Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) ([al menos la versión 6.7.0 o superior](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), que incluye una interfaz de usuario para administrar las asignaciones de URL y también puede publicar el archivo de asignación de reescritura.
* Instalando [ACS Commons Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) ([al menos la versión 6.10.0 o superior](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)), que también incluye una interfaz de usuario para administrar las asignaciones de URL y también puede publicar el archivo de asignación de reescritura.
* Flexibilidad total al escribir una aplicación personalizada. Por ejemplo, una interfaz de usuario o de línea de comandos para administrar las asignaciones de URL o, alternativamente, un formulario para cargar una asignación de reescritura, que luego utiliza las API de AEM para publicar el archivo de asignación de reescritura.

>[!NOTE]
> Esta característica requiere la versión de AEM **18311 o superior**.

>[!NOTE]
> El uso de esta característica del Administrador de mapas de redireccionamiento requiere ACS Commons versión **6.7.0 o superior**, mientras que el uso de Redirect Manager requiere la versión **6.10.0 o superior**.

Para obtener una guía detallada de implementación paso a paso, consulte el tutorial [Implementación de redirecciones de URL sin canalización](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects).

## El mapa de reescritura {#rewrite-map}

El servidor HTTP Apache recarga el mapa de reescritura (si se cambia) cada 300 segundos de forma predeterminada (el valor es configurable). El formato de archivo debe seguir el archivo RewriteMap del mapa clave-valor sin formato formato describe en la documentación[&#128279;](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt) de Apache.

Se debe crear un archivo con nombre `managed-rewrite-maps.yaml` para especificar la ubicación del archivo de mapa de reescritura y debe implementarse una vez, mediante la canalización de pila completa de Cloud Manager o la canalización de nivel web. El archivo debe crearse en la carpeta src/inclusión[&#128279;](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) de la [configuración de Dispatcher. Asegúrese de utilizar la estructura](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure) de archivos de modo flexible.

Puede configurarlo con el siguiente patrón:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

Si, por ejemplo, el método elegido para colocar el archivo de asignación de reescritura es ingerirlo en AEM como un recurso denominado `mysite-redirectmap.txt` y, a continuación, publicarlo, puede especificar una carpeta en `/content/dam`:

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

A continuación, en un archivo de configuración de Apache como `rewrites/rewrite.rules` o `<yourfile>.vhost`, debe configurar el archivo de asignación al que hace referencia la propiedad de nombre (`my.map` en el ejemplo anterior). Una vez cargado, este archivo de asignación se guarda en el almacenamiento local de Dispatcher en la ubicación **fija** `/tmp/rewrites/`.

La directiva `RewriteMap` debe indicar que los datos se almacenan en un formato de archivo de administrador de base de datos (DBM) utilizando el formato `sdbm` (DBM simple), y la ruta de acceso completa del archivo se deriva del prefijo de ubicación de almacenamiento y de la propiedad name.

El resto de la configuración depende del formato de `redirectmap.txt`. El formato más sencillo, que se muestra en el ejemplo siguiente, es una asignación individual entre la dirección URL original y la asignada:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```

## Consideraciones {#considerations}

Tenga en cuenta lo siguiente:

* De forma predeterminada, al cargar un mapa de reescritura, Apache se inicia sin esperar a que se carguen los archivos de mapa completos, por lo que puede haber inconsistencias temporales hasta que se carguen los mapas completos. Esta configuración se puede cambiar para que Apache espere a que se cargue todo el contenido del mapa, pero Apache tarda más en inicio. Para cambiar este comportamiento para que Apache espere, añádalo `wait:true` `managed-rewrite-maps.yaml` al archivo.
* Para cambiar el Frecuencia entre cargas, añádalo `ttl: <integer>` `managed-rewrite-maps.yaml` al archivo. Por ejemplo: `ttl: 120`.
* Apache tiene un límite de longitud de 1024 para las entradas únicas de RewriteMap.

## Tutoriales {#tutorials}

1. [Implementación de redirecciones de URL sin canalización](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects)
1. [URL redirecciones](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection)
