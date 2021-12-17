---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.12.0
description: Estas son las notas de la versión de Cloud Manager en AEM versión as a Cloud Service 2021.12.0.
feature: Release Information
source-git-commit: fc1eae86097f0cc928860ff7f43e3177f2e8f3a1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.12.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager en AEM as a Cloud Service 2021.12.0 es el 16 de diciembre de 2021. La próxima versión está planificada para enero de 2022.

### Novedades {#what-is-new}

* El hash de confirmación, que ya está visible en la interfaz de usuario, ahora también se proporciona en la API .
* La página Actividad ahora incluye una ventana emergente para la ejecución de canalizaciones que proporciona un resumen de los detalles de la canalización de un vistazo.
* Se agregaron actualizaciones para incluir detalles adicionales presentados en la página Actividades .
* La pestaña Información de Cloud Manager ahora incluye acceso rápido a las guías de API y a los recursos asociados.
* Un usuario con la función Administrador de implementación ahora puede iniciar el asistente de creación de proyectos/ramas para un repositorio sin ramas desde el menú de acción de la página repositorios.
* El administrador de implementación, que se encuentra en el flujo de trabajo de añadir o editar canalización, ahora está informado sobre cómo crear una rama o proyecto si el repositorio seleccionado no tiene ramas.
* Se ha añadido una nueva función de autoservicio de Cloud Manager para permitir [agregar secretos y variables de forma libre en el nivel de entorno.](/help/implementing/cloud-manager/environment-variables.md)
* Con el nuevo [Complemento Demostraciones de Referencia](/help/journey-sites/demos-add-on/overview.md) (disponible el 17 de diciembre de 2021), se pueden instalar las bases de código de demostración más recientes para AEM productos y estar listos para ser implementados a través del nuevo [herramienta de creación rápida de sitios](/help/journey-sites/quick-site/overview.md) en Sitios.
* Las canalizaciones front-end ahora admiten variables de canalización.
* Las pantallas ahora se pueden habilitar en el cuadro de diálogo Editar programa para todos los entornos limitados.
* Las directrices proporcionadas por la tarjeta de llamada a la acción de la página de información general se han actualizado para reflejar con precisión su asociación con la canalización de pila completa de producción.
* Se han añadido mejoras a la página Actividad para obtener detalles adicionales aplicables a las canalizaciones, como código fuente, ID de confirmación, etc.
* Se realizaron actualizaciones menores en la interfaz de usuario al copiar entradas TXT (&quot;valor TXT&quot; en lugar de &quot;registro TXT&quot;) para eliminar posibles confusiones.
* [La documentación relacionada con los errores de certificado](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) se ha actualizado para incluir ejemplos adicionales junto con pasos de solución de problemas.
* Ahora hay disponible una opción en la ejecución de canalización front-end para rechazar o aprobar antes de la implementación en producción.

### Corrección de errores {#bug-fixes}

* Los artefactos de prueba funcionales y de interfaz de usuario no se incluían en el registro de pasos de la compilación.
* No se podía acceder a los registros de los pasos de prueba del producto, la funcionalidad y la interfaz de usuario a través de la API pública.
* En casos excepcionales, el vínculo de la página de detalles del entorno al servicio de publicación o vista previa no funcionaría.
* Las canalizaciones de producción de pila completa siguen denominándose &quot;Canalización de producción&quot; incluso cuando el usuario introduce un nombre diferente en el campo de nombre.
