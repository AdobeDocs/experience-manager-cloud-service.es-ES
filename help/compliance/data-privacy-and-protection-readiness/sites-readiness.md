---
title: 'Reglamentos de protección de datos y privacidad de datos: preparación para AEM Sites'
description: Obtenga información sobre la compatibilidad de Experience Manager as a Cloud Service Sites con los distintos reglamentos de protección de datos y privacidad de datos; incluidos el Reglamento general de protección de datos (RGPD) de la UE y la Ley de Privacidad del Consumidor de California, y cómo cumplirlos al implementar un nuevo proyecto de AEM as a Cloud Service.
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
feature: Compliance
role: Admin, Developer, Leader
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 100%

---

# Preparación de Experience Manager Sites para las regulaciones de protección de datos y de privacidad de datos {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>El contenido de este documento no constituye asesoramiento jurídico y no está pensado para sustituirlo.
>
>Consulte con el departamento legal de su empresa para obtener asesoramiento sobre los reglamentos de protección y privacidad de datos.

>[!NOTE]
>
>Para obtener más información acerca de la respuesta de Adobe a los problemas de privacidad y lo que esto supone para usted como cliente de Adobe, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

Adobe Experience Manager as a Cloud Service Sites está listo para ayudar a los clientes con sus obligaciones de cumplimiento de la protección y la privacidad de datos. Esta página guía a los clientes a través de los procedimientos para tratar estas solicitudes en AEM Sites. Describe la ubicación de los datos privados almacenados y cómo eliminarlos manualmente o mediante programación.

