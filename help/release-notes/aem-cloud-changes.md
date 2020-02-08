---
title: Cambios notables en Adobe Experience Manager (AEM) como servicio de nube
description: Cambios notables en Adobe Experience Manager (AEM) como servicio de nube
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# Cambios notables en Adobe Experience Manager (AEM) como servicio de nube {#notable-changes-aem-cloud}

El servicio de nube AEM ofrece muchas funciones y posibilidades nuevas para la gestión de sus proyectos de AEM. Sin embargo, existen varias diferencias entre los sitios de AEM in situ o en los servicios administrados de Adobe en comparación con los servicios de nube de AEM. Este documento destaca las importantes diferencias.

>[!NOTE]
>En este documento se destacan los cambios notables que se han producido en AEM en su conjunto. Para ver los cambios específicos de la solución, consulte:
>
>* [Cambios notables en los sitios de AEM en el servicio de nube de AEM](/help/sites-cloud/sites-cloud-changes.md)
>* [Cambios notables en AEM Assets en el servicio de nube de AEM](/help/assets/assets-cloud-changes.md)


Las principales diferencias se encuentran en las siguientes áreas:

* [/apps y /libs son inmutables en tiempo de ejecución](#apps-libs-immutable)
* [Los paquetes y la configuración de OSGi deben estar basados en el repositorio](#osgi)
* [No se permiten los cambios en el repositorio de publicación](#changes-to-publish-repo)
* [No se permiten los modos de ejecución personalizados](#custom-runmodes)
* [Eliminación de agentes de replicación](#replication-agents)
* [Eliminación de la IU clásica](#classic-ui)
* [Entrega en el lado de publicación](#publish-side-delivery)
* [Administración y entrega de recursos](#asset-handling)

## /apps y /libs son inmutables en tiempo de ejecución {#apps-libs-immutable}

Cualquier contenido y subcarpetas de `/apps` y `/libs` es de sólo lectura. Cualquier función o código personalizado que espere realizar cambios allí no podrá hacerlo. Se mostrará un error que indica que dicho contenido es de solo lectura y que la operación de escritura no se pudo completar. Esto afecta a varias áreas de AEM:

* No se permite ningún cambio en `/libs` el.
   * Esta regla no es nueva, pero no se aplicaba en versiones anteriores in situ de AEM.
* Las superposiciones de áreas en las `/libs` que se permite la superposición siguen estando permitidas en `/apps`.
   * Estas superposiciones deben proceder de Git a través de la tubería CI/CD.
* La información de diseño de plantilla estática almacenada en no `/apps` se puede editar mediante la interfaz de usuario.
   * En su lugar, se recomienda utilizar plantillas editables.
   * Si las plantillas estáticas siguen siendo necesarias, la información de configuración debe proceder de Git a través de la canalización CI/CD.
* El modelo MSM y las configuraciones de implementación MSM personalizadas deben instalarse desde Git a través de la canalización CI/CD.
* Los cambios en la traducción I18n deben proceder de Git a través de la canalización CI/CD.

## Los paquetes y la configuración de OSGi deben estar basados en el repositorio {#osgi}

La consola web, utilizada en versiones anteriores de AEM para cambiar la configuración de OSGi, no está disponible en el servicio de nube de AEM. Por lo tanto, los cambios en OSGi deben introducirse a través de la canalización CI/CD.

* Los cambios en la configuración de OSGi sólo pueden realizarse mediante la persistencia de Git como ajustes OSGi basados en JCR.
* Los paquetes OSGi nuevos o actualizados deben introducirse a través de Git como parte del proceso de construcción de la canalización CI/CD.

## No se permiten los cambios en el repositorio de publicación {#changes-to-publish-repo}

No se permiten cambios directos en el repositorio de publicación en el servicio de nube de AEM. En versiones anteriores de AEM o AEM in situ en AMS, los cambios de código se podían realizar directamente en el repositorio de publicación; por ejemplo, para crear usuarios, actualizar el perfil de usuario y crear nodos. Esto ya no es posible y puede mitigarse de las siguientes formas:

* Para la configuración basada en contenido y contenido: realice los cambios en la instancia de autor y publíquelos.
* Para código y configuración: realice los cambios en el repositorio de GIT y ejecute la canalización CI/CD para implementarlos.
* Para datos relacionados con el usuario, como envíos de formularios o datos de perfil: utilice el servicio de perfil unificado de la plataforma de Experience Cloud u otro almacén de reconocimiento de sesiones de terceros.

## No se permiten los modos de ejecución personalizados {#custom-runmodes}

Se proporcionan los siguientes modos de ejecución predeterminados para el servicio de nube AEM:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

Los modos de ejecución adicionales o personalizados no son posibles en AEM Cloud Service.

## Eliminación de agentes de replicación {#replication-agents}

En AEM Cloud Service, el contenido se publica mediante [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Los agentes de replicación utilizados en versiones anteriores de AEM ya no se utilizan ni se proporcionan, lo que podría afectar a las siguientes áreas de los proyectos de AEM existentes:

* Flujos de trabajo personalizados que llevan contenido a los agentes de replicación de los servidores de vista previa, por ejemplo.
* Personalización a agentes de replicación para transformar contenido
* Uso de la replicación inversa para devolver el contenido de la publicación al autor

## Eliminación de la IU clásica {#classic-ui}

La IU clásica ya no está disponible en el servicio de nube de AEM.

## Entrega en el lado de publicación {#publish-side-delivery}

La aceleración HTTP, incluida la CDN y la administración de tráfico para los servicios de creación y publicación, se proporcionan de forma predeterminada en el servicio de nube de AEM.

Para la transición de proyectos desde AMS o una instalación local, Adobe recomienda enfáticamente aprovechar la CDN integrada, ya que las funciones del servicio de nube AEM están optimizadas para la CDN proporcionada.

## Administración y entrega de recursos {#asset-handling}

La carga, el tratamiento y la descarga de recursos se han optimizado en el servicio de nube de AEM para ser más eficientes y permitir una mejor escala y cargas y descargas más rápidas. Sin embargo, esto puede afectar a algunos códigos personalizados existentes.

* El flujo de trabajo predeterminado de actualización **de recursos** DAM en versiones anteriores de AEM ya no está disponible.
* Los componentes del sitio Web que entregan un archivo binario **sin transformación** deben utilizar la descarga directa.
   * El servlet Sling GET se ha cambiado para hacerlo de forma predeterminada.
* Los componentes del sitio Web que proporcionan un archivo binario **con transformación** (por ejemplo, cambiar el tamaño mediante servlet) pueden seguir funcionando como lo han hecho.
* Los recursos que se incluyen mediante el Administrador de paquetes requieren un reprocesamiento manual mediante la acción **Volver a procesar recursos** de la interfaz de Recursos.
