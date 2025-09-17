---
title: Solución de problemas en AEM Assets y Forms
description: Solucione problemas comunes de AEM Assets y Forms mediante los vínculos del artículo para áreas clave, como cargas, metadatos, búsqueda, entrega, creación de formularios, envío e integración.
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# Solución de problemas de AEM Assets y Forms {#troubleshoot-aem-assets-forms}

AEM as a Cloud Service ofrece soluciones completas para la administración de activos digitales a través de AEM Assets y potentes funciones de creación de formularios a través de AEM Forms. Ambos servicios proporcionan soluciones PaaS nativas en la nube con funciones inteligentes de próxima generación, como IA/ML, todo ello dentro de un sistema que siempre está actualizado, disponible y aprendiendo.

Sin embargo, los entornos empresariales complejos pueden encontrar varios desafíos técnicos en diferentes áreas.

Esta completa guía de solución de problemas proporciona enfoques de diagnóstico sistemáticos, soluciones por categorías y rutas de resolución paso a paso tanto para AEM Assets como para Forms. Cada sección incluye guías de referencia rápida, metodologías detalladas de solución de problemas y amplios vínculos a recursos para ayudarle a resolver problemas de forma eficaz y optimizar su entorno de AEM Cloud Service.

## Solución de problemas de AEM Assets {#aem-assets-troubleshooting}

AEM Assets optimiza la forma en que se administran, organizan y entregan los recursos digitales a través de las experiencias. Sin embargo, pueden surgir problemas que afecten a las cargas de recursos, los metadatos, las integraciones o la entrega. Este artículo proporciona pasos de solución de problemas para ayudarle a diagnosticar y resolver problemas comunes de los AEM Assets. Al seguir las directrices que se indican a continuación, puede restaurar los flujos de trabajo de forma eficaz y garantizar que los recursos sigan siendo accesibles, precisos y estén listos para su uso en todos los canales.

### Procesamiento y representaciones de recursos {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Carga y procesamiento</strong></td>
    <td><strong>Representaciones</strong></td>
    <td><strong>PDF y extracción de texto</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26610">Error al procesar recursos para archivos MP4 grandes en AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26639">Las representaciones DAM no coinciden con los archivos originales</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM trunca el texto extraído de archivos PDF grandes después de 100 000 tokens</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-23916">El archivo Tiff con cargas de compresión ZIP no genera representaciones</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26233">Las imágenes no muestran representaciones de miniaturas en AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitaciones de extracción de texto para PDF grandes en AEM as a Cloud Service</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-21865">Error al arrastrar y soltar una carpeta de recursos en la interfaz de usuario web de AEM Assets</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26528">El problema de rotación de recursos hace que las rotaciones subsiguientes sean invisibles</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento del límite de carga de recursos de una sola parte para la integración de API de Photoshop Firefly</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Vídeo</strong></td>
    <td><strong>Conjuntos de giros y recorte inteligente</strong></td>
    <td><strong>Entrega y configuración</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26533">Corrección de problemas de carga, procesamiento y procesamiento de vídeo en AEM</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26715">Conjuntos de giros atascados en estado de procesamiento</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-17628">Cambiar la URL de Dynamic Media para los recursos</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26677">No coinciden las miniaturas de vídeo entre Dynamic Media y la vista de tarjeta DAM</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26873">Representaciones de recortes inteligentes no generadas en AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26367">Problema de imagen dañada con el recorte inteligente en AEM 6.5</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26610">Error de procesamiento de recursos en AEM Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26637">Problema de color de fondo para representaciones de TIFF</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25294">La página Configuración general de Dynamic Media no se abre</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26197">Resolución de problemas de audio en archivos de vídeo con Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25885">Error de sincronización de recursos en Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26461">Resolver discrepancias de nombres de recursos entre entornos</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26871">El reproductor de vídeo Dynamic Media no funciona en entornos más bajos</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25471">Recomendaciones de usuario de sincronización de Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26902">Exportación de recursos y metadatos desde Dynamic Media mediante API</a></td>
  </tr>
  </tbody>
</table>

