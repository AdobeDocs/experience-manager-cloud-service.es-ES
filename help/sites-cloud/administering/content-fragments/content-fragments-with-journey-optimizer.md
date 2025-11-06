---
title: Uso de fragmentos de contenido con Adobe Journey Optimizer
description: Descubra cómo se pueden integrar y utilizar los fragmentos de contenido con Adobe Journey Optimizer.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# Fragmentos de contenido con Adobe Journey Optimizer {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started) le ayuda a ofrecer a sus clientes experiencias conectadas, contextuales y personalizadas. Al integrar Adobe Experience Manager (AEM) as a Cloud Service con Adobe Journey Optimizer (AJO), puede reutilizar el contenido de AEM en sus canales entrantes de AJO y en sus canales salientes de AJO; incluidos la web, SMS, correo electrónico y otros.

Por ejemplo, puede hacer lo siguiente:

* incorpora sin problemas tus [fragmentos de contenido de AEM](/help/sites-cloud/administering/content-fragments/overview.md) en tu contenido de [correo electrónico de Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/email-landing-page)
* previsualice la experiencia de AJO directamente desde AEM

La conexión entre los fragmentos de contenido y AJO simplifica el proceso de acceso y uso del contenido de AEM, lo que permite crear campañas y recorridos personalizados y dinámicos.

Para obtener más información, comience con la documentación de AJO:

* [Uso de fragmentos de contenido en AJO](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html#integrations)
* [Ofertas de AJO de integración con fragmento de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Configuración de Dispatcher {#dispatcher-configuration}

Para permitir que AJO acceda a los fragmentos de contenido de AEM a través de la [API de administración de fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/), debe configurar Dispatcher:

* En `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

* Agregar:

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## Información adicional {#further-information}

Para obtener más información, consulte lo siguiente:

* La [extensión de referencias externas de AJO](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
