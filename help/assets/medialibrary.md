---
title: AEM Assets y Biblioteca de medios de AEM
description: Preguntas más frecuentes sobre AEM Assets y. Biblioteca de medios AEM, incluidas las diferencias entre los dos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e98179379a97e7270b755042928133ddbd8de3fa
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 3%

---


# Preguntas frecuentes de AEM Assets y AEM MediaLibrary {#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager (AEM) Assets es una parte integral de la plataforma AEM. Esta integración suave se considera una ventaja importante de la AEM y garantiza la consistencia en gestor de contenido y alta productividad para los autores de contenido.

## ¿Qué es AEM Assets? {#what-is-aem-assets}

AEM Assets es una aplicación de la Plataforma de AEM que permite a nuestros clientes gestionar sus recursos digitales (imágenes, vídeos, documentos y clips de audio) en un repositorio basado en web. AEM Assets incluye compatibilidad con metadatos, representaciones, el buscador de Digital Asset Management y administración a través de la interfaz de usuario.

## ¿Qué es la biblioteca de medios AEM? {#what-is-the-aem-media-library}

La biblioteca de medios de AEM es una parte designada del repositorio de contenido de WCM AEM donde se almacenan las imágenes y otros recursos compartidos. La biblioteca de medios utiliza las funciones de administración de recursos digitales de AEM WCM.

## ¿Qué obtengo de AEM Assets que no forma parte de AEM WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Las funciones únicas que solo están disponibles para los clientes de AEM Assets son:

1. La capacidad para extraer y editar metadatos que no sean título, etiquetas y descripción.
1. El administrador de AEM Assets, disponible en la pantalla de bienvenida haciendo clic en la segunda opción junto a `siteadmin`.
1. Todos los pasos del flujo de trabajo relacionados con la administración de recursos digitales, a saber, AEM Assets Ingestion, AEM Assets Delete, AEM Assets Sub-Asset-Handling, AEM Assets metadata extracción.
1. Bibliotecas que incluyen &quot;dam&quot; en el espacio del paquete.

El uso de estas funciones requiere una licencia válida de AEM Assets.

## ¿AEM Assets está disponible como paquete independiente? {#is-aem-assets-available-as-a-separate-package}

No. Para facilitar la instalación e implementación, todas las aplicaciones y complementos AEM se entregan en un único paquete con todas las funcionalidades incluidas. Esto no implica que tenga permiso para utilizar todas las funciones del paquete.

## Quiero editar metadatos de recursos digitales. ¿Necesito AEM Assets? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si planea editar metadatos que no sean título, descripción y etiquetas, es necesario otorgar licencias de AEM Assets.

## Quiero usar el predicado de categoría en mi sitio web. ¿Necesito AEM Assets? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sí, el predicado de categoría, junto con todos los demás componentes son parte de AEM Assets y requieren una licencia de AEM Assets.

## Deseo cambiar automáticamente el tamaño de las imágenes al importarlas. ¿Necesito AEM Assets? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Sí. El cambio de tamaño de la imagen y la transformación automática impulsada por el flujo de trabajo, así como la capacidad de administrar representaciones, forman parte de AEM Assets y requieren una licencia de AEM Assets.

## Quiero cambiar el tamaño de las imágenes con un componente de imagen personalizado. ¿Necesito AEM Assets? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

El componente de imagen forma parte de AEM WCM. La biblioteca de gráficos que utiliza el componente de imagen (pero también AEM Assets) forma parte de la plataforma de AEM y no requiere una licencia de AEM Assets.

## ¿Cómo puedo evitar que mis usuarios utilicen AEM Assets si no he obtenido la licencia de AEM Assets? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puede eliminar todos los flujos de trabajo, componentes, taxonomías, opciones específicos de AEM Assets y el administrador de AEM Assets de AEM. Al hacerlo, evita que los usuarios utilicen accidentalmente las funciones de AEM Assets que no obtuvo la licencia.

## Quiero añadir imágenes a una página y recortar y cambiar el tamaño de estas imágenes. ¿Necesito AEM Assets? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

En este caso de uso no es necesario comprar AEM Assets, incluso el uso de la biblioteca de medios no es necesario para utilizar imágenes en un sitio web, ya que el componente de imagen inteligente permite cargar imágenes directamente en la página.

## Una lista detallada de las funciones disponibles en AEM Assets vs. Biblioteca de medios {#listoffeatures}

**AEM Assets**

* Colecciones y caja de luz
* Administración y propiedades avanzadas de metadatos
* Vínculo de recurso de Adobe (conexión con Creative Cloud para empresas)
* Aplicación de escritorio de AEM
* Perfiles de procesamiento
* Integración del servidor InDesign
* Plantillas de activos y marco de productores de catálogos
* Recursos vinculados a Adobe Photoshop, Illustrator y InDesign
* Administración de activos multilingües
* Integración de PIM
* Rights Management
* Asistencia Camera Raw
* Administración y configuración de facetas de búsqueda
* Flujos de trabajo DAM previamente compilados (por ejemplo, sesión fotográfica)
* Sistema de informes de recursos y análisis: Perspectivas de recursos
* Administración de activos 3D
* Recursos conectados
* Brand Portal
* Acceso de autoservicio
* Explorar, buscar y descargar
* Colecciones y uso compartido de carpetas
* Herramientas de administración
* Etiquetas inteligentes
* Búsqueda visual
* Interfaz de usuario del administrador de recursos

**Biblioteca de medios**

* Propiedades de metadatos básicas
* Administración de etiquetas
* Control de versión
* Representaciones estáticas
* Proyectos, Tareas, creación de flujos de trabajo
* Flujo de actividad (escala de tiempo)
* Consulta Builder (API)
* Integración de Marketing Cloud
* Personalización y extensión de la interfaz de usuario
* Comentarios y anotaciones