### Metadatos, etiquetado y uso compartido {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Metadatos</strong></td>
    <td><strong>Etiquetas inteligentes</strong></td>
    <td><strong>Acceso y uso compartido</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepancia de metadatos de imagen en AEM Assets</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25925">Etiquetado automático de recursos recién cargados</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26928">Comentarios restringidos en la vista de Assets a pesar del acceso de lectura</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26655">Resolución de problemas de visibilidad del esquema de metadatos para usuarios no administradores</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25889">Las etiquetas inteligentes no funcionan después de la migración de JWT a OAuth</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25903">Resolución de problemas de vínculos compartidos en AEM Managed Services</a></td>
  </tr>

</tbody>
</table>

### Integraciones y acceso {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>Licencias y personalizaciones</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset Link deja los vínculos inaccesibles en InDesign</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26616">Fragmentos de contenido no incluidos en la licencia para AEM Assets</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25562">Solución de problemas de conexión de AEM Asset Link en InDesign</a></td>
      <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25525">Resolución de problemas de procesamiento de recursos en AEM as a Cloud Service</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25506">Error de red del complemento Adobe Asset Link: Servidor inaccesible</a></td>
      <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-25829">Actualizando miniaturas personalizadas para recursos de vídeo en AEM as a Cloud Service</a>
      </td>
    </tr>
  </tbody>
</table>




## Solución de problemas de AEM Forms {#aem-forms-troubleshooting}

AEM Forms as a Cloud Service ofrece potentes funciones de creación y administración de formularios. Sin embargo, puede encontrar problemas durante los procesos de instalación, configuración, creación de formularios o envío. En esta sección se proporcionan instrucciones completas para la resolución de problemas en problemas comunes de AEM Forms.

### Problemas de instalación y configuración

<table>
  <tbody>
  <tr>
    <td><strong>Configuración y configuración</strong></td>
    <td><strong>Problemas de creación de formularios</strong></td>
    <td><strong>Rendimiento y almacenamiento en caché</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Opción Forms no disponible en navegación</a></td>
    <td><a href="/help/forms/form-creation-failing.md">La creación del formulario falla tras la publicación de la plantilla</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">Problemas de almacenamiento en caché de Forms adaptable</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">Errores de canalización de compilación</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">Problemas de secuencia de publicación de plantilla</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Problemas de invalidación de caché de Dispatcher</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">Problemas de activación del paquete</a></td>
    <td><a href="/help/forms/known-issues.md">Limitaciones de creación de formularios conocidas</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">Errores de almacenamiento en caché de CDN</a></td>
  </tr>
  </tbody>
</table>

### Problemas de envío e integración de formularios

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>Acciones de envío personalizadas</strong></td>
    <td><strong>Problemas de integración</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 Errores prohibidos en el envío de formularios</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">Errores 502 en las acciones de envío personalizadas</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-27434">Errores de redirección de DRM-SAML</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">Problemas de configuración de CORS</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">Control de excepciones no controlado</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-27075">Botón Enviar desactivado en AEM Sites</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">Configuración del filtro de referente</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">Prácticas recomendadas para acciones personalizadas</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26532">Visibilidad de campos ocultos tras las actualizaciones</a></td>
  </tr>
  </tbody>
</table>

### Designer y problemas de desarrollo

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>Entorno de desarrollo</strong></td>
    <td><strong>Versión y compatibilidad</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26558">Designer 6.5 no se abre después de la actualización</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-27089">Los localizadores no pueden iniciarse con JDK 8/11</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26862">Problemas de visualización de la versión del paquete de AEM Forms (AEMFD)</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-21018">Errores de PDF Generator JPEG 2000</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-22689">Configuración de ruta de registro JBoss</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-26846">Números de versión incorrectos en Windows</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-27406">Falta un botón en la salida de PDF</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-18084">Errores de actualización del Administrador de configuración</a></td>
    <td><a href="https://experienceleague.adobe.com/es/docs/experience-cloud-kcs/kbarticles/ka-17339">Soluciones alternativas para la corrupción de índices</a></td>
  </tr>
  </tbody>
</table>



