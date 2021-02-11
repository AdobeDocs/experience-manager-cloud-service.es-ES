---
title: Solución de problemas de Dynamic Media
description: Sugerencias para la resolución de problemas al usar Dynamic Media.
translation-type: tm+mt
source-git-commit: fd75af0bf0c16e20c3b98703af14f329ea6c6371
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 2%

---


# Solución de problemas de Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

En el siguiente tema se describe la solución de problemas de Dynamic Media.

## Nueva configuración de Dynamic Media {#new-dm-config}

Consulte [Solución de problemas de una nueva configuración de Dynamic Media.](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)

## General (Todos los recursos) {#general-all-assets}

Los siguientes son algunos trucos y sugerencias generales para todos los recursos.

### Propiedades de estado de sincronización de recursos {#asset-synchronization-status-properties}

Las siguientes propiedades de recurso se pueden revisar en CRXDE Lite para confirmar que la sincronización del recurso se ha realizado correctamente de AEM a Dynamic Media:

| **Propiedad** | **Ejemplo** | **Descripción** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador general de que el nodo está vinculado a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** PublicarCompletar o texto de error | Estado de la carga de recursos a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Debe rellenarse para poder generar direcciones URL para el recurso remoto de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** sucesor  **fallido:`<error text>`** | Estado de sincronización de conjuntos (conjuntos de giros, conjuntos de imágenes, etc.), ajustes preestablecidos de imagen, ajustes preestablecidos de visor, actualizaciones de mapas de imagen para un recurso o imágenes editadas. |

### Registro de sincronización {#synchronization-logging}

Los errores y problemas de sincronización se registran en `error.log` (directorio de servidor AEM `/crx-quickstart/logs/`). Hay suficiente registro para determinar la causa raíz de la mayoría de los problemas, pero puede aumentar el registro en DEBUG en el paquete `com.adobe.cq.dam.ips` a través de la Consola de Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para recopilar más información.

### Control de versión {#version-control}

Al reemplazar un recurso de Dynamic Media existente (el mismo nombre y la misma ubicación), tiene la opción de conservar ambos recursos o de reemplazar o crear una versión:

* Al mantener ambos, se creará un nuevo recurso con un nombre único para la URL del recurso publicado. Por ejemplo, `image.jpg` es el recurso original y `image1.jpg` es el recurso recién cargado.

* La creación de una versión no es compatible con Dynamic Media. La nueva versión reemplazará al recurso existente en envío.

## Imágenes y conjuntos {#images-and-sets}

