---
title: Solución de problemas en AEM Assets
description: Solucione problemas comunes de los AEM Assets con los vínculos del artículo para áreas clave s=s de los AEM Assets, como cargas, metadatos, búsquedas, envíos, etc.
hidefromtoc: true
hide: true
source-git-commit: 60667c265cf480521fe0c0d646c2665540f110d0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# Solución de problemas en AEM Assets {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service ofrece una solución PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y medios dinámicos, sino que también utilicen funciones inteligentes de próxima generación, como IA y aprendizaje automático. Todo desde un sistema que siempre está actualizado, siempre disponible y aprendiendo.

Sin embargo, pueden surgir problemas que afecten a las cargas de recursos, los metadatos, la búsqueda o la entrega, y otras áreas clave de los AEM Assets. Este artículo proporciona pasos de solución de problemas para ayudarle a diagnosticar y resolver estos problemas comunes de los AEM Assets.

<table>
  <tbody>
  <tr>
    <td>Faltan <a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">representaciones en el archivo ZIP de descarga de recursos en AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">Fragmentos de contenido no incluidos en la licencia para AEM Assets</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">Comentarios restringidos en la vista de Assets a pesar del acceso de lectura</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715"> (Dynamic Media) Conjuntos de giros atascados en el estado de procesamiento en AEM Dynamic Media</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">Las representaciones de administración de activos digitales (DAM) no coinciden con los archivos originales en AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">No se han generado representaciones de recorte inteligente en AEMaaCS</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamic Media) Solucionar problemas de carga, procesamiento y procesamiento de vídeo en AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">(Asset Link) Adobe Asset Link deja los vínculos en un estado inaccesible al usar InDesign</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">No coinciden las miniaturas de vídeo entre Dynamic Media y la vista de tarjeta DAM en AEMaaCS</a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">Error al procesar recursos para archivos MP4 grandes en AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) El reproductor de vídeo de Dynamic Media no funciona en entornos más bajos</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">(Dynamic Media con OpenAPI) Active el acceso restringido de Assets a Dynamic Media con las API abiertas en función de los grupos de usuarios de IMS</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">Cuando se carga un archivo Tiff con formato de compresión ZIP en AEM Assets, no se generan representaciones</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM trunca el texto extraído de archivos PDF grandes después de 100 000 tokens</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media) Cambio de la URL de Dynamic Media para DM Assets</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">Resolución de problemas de visibilidad del esquema de metadatos para usuarios no administradores en AEMaaCS</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Problema de cambio de color de fondo para representaciones de imágenes de TIFF en Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">El problema de rotación de recursos AEMaaCS hace que las rotaciones posteriores sean invisibles</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media) Solución de un problema de imagen dañada con el recorte inteligente en Dynamic Media de Adobe Experience Manager 6.5</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">Aumento del límite de carga de recursos de una sola parte para la integración de API de Photoshop Firefly</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media) Resuelva las discrepancias de nombres de recursos de Dynamic Media en los entornos de AEM para archivos de PDF</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Algunas imágenes no muestran representaciones de miniaturas en Adobe Experience Manager (AEM) as a Cloud Service - Recurso</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media) La página Configuración general de Dynamic Media no se abre</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media) Resuelva problemas de audio en archivos de vídeo con Dynamic Media en AEM</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">Etiquetado automático de los recursos recién cargados en AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">La funcionalidad Etiquetas inteligentes no funciona después de la migración de JWT a OAuth en AEM</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">Resolución de problemas de vínculos compartidos en AEM Managed Services</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) Error de procesamiento de recursos en AEM Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Error de sincronización de recursos en Adobe Experience Manager (AEM) Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">Actualizar miniaturas personalizadas para recursos de vídeo en AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Discrepancia de metadatos de imagen en Adobe Experience Manager (AEM) Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">Error al arrastrar y soltar una carpeta de recursos en la interfaz de usuario web de AEM Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media) Resolución de problemas de procesamiento de recursos en AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Limitaciones de extracción de texto para PDF grandes en Adobe Experience Manager as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">(Asset Link) Resolución de problemas de conexión de Asset Link de Adobe Experience Manager (AEM) en InDesign</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">(Asset Link) Error de red del complemento Adobe Asset Link: No se puede acceder al servidor</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">(Dynamic Media) Recomendaciones de usuario de sincronización de Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media) Exportar recursos y metadatos de Dynamic Media mediante API</a></td>
  <td></td>
</tr>

</tbody>
  <table>


