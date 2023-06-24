---
title: Protección del nivel de Author
description: Protección del nivel de Author
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 35%

---

# Protección del nivel de Author {#securing-the-author-tier}

AEM Al crear un entorno con as a Cloud Service, el nivel de creación resultante es accesible desde Internet de forma predeterminada. Es posible seguir configurando las directivas de red para proteger el acceso a su nivel de Author. Consulte [Aplicación de una Lista de permitidos IP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) para obtener más información. El procedimiento consiste en la autorización de los rangos IP a los que se debe otorgar acceso de red al entorno de Author.

Para establecer estas reglas, presente un vale de soporte desde el [Adobe Admin Console](https://adminconsole.adobe.com/) con la información solicitada:

* ID del programa,
* ID del entorno,
* intervalos de direcciones IP para autorizar.

