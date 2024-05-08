---
title: Lista de comprobación para el lanzamiento
description: AEM Obtenga información acerca de todos los elementos que deben estar en su lugar para tener un lanzamiento exitoso con el servicio de vida en tiempo de ejecución de as a Cloud Service.
source-git-commit: 4a03e2fe3519fd9e0d8d646526ea6c9cc6637f52
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 6%

---


# Lista de comprobación para el lanzamiento {#Go-Live-Checklist}

Revise esta lista de actividades para asegurarse de que el lanzamiento se realiza correctamente y sin problemas.

* Ejecute una canalización de producción integral con pruebas funcionales y de interfaz de usuario para garantizar un **siempre actual** AEM Experiencia del producto de la. Consulte los siguientes recursos.
   * [Actualizaciones de la versión de AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Prueba funcional personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Pruebas de IU](/help/implementing/cloud-manager/ui-testing.md)
* AEM Si está migrando desde la versión 6.5 de la versión, debe migrar el contenido a producción y asegurarse de que haya un subconjunto relevante disponible en el ensayo para realizar pruebas.
   * AEM Las prácticas recomendadas de DevOps para los entornos de producción implican que el código asciende desde el desarrollo al entorno de producción, mientras que el contenido baja desde los entornos de producción.
* Programe un período de congelación de contenido y código.
   * Consulte también la sección [Cronología de congelación de código y contenido para la migración](#code-content-freeze)
* Realice la recarga final del contenido.
* Valide las configuraciones de Dispatcher.
   * Utilizar un validador de Dispatcher local que facilite la configuración, validación y simulación del Dispatcher localmente
      * [Configure las herramientas locales de Dispatcher.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
   * Revise detenidamente la configuración del host virtual.
      * La solución más fácil (y predeterminada) es incluir `ServerAlias *` en el archivo host virtual en el `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Esto permitirá que funcionen los alias de host utilizados por las pruebas funcionales del producto, la invalidación de la caché del despachante y los clones.
      * Sin embargo, si `ServerAlias *` no es aceptable, como mínimo lo siguiente `ServerAlias` se deben permitir las entradas además de los dominios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL y DNS.
   * Si utiliza su propia CDN, introduzca un ticket de asistencia para configurar el enrutamiento adecuado.
      * Consulte la sección [AEM Los puntos de CDN del cliente a CDN administrada de](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) en la documentación de CDN para obtener más información.
      * Configure SSL y DNS según la documentación de su proveedor de CDN.
   * Si no utiliza una CDN adicional, administre SSL y DNS según la siguiente documentación:
      * Administración de certificados SSL
         * [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Administración de nombres de dominio personalizados (DNS)
         * Para asegurarse de que la migración a DNS no introducirá problemas inesperados, es mejor crear un subdominio de prueba al que conectar la instancia de producción antes de publicarla y realizar una ronda de pruebas UAT. Por lo tanto, si el dominio es example.com, puede crear un subdominio test.example.com y aplicarlo a la producción. Durante la prueba UAT del dominio, querrá buscar cosas como la redirección de vínculos adecuada, el almacenamiento en caché y las configuraciones de Dispatcher.
         * [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Administrar el nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Recuerde validar el TTL establecido para el registro DNS.
      * El TTL es la cantidad de tiempo que un registro DNS permanece en una caché antes de solicitar una actualización al servidor.
      * Si tiene un TTL muy alto, las actualizaciones del registro DNS tardarán más en propagarse.
* Ejecute pruebas de rendimiento y seguridad que cumplan los requisitos y objetivos de su empresa.
   * Realizar pruebas en el entorno de ensayo.  Tiene el mismo tamaño que la producción.
   * Los entornos de desarrollo no tienen el mismo tamaño que los de fase y producción.
* Pase el ratón por encima y asegúrese de que el go-live real se realiza sin ninguna implementación nueva o actualización de contenido.
* Crear perfiles de notificación de usuario Admin Console. Consulte [Perfiles de notificación](/help/journey-onboarding/notification-profiles.md)
* Considere la posibilidad de configurar reglas de filtro de tráfico para controlar qué tráfico no debe permitirse en el sitio web.
   * Las reglas de filtro de tráfico de límite de velocidad pueden ser una herramienta eficaz contra ataques DDoS. Una categoría especial de reglas de filtro de tráfico, denominadas reglas WAF, requieren una licencia independiente.
   * Consulte la documentación para ver algunos [reglas de inicio sugeridas](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Siempre puede hacer referencia a la lista en caso de que necesite volver a calibrar las tareas durante el lanzamiento.