---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.3.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.3.0
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.3.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.3.0 es el 11 de marzo de 2021.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Clientes con entornos con configuraciones de nombre de dominio personalizado preexistentes para [LISTAS DE PERMITIDOS IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) y [Nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) Verá un mensaje sobre las configuraciones existentes anteriormente y podrá autoabastecerse a través de la interfaz de usuario.

* Los usuarios con los permisos necesarios ahora pueden editar un programa, lo que les permite hacer lo siguiente de forma autoservicio:
   * Agregar la solución Sitios a un programa existente con Assets o viceversa.
   * Elimine Sitios o Recursos de un programa existente con Sitios y Recursos.
   * Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

* **Actualización de AEM** ahora se muestra para las pantallas Ejecución de la canalización y Actividad .

* Si un entorno está en hibernación pero también hay una actualización de AEM disponible, la variable **Hibernado** el estado tendrá prioridad sobre **Actualización disponible**.

* Los usuarios ahora pueden ver sus funciones de Cloud Manager seleccionando la opción &quot;Ver funciones de Cloud Manager&quot; después de navegar al icono de perfil de usuario (parte superior derecha) del shell unificado.

* La etiqueta **Solicitud de aprobación** se ha vuelto a etiquetar como **Aprobación de producción** para una buena claridad.

* La variable **Versión** se ha vuelto a etiquetar como **Etiqueta de Git** en la pantalla de ejecución de la canalización de producción.

* Las etiquetas que definen el comportamiento cuando métricas importantes no alcanzan el umbral definido se han vuelto a etiquetar para reflejar su verdadero comportamiento: **Cancelar inmediatamente** y **Aprobar inmediatamente**.

* Las listas de desaprobación de clases y métodos se han actualizado en función de la versión `2021.3.4997.20210303T022849Z-210225` del SDK de AEM Cloud Service.

* La canalización de producción de Cloud Manager ahora incluye [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) capacidad.

### Corrección de errores  {#bug-fixes}

* En algunos casos, las versiones de paquetes se omitían durante AEM actualización push.

* Algunos problemas de calidad no se descubrieron correctamente cuando los paquetes estaban incrustados en otros paquetes.

* En situaciones oscuras, el nombre predeterminado del programa generado al abrir el cuadro de diálogo Agregar programa podría ser un duplicado de un nombre de programa existente.

* En ocasiones, si el usuario sale de la página de ejecución de la canalización inmediatamente después de iniciar una canalización, aparece un mensaje de error que indica que la acción ha fallado, aunque la ejecución realmente se inicia.

* El paso de compilación se reinició innecesariamente cuando las compilaciones de clientes generaron paquetes no válidos.

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .
