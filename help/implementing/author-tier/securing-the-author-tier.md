---
title: Protección del nivel de Author
description: Protección del nivel de Author
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 53%

---

# Protección del nivel de Author {#securing-the-author-tier}

Al crear un nuevo entorno con AEM as a Cloud Service, el nivel de Author resultante es accesible desde internet de forma predeterminada. Es posible seguir configurando las directivas de red para proteger el acceso a su nivel de Author. Consulte [Aplicación de una Lista de permitidos IP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) para obtener más información. El procedimiento consiste en la autorización de los rangos IP a los que se debe otorgar acceso de red al entorno de Author.

Para establecer estas reglas, presente un vale de soporte desde el [Adobe Admin Console](https://adminconsole.adobe.com/) con la información solicitada:

* ID del programa,
* ID del entorno,
* intervalos de direcciones IP para autorizar.

