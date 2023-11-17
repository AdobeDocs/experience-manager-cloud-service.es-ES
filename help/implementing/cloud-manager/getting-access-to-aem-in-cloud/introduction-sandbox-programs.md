---
title: Introducción a los programas de zona protegida
description: Descubra cuáles son las diferencias entre los programas de zona protegida y los programas de producción.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 98%

---


# Introducción a los programas de zona protegida {#sandbox-programs}

Descubra cuáles son las diferencias entre los programas de zona protegida y los programas de producción.

## Introducción {#introduction}

Un programa de zona protegida se suele crear para servir a los fines de formación, ejecución de demostraciones, habilitación o prueba de conceptos (POC) y, por lo tanto, no están pensados para transportar tráfico en directo.

Un programa de zona protegida es uno de los dos tipos de programas disponibles en AEM Cloud Service, el otro es un [programa de producción.](introduction-production-programs.md) Consulte [Explicación de programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obtener más información sobre los tipos de programas.

## Creación automática {#auto-creation}

Los programas de zona protegida incluyen la creación automática. Siempre que cree un programa de zona protegida, Cloud Manager hará lo siguiente automáticamente:

* Agregar AEM Sites y AEM Assets como soluciones en su programa.
* Establecer un repositorio Git de proyecto con un proyecto de ejemplo basado en el arquetipo del [proyecto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)
* Crear un entorno de desarrollo.
* Crear una canalización que no sea de producción y se implemente en el entorno de desarrollo.

Un programa de zona protegida solo tendrá un entorno de desarrollo.

## Limitaciones y condiciones {#limitations}

Como no están pensados para el tráfico en directo, los programas de zonas protegidas tienen ciertas limitaciones y condiciones de uso, lo que los diferencia de los programas de producción.

### Sin tráfico en directo {#live-traffic}

Los programas de zona protegida no están pensados para transportar tráfico en directo y, por lo tanto, no están sujetos a los [Compromisos de AEM as a Cloud Service.](https://www.adobe.com/es/legal/service-commitments.html)

### Sin escalado automático {#auto-scaling}

Los entornos creados en un programa de zona protegida no están configurados para el escalado automático. Por lo tanto, estos entornos no son adecuados para pruebas de carga o rendimiento.

### Sin dominios personalizados ni listas de IP permitidas {#ip-allow}

Los dominios personalizados y las listas de IP permitidas no están disponibles en los programas de zonas protegidas.

### Sin redes avanzadas {#advanced-networking}

Las [Funciones de red avanzadas](/help/security/configuring-advanced-networking.md) (por ejemplo, el aprovisionamiento de autoservicio de VPN, puertos no estándar, direcciones IP de salida dedicadas, etc.) no están disponibles en los programas de zonas protegidas.

### Actualizaciones de los manuales de AEM {#updates}

Las actualizaciones de AEM no se insertan automáticamente en los programas de zona protegida, pero se pueden aplicar manualmente a sus entornos.

* Una actualización manual solo se puede ejecutar cuando el entorno de destino tiene una canalización configurada correctamente.
* Una actualización manual de un entorno de ensayo o producción actualizará automáticamente el otro. El conjunto de entornos Producción+Fase debe estar en la misma versión de AEM.

Consulte las [Actualizaciones de versión de AEM](/help/implementing/deploying/aem-version-updates.md) para obtener más información.

Consulte [Actualización del entorno](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para aprender a actualizar un entorno.

### Hibernación y eliminación {#hibernation}

Los entornos de un programa de zona protegida hibernan automáticamente tras ocho horas de inactividad. Los entornos de zona protegida se eliminan después de seis meses continuos de hibernación.

Consulte [Entornos de zona protegida en hibernación y dehibernación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) para obtener más información sobre cómo anular la hibernación de entornos y eliminar automáticamente zonas protegidas.

### Sin asistencia técnica {#no-support}

Dado que un programa de zona protegida suele crearse para servir a los fines de formación, ejecución de demostraciones, habilitación o prueba de conceptos (POC), no hay asistencia técnica disponible para los problemas experimentados en un programa de zona protegida.

Si experimenta problemas al crear y administrar sus programas de zona protegida, sigue estando dentro del ámbito de la asistencia técnica.
