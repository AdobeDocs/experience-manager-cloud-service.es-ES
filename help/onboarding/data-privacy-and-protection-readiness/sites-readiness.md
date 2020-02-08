---
title: Regulaciones de protección de datos y privacidad de datos - Adobe Experience Manager como preparación para sitios de servicios en la nube
description: 'Obtenga información sobre la compatibilidad de Adobe Experience Manager como sitios de servicios en la nube para las distintas normativas de protección de datos y privacidad de datos; incluyendo el Reglamento General de Protección de Datos de la UE (RGPD), la Ley de Privacidad del Consumidor de California y cómo cumplir al implementar un nuevo proyecto de AEM como servicio de nube. '
translation-type: tm+mt
source-git-commit: 1130e8a07bc3826380483a7560ebda7e8a17e238

---


# Adobe Experience Manager como preparación para sitios de servicios en la nube para la protección de datos y las regulaciones de privacidad de datos {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no se pretende sustituir al asesoramiento jurídico.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento acerca de las normas de protección de datos y privacidad de datos.

>[!NOTE]
>
>Para obtener más información sobre la respuesta de Adobe a los problemas de privacidad y lo que esto significa para usted como cliente de Adobe, consulte el Centro [de privacidad de](https://www.adobe.com/privacy.html)Adobe.

Adobe Experience Manager como sitios de servicios en la nube está listo para ayudar a los clientes con sus obligaciones de privacidad de datos y de cumplimiento de la protección. Esta página guía a los clientes a través de los procedimientos para gestionar dichas solicitudes en los sitios de AEM. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o con código.

Para obtener más información, consulte [Adobe Privacy Center](https://www.adobe.com/privacy.html).

>[!NOTE]
>
>Consulte [Adobe Experience Manager como preparación para servicios en la nube para protección de datos y normativas](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md) de privacidad de datos para obtener más información.

## Nivel de AEM Author {#aem-author-tier}

Las cuentas de usuario y el contenido UGC del servidor de creación se tratan en la documentación [de](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)AEM Foundation.

## Nivel de publicación de AEM {#aem-publish-tier}

Las cuentas de usuario utilizadas para autenticar a los visitantes en el sitio y el contenido UGC en el servidor de publicación se tratan en la documentación [de](/help/onboarding/data-privacy-and-protection-readiness/aem-readiness.md)AEM Foundation.

De forma predeterminada, los componentes de AEM Sites no almacenan los datos de formulario introducidos por los visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager está sujeto a un servicio de exclusión de cookies que se utiliza para administrar la inclusión y la exclusión de los usuarios.

Para la exclusión:

1. Ir a:
   [Centro de privacidad de Adobe: exclusión](https://www.adobe.com/privacy/opt-out.html)

1. Desplácese hacia abajo hasta **Servicios** : datos **de uso del servicio de** Experience Cloud.

1. Seleccione el vínculo al que se hace referencia; se titula **aquí**.

1. Se le presentarán los siguientes detalles, junto con las opciones de desactivación o desactivación:

   * Para optar por la exclusión del agregado y análisis de datos sobre su visita a este sitio, es necesario instalar una cookie en su explorador. Esta cookie identifica que usted ha optado por la exclusión.

      Si elimina la cookie de exclusión, o si cambia de equipo o de explorador Web, tendrá que volver a optar por la exclusión.

      Opción de exclusión: Excluirme del agregado y análisis de sesiones de visitantes (instalar la cookie de `amcglobal.sc.omtrdc.net` exclusión) - Haga clic aquí.

      Inclusión: Incluirme en el agregado y análisis de sesiones de visitantes (no instalar la cookie de `amcglobal.sc.omtrdc.net` exclusión). Haga clic aquí.
   Siga los pasos anteriores para acceder a los vínculos reales.

   >[!NOTE]
   >
   > Hay una descripción adicional en la sección Política **de** privacidad de las [Condiciones de uso](https://marketing.adobe.com/resources/help/en_US/terms.html).

## Analytics Foundation {#analytics-foundation}

AEM Sites incluye una integración opcional con Analytics Foundation que utiliza funciones dentro del servicio a petición de Adobe Analytics.

Para obtener más información sobre la administración de solicitudes de asunto de datos relacionadas con Adobe Analytics, consulte [Adobe Analytics y Privacidad](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-view-settings.html)de datos.

## Personalización por Target {#personalization-foundation-by-target}

AEM Sites incluye una integración opcional con Personalization Foundation por Target que utiliza funciones dentro del servicio a petición de Adobe Target.

Para obtener más información sobre la administración de solicitudes de asunto de datos relacionadas con Adobe Target, consulte [Adobe Target - Privacy and General Data Protection Regulation](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM proporciona una capa de datos opcional con ContextHub. Esto mantiene los datos específicos del visitante en el explorador, para utilizarlos en la personalización basada en reglas.

De forma predeterminada, los datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el navegador.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como opción predeterminada. Por lo tanto, un visitante del sitio web debe aceptar claramente antes de que cualquier dato personal se almacene en la persistencia del navegador (del lado del cliente).

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones que se relacionan con la protección de datos y la privacidad del sitio web deben mostrarse al visitante del sitio web, permitiéndole:

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

Para obtener una vista previa de la persistencia utilizada por ContextHub, un usuario puede:

* Utilice la consola del navegador; por ejemplo:

   * Chrome:

      * Abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

         * Almacenamiento local > (sitio web) > ContextHubPersistence
         * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Cookies > (sitio web) > SessionPersistence
   * Firefox:

      * Abra Herramientas para desarrolladores > Almacenamiento:

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
      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar el estado actual de la persistencia en todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

Para obtener una vista previa de la persistencia utilizada por ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence
   * Firefox: abra Herramientas para desarrolladores > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence


* Utilice la API de ContextHub, en la consola del navegador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`
      El almacén de ContextHub define qué capa de persistencia se utilizará, por lo que se debe comprobar el estado actual de la persistencia en todas las capas.


Por ejemplo, para ver los datos almacenados en localStorage:

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
