---
title: 'Aprovisionamiento de entornos: lo que es necesario'
description: 'Aprovisionamiento de entornos: lo que es necesario'
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# Entornos aprovisionados {#environments-provisioning}

## Aprovisionamiento {#provisioning}

Todos los entornos de la nube AEM adquiridos por un cliente se aprovisionan automáticamente mediante Adobe y se vinculan de nuevo a su programa en Cloud Manager. Estos entornos de nube de AEM se incluyen en cada suscripción a Adobe Managed Services y suelen estar compuestos por al menos un entorno de producción, un entorno de fase y, opcionalmente, uno o más entornos de desarrollo o prueba.

## Correo electrónico de bienvenida {#welcome-email}

Una vez completado el proceso de aprovisionamiento del entorno, el administrador de clientes designado recibe un correo electrónico de bienvenida con la confirmación de que se les ha concedido acceso a Adobe Experience Cloud. El correo electrónico contiene información detallada sobre cómo empezar a utilizar los servicios de Experience Cloud y el portal de autoservicio de Cloud Manager. Además, el correo electrónico contiene información importante, como dónde buscar recursos de asistencia técnica, foros o preguntas frecuentes, entre otras cosas. En la lista de recursos que se proporcionan en el correo electrónico, también encontrará detalles sobre cómo acceder a Cloud Manager o a los entornos de la nube de AEM.

## Siguientes pasos {#next-steps}

Después de recibir el correo electrónico de bienvenida, está listo para iniciar sesión en Cloud Manager como administrador, con sus credenciales de Adobe IMS. Una vez que haya iniciado sesión, podrá comprobar que los entornos de producción y no producción de la nube de AEM están disponibles y se ejecutan correctamente.

Cloud Manager utilizará estos entornos de nube de AEM para ejecutar la canalización de CI/CD al implementar su código, empezando por el repositorio Git de Cloud Manager, a través del entorno de ensayo y hasta su entorno de producción de AEM. También podrá acceder a sus entornos de nube de AEM directamente desde Cloud Manager, cuando esté listo para empezar a crear experiencias digitales para sus propiedades web.