---
title: 'Creación de una carpeta de recursos: configuración sin encabezado'
description: Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 95624ebf1a77dac1f535e199b660096c8efdfa76
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 72%

---

# Creación de una carpeta de recursos: configuración sin encabezado {#creating-an-assets-folder}

Utilice modelos de fragmentos de contenido de AEM para definir la estructura de los fragmentos de contenido, la base del contenido sin encabezado. A continuación, los fragmentos de contenido se almacenan en carpetas de recursos.

## ¿Qué es una carpeta de recursos? {#what-is-an-assets-folder}

[Ahora que ha creado modelos de fragmentos de contenido](create-content-model.md) que definen la estructura que desea para los futuros fragmentos de contenido, probablemente tenga ganas de crear algunos fragmentos.

Sin embargo, primero debe crear una carpeta de recursos en la que almacenarlos.

Las carpetas de recursos se utilizan para [organizar los recursos de contenido tradicionales](/help/assets/manage-digital-assets.md) como imágenes y vídeos, junto con los fragmentos de contenido.

## Creación y configuración de una carpeta de Assets {#create-and-configure-an-assets-folder}

Un administrador solo tendría que crear carpetas ocasionalmente para organizar el contenido a medida que se crea. Utilice la consola de Assets para crear la nueva carpeta.

Una vez creada, debes aplicar tu [configuración](/help/headless/setup/create-configuration.md) a la carpeta. Para obtener más información, consulte [Aplicar la configuración a su carpeta](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder).

Puede crear subcarpetas adicionales dentro de la carpeta que ha creado. Las subcarpetas heredarán la **Configuración de nube** de la carpeta principal. Sin embargo, esto se puede sobrescribir si desea utilizar modelos de otra configuración.

Si está usando una estructura de sitio localizada, puede [crear una raíz de idioma](/help/assets/translate-assets.md) debajo de la nueva carpeta.

## Siguientes pasos {#next-steps}

Ahora que ha creado una carpeta para los fragmentos de contenido, puede pasar a la cuarta parte de la guía de introducción y [crear fragmentos de contenido](create-content-fragment.md).

>[!TIP]
>
>Para obtener información detallada acerca de la administración de fragmentos de contenido, consulte la [Documentación de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)
