---
title: Informe Activación de AEM Assets (Beta)
description: Definiciones para métricas del informe de activación de AEM Assets (Beta) que abarcan activaciones (descargas, recursos compartidos) y distribuciones (Dynamic Media, Sites)".
role: Admin
hide: true
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
source-git-commit: 0b5e61f75a97bd31da034ebf282779a634217366
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---


# Informe Activación de AEM Assets (Beta): Definiciones de métricas

## Explicación de las métricas de rendimiento de los recursos

Cada recurso del sistema de AEM Assets cuenta una historia: desde la carga y la aprobación hasta el momento en que llega a un comprador como imagen de producto, vínculo compartido o banner a pantalla completa. Ese recorrido genera miles de millones de impresiones de marca, y entenderlo es clave para desbloquear el valor de su inversión en activos.

Este artículo desglosa las métricas detrás de ese recorrido, agrupadas por la forma en que los equipos realmente trabajan con los recursos:

- **Activaciones (iniciadas por empleados y socios)**: descargas, recursos compartidos y activaciones entre los AEM Assets (vista de Assets y Content Hub).
- **Distribuciones (externas para usuarios finales)**: entrega al mundo a través de canales como Dynamic Media y AEM Sites.

Juntas, estas métricas conectan la actividad de recursos interna con el alcance y la participación externos, lo que le ayuda a ver cómo las operaciones de contenido se traducen en resultados comerciales reales.

Este es solo el comienzo del recorrido con los AEM Assets, y estas métricas seguirán evolucionando a la vez. Nos encantaría que sus comentarios se utilizaran, por lo que podemos seguir haciendo que este informe sea más útil para usted.

**Nota**: si deseas revisarlos con el equipo de ingeniería/producto de Adobe o deseas recibir comentarios, envía un correo electrónico a `GRP-AEM-DAM-METRICS-BETA@ADOBE.COM`.

| | Métrica | Definición |
|---|---|---|
| **Activaciones** | **Descargas (Vista Assets)** | El número de veces que los recursos se descargan directamente del entorno de AEM Assets principal; por ejemplo, cuando los usuarios internos navegan y descargan archivos a través de la interfaz de vista de Assets. |
| | **Recursos compartidos (vista Assets)** | El número de recursos compartidos (a través de vínculos que se pueden compartir) desde la vista AEM Assets para proporcionar a los usuarios externos o no autenticados acceso directo a recursos, carpetas o colecciones específicos sin necesidad de iniciar sesión. |
| | **Descargas (Content Hub)** | El número de veces que los usuarios descargan los recursos a través de Content Hub, la interfaz de usuario de autoservicio que permite a equipos más amplios examinar y descargar recursos aprobados y listos para su marca. |
| | **Recursos compartidos (Content Hub)** | El número de recursos compartidos (a través de vínculos compartibles generados) desde Content Hub para proporcionar a otros usuarios acceso directo a los recursos o colecciones seleccionados. |
| | **Activar en Content Hub** | Acción de aprobar o publicar un recurso de los AEM Assets para que esté disponible para los usuarios finales en Content Hub. En Content Hub solo aparecen los recursos aprobados. |
| | **Activar en Dynamic Media** | Acción de publicar un recurso de AEM Assets en el servicio de Dynamic Media, lo que permite procesarlo en representaciones y entregarlo en tiempo real mediante la canalización de imágenes/vídeo y la CDN de Dynamic Media. |
| **Distribuciones** | **Solicitudes de entrega de Dynamic Media** | Número total de veces que se solicitó un recurso y se entregó en todos los canales a través de Dynamic Media. |
| | **Assets exclusivo de medios dinámicos servido** | El número de recursos distintos que se entregaron al menos una vez mediante Dynamic Media en un período determinado, contabilizados una vez por recurso independientemente de cuántas veces se solicitaron o de cuántas representaciones diferentes se ofrecieron. |
| | **Transformaciones únicas de Dynamic Media** | La cantidad de variaciones distintas de los recursos que se entregaron a través de Dynamic Media en un período determinado. Esto muestra cómo el contenido se adapta entre dispositivos, tamaños de pantalla y casos de uso. |
| | **Publicar en sitios** | La acción de publicar un recurso desde AEM Assets para que esté disponible para su uso en páginas de AEM Sites activas. |



