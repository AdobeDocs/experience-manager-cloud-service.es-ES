---
title: Internacionalización de cadenas de IU
description: AEM proporciona una consola para administrar las distintas traducciones de textos utilizados en la interfaz de usuario del componente.
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Usar Translator para administrar diccionarios{#using-translator-to-manage-dictionaries}

AEM proporciona una consola para administrar las distintas traducciones de textos utilizados en la interfaz de usuario del componente. Esta consola está disponible en:

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

Utilice la herramienta de traducción para gestionar cadenas en inglés y sus traducciones. Los diccionarios se crean en el repositorio, por ejemplo, `/apps/myproject/i18n`.

La herramienta de traducción y los diccionarios que administra se utilizan para presentar la interfaz de usuario de los componentes en diferentes idiomas. Si desea traducir páginas, consulte [Traducción de contenido para sitios multilingües](/help/sites-cloud/administering/translation/overview.md).

## Crear un diccionario {#creating-a-dictionary}

AEM Los desarrolladores pueden crear diccionarios de i18n en el para administrar cadenas de componentes localizadas en el sitio de trabajo de la interfaz de usuario. Los diccionarios suelen formar parte del código de componente en `/apps`. AEM A continuación se muestra un ejemplo del código de WKND de con un par clave/valor que se utiliza en todos los componentes de WKND.

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

Los desarrolladores pueden crear diccionarios adicionales agregando un nodo raíz (`sling:Folder`) para un nuevo diccionario que contenga definiciones de idioma para cadenas de componentes.

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>Esta es la estructura del [módulo i18n de Sling](https://sling.apache.org/site/internationalization-support.html).

AEM AEM Una vez creados en un repositorio de GitHub de, los diccionarios se pueden implementar a través de una canalización de CD/CI [CI](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) de.

## Ubicaciones del diccionario {#dictionary-locations}

Los desarrolladores pueden crear un diccionario de idioma de origen en `/apps` o `/content/cq:i18n`. AEM Comenzando por el código de ejemplo del tipo de archivo de la, los diccionarios iniciales generalmente se encuentran en la ruta de acceso `/apps`. Si el objetivo es almacenar las copias de idioma de diccionario correspondientes también en `/apps`, los desarrolladores deben crear y mantener manualmente esas copias de idioma en el código de componente.

AEM Como alternativa, el nuevo proceso de traducción en tiempo de ejecución de la nueva versión de los diccionarios i18n creará diccionarios traducidos en `/content/cq:i18n/<projectName>`, independientemente de si el diccionario de origen está almacenado en `/apps` o `/content`.

Las decisiones sobre dónde ubicar los diccionarios i18n, las copias de origen y de idioma, deben tomarse según los siguientes criterios:

* `/apps`
   * AEM ubicación predeterminada para diccionarios con traducciones de cadenas de componentes, siguiendo el tipo de archivo de la y el código de ejemplo de WKND
   * orden de procesamiento más alto, por Sling ([Jerarquías de búsqueda del paquete de recursos](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies))
   * pero no es posible editar ni traducir diccionarios en tiempo de ejecución, ya que `/apps` es inmutable en entornos de AEM as a Cloud Service

* `/content/cq:i18n`
   * ubicación alternativa para diccionarios i18n si
      * se requiere la traducción en tiempo de ejecución de los diccionarios
      * se requiere la capacidad de editar un diccionario durante la ejecución
   * ubicación predeterminada en la que la traducción del diccionario de tiempo de ejecución creará copias de idioma.

Dado que `/apps` siempre reemplaza a `/content` en el orden de procesamiento de Sling, es importante tener en cuenta que los diccionarios con pares clave/valor idénticos no deben existir simultáneamente en `/apps` y `/content/cq:i18n`, ya que el diccionario de `/content/cq:i18n` nunca se utilizará para el procesamiento. Si ya existe una copia de idioma de diccionario, es decir, un destino de traducción, en `/apps`, y el objetivo es que se pueda traducir en tiempo de ejecución en AEM as a Cloud Service, entonces la copia de idioma de diccionario original en `/apps` debe moverse a `/content/cq:i18n` o eliminarse en `/apps` y volverse a crear automáticamente en `/content/cq:i18n` traduciendo el diccionario de origen. Este proceso de traducción creará automáticamente las copias de idioma en `/content/cq:i18n`.

## Creación automática de diccionario {#automatic-creation}

AEM AEM Para las páginas y fragmentos de experiencia de la que contengan componentes principales, el nuevo proceso de traducción de diccionarios también explorará esas páginas o fragmentos de experiencia para buscar componentes y cadenas de componentes que se deben traducir. El sistema creará automáticamente las copias de idioma de diccionario nuevas correspondientes en `/content/cq:i18n`. AEM Esto no se aplica a los fragmentos de contenido, ya que son contenido puro y estructurado sin el uso de componentes principales de la.

## Exportación de un diccionario {#exporting-a-dictionary}

Mientras que la traducción en tiempo de ejecución de diccionarios i18n en ubicaciones `/apps` o `/libs` no es posible en AEM as a Cloud Service AEM, ya que esas ubicaciones son inmutables, esos diccionarios se pueden exportar en tiempo de ejecución para su traducción asincrónica fuera de la.

Para exportar las cadenas de idioma de origen de un diccionario a un archivo XLIFF:

1. Abrir la herramienta de traducción `http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >AEM La herramienta solo está disponible a través de esta dirección URL y no se puede acceder a ella desde la interfaz de usuario del producto de la.

1. Utilice el menú desplegable Diccionarios para seleccionar el diccionario que desea exportar.
1. Haga clic en Exportar traducción XLIFF y, a continuación, en Exportar xliff `<locale>` completo.

## Importación de un diccionario {#importing-a-dictionary}

Para importar un archivo XLIFF en un diccionario para rellenar el contenido del diccionario:

1. Abrir la herramienta de traducción `http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. Haga clic en Importar y luego en Traducciones XLIFF.
1. Seleccione el archivo que desea importar y haga clic en Aceptar.
