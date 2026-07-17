---
title: Informe Activación de AEM Assets (Beta)
description: Definiciones para métricas del informe de activación de AEM Assets (Beta) que abarcan activaciones (descargas, recursos compartidos) y distribuciones (Dynamic Media, Sites)".
role: Admin
hide: true
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
source-git-commit: add9db9da22478bfce625bc43e4c1cf6132fe2c1
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# AEM Asset Insights (Beta): Métricas explicadas {#aem-asset-insights-beta-metrics-explained}


## ¿Qué es Asset Insights? {#what-is-asset-insights}

Asset Insights muestra cómo su equipo utiliza los recursos y dónde llegan a los clientes, desde la carga y la aprobación hasta el momento en que un recurso aparece como una imagen de producto, un vínculo compartido o un banner a pantalla completa. Conecta lo que sucede dentro de su equipo con el alcance que su contenido gana fuera de él.

**Las métricas se agrupan en torno a dos preguntas:**

- ¿Cómo trabaja su equipo con los recursos? — buscar y compartir, aprobar la publicación y actuar según las directrices de IA.
- ¿Dónde llegan esos activos a los clientes? : donde los recursos se muestran en experiencias en directo, entregados a través de Dynamic Media y AEM Sites.

<a id="quick-reference"></a>

<table>
  <thead>
    <tr>
      <th>Sección</th>
      <th>Métrica</th>
      <th>Lo que cuenta</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="7"><strong>Actividad de equipo</strong></td>
      <td><strong>Descargas (vista de Assets)</strong></td>
      <td>Assets descargado directamente de los AEM Assets principales</td>
    </tr>
    <tr>
      <td><strong>Recursos compartidos (vista Assets)</strong></td>
      <td>Vínculos compartidos creados en la vista Assets</td>
    </tr>
    <tr>
      <td><strong>Descargas (Content Hub)</strong></td>
      <td>Assets descargado a través de Content Hub</td>
    </tr>
    <tr>
      <td><strong>Recursos compartidos (Content Hub)</strong></td>
      <td>Vínculos compartidos creados en Content Hub</td>
    </tr>
    <tr>
      <td><strong>Aprobar en Content Hub</strong></td>
      <td>Assets aprobado y publicado en Content Hub</td>
    </tr>
    <tr>
      <td><strong>Activar en Dynamic Media</strong></td>
      <td>Assets publicado en Dynamic Media</td>
    </tr>
    <tr>
      <td><strong>Asesor de contenido</strong></td>
      <td>Recomendaciones de IA cumplidas</td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Contacto con el cliente</strong></td>
      <td><strong>Solicitudes de envío de Dynamic Media</strong></td>
      <td>Total de envíos de recursos en todos los canales</td>
    </tr>
    <tr>
      <td><strong>Assets exclusivo de Dynamic Media servido</strong></td>
      <td>Recursos distintos entregados al menos una vez</td>
    </tr>
    <tr>
      <td><strong>Transformaciones únicas de Dynamic Media</strong></td>
      <td>Variaciones de recursos distintas entregadas</td>
    </tr>
    <tr>
      <td><strong>Distribución de AEM Sites</strong> <em>(próximamente)</em></td>
      <td>Assets publicado en páginas de AEM Sites activas</td>
    </tr>
  </tbody>
</table>

## ¿Cómo trabaja su equipo con los recursos? {#how-is-your-team-working-with-assets}


### Búsqueda y uso compartido {#finding--sharing}

- **Descargas (vista de Assets)**: las veces que los recursos se descargan directamente del entorno de AEM Assets principales.
- **Recursos compartidos (vista de Assets)**: vínculos que se pueden compartir creados en la vista de Assets, que proporcionan a los usuarios externos o no autenticados acceso sin iniciar sesión.
- **Descargas (Content Hub)**: las veces que los recursos se descargan a través de Content Hub, el espacio de autoservicio donde equipos más amplios obtienen recursos aprobados y listos para usar su marca.
- **Recursos compartidos (Content Hub)**: vínculos que se pueden compartir creados en Content Hub para que otros usuarios tengan acceso a los recursos o colecciones seleccionados.

Dividir las descargas y los recursos compartidos por fuente muestra si la actividad procede de las operaciones creativas principales (vista de Assets) o de la organización en general mediante recursos aprobados (Content Hub): dos señales diferentes sobre cómo se propaga el contenido.

## Aprobación para publicar {#approving-to-publish}

- **Aprobar en Content Hub**: aprueba un recurso de los AEM Assets para que esté disponible para los usuarios finales en Content Hub. Aquí solo aparecen los recursos aprobados.
- **Activar en Dynamic Media**: Publicación de un recurso en Dynamic Media para que se pueda procesar y entregar en representaciones en tiempo real.

Ambos son pasos de publicación en diferentes destinos. La aprobación en Content Hub hace que las personas puedan examinar y descargar un recurso; la activación en Dynamic Media lo pone en la canalización que sirve para las experiencias de los clientes en directo.

### Obtener orientación sobre IA {#getting-ai-guidance}

- **Asesor de contenido**: El número de recomendaciones generadas por IA en las que actuó su equipo.

Un número bajo no es un problema; solo significa que hay espacio para apoyarse más en estas sugerencias a medida que avanza. Es una señal de oportunidad, no una advertencia.

## ¿Dónde llegan esos activos a los clientes? {#where-are-those-assets-reaching-customers}

- **Solicitudes de entrega de Dynamic Media**: El número total de veces que se solicitó y entregó un recurso en todos los canales a través de Dynamic Media. Su volumen total de envío.
- **Servicio único de Assets de Dynamic Media**: Recursos distintos entregados al menos una vez durante el período, contabilizados una vez cada uno independientemente de solicitudes o representaciones.
- **Transformaciones únicas de Dynamic Media**: variaciones distintas de los recursos que se entregaron en el período, que muestran cómo se adapta el contenido entre dispositivos, pantallas y casos de uso.
- **Distribución de AEM Sites** *(próximamente)*: Assets publicado desde AEM Assets a páginas de AEM Sites activas y que llegará a los clientes de su sitio web.

Estas tres responden a preguntas diferentes acerca de la misma actividad. Las solicitudes de entrega son un volumen sin procesar; Unique Assets Served es una amplitud (la cantidad de su biblioteca que está en uso); Unique Transformations es adaptabilidad. Un recuento de solicitudes alto con pocos recursos únicos significa que un conjunto pequeño está haciendo un trabajo pesado.

### Asset Insights sigue evolucionando {#asset-insights-is-still-evolving}

Estas métricas seguirán creciendo a la par que su uso de AEM Assets. Nos encantaría recibir sus comentarios a medida que los ponga a trabajar.

**Preguntas o comentarios?** Envíe un correo electrónico a [GRP-AEM-DAM-METRICS-BETA@ADOBE.COM](mailto:GRP-AEM-DAM-METRICS-BETA@ADOBE.COM) para comunicarse con el equipo de ingeniería y productos de Adobe.

