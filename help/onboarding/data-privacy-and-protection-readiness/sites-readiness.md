---
title: 'Normas de protección de datos y privacidad de datos: Adobe Experience Manager como Cloud Service está listo para los sitios'
description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager como Cloud Service Sites con las distintas normas de protección de datos y privacidad de datos; incluyendo el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Privacidad del Consumidor de California y cómo cumplir con la implementación de un nuevo AEM como proyecto Cloud Service. '
translation-type: tm+mt
source-git-commit: 7b5a427853075054d56bc7ea6569d5d839e282a1
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---


# Adobe Experience Manager como Cloud Service está preparado para la protección de datos y las regulaciones de privacidad de datos {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido del presente documento no constituye asesoramiento jurídico y no sustituye al asesoramiento jurídico.
>
>Consulte con el departamento legal de su compañía para obtener asesoramiento sobre las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta del Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte [Centro de privacidad de Adobe](https://www.adobe.com/privacy.html).

Adobe Experience Manager como Cloud Service de sitios está listo para ayudar a los clientes con sus obligaciones de cumplimiento de protección y privacidad de datos. Esta página guía a los clientes a través de los procedimientos para gestionar dichas solicitudes en AEM Sites. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o con código.

Para obtener más información, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Consulte [Adobe Experience Manager como Cloud Service listo para la protección de datos y las normas de privacidad de datos](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) para obtener más información.

## Nivel de AEM Author {#aem-author-tier}

Las cuentas de usuario y el contenido UGC del servidor de creación se tratan en la [documentación de AEM Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

## Nivel de AEM Publish {#aem-publish-tier}

Las cuentas de usuario utilizadas para autenticar visitantes en el sitio y el contenido de UGC en el servidor de publicación se tratan en la [documentación de AEM Foundation](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md).

De forma predeterminada, los componentes de AEM Sites no almacenan datos de formulario introducidos por visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager está sujeto a un servicio de exclusión de cookies que se utiliza para administrar la inclusión y la exclusión de los usuarios.

Para la exclusión:

1. Ir a:
   [Centro de privacidad de Adobe: exclusión](https://www.adobe.com/privacy/opt-out.html)

1. Desplácese hacia abajo hasta **Servicios** - **datos de uso del servicio de Experience Cloud**.

1. Seleccione el vínculo al que se hace referencia; se titula **aquí**.

1. Se le presentarán los siguientes detalles, junto con las opciones para exclusión o en:

   * Para optar por la exclusión del agregado y la análisis de datos sobre su visita a este sitio, es necesario instalar una cookie en su explorador. Esta cookie identifica que usted ha optado por la exclusión.

      Si elimina la cookie de exclusión, o si cambia de equipo o de explorador Web, tendrá que volver a optar por la exclusión.

      Opción de exclusión: Excluirme de la agregación y análisis de sesiones de visitante (instalar la cookie de exclusión `amcglobal.sc.omtrdc.net`) - Haga clic aquí.

      Inclusión: Incluirme en la agregación y análisis de sesiones de visitante (no instalar la cookie de exclusión `amcglobal.sc.omtrdc.net`) - Haga clic aquí.
   Siga los pasos anteriores para acceder a los vínculos reales.

   >[!NOTE]
   >
   > Hay otra descripción en el **2. Privacidad.** de las Condiciones de uso [ generales del ](https://www.adobe.com/legal/terms.html)Adobe.

## Analytics Foundation {#analytics-foundation}

AEM Sites incluye una integración opcional con Analytics Foundation que utiliza la funcionalidad del servicio a petición de Adobe Analytics.

Para obtener más información sobre la administración de solicitudes de asunto de datos relacionadas con Adobe Analytics, consulte [Adobe Analytics y Privacidad de datos](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html).

## Personalización por Destinatario {#personalization-foundation-by-target}

AEM Sites incluye una integración opcional con Personalization Foundation por Destinatario que utiliza la funcionalidad dentro del servicio a petición de Adobe Target.

Para obtener más información sobre la administración de solicitudes de asunto de datos relacionadas con Adobe Target, consulte [Adobe Target - Privacy and General Data Protection Regulation](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM proporciona una capa de datos opcional con ContextHub. Esto mantiene los datos específicos del visitante en el navegador, para utilizarlos en la personalización basada en reglas.

De forma predeterminada, estos datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el explorador.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como opción predeterminada. Por lo tanto, un visitante del sitio web debe estar claramente de acuerdo, antes de que cualquier dato personal se almacene en la persistencia del navegador (del lado del cliente).

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones que se relacionan con la protección de datos y la privacidad del sitio web deben mostrarse en el visitante del sitio web, permitiéndoles:

   * aceptar
   * rechazar
   * cambiar la opción anterior

* Si un visitante del sitio acepta los términos y condiciones del sitio, se debe eliminar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Si un visitante del sitio no acepta los términos y condiciones del sitio, se debe configurar la cookie de exclusión de ContextHub:

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Para comprobar si ContextHub se está ejecutando en modo de exclusión, se debe realizar la siguiente llamada en la consola del explorador:

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Vista previa de la persistencia de ContextHub {#previewing-persistence-of-contexthub}

Para obtener la previsualización de la resistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del navegador; por ejemplo:

   * Chrome:

      * Abra Herramientas de desarrollador > Aplicación > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Firefox:

      * Abra Herramientas de desarrollador > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Safari:

      * Abra Preferencias > Avanzadas > Mostrar menú Desarrollar en la barra de menús
      * Abra Desarrollar > Mostrar consola de JavaScript

         * Consola > Almacenamiento > Almacenamiento local > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Cookies > (sitio web) > ContextHubPersistence
   * Internet Explorer:

      * Abrir Herramientas para desarrolladores > Consola

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar la vista del estado actual de la persistencia.


Por ejemplo, para vista de datos almacenados en localStorage:

Para obtener la previsualización de la resistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence
   * Firefox: abra Herramientas de desarrollador > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence


* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar la vista del estado actual de la persistencia.


Por ejemplo, para vista de datos almacenados en localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Borrado de la persistencia de ContextHub {#clearing-persistence-of-contexthub}

Para borrar la persistencia de ContextHub:

* Para borrar la persistencia de los almacenes cargados actualmente:

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Para borrar una capa de persistencia específica; por ejemplo, sessionStorage:

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Para borrar todas las capas de persistencia de ContextHub, se debe llamar al código adecuado para todas las capas:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
