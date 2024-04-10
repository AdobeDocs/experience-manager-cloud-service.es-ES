---
title: Actualizaciones de la versión de AEM
description: Descubra cómo Adobe Experience Manager AEM () as a Cloud Service utiliza la integración y la entrega continuas (CI/CD) para mantener sus proyectos en la última versión.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: 72fc611e006f80fdda672f08b0b795432f5899e2
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

Descubra cómo Adobe Experience Manager AEM () as a Cloud Service utiliza la integración y la entrega continuas (CI/CD) para mantener sus proyectos en la última versión.

## CI/CD {#ci-cd}

AEM as a Cloud Service AEM utiliza la integración y la entrega continuas (CI/CD) para garantizar que sus proyectos se encuentren en la versión de la aplicación más actual de la. Este proceso actualiza sin problemas las instancias de producción, ensayo y desarrollo sin causar ninguna interrupción a los usuarios.

>[!NOTE]
> Como las instancias de desarrollo ya se actualizan automáticamente, es posible que las actualizaciones manuales de las instancias de desarrollo no estén disponibles para _algunos_ de sus programas. Esta función se está migrando a actualizaciones automáticas.

AEM Antes de que las instancias se actualicen automáticamente, se publica una nueva versión de mantenimiento de la con 3-5 días de antelación. Durante este periodo, la instancia de desarrollo puede actualizarse automáticamente o, si está disponible, puede [Almacene en déclencheur la actualización para las instancias de desarrollo](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment). Las actualizaciones de versión se aplican automáticamente primero a los entornos de desarrollo. Si la actualización se realiza correctamente, el proceso de actualización continúa con las instancias de fase y producción. Las instancias de desarrollo y ensayo actúan como una puerta de calidad automatizada, donde las pruebas escritas a medida se ejecutan antes de que la actualización se aplique en el entorno de producción.

### NIMU (actualizaciones de mantenimiento no intrusivas) {#nimu}

Las actualizaciones de mantenimiento no intrusivas son actualizaciones automáticas que se aplican sin involucrar a las canalizaciones del cliente.
AEM A través de NIMU, el cliente puede utilizar la canalización en cualquier momento, incluso si se ha programado o está en curso una actualización de la versión de la aplicación y las actualizaciones de mantenimiento ya no aparecerán en el historial de ejecución de la canalización del cliente, lo que facilita el seguimiento del historial de implementaciones de código.

#### Actualizar actividades

AEM La versión actual de la interfaz de usuario aún se puede comprobar para cada entorno, como antes, mediante el panel Entornos de la interfaz de usuario de Cloud Manager. Las actualizaciones de mantenimiento no intrusivas utilizan las mismas puertas de calidad que se utilizan en la canalización, incluidas las pruebas escritas por el cliente.
Se enviará una notificación de la interfaz de usuario de Cloud Manager cada vez que se aplique una actualización de mantenimiento no intrusiva a los entornos del programa. Puede configurarlo para que también se envíe a su correo electrónico.

>[!NOTE]
>
> Nota: Las actualizaciones de mantenimiento no intrusivas se habilitarán progresivamente para todos los clientes en 2024.


## Tipo de actualizaciones {#update-types}

Existen dos tipos de actualizaciones versión de AEM:

* [AEM **Actualizaciones de mantenimiento**](/help/release-notes/maintenance/latest.md)

   * Se utilizan principalmente con fines de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.
   * Tiene un impacto mínimo porque los cambios se aplican con regularidad.

* [AEM **Activación de funciones**](/help/release-notes/release-notes-cloud/release-notes-current.md)

   * Se publican con un calendario mensual predecible.

