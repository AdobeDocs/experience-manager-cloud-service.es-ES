---
title: Actualizaciones de la versión de AEM
description: AEM Descubra cómo utiliza la integración y el envío continuos (CI/CD) para mantener sus proyectos en la versión más reciente de los que utiliza as a Cloud Service.
feature: Deploying
exl-id: 36989913-69db-4f4d-8302-57c60f387d3d
source-git-commit: ca91e969014415e872ecf8e42fe86ffc9ca41e10
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 9%

---


# Actualizaciones de la versión de AEM {#aem-version-updates}

AEM Descubra cómo utiliza la integración y el envío continuos (CI/CD) para mantener sus proyectos en la versión más reciente de los que utiliza as a Cloud Service.

## CI/CD {#ci-cd}

AEM as a Cloud Service AEM utiliza la integración y la entrega continuas (CI/CD) para garantizar que sus proyectos se encuentren en la versión de la aplicación más actual de la. Este proceso actualiza sin problemas las instancias de producción, ensayo y desarrollo sin causar ninguna interrupción a los usuarios.

AEM Antes de que las instancias se actualicen automáticamente, se publican nuevas versiones de mantenimiento de la con 3-5 días de antelación. Durante este periodo, tiene la opción de [déclencheur de actualizaciones manuales para las instancias de desarrollo](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment).Una vez transcurrido este tiempo, las actualizaciones de versión se aplican automáticamente en primer lugar a los entornos de desarrollo. Si la actualización se realiza correctamente, el proceso de actualización continúa con las instancias de fase y producción. Las instancias de desarrollo y ensayo actúan como una puerta de calidad automatizada, donde las pruebas escritas a medida se ejecutan antes de que la actualización se aplique en el entorno de producción.

>[!NOTE]
>
> Nota: Las actualizaciones automáticas para entornos de desarrollo se habilitarán progresivamente en 2023 para todos los clientes. Si los entornos de desarrollo no se actualizan automáticamente, puede utilizar actualizaciones manuales para mantenerlos sincronizados con los entornos de ensayo y producción.


## Tipo de actualizaciones {#update-types}

Existen dos tipos de actualizaciones versión de AEM:

* **Actualizaciones de mantenimiento de AEM**

   * Se pueden publicar diariamente.
   * Se utilizan principalmente para fines de mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.
   * Tienen un impacto mínimo, ya que los cambios se aplican con regularidad.

* **Nuevas actualizaciones de funciones**

   * Se lanzan el [un horario mensual predecible.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es)

## Error de actualización {#update-failure}

AEM Las actualizaciones de los productos pasan por un proceso de validación de productos intenso y totalmente automatizado que incluye varios pasos, lo que garantiza que no se interrumpa el servicio de ningún sistema en producción. Las comprobaciones de estado se utilizan para supervisar el estado de la aplicación. AEM Si estas comprobaciones fallan durante una actualización as a Cloud Service del estado, la versión no continúa y Adobe investigará por qué la actualización ha provocado este comportamiento inesperado.

Cuando se implementa una nueva versión de un código personalizado de en los entornos, [Pruebas funcionales de productos y personalizadas](/help/implementing/cloud-manager/overview-test-results.md#functional-testing) desempeñar un papel crucial a la hora de garantizar que los sistemas de producción se mantengan estables y funcionales incluso después de aplicar un cambio. AEM Estas pruebas también se aprovechan en el proceso de actualización de la versión de la versión de la.

Si la actualización al entorno de producción falla, Cloud Manager restablecerá automáticamente el entorno de ensayo. AEM Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de ensayo como de producción estén en la misma versión de.
Del mismo modo, si falla una actualización automatizada de un entorno de desarrollo, los entornos de ensayo y producción no se actualizarán.

>[!NOTE]
>
>AEM Si el código personalizado se insertó en el ensayo y no en la producción, la siguiente actualización de la eliminará esos cambios para reflejar la etiqueta de Git de la última versión correcta del cliente en producción. Por lo tanto, el código personalizado que solo estaba disponible en el ensayo deberá implementarse de nuevo.

## Prácticas recomendadas {#best-practices}

* 
   * **Uso del entorno de ensayo**
   * Utilice un entorno diferente (no una fase) para ciclos largos de control de calidad/UAT.
   * Una vez finalizada la prueba de corrección en Fase, continúe para verificar en Producción.

* 
   * **Canalización de producción**
   * Pausar antes de implementar en Producción.
   * Si cancela la canalización después de una implementación de fase, el código es &quot;desechable&quot; y no es un candidato válido para Producción, consulte [Configuración de una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

* 
   * **Canalización que no es de producción**
* Configurar [Canalización que no es de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).
* 
   * Acelere la velocidad y frecuencia de entrega para los errores de canalización de producción.  Identifique los problemas en las canalizaciones que no son de producción habilitando Prueba funcional del producto, Prueba funcional personalizada y Prueba de IU personalizada.

* 
   * **Copia de contenido**
   * Uso [Copia de contenido](/help/implementing/developing/tools/content-copy.md) para mover conjuntos de contenido similares a un entorno que no sea de producción.

* 
   * **Pruebas funcionales automatizadas**
* Incluya pruebas automatizadas en su canalización para probar la funcionalidad crítica.
* [Pruebas funcionales del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) y [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) AEM están bloqueando, si no se consigue, la versión no se implementará.

## Regresión {#regression}

Si encuentra un problema relacionado con la regresión, envíe un caso de asistencia a través de Admin Console.  Si el problema es un bloqueador y está afectando a la producción, se debe plantear un P1.  Proporcione todos los detalles necesarios para reproducir el problema de regresión.

## Almacén de nodos compuestos {#composite-node-store}

En la mayoría de los casos, las actualizaciones no implican ningún tiempo de inactividad, incluida la instancia de creación, que es un clúster de nodos. Las actualizaciones móviles son posibles debido a [la función de almacén de nodos compuestos en Oak.](https://jackrabbit.apache.org/oak/docs/nodestore/compositens.html)

AEM Esta función permite a los usuarios hacer referencia a varios repositorios de forma simultánea. En un [implementación móvil,](/help/implementing/deploying/overview.md#how-rolling-deployments-work) AEM la nueva versión de la contiene su propio `/libs` AEM (el repositorio inmutable basado en TarMK), distinto de la versión más antigua, aunque ambos hacen referencia a un repositorio mutable basado en DocumentMK compartido que contiene áreas como `/content` , `/conf` , `/etc` y otros.

Porque tanto la versión antigua como la nueva tienen sus propias versiones de `/libs`Sin embargo, ambos pueden estar activos durante la actualización móvil y pueden asumir el tráfico hasta que el antiguo se sustituya completamente por el nuevo.
