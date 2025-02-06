---
title: Internacionalización de componentes
description: Internacionalice los componentes y los cuadros de diálogo para que las cadenas de la interfaz de usuario se puedan presentar en diferentes idiomas
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 401685af02c720994d72cd95d36f0cfcdf15d198
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Internacionalización de componentes{#internationalizing-components}

Internacionalice los componentes y los cuadros de diálogo para que las cadenas de la interfaz de usuario se puedan presentar en diferentes idiomas. Los componentes diseñados para la internacionalización permiten que las cadenas de interfaz de usuario se externalicen, traduzcan y luego se importen en el repositorio. Durante el tiempo de ejecución, las preferencias de idioma del usuario o la configuración regional de la página determinan qué idioma se muestra en la interfaz de usuario.

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

Realice el siguiente proceso para internacionalizar los componentes y proporcionar la interfaz de usuario en diferentes idiomas:

1. [Implemente sus componentes con código que internacionalice las cadenas.](/help/implementing/developing/extending/i18n/dev.md) Su código identifica las cadenas que se van a traducir y selecciona el idioma que se va a presentar durante la ejecución.
1. [Crear diccionarios](/help/implementing/developing/extending/i18n/translator.md#creating-a-dictionary).
1. AEM [Exporte](/help/implementing/developing/extending/i18n/translator.md#exporting-a-dictionary) el diccionario al formato XLIFF, traduzca las cadenas y vuelva a importar los archivos XLIFF a los archivos de formato XLIFF de la lista de distribución de archivos de la lista de archivos de la lista de archivos de la lista de archivos de la lista de archivos de la.
1. Incorpore el diccionario en el proceso de gestión de versiones de su aplicación.

>[!NOTE]
>
>Los métodos que se describen aquí para internacionalizar componentes están pensados para traducir cadenas estáticas. Cuando se espera que las cadenas de componentes cambien, se deben utilizar flujos de trabajo de traducción convencionales. Por ejemplo, cuando los autores pueden editar una cadena de interfaz de usuario mediante propiedades en el cuadro de diálogo Editar de un componente, no debe utilizar un diccionario de idioma para internacionalizar la cadena.

## Diccionarios de idiomas {#language-dictionaries}

AEM El marco de trabajo de internacionalización de la utiliza diccionarios en el repositorio para almacenar cadenas en inglés y sus traducciones en otros idiomas. El marco de trabajo utiliza el inglés como idioma predeterminado. Las cadenas se identifican con su versión en inglés. Normalmente, los marcos de internacionalización utilizan ID alfanuméricos para las cadenas de interfaz de usuario. El uso de la versión en inglés de la cadena como ID tiene varias ventajas:

* El código es fácil de leer.
* El idioma predeterminado siempre está disponible.

La [herramienta de traducción](/help/implementing/developing/extending/i18n/translator.md) le permite administrar todos los diccionarios desde una ubicación central.

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)

AEM Los cambios de traducción deben proceder de Git a través de la [canalización de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) en as a cloud service (servicio en la nube de as a Cloud Service) en el servicio de nube de Adobe Cloud Service.

### Superponer cadenas en diccionarios del sistema {#overlaying-strings-in-system-dictionaries}

AEM Si los componentes utilizan cadenas incluidas en los diccionarios del sistema de, duplique la cadena en su propio diccionario. Todos los componentes utilizarán las cadenas del diccionario.

Tenga en cuenta que no puede predecir qué traducción se utiliza cuando las cadenas están duplicadas en diccionarios que se encuentran todos debajo del nodo `/apps`.