>[!NOTE]
>
> Compruebe las fechas clave de las versiones mensuales en [El Experience Manager publica la hoja de ruta](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es#aem-as-cloud-service) y marque sus calendarios para prepararse para las actividades clave y prepararse para la versión.

## Error de actualización {#update-failure}

AEM Las actualizaciones de los productos pasan por un proceso de validación de productos intenso y totalmente automatizado que incluye varios pasos, lo que garantiza que no se interrumpa el servicio de ningún sistema en producción. Las comprobaciones de estado se utilizan para supervisar el estado de la aplicación. AEM Si estas comprobaciones fallan durante una actualización as a Cloud Service del estado, la versión no continúa y Adobe investiga por qué la actualización ha provocado este comportamiento inesperado.

Cuando implementa una nueva versión del código personalizado en el entorno, [Pruebas funcionales de productos y personalizadas](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) Desempeñan un papel crucial. Garantizan que los sistemas de producción permanezcan estables y funcionales incluso después de aplicar un cambio. AEM Estas pruebas también se aplican en el proceso de actualización de la versión de la aplicación de la versión de la.

Si la actualización al entorno de producción falla, Cloud Manager vuelve atrás automáticamente el entorno de ensayo. AEM Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de ensayo como de producción estén en la misma versión de.
Del mismo modo, si falla una actualización automatizada de un entorno de desarrollo, los entornos de ensayo y producción no se actualizan.

>[!NOTE]
>
>AEM Si el código personalizado se insertó en el ensayo y no en la producción, la siguiente actualización elimina esos cambios para reflejar la etiqueta de Git de la última versión correcta del cliente en producción. Por lo tanto, el código personalizado que solo estaba disponible en el ensayo debe implementarse de nuevo.

## Prácticas recomendadas {#best-practices}

* **Uso del entorno de ensayo**
   * Utilice un entorno diferente (no una fase) para ciclos largos de control de calidad/UAT.
   * Una vez finalizada la prueba de sanidad en Fase, continúe para verificar en Producción.

* **Canalización de producción**
   * Pausar antes de implementar en Producción.
   * Si cancela la canalización después de una implementación de fase, indica que el código es &quot;desechable&quot; y no es un candidato válido para Producción, consulte [Configuración de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* **Canalización que no es de producción**
   * Configurar un [Canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
   * Acelere la velocidad y frecuencia de entrega para los errores de canalización de producción. Identifique los problemas en las canalizaciones que no son de producción habilitando Prueba funcional del producto, Prueba funcional personalizada y Prueba de IU personalizada.

* **Copia de contenido**
   * Uso [Copia de contenido](/help/implementing/developing/tools/content-copy.md) para mover conjuntos de contenido similares a un entorno que no sea de producción.

* **Pruebas funcionales automatizadas**
   * Incluya pruebas automatizadas en su canalización para poder probar funcionalidades críticas.
   * [Pruebas funcionales del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) y [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) AEM se están bloqueando; si no se consigue, la versión de la aplicación no se implementará.

## Regresión {#regression}

Si encuentra un problema relacionado con la regresión, envíe un caso de asistencia por medio del Admin Console. Si el problema es un bloqueador y su impacto en la producción, se debe plantear un P1. Proporcione todos los detalles necesarios para reproducir el problema de regresión.

## Almacén de nodos compuestos {#composite-node-store}

Normalmente, las actualizaciones no implican ningún tiempo de inactividad, incluida la instancia de creación, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a [la función de almacén de nodos compuestos en Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

AEM Esta función permite a los usuarios hacer referencia a varios repositorios de forma simultánea. En un [implementación móvil](/help/implementing/deploying/overview.md#how-rolling-deployments-work)AEM , la nueva versión de la contiene su propia `/libs` (el repositorio inmutable basado en TarMK). AEM Es distinto de la versión de la versión anterior, aunque ambos hacen referencia a un repositorio mutable compartido basado en DocumentMK que contiene áreas como `/content` , `/conf` , `/etc` y otros.

Porque tanto la versión antigua como la nueva tienen sus propias versiones de `/libs`, ambos pueden estar activos durante la actualización móvil. Y, ambos pueden asumir el tráfico hasta que el antiguo sea completamente reemplazado por el nuevo.
