---
title: Descubra qué es Cloud Manager
description: Siga esta página para obtener más información sobre Cloud Manager, los programas de Cloud Manager y los entornos.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 42c565c8c5a3300b95a9153cb402cdb3e847f6a2
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Introducción a Cloud Manager {#intro-cloud-manager}

Cloud Manager es un componente esencial de AEM como Cloud Service y sirve como punto de entrada único para su equipo.

Para dar compatibilidad a los clientes con configuraciones de desarrollo empresarial, AEM as a Cloud Service se integra completamente con Cloud Manager y sus canalizaciones de CD/CI creadas específicamente, que están equipadas para garantizar pruebas exhaustivas y la máxima calidad del código y ofrecer experiencias excepcionales.

Para garantizar que los clientes puedan empezar rápidamente con AEM como Cloud Service, Cloud Manager proporciona todo lo necesario para comenzar de forma autoservicio, incluida la capacidad de crear los recursos y entornos de la nube. De este modo, los desarrolladores de AEM pueden acceder al repositorio de Git a través de Cloud Manager. Con Cloud Manager, los equipos de desarrollo pueden trabajar para confirmar los cambios con frecuencia de forma autoservicio.

El administrador del sistema se encargará de configurar su equipo de Cloud Manager, que incluirá personas que crearán sus recursos y desarrolladores de cloud. Consulte [Configuración de desarrollo de equipo empresarial para AEM as a Cloud Service](/help/implementing/cloud-manager/enterprise-team-dev-setup.md) para obtener información sobre el soporte de Cloud Manager en la configuración de desarrollo de equipo empresarial.

## Programas de Cloud Manager {#cloud-manager-programs}

Los programas de Cloud Manager representan conjuntos de entornos de Cloud Manager que admiten conjuntos lógicos de iniciativas empresariales, que normalmente corresponden a un contrato de nivel de servicio (SLA) adquirido. Por ejemplo, un programa puede representar los recursos AEM para apoyar los sitios web públicos globales, mientras que otro programa representa un DAM central interno. Vea este [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) para obtener más información sobre el uso de los programas de Cloud Manager.

Un usuario puede crear un **Simulador para pruebas** o un programa **Producción**.

* Se crea un *Programa de producción* para habilitar el tráfico en directo en el momento adecuado en el futuro.
Consulte Introducción a los programas de producción para obtener más información.

* Generalmente, se crea un *Programa de espacio aislado* para que sirva a los fines de formación, ejecución de demostración, habilitación, POC o documentación. No está pensado para transportar tráfico en directo y tendrá restricciones que un programa de Producción no tendrá. Incluirá Sites y Assets y se entregará rellenando automáticamente con una rama de Git que incluya código de muestra, un entorno de desarrollo y una canalización que no sea de producción.
Consulte Introducción a los programas de espacio aislado para obtener más información.

## Entornos de Cloud Manager {#cloud-manager-environments}

Los entornos de nube se crearán, accederán y verán a través de Cloud Manager. Pueden ser entorno de producción, entorno de ensayo o entorno de desarrollo. Los distintos entornos admiten diferentes propósitos y se pueden utilizar con diferentes canalizaciones CI/CD. Los entornos están compuestos por servicios como:

* [AEM Author Services](#author-services)
* [AEM Publish Services](#publish-services)
* [Servicios de Dispatcher](#dispatcher-services)

   >[!NOTE]
   > Consulte el vídeo [Uso de entornos de Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) para obtener más información sobre los entornos disponibles. Además, consulte [Administrar entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) para obtener más información sobre los tipos de entorno que un usuario puede crear y cómo puede crearlo.

### AEM Author Service {#author-services}

El servicio de autor de AEM se incluye en un entorno en el que el contenido del sitio y los recursos digitales se crean, administran y actualizan. Normalmente, solo los usuarios internos tienen acceso al servicio de creación y están detrás de una pantalla de inicio de sesión. El servicio de creación está diseñado como entorno de creación y vista previa.

### Servicio de AEM Publish {#publish-services}

El servicio de publicación de AEM se incluye en un entorno que aloja la experiencia del usuario final, como un sitio web. Este es el servicio que los visitantes del sitio verán e interactuarán con él. Normalmente, el servicio de publicación está disponible para el público.

### Servicio de Dispatcher AEM {#dispatcher-services}

Dispatcher es un módulo `Apache HTTP Web server` que proporciona una capa de seguridad y rendimiento que se encuentra frente al servicio de publicación de AEM.