Si tiene problemas con las imágenes y los conjuntos, consulte las siguientes instrucciones para solucionar problemas.

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
       <li>Compruebe si el ajuste preestablecido en el JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definido. Tenga en cuenta que esta ubicación se aplica si ha actualizado de AEM 6.x a 6.4 y ha exclusión la migración. De lo contrario, la ubicación es <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Compruebe que el recurso del JCR tenga <code>dam:scene7FileStatus</code><strong> </strong>en Metadatos se muestra como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualice la página/navegue a otra página y regrese (es necesario volver a compilar JSP del carril lateral)</p> <p>Si eso no funciona:</p>
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
   <td>La imagen no se previsualización con el visor de Dynamic Media</td>
   <td><p>Compruebe que el recurso contiene <code>dam:scene7File</code> en las propiedades de metadatos (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos han terminado de procesarse.</p> </td>
  </tr>
  <tr>
   <td>El recurso cargado no se muestra en el selector de recursos</td>
   <td><p>El recurso de verificación tiene la propiedad <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos han terminado de procesarse.</p> </td>
  </tr>
  <tr>
   <td>La vista de pancarta de la tarjeta muestra <strong>Nuevo</strong> cuando el recurso no ha comenzado a procesarse</td>
   <td>Compruebe que el recurso <code>jcr:content</code> &gt; <code>dam:assetState</code> = si <code>unprocessed</code> no lo recogió el flujo de trabajo.</td>
   <td>Espere hasta que el flujo de trabajo recoja el recurso.</td>
  </tr>
  <tr>
   <td>Las imágenes o los conjuntos no muestran la dirección URL del visor ni el código incrustado</td>
   <td>Compruebe si se ha publicado el ajuste preestablecido de visor.</td>
   <td><p>Vaya a <strong>Herramientas</strong> &gt; <strong>Recursos</strong> &gt; <strong>Ajustes preestablecidos de visor</strong> y publique el ajuste preestablecido de visor.</p> </td>
  </tr>
 </tbody>
</table>

## Vídeo {#video}

Si tiene problemas con el vídeo, consulte las siguientes instrucciones para solucionar problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>No se puede previsualizar el vídeo</td>
   <td>
    <ul>
     <li>Compruebe que la carpeta tiene un perfil de vídeo asignado a ella (si el formato de archivo no es compatible). Si no se admite, solo se muestra una imagen.</li>
     <li>El perfil de vídeo debe contener más de un ajuste preestablecido de codificación para generar un conjunto AVS (las codificaciones únicas se tratan como contenido de vídeo para archivos MP4; para los archivos no admitidos, se trata igual que los archivos no procesados).</li>
     <li>Compruebe que el vídeo ha terminado de procesarse confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Edite el perfil de vídeo para incluir más de un ajuste preestablecido de codificación.</li>
     <li>Espere a que el vídeo termine de procesarse.</li>
     <li>Para volver a cargar el vídeo, asegúrese de que el flujo de trabajo de Dynamic Media Encode Video no se está ejecutando.<br/> </li>
     <li>Vuelva a cargar el vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El vídeo no está codificado</td>
   <td>
    <ul>
     <li>Compruebe si el servicio en la nube de Dynamic Media está configurado.</li>
     <li>Compruebe si un perfil de vídeo está asociado a la carpeta de carga.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Compruebe que la configuración de Dynamic Media en Cloud Services está correctamente configurada.</li>
     <li>Compruebe que la carpeta tiene un perfil de vídeo. Además, compruebe el perfil del vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El procesamiento de vídeo tarda demasiado</td>
   <td><p>Para determinar si la codificación de vídeo sigue en curso o si ha entrado en un estado de error:</p>
    <ul>
     <li>Compruebe el estado del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Falta la representación de vídeo</td>
   <td><p>Cuando se carga el vídeo, pero no hay representaciones codificadas:</p>
    <ul>
     <li>Compruebe que la carpeta tiene un perfil de vídeo asignado.</li>
     <li>Compruebe que el vídeo ha terminado de procesarse confirmando <code>dam:scene7FileAvs</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Espere a que el vídeo termine de procesarse.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visores {#viewers}

Si tiene problemas con los visores, consulte las siguientes instrucciones para solucionar problemas.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Cómo depurar</strong></td>
   <td><strong>Solución</strong></td>
  </tr>
  <tr>
   <td>Los ajustes preestablecidos de visor no se publican</td>
   <td><p>Vaya a la página de diagnóstico del administrador de muestra: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Observe los valores calculados. Cuando funcione correctamente, debería ver:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: Los recursos del visor pueden tardar unos 10 minutos en sincronizarse tras la configuración de la nube de Dynamic Media.</p> <p>Si los recursos inactivados permanecen, haga clic en cualquiera de los botones <strong>Lista de todos los recursos inactivados</strong> para ver los detalles.</p> </td>
   <td>
    <ol>
     <li>Vaya a la lista de ajustes preestablecidos de visor en las herramientas de administración: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Seleccione todos los ajustes preestablecidos de visor y haga clic en <strong>Publicar</strong>.</li>
     <li>Vuelva al administrador de muestra y observe que el recuento de recursos no activado es ahora cero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>La ilustración de Ajustes preestablecidos de visor devuelve 404 desde la previsualización en los detalles del recurso o desde la URL de copia o el código incrustado</td>
   <td><p>En CRXDE Lite, haga lo siguiente:</p>
    <ol>
     <li>Vaya a la carpeta <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> de la carpeta de sincronización de Dynamic Media (por ejemplo, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Busque el nodo de metadatos del recurso problemático (por ejemplo, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Compruebe la presencia de propiedades <code>dam:scene7*</code>. Si el recurso se sincronizó y publicó correctamente, verá que el <code>dam:scene7FileStatus</code> conjunto es <strong>PublishComplete</strong>.</li>
     <li>Intente solicitar la ilustración directamente desde Dynamic Media concatenando los valores de las siguientes propiedades y literales de cadena
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Ejemplo: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Si los recursos de muestra o la ilustración de ajustes preestablecidos de visor no se han sincronizado o publicado, reinicie todo el proceso de copia/sincronización:</p>
    <ol>
     <li>Ir a <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>Seleccione las siguientes acciones en orden:
      <ol>
       <li>Eliminar carpetas de sincronización.</li>
       <li>Eliminar carpeta de ajustes preestablecidos (debajo de <code>/conf</code>).
       <li>Trabajo asincrónico de la configuración de déclencheur DM.</li>
      </ol> </li>
     <li>Espere a que se notifique la sincronización correcta en la Bandeja de entrada de AEM.
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

