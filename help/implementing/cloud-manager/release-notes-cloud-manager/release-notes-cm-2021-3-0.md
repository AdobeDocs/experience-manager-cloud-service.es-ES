---
title: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.3.0
description: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.3.0
feature: Información de la versión
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.3.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.3.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.3.0 es el 11 de marzo de 2021.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Los clientes con entornos con configuraciones de nombre de dominio personalizado preexistentes para [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) y [nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) verán un mensaje sobre las configuraciones existentes anteriormente y podrán autoabastecerse mediante la interfaz de usuario.

* Los usuarios con los permisos necesarios ahora pueden editar un programa, lo que les permite hacer lo siguiente de forma autoservicio:
   * Agregar la solución Sitios a un programa existente con Assets o viceversa.
   * Elimine Sitios o Recursos de un programa existente con Sitios y Recursos.
   * Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

* **AEM** actualización push ahora se mostrará para las pantallas Ejecución de canalización y Actividad .

* Si un entorno está en hibernación pero también hay una actualización AEM disponible, el estado **Hibernated** tendrá prioridad sobre **Update available**.

* Los usuarios ahora pueden ver sus funciones de Cloud Manager seleccionando la opción &quot;Ver funciones de Cloud Manager&quot; después de navegar al icono de perfil de usuario (parte superior derecha) del shell unificado.

* La etiqueta **Application for Approval** se ha vuelto a etiquetar como **Production Approval** para una buena claridad.

* La etiqueta **Version** se ha vuelto a etiquetar como **Git Tag** en la pantalla de ejecución de la canalización de producción.

* Las etiquetas que definen el comportamiento cuando métricas importantes no alcanzan el umbral definido se han vuelto a etiquetar para reflejar su verdadero comportamiento: **Cancelar inmediatamente** y **Aprobar inmediatamente**.

* Las listas de deprecación de clases y métodos se han actualizado en función de la versión `2021.3.4997.20210303T022849Z-210225` del SDK del Cloud Service de AEM.

* La canalización de producción de Cloud Manager ahora incluirá la capacidad [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Corrección de errores  {#bug-fixes}

* En algunos casos, las versiones de paquetes se omitían durante AEM actualización push.

* Algunos problemas de calidad no se descubrieron correctamente cuando los paquetes estaban incrustados en otros paquetes.

* En situaciones oscuras, el nombre predeterminado del programa generado al abrir el cuadro de diálogo Agregar programa podría ser un duplicado de un nombre de programa existente.

* En ocasiones, si el usuario sale de la página de ejecución de la canalización inmediatamente después de iniciar una canalización, aparece un mensaje de error que indica que la acción ha fallado, aunque la ejecución realmente se inicia.

* El paso de compilación se reinició innecesariamente cuando las compilaciones de clientes generaron paquetes no válidos.

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .
