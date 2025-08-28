---
title: Crear entornos
description: Aprenda a utilizar Cloud Manager para crear sus primeros entornos.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
feature: Onboarding
source-git-commit: 9c5838a01ceecf094aea19578e6560a5e5ca8c4c
workflow-type: ht
source-wordcount: '775'
ht-degree: 100%

---

# Crear entornos {#create-environments}

En esta parte del [recorrido de incorporación](overview.md), aprenderá a utilizar Cloud Manager para crear sus primeros entornos.

## Objetivo {#objective}

Después de leer el documento anterior, [Creación de programas](create-program.md), en este recorrido de incorporación, ahora tiene su propio programa de Cloud Manager. Ahora puede aprender a utilizar Cloud Manager para crear sus primeros entornos para ese programa.

Después de leer este documento, debería poder hacer lo siguiente:

* Comprender lo que es un entorno.
* Conocer la diferencia entre los diferentes entornos.
* Crear su propio entorno.

## ¿Qué es un entorno? {#environments}

Los entornos se sientan debajo de los programas dentro de la jerarquía de Cloud Manager. Aunque los programas le permiten organizar su solución y conceder acceso a miembros concretos del equipo a esos programas, los entornos pertenecen a programas específicos y son instancias individuales de las soluciones de Adobe dentro de esos programas. Los entornos se utilizan para un propósito específico, como la creación de contenido o la prueba de nuevos desarrollos. Las canalizaciones CI/CD de Cloud Manager facilitan la implementación de código en estos entornos desde repositorios Git.

Si recuerda el ejemplo de WKND Travel and Adventure Enterprises teórico, se trata de un inquilino que se centra en los medios de comunicación relacionados con los viajes. Podría tener dos programas. Es decir, un programa de Sites para su división WKND Magazine y un programa de Assets para la división de WKND Media. Es probable que cada programa tenga un par de entornos, como uno de producción que sirve al tráfico real del sitio y uno de desarrollo para probar el nuevo código de aplicación.

Existen cinco tipos diferentes de entornos:

* **Producción y ensayo**: los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente.
* **Desarrollo**: se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se puede asociar con canalizaciones que no sean de producción.
* **Desarrollo rápido**: un entorno de desarrollo rápido (RDE) permite que un desarrollador implemente y revise los cambios rápidamente. Minimiza el tiempo necesario para probar las características que se ha comprobado que funcionan en un entorno de desarrollo local.
* **Entorno de prueba especializado**: proporciona un espacio dedicado para validar características en condiciones próximas a la producción, ideal para pruebas de esfuerzo y comprobaciones avanzadas previas a la implementación.

A efectos de este proceso de incorporación, para empezar con lo mínimo, cree un entorno de desarrollo que pueda utilizar para explorar las capacidades de AEM as a Cloud Service.

## Crear un entorno {#creating-environments}

>[!NOTE]
>
>El sistema registra al usuario que crea un entorno como su creador. Dado que a veces se pueden restaurar los usuarios eliminados, elija cuidadosamente al creador del entorno.

**Para crear un entorno:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea agregar un entorno.

1. Para añadir un entorno, en la página **Información general del programa**, en la tarjeta **Entornos**, seleccione la opción **Añadir entorno**.

   ![Tarjeta Entornos](/help/implementing/cloud-manager/assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la pestaña **Entornos**.

     ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Añadir entorno**, haga lo siguiente:

   * Seleccione un **Tipo de entorno**.
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del tipo de entorno de desarrollo.
   * Proporcione un **Nombre del entorno**.
   * Proporcione una **Descripción del entorno**.
   * Seleccione una **Región de nube**.

   ![Cuadro de diálogo Agregar entorno](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

Una vez que el entorno esté disponible, los miembros de la organización asignados al perfil de producto **Desarrollador** pueden iniciar sesión en Cloud Manager y administrar los repositorios de Git de Cloud Manager.

## Siguientes pasos {#whats-next}

Ahora que ha leído esta parte del recorrido de incorporación, debe poder:

* Comprender lo que es un entorno.
* Conocer la diferencia entre los diferentes entornos.
* Crear su propio entorno.

Su equipo ahora puede acceder a los recursos de la nube que ha creado. Como administrador del sistema, primero debe asignar a los integrantes del equipo perfiles de producto en AEM as a Cloud Service desde Adobe Admin Console para que puedan acceder a esos recursos.

Por lo tanto, debe continuar con su recorrido de incorporación revisando el documento [Asignación de integrantes del equipo a perfiles de producto de AEM as a Cloud Service](assign-profiles-aem.md). En ese documento, aprenderá a otorgar a los integrantes del equipo los derechos que necesitan sobre sus nuevos entornos.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos opcionales adicionales si desea ir más allá del contenido del recorrido de incorporación.

* [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md): obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager
* [Uso de entornos de Adobe Cloud Manager:](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/cloud-manager/environments) los entornos de Cloud Manager están compuestos por los servicios de publicación, creación y Dispatcher de AEM. Aprenda cómo los distintos entornos admiten funciones y se pueden utilizar con diferentes canalizaciones de CI/CD.
* [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md): consulte esta documentación para obtener detalles sobre cómo utilizarlos.
<!-- ERROR: Not Found (HTTP error 404) FIND AN ALTERNATE RESOURCE? * [AEM Champion Tips and Tricks - Cloud Manager Environment Types](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) - Watch this video for an overview of Cloud Manager environment types from an AEM champion. -->

