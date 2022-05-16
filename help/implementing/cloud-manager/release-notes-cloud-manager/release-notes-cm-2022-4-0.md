---
title: Notas de la versión para Cloud Manager 2022.4.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión de Cloud Manager 2022.4.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: e7ff623b-aeca-40a6-bf48-98af270a4117
source-git-commit: 458d63c27bb2ab4d09237aa3ecb96c0f6d5e67ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de la versión para Cloud Manager 2022.4.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión de Cloud Manager 2022.4.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager 2022.4.0 en AEM as a Cloud Service es el 7 de abril de 2022. La próxima versión está planificada para el 5 de mayo de 2022.

## Novedades {#what-is-new}

* Se han implementado mejoras en la duración y la tasa de éxito de los pasos de compilación de la canalización, que se implementarán gradualmente para todos los clientes durante el mes de abril.
* Ahora puede encontrar fácilmente una rama de Git escribiendo los primeros caracteres del nombre en el campo de entrada en el asistente de añadir y editar canalización y seleccionando entre las coincidencias sugeridas para ambas [producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) y [sin producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) canalizaciones.
* Poco después de la versión de abril, India estará disponible para su selección al definir la región de la nube durante la creación del entorno.
* La variable **Canalizaciones** ahora tiene paginación para mejorar la capacidad de uso de los programas con un gran número de canalizaciones.
   * 50 filas por página se muestran en la tabla.
* La versión de [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) utilizado por Cloud Manager se ha actualizado a la versión 36.
* Oracle JDK es ahora el JDK predeterminado para el desarrollo y funcionamiento de aplicaciones AEM. El proceso de creación de Cloud Manager cambiará automáticamente al uso de JDK de Oracle, aunque se haya seleccionado explícitamente una opción alternativa en la cadena de herramientas de Maven.
   * Para obtener más información sobre cómo cambiar a Oracle JDK, consulte [la documentación Entorno de compilación .](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * Consulte [Preguntas frecuentes sobre la política de asistencia de Java para Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) para abordar preguntas comunes sobre este cambio.
* La ejecución de la canalización ahora fallará más rápido al detectar versiones de AEM anteriores durante el paso de validación. A los usuarios se les mostrará un mensaje en la interfaz de usuario para que los guíen.

## Correcciones de errores {#bug-fixes}

* El registro creado en el paso Prueba de IU ahora está disponible para su descarga a través de la interfaz de usuario.
* Las canalizaciones de configuración de nivel web ahora solo pueden reutilizar paquetes desde ejecuciones de configuración de nivel web.
* Se ha añadido buena claridad a los mensajes de la interfaz de usuario sobre cómo actualizar AEM en un entorno obsoleto.
