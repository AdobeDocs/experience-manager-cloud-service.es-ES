---
title: Problemas y limitaciones conocidos de [!DNL AEM Forms] entorno as a Cloud Service
description: Problemas y limitaciones conocidos del entorno de  [!DNL AEM Forms]  as a Cloud Service.
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 92f89243b79c6c2377db3ca2b8ea244957416626
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 98%

---

# Problemas y limitaciones conocidos {#known-issues-and-limitations}

Antes de empezar a usar [!DNL AEM Forms] as a Cloud Service, revise los siguientes problemas y limitaciones conocidos:

## Problemas conocidos {#known-issues}

* No agregue ni ejecute pruebas que envíen un formulario adaptable desde una instancia de publicación a un flujo de trabajo de AEM que se ejecute en una instancia de autor hasta nuevo aviso.

* Al importar un formulario adaptable que utiliza una plantilla con el botón **[!UICONTROL Guardar]**, **[!UICONTROL este]** botón sigue apareciendo en el formulario adaptable incluso después de quitarlo de la plantilla correspondiente. Quite el botón **[!UICONTROL Guardar]** del formulario adaptable antes de publicarlo. Consulte la disponibilidad del portal de Forms y de la función Guardar como borrador en las notas de la versión para restaurar y utilizar el botón.

* El paso **[!UICONTROL Establecer variable]** de los flujos de trabajo de AEM no admite variables de tipo Lista de matrices. Puede utilizar el paso Procesar para establecer variables de tipo Lista de matrices.

* Cuando se envía un formulario adaptable que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Este problema se produce de forma intermitente y solo cuando se utiliza el envío sincrónico. Se trata de un [problema conocido](https://feedbackassistant.apple.com/feedback/9117687) de iOS de Apple.

* Cuando se envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Se trata de un problema conocido de iOS de Apple. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service no genera miniaturas para los archivos de esquema XDP y JSON. El servicio muestra los iconos predeterminados en lugar de las miniaturas.

  ![Problema conocido de la miniatura de Forms](/help/forms/assets/forms-tumbnail-known-issue.png)

* Cuando se utiliza un esquema con elementos repetibles para crear un formulario adaptable basado en componentes principales, la opción de arrastrar y soltar elementos repetibles del árbol del modelo de datos en el editor de formularios adaptables no funciona.

## Restricciones {#limitations}

* La compatibilidad con formularios adaptables basados en XFA no está disponible de forma predeterminada. Si tiene intención de utilizar formularios adaptables basados en XFA, póngase en contacto con el servicio de soporte de Adobe e incluya información sobre su caso de uso y los requisitos específicos en el mensaje.