Para obtener más información, consulte el [Centro de privacidad de Adobe](https://www.adobe.com/es/privacy.html).

>[!NOTE]
>
>Consulte [Preparación de Adobe Experience Manager as a Cloud Service para los reglamentos de protección de datos y privacidad de datos](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md) para obtener más información.

## Nivel de AEM Author {#aem-author-tier}

Las cuentas de usuario y el contenido generado por usuarios en el servidor de creación se tratan en la [Documentación de AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Nivel de AEM Publish {#aem-publish-tier}

Las cuentas de usuario utilizadas para autenticar a los visitantes en el sitio y el contenido generado por usuarios en el servidor de publicación se tratan en la [Documentación de AEM Foundation](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md).

De forma predeterminada, los componentes de AEM Sites no almacenan los datos de formulario introducidos por los visitantes en el servidor de publicación. Se recomienda reenviar los datos a un sistema de terceros o a Adobe Campaign para un procesamiento posterior.

## Inclusión/exclusión {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager está sujeto a un servicio de exclusión de cookies que se utiliza para administrar la inclusión/exclusión de los usuarios.

Para la exclusión:

1. Vaya a:
   [Centro de privacidad de Adobe: exclusión](https://www.adobe.com/es/privacy/opt-out.html)

1. Desplácese hacia abajo hasta **Servicios** - **Datos de uso del servicio de Experience Cloud**.

1. Seleccione el vínculo al que se hace referencia; actualmente con el título **aquí**.

1. Se le presentarán los siguientes detalles, junto con las opciones de exclusión o inclusión:

   * Para no participar en la agregación y el análisis de los datos acerca de su visita a este sitio, es necesario instalar una cookie en su explorador. Esta cookie identifica que se ha excluido.

     Si elimina la cookie de exclusión, o si cambia de equipo o de explorador web, tendrá que volver a excluirse.

     Exclusión - Excluirme del análisis y la agregación de sesiones del visitante (instale la cookie de exclusión `amcglobal.sc.omtrdc.net`): haga clic aquí.

     Inclusión - Inclúyanme en el análisis y agregación de sesiones del visitante (no instale la cookie de exclusión `amcglobal.sc.omtrdc.net`): haga clic aquí.

   Siga los pasos anteriores para acceder a los vínculos reales.

   >[!NOTE]
   >
   > Hay una descripción adicional en la sección **2. Privacidad.** de las [Condiciones de uso generales de Adobe](https://www.adobe.com/es/legal/terms.html).

## Analytics Foundation {#analytics-foundation}

AEM Sites incluye una integración opcional con Analytics Foundation que utiliza la funcionalidad dentro del servicio bajo demanda de Adobe Analytics.

Para obtener más información sobre la administración de solicitudes de titulares de los datos relacionadas con Adobe Analytics, consulte [Adobe Analytics y privacidad de datos](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html?lang=es).

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites incluye una integración opcional con Personalization Foundation by Target que utiliza la funcionalidad dentro del servicio bajo demanda de Adobe Target.

Para obtener más información sobre la administración de solicitudes de titulares de los datos relacionadas con Adobe Target, consulte [Adobe Target: el reglamento general de protección de datos](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=es).

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM proporciona una capa de datos opcional con ContextHub. Esto mantiene los datos específicos del visitante en el explorador, para usarlos para la personalización basada en reglas.

De forma predeterminada, estos datos de visitante no se almacenan en AEM; AEM envía reglas a la capa de datos para tomar decisiones de personalización en el explorador.

### Implementación de la inclusión/exclusión {#implementing-opt-in-opt-out}

El propietario del sitio debe implementar un componente de exclusión según las siguientes directrices.

Estas directrices implementan la inclusión como predeterminada. Por lo tanto, un visitante de un sitio web debe aceptar claramente antes de que cualquier dato personal se almacene en la persistencia del explorador (del lado del cliente).

* El componente de exclusión debe incluirse cada vez que se incluya el componente ContextHub.
* Los términos y condiciones relacionados con la protección de datos y la privacidad del sitio web deben mostrarse al visitante del sitio web, lo que le permite:

   * Aceptar
   * Rechazar
   * Cambiar su opción anterior

* Si el visitante de un sitio acepta los términos y condiciones del sitio, se debe eliminar la cookie de exclusión de ContextHub:

  ```
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* Si el visitante de un sitio no acepta los términos y condiciones del sitio, se debe configurar la cookie de exclusión de ContextHub:

  ```
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* Para comprobar si ContextHub se está ejecutando en modo de exclusión, la siguiente llamada debe realizarse en la consola del explorador:

  ```
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### Previsualización de la persistencia de ContextHub {#previewing-persistence-of-contexthub}

Para obtener una vista previa de la persistencia utilizada en ContextHub, un usuario puede:

* Utilizar la consola del explorador; por ejemplo:

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

      * Abra Preferencias > Avanzado > Mostrar el menú Desarrollo en la barra de menús
      * Abra Desarrollo > Mostrar consola de JavaScript

         * Consola > Almacenamiento > Almacenamiento local > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Almacenamiento de sesión > (sitio web) > ContextHubPersistence
         * Consola > Almacenamiento > Cookies > (sitio web) > ContextHubPersistence

   * Internet Explorer:

      * Abra Herramientas para desarrolladores > Consola

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`

* Utilice la API de ContextHub en la consola del explorador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     El almacén de ContextHub define qué capa de persistencia se utiliza, por lo que para ver el estado actual de la persistencia se deben comprobar todas las capas.

Por ejemplo, para ver los datos almacenados en localStorage:

Para obtener una vista previa de la persistencia utilizada en ContextHub, un usuario puede:

* Utilice la consola del explorador:

   * Chrome: abra Herramientas para desarrolladores > Aplicación > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence

   * Firefox: abra Herramientas para desarrolladores > Almacenamiento:

      * Almacenamiento local > (sitio web) > ContextHubPersistence
      * Almacenamiento de sesión > (sitio web) > ContextHubPersistence
      * Cookies > (sitio web) > SessionPersistence

* Utilice la API de ContextHub en la consola del explorador:

   * ContextHub proporciona las siguientes capas de persistencia de datos:

      * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

     El almacén de ContextHub define qué capa de persistencia se utiliza, por lo que para ver el estado actual de la persistencia se deben comprobar todas las capas.

Por ejemplo, para ver los datos almacenados en localStorage:

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Eliminación de la persistencia de ContextHub {#clearing-persistence-of-contexthub}

Para borrar la persistencia de ContextHub:

* Para borrar la persistencia de las tiendas cargadas actualmente:

  ```
  // to be able to fully access persistence layer, Opt-Out must be turned off
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

* Para borrar todas las capas de persistencia de ContextHub, se debe llamar al código apropiado para todas las capas:

   * `ContextHub.Utils.Persistence.Modes.LOCAL` (predeterminada)
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
