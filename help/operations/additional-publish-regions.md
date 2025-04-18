---
title: Regiones de publicación adicionales
description: Descubra cómo AEM as a Cloud Service admite regiones de publicación adicionales para aumentar la disponibilidad y reducir la latencia.
exl-id: b9ac3c6a-eb8b-461d-8f1d-a0356046a3f9
feature: Operations
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 71%

---


# Regiones de publicación adicionales {#additional-publish-regions}

Se pueden autorizar y habilitar regiones de publicación adicionales en programas configurados con AEM Sites. Cuando se configura, el tráfico en los entornos de ensayo y producción se enruta a varias granjas de publicación, lo que tiene las siguientes ventajas:

* Latencia reducida: las solicitudes que se dirigen desde la CDN a las instancias de publicación de AEM se dirigen a la región de publicación más cercana, lo que resulta ventajoso para los sitios web y las aplicaciones visitadas por usuarios en varias regiones geográficas.
* Mayor disponibilidad: si una región no está disponible, la CDN dirige el tráfico a las demás regiones disponibles.

Las organizaciones pueden autorizar hasta tres regiones de publicación adicionales.

>[!NOTE]
>
>* Esta función está disponible para las soluciones Sites y Forms.
>* Esta característica no se puede aplicar a [programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).
>* AEM Esta función requiere que el programa se actualice a la versión de lanzamiento de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la versión de la aplicación o de la versión 12142.

## Casos de uso {#use-cases}

A continuación se indican algunos casos de uso en los que las organizaciones pueden beneficiarse de la concesión de licencias para regiones de publicación adicionales.

1. Para las organizaciones que reciben tráfico significativo o crítico para el negocio de usuarios alejados de la región principal, las regiones de publicación adicionales pueden reducir la latencia que experimentan esos visitantes.
1. Para las organizaciones que pueden sufrir un daño monetario o de reputación significativo cuando un sitio no está disponible, esto se puede mitigar mediante el uso de regiones de publicación adicionales para hacer que el nivel de publicación de AEM sea más resistente al fracaso regional.
1. Para las organizaciones cuyos autores de contenido se encuentran en una ubicación geográfica distante de la mayoría de los visitantes del nivel de publicación, la región principal se puede elegir cerca de la ubicación de los autores de contenido, mientras que se pueden configurar regiones de publicación adicionales cerca del tráfico del lado de publicación, con ambas audiencias beneficiándose de una experiencia optimizada.

## Activación y configuración {#enabling-and-configuring}

Después de autorizar una región de publicación adicional, las regiones se configuran haciendo uso de Cloud Manager. Consulte la [Documentación de Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) para obtener instrucciones detalladas.

Las regiones de publicación adicionales se aplican a entornos de ensayo y producción, pero no a entornos de RDE o desarrollo.

En caso de que una región deje de estar disponible, los clientes no necesitan administrar el enrutamiento del tráfico a las regiones disponibles, ya que lo administra la CDN de Adobe.

Como se describe en la sección Consideraciones avanzadas de red que aparece a continuación, se recomienda que los clientes que utilicen redes avanzadas la configuren para cada región de publicación adicional a fin de mantener la disponibilidad si una región deja de estar disponible.


## Consideraciones avanzadas de red {#advanced-networking-considerations}

Cuando se habilita una región de publicación adicional en un programa con una red avanzada ya configurada, el tráfico en la región de publicación adicional que coincide con las reglas de red avanzadas se enrutará de forma predeterminada a través de la región principal. Para aprovechar la mayor disponibilidad, se recomienda habilitar redes avanzadas en las regiones adicionales.

Consulte la sección [Configuración avanzada de redes para regiones de publicación adicionales](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) en la documentación de redes avanzadas para obtener más información, incluido cómo agregar configuraciones de red avanzadas a regiones adicionales sin incurrir en pérdida de conectividad.

## Registro {#logging}

Si se habilitan regiones de publicación adicionales, se habilitarán registros independientes para cada región a través de Cloud Manager. Para obtener más información, vea [Obtener acceso y administrar registros](/help/implementing/cloud-manager/manage-logs.md) y [Registros para regiones de Publish adicionales](/help/implementing/developing/introduction/logging.md#logs-for-additional-publish-regions).

## Restricciones {#limitations}

Tenga en cuenta las siguientes limitaciones cuando considere la posibilidad de utilizar regiones de publicación adicionales.

* Solo se pueden añadir regiones de publicación adicionales a AEM Sites o AEM Forms.
   * AEM Las regiones de publicación adicionales no se extienden a otras soluciones de publicación o funcionalidades relacionadas implementadas en el mismo programa (por ejemplo, AEM Assets o Adobe Learning Manager).
   * Sin embargo, estas soluciones se pueden agregar a un programa siempre y cuando tenga al menos una solución de Sites o Forms que se aplique a él.
* Solo se pueden agregar regiones adicionales si los derechos asociados están disponibles y no se utilizan en el inquilino.
* Se puede agregar un máximo de tres regiones de publicación adicionales a cualquier entorno individual.
* Las regiones adicionales solo están disponibles en los programas de producción. La función no está disponible en programas de zona protegida.
* Las regiones de publicación adicionales se aplican solo a entornos de ensayo y producción, no a entornos de RDE o desarrollo.
* Las regiones de publicación adicionales requieren que el programa se actualice a la versión de lanzamiento de AEM de la versión 12142 o superior.
