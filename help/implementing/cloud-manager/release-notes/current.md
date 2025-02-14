---
title: Notas de la versión para Cloud Manager 2025.2.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2025.2.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aaef376b733c10643e44205e55a0921c22008990
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 18%

---

# Notas de la versión para Cloud Manager 2025.2.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.2.0 en AEM (Adobe Experience Manager) as a Cloud Service.


Vea también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.2.0 en AEM as a Cloud Service es el viernes, 13 de febrero de 2025.

La próxima versión planificada es el viernes, 13 de marzo de 2025.

## Novedades {#what-is-new}

* **Actualización de las reglas de calidad del código**

  A partir del jueves, 13 de febrero de 2025, el paso de calidad del código de Cloud Manager ahora utiliza SonarQube 9.9.5.90363.

  Las reglas actualizadas, disponibles para Cloud Manager en AEM as a Cloud Service en [este vínculo](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules), determinan las puntuaciones de seguridad y la calidad del código para las canalizaciones de Cloud Manager.

* SonarQube 9.9 es ahora el motor de análisis de calidad de código predeterminado para todos los clientes.

* **Compatibilidad con la versión Java 17 y Java 21**

  Los clientes ahora pueden compilar con Java 17 o Java 21, y obtener acceso a las mejoras de rendimiento y a las nuevas funciones de idioma. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Cuando la versión de compilación se establece en Java 17 o Java 21, el tiempo de ejecución implementado es Java 21.

* **99,99% de informes de tiempo de actividad de SLA para Edge Delivery Services**

  Los informes de tiempo de actividad del 99,99 % de alta disponibilidad ya están disponibles para los programas Edge Delivery Services aptos. Para habilitar esta función, los clientes deben incorporar correctamente sus sitios de Edge Delivery Services y aplicar su Service level agreement (SLA) al 99,99 % en Cloud Manager.

  Ver también [SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla).

* **Se mejoró la experiencia de invitación de usuarios para Edge Delivery Services**

  Se mejoró la experiencia al invitar a usuarios al repositorio de contenido asociado con Edge Delivery Services. <!-- CMGR-65331 -->

* **Creación automática de perfiles de administración en instancias de publicación**

  Anteriormente, Cloud Manager permitía la creación manual de perfiles de administración en instancias de publicación, pero no admitía la creación automática de forma predeterminada. Con esta actualización, los perfiles de administración ahora se crean automáticamente en instancias de publicación, lo que mejora la facilidad de uso y reduce el tiempo de configuración para los clientes.

  Para obtener más información, consulte [Permisos personalizados](/help/implementing/cloud-manager/custom-permissions.md).

  ![Filtrado de actividades de canalización](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **Transición a OAuth para entornos Cloud Service**

  Los nuevos entornos de Cloud Service ahora utilizan la autenticación de servicio a servicio basada en OAuth para proyectos de integración de Adobe Developer Console en lugar del método de autenticación JWT utilizado anteriormente. La autenticación JWT está en desuso y su finalización está prevista para junio de 2025.

* **Compatibilidad con claves privadas EC (Elliptic Curve) (secp384r1)**

  Cloud Manager ahora admite claves privadas de curva elíptica (EC) `secp384r1`, lo que proporciona una seguridad y conformidad mejoradas para los certificados SSL OV/EV administrados por el cliente.
Para obtener más información, consulte [Requisitos para los certificados SSL OV/EV administrados por el cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements). <!-- CMGR-63636 -->

* **Entornos de prueba especializados**

  A partir del 27 de febrero de 2025, se pondrá a disposición de los primeros usuarios un nuevo entorno de desarrollo con recursos mejorados.


<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## Correcciones de errores

* **(IU) Se ha corregido un problema que impedía la configuración de CDN para dominios en Cloud Manager.**
Los clientes que intentaban añadir una configuración de CDN en Cloud Manager encontraban un error de pantalla al seleccionar un dominio del menú desplegable. Este error de interfaz de usuario impedía la asignación de dominios en entornos de producción, lo que bloqueaba el proceso de configuración.

  Además, algunos dominios seguían siendo inaccesibles en el servidor, a pesar de haberse eliminado de la interfaz de usuario. Este problema provocaba conflictos con las configuraciones de CDN existentes.

  Con esta corrección, ahora puede seleccionar correctamente un dominio de la lista desplegable sin encontrar un error. Se han corregido las incoherencias del servidor que impedían la reconfiguración del dominio. Y, por último, la validación mejorada ahora garantiza que los dominios en conflicto se eliminen correctamente antes de volver a agregarlos.<!-- CMGR-64888 -->
* **(backend) Se ha corregido un problema que hacía que las notificaciones de caducidad SSL se enviaran varias veces.**
Se identificó un error en el que el programador de notificaciones de caducidad SSL, diseñado para ejecutarse una vez al día a medianoche, se activaba incorrectamente dos veces al día: una a medianoche y otra vez a las 12:30 a. m. Este problema provocaba que se enviaran varias notificaciones redundantes con respecto a los certificados SSL caducados.

  El programador de notificaciones ahora se ejecuta correctamente solo una vez al día según lo previsto. Además, ya no recibirá notificaciones de caducidad SSL duplicadas. <!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
