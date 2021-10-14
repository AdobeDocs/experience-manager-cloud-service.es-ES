---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.10.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.10.0
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 3b1ff5f1715cd18228a9b7e5c57b0f3d84ee0eb0
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 3%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.10.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.10.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.10.0 es el 14 de octubre de 2021.
La próxima versión está planificada para el 4 de noviembre de 2021.

### Novedades {#what-is-new}

* Como preparación para algunos cambios futuros, ahora se hará referencia a las canalizaciones de implementación existentes y se etiquetarán en la interfaz de usuario como canalizaciones de **Pila completa**.

* La tarjeta de canalización se ha actualizado para que ahora muestre una sola cara integrada que muestre tanto las canalizaciones de producción como las que no son de producción, y el usuario puede seleccionar Ejecutar/Pausar/Reanudar directamente en el menú de acción asociado con cada canalización.

* Un usuario con la función de administrador de implementación ahora puede eliminar la canalización de producción de forma autoservicio mediante la interfaz de usuario.

* Se han actualizado las experiencias de adición y edición de canalización para que ahora utilicen modelos modernos y conocidos.

* Los usuarios de Cloud Manager ahora pueden enviar comentarios directamente desde la interfaz de usuario mediante el botón **Comentarios** en la parte superior derecha de la página de aterrizaje.

* Los gráficos SLA anuales ahora se pueden descargar desde la interfaz de usuario de Cloud Manager.

* La calidad del código y las ejecuciones de canalizaciones que no sean de producción ahora utilizarán un proceso de clonación superficial más eficiente durante el paso de compilación, lo que conllevará un tiempo de compilación más rápido para los clientes con repositorios Git especialmente grandes.

* El asistente para agregar Lista de permitidos de IP ahora informará al usuario si se ha alcanzado el número máximo permitido de Listas de permitidos de IP.

* La documentación de la API de Cloud Manager ahora incluye un área de reproducción interactiva que permite a los usuarios que iniciaron sesión experimentar con la API desde su explorador. Consulte [Reproducción de la API de Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/)

* La información del objeto de la tarjeta de programa será más descriptiva si se desactiva una opción de selección en &quot;Navegar a&quot;. Ahora muestra &quot;Un entorno de producción no existe&quot;.

### Corrección de errores {#bug-fixes}

* En raras ocasiones, cuando el personal de un Adobe restauraba el entorno de un cliente, la restauración se consideraba completa antes de que el entorno fuera completamente operativo.

* Algunas solicitudes internas realizadas durante la creación del entorno no se estaban reintentando.

