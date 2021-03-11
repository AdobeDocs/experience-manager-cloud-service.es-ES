---
title: Explicación de los tipos de programas y programas
description: 'Explicación de los tipos de programas y programas: Cloud Services'
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# Explicación de programas y tipos de programas {#understanding-programs}

En Cloud Manager, tiene la entidad inquilina en la parte superior, que puede tener varios Programas dentro de ella. Cada programa no puede contener más de un entorno de producción y varios entornos que no sean de producción.

El diagrama siguiente muestra la jerarquía de entidades en Cloud Manager.

![image](assets/program-types1.png)

## Tipos de Programa {#program-types}

Un usuario puede crear un **Simulador para pruebas** o un programa **Producción**.

* Se crea un *Programa de producción* para habilitar el tráfico en directo en el momento adecuado en el futuro.
Consulte [Introducción a los programas de producción](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obtener más información.


* Generalmente, se crea un *Programa de espacio aislado* para que sirva a los fines de formación, ejecución de demostración, habilitación, POC o documentación. No está pensado para transportar tráfico en directo y tendrá restricciones que un programa de Producción no tendrá. Incluirá Sites y Assets y se entregará rellenando automáticamente con una rama de Git que incluya código de muestra, un entorno de desarrollo y una canalización que no sea de producción.
Consulte [Introducción a los programas de espacio aislado](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obtener más información.

