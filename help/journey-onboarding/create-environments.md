---
title: Crear entornos
description: Aprenda a utilizar Cloud Manager para crear sus primeros entornos.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 86%

---

# Crear entornos {#create-environments}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a utilizar Cloud Manager para crear sus primeros entornos.

## Objetivo {#objective}

Después de leer el documento anterior en este recorrido de incorporación, [Creación de programas,](create-program.md) ahora tiene su propio programa de Cloud Manager. Ahora puede aprender a utilizar Cloud Manager para crear sus primeros entornos para ese programa.

Después de leer este documento, debería poder hacer lo siguiente:

* Comprender lo que es un entorno.
* Conocer la diferencia entre los diferentes entornos.
* Crear su propio entorno.

## ¿Qué es un entorno? {#environments}

Los entornos se sientan debajo de los programas dentro de la jerarquía de Cloud Manager. Aunque los programas le permiten organizar su solución y conceder acceso a miembros concretos del equipo a esos programas, los entornos pertenecen a programas específicos y son instancias individuales de las soluciones de Adobe dentro de esos programas. Los entornos se utilizan para un propósito específico, como la creación de contenido o la prueba de nuevos desarrollos. Las canalizaciones CI/CD de Cloud Manager facilitan la implementación de código en estos entornos desde repositorios Git.

Si recuerdan el ejemplo de WKND Travel and Adventure Enterprises teórico, que es un arrendatario que se centra en medios relacionados con viajes, podrían tener dos programas: un programa Sites para su división WKND Magazine y un programa de activos para la división WKND Media. Es probable que cada programa tenga un par de entornos, como un entorno de producción que sirve al tráfico real del sitio y un entorno de desarrollo para probar el nuevo código de aplicación.

Existen cuatro tipos diferentes de entornos:

* **Producción y ensayo**: los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente.
* **Desarrollo**: se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se puede asociar con canalizaciones que no sean de producción.
* **Desarrollo rápido**: Un entorno de desarrollo rápido (RDE) permite al desarrollador implementar y revisar cambios rápidamente, minimizando la cantidad de tiempo necesario para probar funciones que han demostrado funcionar en un entorno de desarrollo local.

Para los fines de este recorrido de integración, para empezar con un mínimo, creará un entorno de desarrollo que puede utilizar para explorar AEM capacidades de as a Cloud Service.

## Crear entornos {#creating-environments}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea agregar un entorno.

1. En la página **Información general del programa**, haga clic en **Agregar entorno** en la tarjeta **Entornos** para agregar un entorno.

   ![Tarjeta Entornos](/help/implementing/cloud-manager/assets/no-environments.png)

   * La opción **Agregar entorno** también está disponible en la pestaña **Entornos**.

      ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La opción **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el cuadro de diálogo **Agregar entorno** que aparece:

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

Se han creado los recursos de la nube y su equipo puede acceder a ellos. Como administrador del sistema, primero debe asignar los integrantes del equipo a perfiles de producto de AEM as a Cloud Service desde Adobe Admin Console para que puedan acceder a esos recursos.

Por lo tanto, debe continuar con su recorrido de incorporación revisando el documento [Asignación de miembros del equipo a perfiles de producto de AEM as a Cloud Service.](assign-profiles-aem.md)  En ese documento, aprenderá a otorgar a los integrantes del equipo los derechos que necesitan para acceder a sus nuevos entornos.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos adicionales y opcionales si desea ir más allá del contenido del recorrido de incorporación.

* [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md): obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager
* [Uso de entornos de Adobe Cloud Manager:](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=es) los entornos de Cloud Manager están compuestos por los servicios de publicación, creación y Dispatcher de AEM. Aprenda cómo los distintos entornos admiten funciones y se pueden utilizar con diferentes canalizaciones de CD/CI.
* [AEM consejos y trucos de campeón: tipos de entorno de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/environment-types.md) : Vea este vídeo para obtener una descripción general de los tipos de entorno de Cloud Manager de un AEM campeón.
* [Entornos de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) - Consulte esta documentación para obtener detalles sobre cómo utilizar un RDE
