---
title: Mantenimiento de un conector de AEM
description: Mantenimiento de un conector de AEM
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---


Mantenimiento de un conector de AEM
============================

Este artículo contiene información sobre el mantenimiento de un conector AEM y se debe leer junto con artículos sobre la [implementación](implement.md) y el [envío](submit.md) de conectores.

Incluso después del envío inicial, puede haber razones para que un socio actualice su conector de AEM, ya sea debido a una nueva versión de AEM o independiente de ella (por ejemplo, para agregar funciones o corregir errores). Este artículo describe el proceso para ambos escenarios y también describe el proceso típico de un cliente para validar los conectores al actualizar AEM.

AEM como aplicaciones Cloud Service se actualizan diariamente con AEM parches de mantenimiento, con cambios más grandes activados mensualmente durante un lanzamiento de funciones. Aunque AEM actualizaciones están pensadas para que sean retrocompatibles y por lo tanto no interrumpan las aplicaciones, se aconseja a los socios proveedores que validen periódicamente que sus conectores se comportan como esperarían. El acceso a un programa/entorno AEM será determinado por el equipo del socio.