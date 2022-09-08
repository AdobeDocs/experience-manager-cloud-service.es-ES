---
title: Crear un programa
description: Aprenda a utilizar Cloud Manager para crear su primer programa.
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 4%

---

# Crear un programa {#create-program}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a usar Cloud Manager para crear su primer programa.

## Objetivo {#objective}

Tras revisar el documento anterior de este recorrido de incorporación, [Acceso a Cloud Manager,](cloud-manager.md) se ha asegurado de tener acceso adecuado a Cloud Manager. Ahora puede crear su primer programa.

Después de leer este documento:

* Comprender lo que es un programa.
* Conocer la diferencia entre los programas de producción y los de entornos limitados.
* Poder crear su propio programa.

## ¿Qué es un programa? {#programs}

Los programas son el nivel más alto de organización en Cloud Manager. Según la licencia con Adobe, los programas permiten organizar la solución y conceder acceso a miembros concretos del equipo a esos programas.

Los programas de Cloud Manager representan conjuntos de entornos de Cloud Manager. Estos programas admiten conjuntos lógicos de iniciativas del negocio, que normalmente corresponden a un Contrato de Nivel de Servicio (SLA, Service Level Agreement ) con licencia. Por ejemplo, un programa puede representar los recursos AEM para apoyar un sitio web público mundial para una organización, mientras que otro programa representa un DAM central interno.

Si recuerdan el ejemplo de WKND Travel and Adventure Enterprises teórico, que es un arrendatario que se centra en medios relacionados con viajes, podrían tener dos programas: un programa Sites para su división WKND Magazine y un programa de activos para la división WKND Media. Los distintos integrantes del equipo tendrían entonces acceso a los diferentes programas debido a su propia división de las necesidades laborales.

Existen dos tipos diferentes de programas:

* A **programa de producción** se crea para habilitar el tráfico en directo para el sitio. Este es su entorno &quot;real&quot;.
* A **programa de simulación de pruebas** normalmente se crea para servir los propósitos de formación, ejecución de demostraciones, habilitación, POCs o documentación.

Dado que sirven para diferentes propósitos, los diferentes entornos tienen diferentes opciones. Sin embargo, el proceso de creación es similar. Para este recorrido de integración crearemos un entorno de entorno limitado.

>[!NOTE]
>
>De forma predeterminada, un usuario con acceso a un entorno AEM también tendrá la función de usuario de Cloud >Manager. Esta función por sí sola no es suficiente para dar al usuario acceso a la vista de detalles del programa. Un usuario de este tipo que solo tenga la función de usuario de Cloud Manager puede navegar mediante las opciones del menú de programa a la URL de creación del entorno de AEM (si existen entornos). Estos usuarios deben ponerse en contacto con su administrador si desean obtener acceso a nivel de programa.

## Creación de un programa de zona protegida {#create-sandbox}

Siga estos pasos para crear un programa de simulación de pruebas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la página de aterrizaje de Cloud Manager, haga clic en **Agregar programa** en la esquina superior derecha de la pantalla.

   ![Página de aterrizaje de Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. En el asistente crear programa, seleccione **Configuración de un simulador para pruebas**, proporcione un nombre de programa y haga clic en **Crear**.

   ![Creación de tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

Verá una nueva tarjeta de programa de simulación de pruebas en la página de aterrizaje con un indicador de estado a medida que avance el proceso de configuración.

![Creación de Simulador para pruebas desde la página de información general](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

Una vez completado el programa, los miembros de la organización asignados a la función **Desarrollador** el perfil de producto puede iniciar sesión en Cloud Manager y administrar los repositorios de Git de Cloud Manager.

## Siguientes pasos {#whats-next}

Ahora que se ha creado el primer programa, puede crear entornos para él. Debe continuar con su recorrido de incorporación revisando el documento [Crear entornos.](create-environments.md)

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) : Obtenga información sobre la jerarquía de Cloud Manager y cómo encajan los distintos tipos de programas en su estructura y cómo difieren.
* [Creación de programas de Simulador para pruebas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) : Aprenda a utilizar Cloud Manager para crear su propio programa de simulación de pruebas para formación, demostración, POC u otros fines que no sean de producción.
* [Creación de programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) : Aprenda a utilizar Cloud Manager para crear su propio programa de producción y alojar tráfico en directo.
* [Uso de Adobe Cloud Manager: Programas](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) : los programas de Cloud Manager representan conjuntos de entornos AEM que admiten conjuntos lógicos de iniciativas del negocio, que normalmente corresponden a un contrato de nivel de servicio (SLA) adquirido.
