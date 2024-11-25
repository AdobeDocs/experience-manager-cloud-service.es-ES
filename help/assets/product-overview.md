---
title: Información general sobre Content Hub
description: Obtenga más información sobre Content Hub, sus principales ventajas, cómo acceder a él y cómo dar su opinión sobre las opciones disponibles en él.
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 96%

---

# Información general sobre Content Hub {#overview-content-hub}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![Información general sobre Content Hub](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>La guía de Content Hub ya está disponible en formato de PDF. Descargue toda la guía y utilice Adobe Acrobat AI Assistant para responder a sus consultas.
>
>[!BADGE PDF de guía de Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Centro de contenido está disponible como parte de Experience Manager Assets as a Cloud Service para democratizar el acceso al contenido sobre la marca por parte de las organizaciones y sus socios comerciales. Se centra en la distribución de recursos para su activación a escala y la creación de variantes de contenido de la marca para mejorar la agilidad comercial.

## ¿Por qué utilizar Content Hub?

Content Hub ofrece las siguientes ventajas clave:

**Busque y comparta todos los recursos aprobados de la marca disponibles en un portal intuitivo**

AEM Assets sirve como una única fuente de confianza y todos los recursos aprobados están disponibles automáticamente en Content Hub en una jerarquía plana para mejorar la experiencia de búsqueda.

**Interfaz de usuario configurable**

Las propiedades más comunes del centro de contenido, como los filtros para la búsqueda, los campos disponibles al añadir o importar recursos, las propiedades de recursos o el contenido del titular para la promoción de la marca, se pueden configurar. Además, un administrador puede configurar fácilmente la interfaz de usuario de Content Hub según sus necesidades.

**Habilite a las personas no creativas para editar y crear versiones de contenido que sea fiel a la marca**

Content Hub le permite crear contenido nuevo con Adobe Express (si tiene derechos de Adobe Express). Puede editar el contenido existente con herramientas fáciles de usar, producir variaciones alineadas con la marca con plantillas y elementos de marca, y crear contenido nuevo con las últimas funciones de IA generativa de Adobe Firefly.

**Obtener información sobre cómo se usa el contenido en los equipos**

[!DNL Content Hub] proporciona información valiosa sobre los recursos que responde a un reto común con el que se encuentran a menudo los profesionales del marketing: las estadísticas de uso de los recursos utilizados en las campañas de marketing, los canales y las distintas regiones. Al obtener una comprensión clara del rendimiento y la popularidad de los recursos, proporciona información útil esencial para mejorar la experiencia del usuario.

## Requisitos previos {#prerequisites-content-hub}

Content Hub requiere un entorno de creación de producción de Experience Manager como servicio en la nube, versión 2024.6 o posterior (la versión mínima es 2024.6.16799).

## ¿Cómo acceder a Content Hub? {#access-content-hub}

[Después de configurar Content Hub](/help/assets/deploy-content-hub.md) y añadir un usuario al [perfil de producto de Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile), se puede acceder a este de las siguientes formas:

* Acceda a Content Hub a través del siguiente vínculo:

  `https://experience.adobe.com/#/assets/contenthub`

* Acceda a experience.adobe com y haga clic en **[!UICONTROL Content Hub de Experience Manager Assets]**, disponible en la sección **[!UICONTROL Acceso rápido]**:
  ![Acceso a Content Hub](assets/access-content-hub.png)

* Acceda a experience.adobe com y haga clic en **[!UICONTROL Content Hub de Experience Manager Assets]**, disponible en el conmutador de productos:
  ![Método 3 de acceso a Content Hub](assets/access-content-hub-alternate.png)



## Proporcionar comentarios sobre Content Hub {#provide-content-hub-feedback}

Para recomendar cualquier mejora relacionada con el producto, haga clic en **[!UICONTROL Comentarios]** junto al nombre de su organización en la parte superior de la interfaz de usuario de Content Hub.

Especifique un asunto, una descripción de la recomendación y adjunte archivos, si es necesario. Haga clic en **[!UICONTROL Enviar]** para enviar los comentarios a Adobe.

![Comentarios sobre Content Hub](assets/content-hub-feedback.png)

## Configuración de Content Hub para su equipo {#setup-content-hub}

Siga estos pasos para configurar Content Hub para su equipo:

1. [Habilite Content Hub para los recursos de Experience Manager mediante Cloud Manager](deploy-content-hub.md#enable-content-hub).

1. [Incorpore al administrador de Content Hub](deploy-content-hub.md#onboard-content-hub-administrator).

1. [Añada usuarios clave de Content Hub](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Los autores o administradores de DAM deben aprobar los recursos mediante recursos de Experience Manager](approve-assets.md).

1. [Los administradores pueden configurar la interfaz de usuario de Content Hub para otros usuarios](configure-content-hub-ui-options.md).

1. [Otorgue acceso a Content Hub a más usuarios del equipo](deploy-content-hub.md#onboard-content-hub-consumer-users).

1. [Acceda al portal de Content Hub](#access-content-hub).

1. [Proporcione comentarios sobre Content Hub](#provide-content-hub-feedback).


## Más información sobre las funcionalidades clave {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Implementación de Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>Configuración de la interfaz de usuario de Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Descubra cómo los administradores pueden configurar la interfaz de usuario de Content Hub. </em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="Búsqueda de recursos disponibles en Content Hub" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>Búsqueda de recursos disponibles en Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a utilizar diversas funciones para reducir los resultados de búsqueda.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Edición de imágenes mediante Adobe Express" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Editar imágenes utilizando Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a crear variantes de imágenes en Content Hub mediante Adobe Express</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="Compartir recursos disponibles en Content Hub" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>Compartir recursos disponibles en Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo compartir uno o varios recursos como vínculo y, a continuación, obtener acceso a ellos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="Administración de colecciones en Content Hub" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>Administración de colecciones en Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a crear colecciones utilizando recursos y, a continuación, administrarlos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Compartir recursos disponibles en Content Hub" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Ver información de los recursos en Content Hub</strong>
      </a>
   </div>
   <p>
      <em> El módulo de contenido proporciona información valiosa sobre los recursos y responde a un reto común con el que se encuentran a menudo los profesionales del marketing</em>.
   </p>
</td>
</table>
