---
title: Lista de comprobación para el lanzamiento
description: Obtenga información acerca de todos los elementos que deben estar presentes para que el lanzamiento de AEM as a Cloud Service sea un éxito.
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# Lista de comprobación para el lanzamiento {#Go-Live-Checklist}

Revise esta lista de actividades para asegurarse de que el lanzamiento se realiza correctamente y sin problemas.

* Ejecute una canalización de producción integral con pruebas funcionales y de IU para garantizar una experiencia de producto de AEM **siempre actual**. Consulte los siguientes recursos.
   * [Actualizaciones de la versión de AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Prueba funcional personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Pruebas de IU](/help/implementing/cloud-manager/ui-testing.md)
* Si está migrando desde la versión AEM 6.5, debe migrar el contenido a producción y asegurarse de que un subconjunto relevante esté disponible en el ensayo de las pruebas.
   * Las prácticas recomendadas de DevOps para AEM implican que el código asciende del desarrollo al de producción, mientras que el contenido desciende desde los entornos de producción.
* Programación de un código y del período de congelación de contenido.
   * Consulte también la sección [Cronologías de código y de congelación de contenido para la migración](#code-content-freeze)
* Realice una recarga de contenido final.
* Valide las configuraciones de Dispatcher.
   * Utilice un validador de Dispatcher local que facilite la configuración, validación y simulación de Dispatcher localmente
      * [Configure las herramientas locales de Dispatcher.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=es#prerequisites)
   * Revise detenidamente la configuración del host virtual.
      * La solución más fácil (y predeterminada) es incluir `ServerAlias *` en el archivo de host virtual en `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Esto permitirá que funcionen los alias de host utilizados por las pruebas funcionales del producto, la invalidación de la caché de Dispatcher y los clones.
      * Sin embargo, si `ServerAlias *` no es aceptable, como mínimo las siguientes entradas `ServerAlias` se deben permitir además de los dominios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL y DNS.
   * Si utiliza su propia CDN, entre un vale de asistencia para configurar el enrutamiento adecuado.
      * Consulte la sección [Puntos de CDN del cliente a CDN administrada por AEM](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) en la documentación de CDN para obtener más información.
      * Configure SSL y DNS según la documentación de su proveedor de CDN.
   * Si no utiliza una CDN adicional, administre SSL y DNS según la siguiente documentación:
      * Administración de certificados SSL
         * [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Administrar nombres de dominio personalizados (DNS)
         * Para asegurarse de que la migración a DNS no introducirá problemas inesperados, es mejor crear un subdominio de prueba al que conectar la instancia de producción antes de publicarla y realizar una ronda de pruebas UAT. Por lo tanto, si el dominio es example.com, puede crear un subdominio test.example.com y aplicarlo a la producción. Durante la prueba UAT del dominio, querrá buscar cosas como la redirección de vínculos adecuada, el almacenamiento en caché y las configuraciones de Dispatcher.
         * [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Recuerde validar el TTL establecido para el registro de DNS.
      * El TTL es la cantidad de tiempo que un registro de DNS permanece en una caché antes de solicitar una actualización al servidor.
      * Si tiene un TTL muy alto, las actualizaciones del registro de DNS tardarán más en propagarse.
* Ejecute pruebas de rendimiento y seguridad que cumplan los requisitos y objetivos de su empresa.
   * Realice pruebas en el entorno de ensayo. Tiene el mismo tamaño que la producción.
   * Los entornos de desarrollo no tienen el mismo tamaño que los de ensayo y producción.
* Pase el ratón por encima y asegúrese de que el lanzamiento real se realice sin ninguna implementación nueva o actualización de contenido.
* Cree perfiles de notificación de usuario de Admin Console. Consulte [Perfiles de notificación](/help/journey-onboarding/notification-profiles.md)
* Considere la posibilidad de configurar reglas de filtro de tráfico para controlar qué tráfico no debe permitirse en el sitio web.
   * Las reglas de filtro de tráfico de límite de velocidad pueden ser una herramienta eficaz contra ataques DDoS. Una categoría especial de reglas de filtro de tráfico, denominadas reglas WAF, requieren una licencia independiente.
   * Consulte la documentación para ver algunas [reglas de inicio sugeridas](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Siempre puede hacer referencia a la lista en caso de que necesite volver a calibrar las tareas durante el lanzamiento.
