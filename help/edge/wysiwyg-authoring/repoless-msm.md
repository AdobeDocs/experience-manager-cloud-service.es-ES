---
title: Repoless Multi Site Management
description: Conozca las recomendaciones de prácticas recomendadas sobre cómo configurar un proyecto con sitios multilingües que aprovechen una sola base de código de forma independiente.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Repoless Multi Site Management {#repoless-msm}

AEM Este documento supone que ya ha creado un sitio base para el proyecto denominado `my-aem-site` y que desea localizarlo mediante la característica de MSM de la aplicación de la función de traducción de recursos de la aplicación (MSM) que se encuentra en el sitio de base para el proyecto.

Si ya ha configurado el proyecto para el caso de uso de reinicios, la configuración de nube se asigna al nivel de la página raíz, `/content/my-aem-site`. Para sitios multilingües, esta asignación de configuración debe cambiarse a la raíz del idioma como `/content/my-aem-site/language-master/de`.

