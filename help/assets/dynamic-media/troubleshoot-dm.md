---
title: Resolución de problemas de Dynamic Media
description: Obtenga información acerca de sugerencias para la resolución de problemas que puede probar al trabajar con imágenes, conjuntos y visores en Dynamic Media.
contentOwner: Rick Brough
feature: Troubleshooting,Image Sets,Viewers
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Resolución de problemas de Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

En el siguiente tema se describe la solución de problemas para Dynamic Media.

## Nueva configuración de Dynamic Media {#new-dm-config}

Ver [Solucionar problemas de una nueva configuración de Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## General (Todos los Assets) {#general-all-assets}

A continuación se ofrecen algunos consejos y trucos generales para todos los recursos.

### Propiedades del estado de sincronización de recursos {#asset-synchronization-status-properties}

Las siguientes propiedades de recursos se pueden revisar en CRXDE Lite para confirmar que la sincronización del recurso de Adobe Experience Manager a Dynamic Media se ha realizado correctamente:

| **Propiedad** | **Ejemplo** | **Descripción** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a\|364266`** | Indicador general de que el nodo está vinculado a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** o texto de error | Estado de carga del recurso en Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Debe rellenarse para generar direcciones URL en el recurso remoto de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **éxito** o **error:`<error text>`** | Estado de sincronización de conjuntos (conjuntos de giros, conjuntos de imágenes, etc.), ajustes preestablecidos de imagen, ajustes preestablecidos de visualizador, actualizaciones de mapa de imagen para un recurso o imágenes que se han editado. |

### Registro de sincronización {#synchronization-logging}

Los errores y problemas de sincronización se registran en `error.log` (directorio de servidor de Experience Manager `/crx-quickstart/logs/`). Hay suficiente registro disponible para determinar la causa raíz de la mayoría de los problemas; sin embargo, puede aumentar el registro en DEPURACIÓN en el paquete `com.adobe.cq.dam.ips` a través de la consola de Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para recopilar más información.

### Control de versión {#version-control}

Al reemplazar un recurso de Dynamic Media existente (mismo nombre y ubicación), puede mantener ambos recursos o reemplazar o crear una versión:

* Al mantener ambos, se crea un recurso con un nombre único para la URL del recurso publicado. Por ejemplo, `image.jpg` es el recurso original y `image1.jpg` es el recurso que se acaba de cargar.

* La creación de una versión no es compatible con Dynamic Media. La nueva versión reemplaza el recurso existente en la entrega.

## Imágenes y conjuntos {#images-and-sets}

Si tiene problemas con imágenes y conjuntos, consulte las siguientes directrices para la resolución de problemas.

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
       <li>Compruebe si se ha definido el ajuste preestablecido en el JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code>. Esta ubicación se aplica si ha actualizado de Experience Manager 6.x a 6.4 y ha excluido la migración. De lo contrario, la ubicación es <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Asegúrese de que el recurso del JCR tiene <code>dam:scene7FileStatus</code><strong> </strong>en Metadatos que se muestra como <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Actualizar página/navegar a otra página y volver (se debe volver a compilar el JSP del carril lateral)</p> <p>Si esto no funciona:</p>
    <ul>
     <li>Publicar recurso.</li>
     <li>Vuelva a cargar el recurso y publíquelo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>El punto interactivo del carrusel se mueve después de cambiar entre diapositivas</td>
   <td><p>Compruebe que todas las diapositivas tienen el mismo tamaño.</p> </td>
   <td><p>Utilice únicamente imágenes con el mismo tamaño para el carrusel.</p> </td>
  </tr>
  <tr>
   <td>La imagen no se previsualiza con el visor de Dynamic Media</td>
   <td><p>Compruebe que el recurso contenga <code>dam:scene7File</code> en las propiedades de metadatos (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>El recurso cargado no se muestra en el selector de recursos</td>
   <td><p>El recurso de comprobación tiene la propiedad <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>El titular de la vista de tarjeta muestra <strong>Nuevo</strong> cuando el recurso no ha comenzado a procesarse</td>
   <td>Comprobar el recurso <code>jcr:content</code> &gt; <code>dam:assetState</code> = si <code>unprocessed</code> no fue recogido por el flujo de trabajo.</td>
   <td>Espere hasta que el flujo de trabajo seleccione el recurso.</td>
  </tr>
  <tr>
   <td>Las imágenes o los conjuntos no muestran la dirección URL del visor ni el código incrustado</td>
   <td>Compruebe si se ha publicado el ajuste preestablecido de visualizador.</td>
   <td><p>Vaya a <strong>Herramientas</strong> &gt; <strong>Assets</strong> &gt; <strong>Ajustes preestablecidos de visor</strong> y publique el ajuste preestablecido de visor.</p> </td>
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
   <td>No se puede previsualizar el vídeo</td>
   <td>
    <ul>
     <li>Compruebe que la carpeta tenga asignado un perfil de vídeo (si el formato de archivo no es compatible). Si no se admite, solo se muestra una imagen.</li>
     <li>El perfil de vídeo debe contener más de un ajuste preestablecido de codificación para generar un conjunto AVS (las codificaciones únicas se tratan como contenido de vídeo para archivos MP4; para archivos no compatibles, se tratan igual que no procesados).</li>
     <li>Compruebe que el vídeo haya finalizado el procesamiento confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Editar perfil de vídeo para incluir más de un ajuste preestablecido de codificación.</li>
     <li>Espere a que el vídeo termine de procesarse.</li>
     <li>Antes de volver a cargar el vídeo, asegúrese de que el flujo de trabajo de codificación de vídeo de Dynamic Media no se esté ejecutando.<br/> </li>
     <li>Vuelva a cargar el vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El vídeo no está codificado</td>
   <td>
    <ul>
     <li>Compruebe si Dynamic Media Cloud Service está configurado.</li>
     <li>Compruebe si un perfil de vídeo está asociado a la carpeta de carga.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Compruebe que la Configuración de Dynamic Media en Cloud Services esté configurada correctamente.</li>
     <li>Compruebe que la carpeta tenga un perfil de vídeo. Además, compruebe el perfil de vídeo.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>El procesamiento de vídeo tarda demasiado</td>
   <td><p>Para determinar si la codificación de vídeo sigue en curso o si ha entrado en un estado de error:</p>
    <ul>
     <li>Comprobar el estado del vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Falta la representación de vídeo</td>
   <td><p>Cuando se carga un vídeo, pero no hay representaciones codificadas:</p>
    <ul>
     <li>Compruebe que la carpeta tenga un perfil de vídeo asignado.</li>
     <li>Compruebe que el vídeo haya finalizado el procesamiento confirmando <code>dam:scene7FileAvs</code> en los metadatos.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Asigne un perfil de vídeo a la carpeta.</li>
     <li>Esperar a que finalice el procesamiento del vídeo.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visores {#viewers}

Si tiene problemas con los visores, consulte las siguientes instrucciones para la resolución de problemas.

### Problema: Los ajustes preestablecidos del visor no se publican {#viewers-not-published}

**Cómo depurar**

1. Continúe con la página de diagnóstico del administrador de muestras: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Observe los valores calculados. Si funciona correctamente, verá lo siguiente: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Puede tardar unos 10 minutos después de la configuración de la nube de Dynamic Media en que los recursos del visualizador se sincronicen.

1. Si quedan recursos no activados, seleccione cualquiera de los **botones Enumerar todos los recursos no activados de Assets** para ver los detalles.

**Solución**

1. Vaya a la lista de ajustes preestablecidos de visor en las herramientas de administración: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Seleccione todos los ajustes preestablecidos de visor y, a continuación, seleccione **Publicar**.
1. Vuelva al administrador de muestras y observe que el recuento de recursos no activados ahora es cero.

### Problema: La ilustración preestablecida del visualizador devuelve 404 desde Vista previa en los detalles del recurso o Copiar URL/Código incrustado {#viewer-preset-404}

**Cómo depurar**

En CRXDE Lite, haga lo siguiente:

1. Vaya a la carpeta `<sync-folder>/_CSS/_OOTB` de la carpeta de sincronización de Dynamic Media (por ejemplo, `/content/dam/_CSS/_OOTB`).
1. Busque el nodo de metadatos del recurso problemático (por ejemplo, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Comprobar la presencia de las propiedades de `dam:scene7*`. Si el recurso se sincronizó y publicó correctamente, verá que el conjunto `dam:scene7FileStatus` se ha establecido en **PublishComplete**.
1. Intente solicitar la ilustración directamente desde Dynamic Media concatenando los valores de las siguientes propiedades y literales de cadena:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Ejemplo: `https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solución**

Si los recursos de muestra o la ilustración preestablecida del visualizador no se han sincronizado o publicado, reinicie todo el proceso de copia o sincronización:

1. Vaya a CRXDE Lite.
1. Eliminar `<sync-folder>/_CSS/_OOTB`.
1. Vaya al Administrador de paquetes de CRX: `https://localhost:4502/crx/packmgr/`.
1. Busque el paquete de visor en la lista; comienza con `cq-dam-scene7-viewers-content`.
1. Seleccione **Reinstalar**.
1. En Cloud Services, vaya a la página Configuración de Dynamic Media y, a continuación, abra el cuadro de diálogo Configuración de Dynamic Media - S7.
1. No realice cambios, seleccione **Guardar**.
Esta acción de guardar vuelve a almacenar en déclencheur la lógica para crear y sincronizar los recursos de muestra, el CSS preestablecido de visualizador y las ilustraciones.

### Problema: La previsualización de imagen no se carga en la creación de ajustes preestablecidos de visualizador {#image-preview-not-loading}

**Solución**

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el carril izquierdo, vaya a la carpeta de contenido de ejemplo en la siguiente ubicación:

   `/content/dam/_DMSAMPLE`

1. Elimine la carpeta `_DMSAMPLE`.
1. En el carril izquierdo, vaya a la carpeta de ajustes preestablecidos en la siguiente ubicación:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Elimine la carpeta `viewer`.
1. Cerca de la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.
1. En la esquina superior izquierda de la página CRXDE Lite, seleccione el icono **Volver a inicio**.
1. Volver a crear una [configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
