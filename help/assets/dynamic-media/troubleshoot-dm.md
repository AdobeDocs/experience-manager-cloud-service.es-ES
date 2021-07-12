---
title: Solución de problemas de Dynamic Media
description: Sugerencias de solución de problemas al usar Dynamic Media.
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 2%

---

# Solución de problemas de Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

En el siguiente tema se describe la solución de problemas para Dynamic Media.

## Nueva configuración de Dynamic Media {#new-dm-config}

Consulte [Solución de problemas de una nueva configuración de Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## General (Todos los recursos) {#general-all-assets}

A continuación se ofrecen algunos consejos y trucos generales para todos los recursos.

### Propiedades del estado de sincronización de recursos {#asset-synchronization-status-properties}

Las siguientes propiedades de recursos se pueden revisar en CRXDE Lite para confirmar que la sincronización del recurso se ha realizado correctamente de Adobe Experience Manager a Dynamic Media:

| **Propiedad** | **Ejemplo** | **Descripción** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador general de que el nodo está vinculado a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublicarCompletar o texto de error | Estado de carga de recursos en Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Debe rellenarse para generar direcciones URL para el recurso remoto de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** el sucesor  **falló:`<error text>`** | Estado de sincronización de conjuntos (conjuntos de giros, conjuntos de imágenes, etc.), ajustes preestablecidos de imagen, ajustes preestablecidos de visor, actualizaciones de mapas de imágenes para un recurso o imágenes editadas. |

### Registro de sincronización {#synchronization-logging}

Los errores y problemas de sincronización se registran en `error.log` (directorio del servidor Experience Manager `/crx-quickstart/logs/`). Hay suficientes registros disponibles para determinar la causa raíz de la mayoría de los problemas, pero puede aumentar el registro en DEBUG en el paquete `com.adobe.cq.dam.ips` a través de la Consola Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para recopilar más información.

### Control de versión {#version-control}

Al reemplazar un recurso de Dynamic Media existente (el mismo nombre y ubicación), puede mantener ambos recursos o reemplazar/crear una versión:

* Al mantener ambos, se crea un recurso con un nombre único para la URL del recurso publicado. Por ejemplo, `image.jpg` es el recurso original y `image1.jpg` es el recurso recién cargado.

* Dynamic Media no admite la creación de una versión. La nueva versión sustituye al recurso existente en la entrega.

## Imágenes y conjuntos {#images-and-sets}

Si tiene problemas con las imágenes y los conjuntos, consulte las siguientes directrices para la resolución de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>No se puede acceder al botón Copiar URL/Incrustar en la vista de detalles del recurso</td>
   <td>
    <ol>
     <li><p>Vaya a CRX/DE:</p>
      <ul>
       <li>Compruebe si el ajuste preestablecido en el JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definido. Esta ubicación se aplica si ha actualizado de Experience Manager 6.x a 6.4 y ha excluido la migración. De lo contrario, la ubicación es <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Compruebe que el recurso en el JCR tenga <code>dam:scene7FileStatus</code><strong> </strong>en Los metadatos se muestran como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualice la página/navegue a otra página y vuelva (el JSP del carril lateral debe volver a compilarse)</p> <p>Si eso no funciona:</p>
    <ul>
     <li>Publicar recurso.</li>
     <li>Vuelva a cargar el recurso y publíquelo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>La zona interactiva de carrusel se desplaza después de cambiar entre diapositivas</td>
   <td><p>Compruebe que todas las diapositivas tengan el mismo tamaño.</p> </td>
   <td><p>Utilice solo imágenes con el mismo tamaño para el carrusel.</p> </td>
  </tr>
  <tr>
   <td>La imagen no se previsualiza con el visor de Dynamic Media</td>
   <td><p>Compruebe que el recurso contiene <code>dam:scene7File</code> en las propiedades de metadatos (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>El recurso cargado no se muestra en el selector de recursos</td>
   <td><p>El recurso de verificación tiene la propiedad <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>El titular de la vista de tarjeta muestra <strong>Nuevo</strong> cuando el recurso no ha empezado a procesarse</td>
   <td>Compruebe el recurso <code>jcr:content</code> &gt; <code>dam:assetState</code> = si <code>unprocessed</code> no lo recogió el flujo de trabajo.</td>
   <td>Espere hasta que el flujo de trabajo recoja el recurso.</td>
  </tr>
  <tr>
   <td>Las imágenes o los conjuntos no muestran la dirección URL del visor ni el código incrustado</td>
   <td>Compruebe si se ha publicado el ajuste preestablecido de visualizador.</td>
   <td><p>Vaya a <strong>Tools</strong> &gt; <strong>Assets</strong> &gt; <strong>Viewer Presets</strong> y publique el ajuste preestablecido de visor.</p> </td>
  </tr>
 </tbody>
</table>

## Vídeo {#video}

Si tiene problemas con el vídeo, consulte las siguientes directrices para la resolución de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>El vídeo no se puede previsualizar</td>
   <td>
    <ul>
     <li>Compruebe que la carpeta tenga un perfil de vídeo asignado (si el formato de archivo no es compatible). Si no es compatible, solo se muestra una imagen.</li>
     <li>El perfil de vídeo debe contener más de un ajuste preestablecido de codificación para generar un conjunto AVS (las codificaciones únicas se tratan como contenido de vídeo para archivos MP4; para los archivos no compatibles, se trata igual que para los no procesados).</li>
     <li>Compruebe que el vídeo haya terminado de procesarse confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta .</li>
     <li>Edite el perfil de vídeo para incluir más de un ajuste preestablecido de codificación.</li>
     <li>Espere a que el vídeo termine de procesarse.</li>
     <li>Antes de volver a cargar el vídeo, asegúrese de que el flujo de trabajo de codificación de vídeo de Dynamic Media no se esté ejecutando.<br/> </li>
     <li>Vuelva a cargar el vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El vídeo no está codificado</td>
   <td>
    <ul>
     <li>Compruebe si el Cloud Service de Dynamic Media está configurado.</li>
     <li>Compruebe si un perfil de vídeo está asociado a la carpeta de carga.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Compruebe que la configuración de Dynamic Media en Cloud Services esté correctamente configurada.</li>
     <li>Compruebe que la carpeta tiene un perfil de vídeo. Compruebe también el perfil de vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El procesamiento de vídeo tarda demasiado tiempo</td>
   <td><p>Para determinar si la codificación de vídeo sigue en curso o si ha entrado en estado de error:</p>
    <ul>
     <li>Compruebe el estado del vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Falta la representación de vídeo</td>
   <td><p>Cuando se carga un vídeo, pero no hay representaciones codificadas:</p>
    <ul>
     <li>Compruebe que la carpeta tenga un perfil de vídeo asignado.</li>
     <li>Compruebe que el vídeo haya terminado de procesarse confirmando <code>dam:scene7FileAvs</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta .</li>
     <li>Espere a que el vídeo termine de procesarse.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visores {#viewers}

Si tiene problemas con los visualizadores, consulte las siguientes directrices para la resolución de problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>Los ajustes preestablecidos de visor no se publican</td>
   <td><p>Continúe con la página de diagnóstico del administrador de muestras: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Observe los valores calculados. Cuando funciona correctamente, verá:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: Los recursos del visor pueden tardar unos 10 minutos en sincronizarse tras la configuración de la nube de Dynamic Media.</p> <p>Si quedan recursos desactivados, haga clic en cualquiera de los botones <strong>List all Unactivate Assets</strong> para ver los detalles.</p> </td>
   <td>
    <ol>
     <li>Vaya a la lista de ajustes preestablecidos de visor en las herramientas de administración: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Seleccione todos los ajustes preestablecidos de visor y haga clic en <strong>Publicar</strong>.</li>
     <li>Vuelva al administrador de muestras y observe que el recuento de recursos no activados es ahora cero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>La ilustración de Ajustes preestablecidos de visor devuelve 404 desde la vista previa en los detalles del recurso o copia de la URL o el código incrustado</td>
   <td><p>En CRXDE Lite, haga lo siguiente:</p>
    <ol>
     <li>Vaya a la carpeta <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> dentro de la carpeta de sincronización de Dynamic Media (por ejemplo, <code>/content/dam/_CSS/_OOTB</code>).</li>
     <li>Busque el nodo de metadatos del recurso problemático (por ejemplo, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Compruebe la presencia de las propiedades <code>dam:scene7*</code>. Si el recurso se sincronizó y publicó correctamente, verá que el <code>dam:scene7FileStatus</code> conjunto es <strong>PublishComplete</strong>.</li>
     <li>Intente solicitar la ilustración directamente desde Dynamic Media concatenando los valores de las siguientes propiedades y literales de cadena
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Ejemplo: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Si la ilustración de ajustes preestablecidos de visor o recursos de muestra no se han sincronizado ni publicado, reinicie todo el proceso de copia y sincronización:</p>
    <ol>
     <li>Ir a <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>Seleccione las siguientes acciones en orden:
      <ol>
       <li>Eliminar carpetas de sincronización.</li>
       <li>Eliminar carpeta de ajustes preestablecidos (debajo de <code>/conf</code>).
       <li>Trabajo asincrónico de configuración de déclencheur DM.</li>
      </ol> </li>
     <li>Espere a que se notifique de la sincronización correcta en la bandeja de entrada del Experience Manager.
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
