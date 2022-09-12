---
title: Asistente para la creación de proyectos
description: Obtenga información sobre el asistente para la creación de proyectos para configurar rápidamente el proyecto después de crear el programa de producción.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 4%

---

# Asistente para la creación de proyectos {#project-creation-wizard}

Después de crear el programa de producción, Cloud Manager ofrece un asistente para crear un proyecto de AEM mínimo basado en la variable [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) para empezar rápidamente.

Siga estos pasos para crear un proyecto de aplicación de AEM en Cloud Manager mediante el asistente.

1. Cree un programa de producción siguiendo los pasos del documento [Creación de programas de producción](creating-production-programs.md)

1. Una vez completada la configuración del programa, acceda a la **Información general** de su programa y consulte la **Crear ramas y proyectos** tarjeta de llamada a acción en la parte superior.

   ![Atención de llamadas a acción para el asistente](assets/create-wizard1.png)

1. Haga clic en **Crear** para iniciar el asistente y confirmar el **Título** y **Nuevo nombre de rama** en el **Crear una rama y un proyecto** ventana.

   ![Crear una rama y un proyecto](assets/create-wizard2.png)

1. Si lo desea, haga clic en el divisor para mostrar los parámetros adicionales del proyecto. Los valores predeterminados los proporciona el tipo de archivo del proyecto AEM y, por lo general, no es necesario cambiarlos.

   ![Parámetros de proyecto adicionales](assets/create-wizard5.png)

1. Haga clic en **Crear** para iniciar el proceso de creación del proyecto.


A **Creación de proyectos en curso** la tarjeta ahora reemplaza a la función **Crear ramas y proyectos** tarjeta de llamada a acción como parte superior del **Información general del programa** en el Navegador.

![Creación del proyecto en curso](assets/create-wizard3.png)

Una vez completada la creación del programa, se muestra una **Agregar entorno** la tarjeta sustituye al **Creación de proyectos en curso** en la parte superior del **Información general del programa** en el Navegador.

![Agregar entorno](assets/create-wizard4.png)

Ahora tiene un proyecto AEM basado en el tipo de archivo AEM agregado al repositorio de Git para servir como base para el desarrollo de su propio proyecto. A continuación, puede crear los entornos en los que puede implementar el código de proyecto.

Consulte el documento [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para aprender a añadir o administrar entornos.

>[!NOTE]
>
>El asistente solo está disponible para programas de producción. Porque [programas de simulación de pruebas](introduction-sandbox-programs.md#auto-creation) incluir la creación automática de proyectos, no es necesario el asistente.