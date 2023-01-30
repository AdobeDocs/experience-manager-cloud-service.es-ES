---
title: Resolución de problemas de Dynamic Media
description: Sugerencias de solución de problemas al usar Dynamic Media.
contentOwner: Rick Brough
role: Admin,User
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 1%

---

# Resolución de problemas de Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

En el siguiente tema se describe la solución de problemas para Dynamic Media.

## Nueva configuración de Dynamic Media {#new-dm-config}

Consulte [Resolución de problemas de una nueva configuración de Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## General (Todos los recursos) {#general-all-assets}

A continuación se ofrecen algunos consejos y trucos generales para todos los recursos.

### Propiedades del estado de sincronización de recursos {#asset-synchronization-status-properties}

Las siguientes propiedades de recursos se pueden revisar en CRXDE Lite para confirmar que la sincronización del recurso se ha realizado correctamente de Adobe Experience Manager a Dynamic Media:

| **Propiedad** | **Ejemplo** | **Descripción** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicador general de que el nodo está vinculado a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** o texto de error | Estado de carga de recursos en Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Debe rellenarse para generar direcciones URL para el recurso remoto de Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **success** o **error:`<error text>`** | Estado de sincronización de conjuntos (conjuntos de giros, conjuntos de imágenes, etc.), ajustes preestablecidos de imagen, ajustes preestablecidos de visor, actualizaciones de mapas de imágenes para un recurso o imágenes editadas. |

### Registro de sincronización {#synchronization-logging}

Los errores y problemas de sincronización se registran en `error.log` (directorio del servidor del Experience Manager) `/crx-quickstart/logs/`). Hay suficientes registros disponibles para determinar la causa principal de la mayoría de los problemas, pero puede aumentar el registro para depurar en la variable `com.adobe.cq.dam.ips` a través de la consola de Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) para recopilar más información.

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
       <li>Compruebe si el ajuste preestablecido en el JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definida. Esta ubicación se aplica si ha actualizado de Experience Manager 6.x a 6.4 y ha excluido la migración. De lo contrario, la ubicación es <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Compruebe que el recurso en el JCR tenga <code>dam:scene7FileStatus</code><strong> </strong>en Metadatos se muestra como <code>PublishComplete</code>.</li>
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
   <td><p>Comprobar que el recurso contiene <code>dam:scene7File</code> en las propiedades de metadatos (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>El recurso cargado no se muestra en el selector de recursos</td>
   <td><p>Comprobar que el recurso tiene propiedad <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Compruebe que todos los recursos hayan finalizado el procesamiento.</p> </td>
  </tr>
  <tr>
   <td>Banner en los programas de vista de tarjeta <strong>Nuevo</strong> cuando el recurso no ha empezado a procesarse</td>
   <td>Comprobar recurso <code>jcr:content</code> &gt; <code>dam:assetState</code> = if <code>unprocessed</code> el flujo de trabajo no lo recogió.</td>
   <td>Espere hasta que el flujo de trabajo recoja el recurso.</td>
  </tr>
  <tr>
   <td>Las imágenes o los conjuntos no muestran la dirección URL del visor ni el código incrustado</td>
   <td>Compruebe si se ha publicado el ajuste preestablecido de visualizador.</td>
   <td><p>Vaya a <strong>Herramientas</strong> &gt; <strong>Recursos</strong> &gt; <strong>Ajustes preestablecidos de visor</strong> y publicar el ajuste preestablecido de visualizador.</p> </td>
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
     <li>Compruebe que el vídeo ha finalizado el procesamiento confirmando <code>dam:scene7FileAvs</code> de <code>dam:scene7File</code> en los metadatos.</li>
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
     <li>Comprobar el estado del vídeo <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Falta la representación de vídeo</td>
   <td><p>Cuando se carga un vídeo, pero no hay representaciones codificadas:</p>
    <ul>
     <li>Compruebe que la carpeta tenga un perfil de vídeo asignado.</li>
     <li>Compruebe que el vídeo ha finalizado el procesamiento confirmando <code>dam:scene7FileAvs</code> en los metadatos.</li>
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

### Problema: Los ajustes preestablecidos de visor no se publican {#viewers-not-published}

**Cómo depurar**

1. Continúe con la página de diagnóstico del administrador de muestras: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`.
1. Observe los valores calculados. Cuando funciona correctamente, puede ver lo siguiente: `_DMSAMPLE status: 0 unsyced assets - activation not necessary _OOTB status: 0 unsyced assets - 0 unactivated assets`.

   >[!NOTE]
   >
   >Los recursos del visor pueden tardar unos 10 minutos en sincronizarse tras la configuración de la nube de Dynamic Media.

1. Si los recursos desactivados permanecen, seleccione cualquiera de los **Lista de todos los recursos no activados** para ver los detalles.

**Solución**

1. Vaya a la lista de ajustes preestablecidos de visor en las herramientas de administración: `https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html`
1. Seleccione todos los ajustes preestablecidos de visor y, a continuación, seleccione **Publicación**.
1. Vuelva al administrador de muestras y observe que el recuento de recursos no activados es ahora cero.

### Problema: La ilustración preestablecida del visor devuelve 404 desde Vista previa en los detalles del recurso o Copiar URL/Código incrustado {#viewer-preset-404}

**Cómo depurar**

En CRXDE Lite, haga lo siguiente:

1. Vaya a `<sync-folder>/_CSS/_OOTB` carpeta dentro de la carpeta de sincronización de Dynamic Media (por ejemplo, `/content/dam/_CSS/_OOTB`).
1. Busque el nodo de metadatos del recurso problemático (por ejemplo, `<sync-folder>/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/`).
1. Compruebe la presencia de `dam:scene7*` propiedades. Si el recurso se sincronizó y publicó correctamente, verá la variable `dam:scene7FileStatus` está configurado para **PublishComplete**.
1. Intente solicitar la ilustración directamente desde Dynamic Media concatenando los valores de las siguientes propiedades y literales de cadena:

   * `dam:scene7Domain`
   * `"is/content"`
   * `dam:scene7Folder`
   * `<asset-name>`
Ejemplo: 
`https://<server>/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png`

**Solución**

Si la ilustración de ajustes preestablecidos de visor o recursos de muestra no se han sincronizado ni publicado, reinicie todo el proceso de copia y sincronización:

1. Vaya al CRXDE Lite.
1. Eliminar `<sync-folder>/_CSS/_OOTB`.
1. Vaya al Administrador de paquetes CRX: `https://localhost:4502/crx/packmgr/`.
1. Busque el paquete del visor en la lista; comienza con `cq-dam-scene7-viewers-content`.
1. Select **Reinstalar**.
1. En Cloud Services, vaya a la página Configuración de Dynamic Media y, a continuación, abra el cuadro de diálogo de configuración para la configuración de Dynamic Media - S7.
1. No realizar cambios, seleccione **Guardar**.
Esta acción de guardar déclencheur la lógica de nuevo para crear y sincronizar los recursos de ejemplo, el CSS preestablecido del visor y la ilustración.

### Problema: La vista previa de imágenes no se carga en la creación de ajustes preestablecidos de visor {#image-preview-not-loading}

**Solución**

1. En el Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el carril izquierdo, vaya a la carpeta de contenido de ejemplo en la siguiente ubicación:

   `/content/dam/_DMSAMPLE`

1. Elimine el `_DMSAMPLE` carpeta.
1. En el carril izquierdo, vaya a la carpeta de ajustes preestablecidos en la siguiente ubicación:

   `/conf/global/settings/dam/dm/presets/viewer`

1. Elimine el `viewer` carpeta.
1. Cerca de la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.
1. En la esquina superior izquierda de la página CRXDE Lite, seleccione la opción **Página de inicio** icono.
1. Vuelva a crear un [Configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
