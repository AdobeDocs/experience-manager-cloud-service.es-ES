---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar la SPA React remota dentro de AEM.
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# El componente RemotePage {#remote-page-component}

Al decidir [qué nivel de integración](/help/implementing/developing/headful-headless.md) le gustaría tener entre su SPA externa y AEM, a menudo queda claro que necesita poder ver y editar la SPA dentro de AEM. El componente RemotePage es un componente de página personalizado solo para este fin.

## Información general {#overview}

El componente RemotePage recupera todos los recursos necesarios del `asset-manifest.json` generado por la aplicación y lo utiliza para procesar el SPA dentro de AEM.

* RemotePage permite insertar las secuencias de comandos y las hojas de estilo de una SPA en el cuerpo de un componente de página de AEM.
* Los componentes del front-end virtual permiten marcar secciones como editables en AEM SPA Editor.
* En conjunto, una SPA alojada en un dominio diferente puede editarse en AEM.

Consulte el artículo [Edición de una SPA externa en AEM](editing-external-spa.md) para obtener más información sobre las SPA externas editables en AEM.

## Requisitos {#requirements}

* Habilitar CORS en desarrollo
* Configuración de URL remota en Propiedades de página
* Representar el SPA en AEM

## Restricciones     {#limitations}

* La implementación actual del componente RemotePage solo admite aplicaciones React remotas.
* El CSS interno definido en el archivo HTML raíz de la aplicación, así como el CSS en línea en el nodo DOM raíz, no estarán disponibles al realizar el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto de SPA de AEM, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
