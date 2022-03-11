---
title: Problemas y limitaciones conocidos
description: Problemas conocidos y limitaciones de  [!DNL AEM Forms] Entorno as a Cloud Service
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 12%

---

# Problemas y limitaciones conocidos {#known-issues-and-limitations}

Antes de empezar a usar [!DNL AEM Forms] as a Cloud Service, revise los siguientes problemas y limitaciones conocidos:

## Problemas conocidos {#known-issues}

* No agregue ni ejecute una prueba que envíe un formulario adaptable desde una instancia de publicación a un flujo de trabajo AEM que se ejecute en una instancia de autor hasta nuevo aviso.

* Al importar un formulario adaptable que utilice una plantilla que contenga la variable **[!UICONTROL Guardar]** el botón **[!UICONTROL Guardar]** sigue apareciendo en el formulario adaptable incluso después de eliminarlo de la plantilla correspondiente. Elimine el **[!UICONTROL Guardar]** del Forms adaptable antes de publicarlo. Observe las notas de la versión de la disponibilidad del portal de Forms y de Guardar como borrador para restaurar y utilizar el botón.

* La variable **[!UICONTROL Establecer variable]** paso de AEM Flujos de trabajo no admite variables de tipo lista de matriz. Puede utilizar el paso de proceso para establecer variables de tipo lista de matriz.

* Cuando se envía un formulario adaptable que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. El problema se produce de forma intermitente y solo cuando se utiliza el envío sincrónico. Esto es un [problema conocido](https://feedbackassistant.apple.com/feedback/9117687) en Apple iOS.

* Cuando se envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Este es un problema conocido en Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## Restricciones     {#limitations}

* La compatibilidad con formularios adaptables basados en XFA no está disponible de forma predeterminada. Si tiene intención de utilizar formularios adaptable basados en XFA, póngase en contacto con el servicio de soporte de Adobe con detalles de su caso de uso y requisitos específicos.

