---
title: Crear entornos
description: Aprenda a utilizar Cloud Manager para crear sus primeros entornos.
role: Admin, User, Developer
exl-id: 31940e1e-fe27-4c5f-b67f-41affebea63a
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 2%

---

# Crear entornos {#create-environments}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a utilizar Cloud Manager para crear sus primeros entornos.

## Objetivo {#objective}

Después de leer el documento anterior en este recorrido de incorporación, [Creación de programas,](create-program.md) ahora tiene su propio programa de Cloud Manager. Ahora puede aprender a utilizar Cloud Manager para crear sus primeros entornos para ese programa.

Tras leer este documento, deberá:

* Comprender lo que es un entorno.
* Conocer la diferencia entre los diferentes entornos.
* Poder crear su propio entorno.

## ¿Qué es un entorno? {#environments}

Los entornos se sientan debajo de los programas dentro de la jerarquía de Cloud Manager. Aunque los programas le permiten organizar su solución y conceder acceso a miembros concretos del equipo a esos programas, los entornos pertenecen a programas específicos y son instancias individuales de las soluciones de Adobe dentro de esos programas. Los entornos se utilizan para un propósito específico, como la creación de contenido o la prueba de nuevos desarrollos. Las canalizaciones CI/CD de Cloud Manager facilitan la implementación de código en estos entornos desde repositorios Git.

Si recuerdan el ejemplo de WKND Travel and Adventure Enterprises teórico, que es un arrendatario que se centra en medios relacionados con viajes, podrían tener dos programas: un programa Sites para su división WKND Magazine y un programa de activos para la división WKND Media. Es probable que cada programa tenga un par de entornos, como un entorno de producción que sirve al tráfico real del sitio y un entorno de desarrollo para probar el nuevo código de aplicación.

Existen tres tipos diferentes de entornos:

* **Producción y fase** - Los entornos de producción y ensayo están disponibles en pareja y se utilizan para fines de producción y prueba, respectivamente.
* **Desarrollo** - Se puede crear un entorno de desarrollo para fines de desarrollo y prueba, y solo se puede asociar con tuberías que no sean de producción.

Para los fines de este recorrido de integración, debe crear un entorno de desarrollo.

## Crear entornos {#creating-environments}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea agregar un entorno.

1. En el **Información general del programa** página, haga clic en **Agregar entorno** en el **Entornos** para agregar un entorno.

   ![Tarjeta de entorno](/help/implementing/cloud-manager/assets/no-environments.png)

   * La variable **Agregar entorno** también está disponible en la **Entornos** pestaña .

      ![Pestaña Entornos](/help/implementing/cloud-manager/assets/environments-tab.png)

   * La variable **Agregar entorno** se puede desactivar debido a la falta de permisos o dependiendo de los recursos con licencia.

1. En el **Agregar entorno** que aparece:

   * Seleccione un **Tipo de entorno**.
      * El número de entornos disponibles/utilizados se muestra entre paréntesis detrás del tipo de entorno de desarrollo .
   * Proporcione un **Nombre del entorno**.
   * Proporcione un **Descripción del entorno**.
   * Seleccione un **Región de nube**.

   ![Agregar cuadro de diálogo de entorno](/help/implementing/cloud-manager/assets/add-environment2.png)

1. Haga clic en **Guardar** para agregar el entorno especificado.

Una vez que el entorno esté disponible, los miembros de la organización asignados a la función **Desarrollador** el perfil de producto puede iniciar sesión en Cloud Manager y administrar los repositorios de Git de Cloud Manager.

## Siguientes pasos {#whats-next}

Ahora que ha leído esta parte del recorrido de incorporación, debe:

* Comprender lo que es un entorno.
* Conocer la diferencia entre los diferentes entornos.
* Poder crear su propio entorno.

Se han creado los recursos de la nube y su equipo puede acceder a ellos. Como administrador del sistema, primero debe asignar los integrantes del equipo a AEM perfiles de producto as a Cloud Service de Adobe Admin Console para que puedan acceder a esos recursos.

Por lo tanto, debe continuar con su recorrido de incorporación revisando el documento [Asignación de miembros del equipo a AEM perfiles de producto as a Cloud Service.](assign-profiles-aem.md)  En ese documento, aprenderá a otorgar a los integrantes del equipo los derechos que necesitan para acceder a sus nuevos entornos.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) : Obtenga información sobre los tipos de entornos que puede crear y cómo crearlos para su proyecto de Cloud Manager
* [Uso de Adobe Cloud Manager: entornos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Los entornos de Cloud Manager están compuestos por AEM servicios de creación, publicación y dispatcher. Aprenda cómo los distintos entornos admiten funciones y se pueden utilizar con diferentes canalizaciones de CD/CI.
