---
title: AEM Assets y Biblioteca de medios de AEM
description: Preguntas más frecuentes sobre Recursos AEM y. Biblioteca de medios de AEM, incluidas las diferencias entre ambos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 3%

---


# AEM Assets frente a AEM MediaLibrary Preguntas más frecuentes {#aem-assets-vs-aem-medialibrary}

Recursos Adobe Experience Manager (AEM) es una parte integral de la plataforma AEM. Esta integración suave se considera una ventaja importante de AEM y garantiza la coherencia en el gestor de contenido y la alta productividad de los creadores de contenido.

## ¿Qué es AEM Assets? {#what-is-aem-assets}

AEM Assets es una aplicación de la plataforma AEM que permite a los clientes gestionar sus recursos digitales (imágenes, vídeos, documentos y clips de audio) en un repositorio basado en web. Recursos AEM incluye compatibilidad con metadatos, representaciones, el buscador de Digital Asset Management y administración mediante la interfaz de usuario.

## ¿Qué es AEM Media Library? {#what-is-the-aem-media-library}

AEM Media Library es una parte designada del repositorio de contenido de AEM WCM, donde se almacenan imágenes y otros recursos compartidos. La biblioteca de medios utiliza las funciones de administración de recursos digitales de AEM WCM.

## ¿Qué puedo obtener de Recursos AEM que no forman parte de AEM WCM? {#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

Las funciones únicas que solo están disponibles para los clientes de Recursos AEM son:

1. la capacidad para extraer y editar metadatos que no sean título, etiquetas y descripción.
1. el administrador de AEM Assets, disponible en la pantalla de bienvenida haciendo clic en el segundo botón situado junto al administrador del sitio.
1. Todos los pasos del flujo de trabajo relacionados con la administración de recursos digitales, a saber, AEM Assets Ingestion, AEM Assets Delete, AEM Assets Sub-Asset-Handling, extracción de metadatos de AEM Assets.
1. bibliotecas incluyendo el espacio del paquete im &quot;dam&quot;.

El uso de estas funciones requiere una licencia válida de Recursos AEM.

## ¿AEM Assets está disponible como paquete independiente? {#is-aem-assets-available-as-a-separate-package}

No. Para facilitar la instalación y la implementación, todas las aplicaciones y complementos de AEM se entregan en un único paquete con todas las funciones incluidas. Esto no implica que tenga permiso para utilizar todas las funciones del paquete.

## Quiero editar metadatos de recursos digitales. ¿Necesito Recursos AEM? {#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

Si tiene previsto editar metadatos que no sean título, descripción y etiquetas, deberá obtener una licencia de Recursos AEM.

## Quiero usar el predicado de categoría en mi sitio web. ¿Necesito Recursos AEM? {#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

Sí, el predicado de categoría, junto con todos los demás componentes utilizados en Geometrixx Press Center forman parte de AEM Assets y requieren una licencia de AEM Assets.

## Deseo cambiar automáticamente el tamaño de las imágenes al importarlas. ¿Necesito Recursos AEM? {#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

Sí. El cambio de tamaño de la imagen y la transformación automática impulsada por el flujo de trabajo, así como la capacidad de gestionar representaciones, forman parte de Recursos AEM y requieren una licencia de Recursos AEM.

## Quiero cambiar el tamaño de las imágenes con un componente de imagen personalizado. ¿Necesito Recursos AEM? {#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

El componente de imagen forma parte de AEM WCM. La biblioteca de gráficos que utiliza el componente de imagen (pero también AEM Assets) forma parte de la plataforma AEM y no requiere una licencia de Recursos AEM.

## ¿Cómo puedo evitar que mis usuarios utilicen Recursos AEM si no he otorgado licencias de Recursos AEM? {#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

Puede eliminar todos los flujos de trabajo, componentes, taxonomías, opciones específicos de Recursos AEM y el administrador de Recursos AEM de AEM. De este modo, evita que los usuarios utilicen accidentalmente las funciones de Recursos AEM que no obtuvo la licencia.

## Quiero añadir imágenes a una página y recortar y cambiar el tamaño de estas imágenes. ¿Necesito Recursos AEM? {#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

En este caso de uso no es necesario comprar Recursos AEM, incluso el uso de la biblioteca de medios no es necesario para utilizar imágenes en un sitio web, ya que el componente de imagen inteligente permite cargar imágenes directamente en la página.

## Una lista detallada de las funciones disponibles en Recursos AEM vs. Biblioteca de medios {#listoffeatures}

**AEM Assets**

* Colecciones y caja de luz
* Administración y propiedades avanzadas de metadatos
* Adobe Asset Link (conéctese a Creative Cloud para empresas)
* Aplicación de escritorio de AEM
* Perfiles de procesamiento
* Integración del servidor de InDesign
* Plantillas de activos y marco de productores de catálogos
* Recursos vinculados de Adobe Photoshop, Illustrator e InDesign
* Administración de activos multilingües
* Integración de PIM
* Rights Management
* Compatibilidad con RAW de cámara
* Administración y configuración de facetas de búsqueda
* flujos de trabajo DAM previamente compilados (por ejemplo, sesión fotográfica)
* Sistema de informes de recursos y análisis: Perspectivas de recursos
* Administración de activos 3D
* Recursos conectados
* Brand Portal
* Acceso a autoservicio
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
* Flujo de Actividad (escala de tiempo)
* Consulta Builder (API)
* Integración de Marketing Cloud
* Personalización y extensión de la interfaz de usuario
* Comentarios y anotaciones