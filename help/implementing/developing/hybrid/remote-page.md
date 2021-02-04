---
title: Componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar la SPA React remota dentro de AEM.
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# El componente RemotePage {#remote-page-component}

Al decidir [qué nivel de integración](/help/implementing/developing/headful-headless.md) le gustaría tener entre la SPA externa y la AEM, a menudo queda claro que necesita poder realizar la vista y editar la SPA dentro de AEM. El componente RemotePage es un componente de página personalizado solo para este propósito.

## Información general {#overview}

El componente RemotePage obtiene todos los recursos necesarios del `asset-manifest.json` generado por la aplicación y lo utiliza para procesar el SPA dentro de AEM.

## Requisitos {#requirements}

* Habilitar CORS en desarrollo
* Configuración de la dirección URL remota en las propiedades de la página
* Representar el SPA en AEM

## Restricciones     {#limitations}

* La implementación actual del componente RemotePage solo admite aplicaciones de React remotas.
* La CSS interna definida en el archivo HTML raíz de la aplicación, así como la CSS en línea en el nodo DOM raíz, no estarán disponibles al realizar la representación remota en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto de SPA AEM, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
