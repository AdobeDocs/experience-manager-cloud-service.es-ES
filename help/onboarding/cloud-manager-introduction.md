---
title: Introducción a Cloud Manager
description: Obtenga información sobre cómo Cloud Manager admite su proyecto de AEM a través de sus programas, entornos y canalizaciones.
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 98%

---

# Introducción a Cloud Manager {#intro-cloud-manager}

Cloud Manager es un componente esencial de AEM as a Cloud Service y sirve como punto de entrada único para su equipo. Sus canalizaciones de CD/CI creadas para fines específicos están equipadas para garantizar pruebas exhaustivas y la máxima calidad del código para ofrecer experiencias excepcionales. Para garantizar que los clientes puedan iniciar sus proyectos rápidamente, Cloud Manager proporciona todo lo necesario en forma de autoservicio, incluida la capacidad de crear los recursos y entornos de la nube y acceder a los repositorios de Git. Estas funciones admiten configuraciones de desarrollo empresarial para que los equipos puedan trabajar con frecuencia para comprometer cambios, ofrecer rápidamente experiencias digitales excepcionales y agilizar el tiempo de obtención de valor.

El administrador del sistema es el responsable de configurar el equipo de Cloud Manager, que incluirá personas que crearán sus recursos y desarrolladores en la nube. Para obtener más información sobre cómo configurar y escalar su equipo de desarrollo empresarial y ver cómo AEM as a Cloud Service puede apoyar su proceso de desarrollo, consulte el documento [Configuración de desarrollo de equipo empresarial para AEM as a Cloud Service.](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## Vaya a la página Información general de Cloud Manager {#navigate-cloud-manager}

Siga estos pasos para navegar a Cloud Manager.

1. Vaya a la página de inicio de sesión de Cloud Manager en [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. Seleccione la página **Programas y productos** de Cloud Manager para abrir la página **Información general**.

También puede navegar a la página Programas y productos de Cloud Manager desde la página de inicio de Adobe Experience Cloud siguiendo estos pasos.

1. Vaya a Adobe Experience Cloud en [`https://experience.adobe.com`](https://experience.adobe.com) e inicie sesión con su Adobe ID.

1. Asegúrese de que se encuentra en la organización correcta haciendo referencia al nombre de la organización que se muestra en la parte superior derecha de la barra de herramientas.

1. Seleccione **Experience Manager**.

1. En la tarjeta **Cloud Manager**, haga clic en **Iniciar**

## Permisos basados en roles en Cloud Manager {#role-based-permissions}

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programa | Desarrollador |
|--- |--- |--- |--- |--- |--- |
| Agregar programa<br>Editar programa | Agregar un nuevo programa<br>Agregar o quitar soluciones o complementos | x |  |  |  |
| Crear entorno | Creación de entornos de producción+ensayo y desarrollo | x | x |  |  |
| Entorno de actualización | Actualización de entornos de producción+ensayo y desarrollo | x | x |  |  |
| Eliminar entorno de desarrollo | Eliminar entornos de desarrollo | x | x |  |  |
| Configuración de canalización | Configuración y edición de canalizaciones |  | x |  |  |
| Ejecución de canalización | Iniciar canalizaciones | x | x |  |  |
| Ejecución de canalización | Rechazar/aprobar errores importantes de puerta de calidad de 3 niveles | x | x | x |  |
| Ejecución de canalización | Proporcionar aprobación de lanzamiento | x | x | x |  |
| Ejecución de canalización | Programar implementaciones de producción | x | x | x |  |
| Eliminación de canalización | Permitir eliminación de canalización |  | x |  |  |
| Cancelación de ejecución | Cancelar ejecución actual |  | x |  |  |
| Generar token de acceso personal | Acceso a Git |  | x |  | x |
| Crear RDE | Crear un Entorno de desarrollo rápido | x |  |  | x |
| Restablecer RDE | Restablecer un Entorno de desarrollo rápido | x |  |  | x |

>[!NOTE]
>
>Se puede asignar a un usuario varias funciones. Por ejemplo, asignar tanto **Propietario empresarial** y **Administrador de implementación** a un usuario le da al usuario la suma de estos permisos.

## Programas de Cloud Manager {#cloud-manager-programs}

Los programas de Cloud Manager representan conjuntos de entornos de Cloud Manager que admiten agrupaciones lógicas de iniciativas empresariales. Estas agrupaciones suelen corresponder a un contrato de nivel de servicio (SLA) adquirido. Por ejemplo, un programa puede representar los recursos de AEM para apoyar el sitio web público de una organización, mientras que otro programa representa un DAM interno.


Vea este [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=es) para obtener más información sobre el uso de los programas de Cloud Manager.

Un usuario puede crear un programa de **zona protegida** o un programa de **producción**.

* Un **programa de producción** se crea para activar el tráfico en el momento adecuado en el futuro.
   * Consulte el documento [Introducción a los programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obtener más información.

* Un **programa de zona protegida** normalmente se crea para servir los propósitos de formación, ejecución de demostraciones, habilitación, creación de POC o para documentación.
   * No está pensado para transportar tráfico en directo y tendrá restricciones que un programa de producción no tendrá.
   * Incluye Sites y Assets y se entrega rellenado automáticamente con una rama de Git que incluye código de muestra, un entorno de desarrollo y una canalización que no es de producción.
   * Consulte el documento [Introducción a los programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obtener más información.

## Entornos de Cloud Manager {#cloud-manager-environments}

Los entornos de nube se crean, acceden y visualizan mediante Cloud Manager. Estos entornos pueden ser entornos de producción, ensayo o desarrollo. Los distintos entornos tienen diferentes propósitos y pueden utilizarse con distintas canalizaciones CI/CD. Los entornos están compuestos por servicios como:

* [Servicios de creación de AEM](#author-services)
* [Servicios de publicación de AEM](#publish-services)
* [Servicios de Dispatcher](#dispatcher-services)

>[!TIP]
>
> Consulte el vídeo [Uso de entornos de Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=es) para ver una descripción general de los entornos disponibles.
>
>Consulte el documento [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información sobre los tipos de entorno que un usuario puede crear y cómo puede hacerlo.

### Servicio de creación de AEM {#author-services}

Se incluye un servicio de creación de AEM en entornos en los que el contenido del sitio y los recursos digitales se crean, administran y actualizan. Normalmente, solo los usuarios internos tienen acceso al servicio de creación y se mantiene tras una pantalla de inicio de sesión. El servicio de creación actúa como entorno de creación y vista previa.

### Servicio de publicación de AEM {#publish-services}

Se incluye un servicio de publicación de AEM en entornos que alojan la experiencia del usuario final, como un sitio web. Este es el servicio que los visitantes del sitio verán e interactuarán con él. Normalmente, el servicio de publicación está disponible públicamente.

### Servicio de Dispatcher de AEM {#dispatcher-services}

Dispatcher es un módulo `Apache HTTP Web server` que proporciona una capa de seguridad y rendimiento que se encuentra frente al servicio de publicación de AEM.
