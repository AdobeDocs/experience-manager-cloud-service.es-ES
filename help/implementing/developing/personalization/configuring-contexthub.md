---
title: Configuración de ContextHub
description: Obtenga información sobre cómo configurar ContextHub.
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 1%

---

# Configuración de ContextHub {#configuring-contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. Para obtener más información sobre ContextHub, consulte la [Información general para desarrolladores de ContextHub](contexthub.md).

Puede configurar la barra de herramientas de ContextHub para controlar si aparece en el modo de vista previa, crear tiendas de ContextHub y añadir módulos de interfaz de usuario.

## Mostrar y ocultar la interfaz de usuario de ContextHub {#showing-and-hiding-the-contexthub-ui}

Configure el servicio OSGi de Adobe Granite ContextHub para mostrar u ocultar el [IU de ContextHub](/help/sites-cloud/authoring/personalization/targeted-content.md) en sus páginas. El PID de este servicio es `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Para configurar el servicio, puede usar el complemento [Consola web](/help/implementing/deploying/configuring-osgi.md) o utilice un nodo JCR en el repositorio:

* **Consola web:** Para mostrar la interfaz de usuario, seleccione la propiedad Mostrar IU. Para ocultar la interfaz de usuario, borre la propiedad Ocultar interfaz de usuario.
* **Nodo JCR:** Para mostrar la interfaz de usuario, establezca el valor booleano `com.adobe.granite.contexthub.show_ui` propiedad a `true`. Para ocultar la interfaz de usuario, establezca la propiedad en `false`.

AEM Al mostrar la interfaz de usuario de ContextHub, solo aparece en las páginas de instancias de autor de la. La interfaz de usuario no aparece en las páginas de instancias de publicación.

## Adición de modos y módulos de IU de ContextHub {#adding-contexthub-ui-modes-and-modules}

Configure los modos y módulos de interfaz de usuario que aparecen en la barra de herramientas de ContextHub en el modo de vista previa:

* Modos de IU: grupos de módulos relacionados
* Módulos: widgets que exponen datos de contexto de un almacén y permiten a los autores manipular el contexto

Los modos de interfaz de usuario aparecen como una serie de iconos en la parte izquierda de la barra de herramientas. Cuando se seleccionan, los módulos de un modo de interfaz de usuario aparecen a la derecha.

![Barra de herramientas de ContextHub](assets/contexthub-toolbar.png)

Los iconos son referencias de [Biblioteca de iconos de Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Adición de un modo de IU {#adding-a-ui-mode}

Añada un modo de interfaz de usuario para agrupar módulos de ContextHub relacionados. Al crear el modo de IU, se indica el título y el icono que aparecen en la barra de herramientas de ContextHub.

1. En el carril del Experience Manager, toque o haga clic en Herramientas > Sitios > Context Hub.
1. Toque o haga clic en el contenedor de configuración predeterminado.
1. Toque o haga clic en Configuración de ContextHub.
1. Toque o haga clic en el botón Crear y, a continuación, toque o haga clic en el modo de IU de Context Hub.

   ![Agregar modo de IU](assets/contexthub-ui-mode.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del modo de IU: título que identifica el modo de IU
   * Icono de modo: el selector para [Icono de Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) para utilizar, por ejemplo `coral-Icon--user`
   * Habilitado: seleccione esta opción para mostrar el modo de IU en la barra de herramientas de ContextHub

1. Toque o haga clic en Guardar.

### Adición de un módulo de IU {#adding-a-ui-module}

Agregue un módulo de IU de ContextHub a un modo de IU para que aparezca en la barra de herramientas de ContextHub para obtener una vista previa del contenido de la página. Al agregar un módulo de IU, se crea una instancia de un tipo de módulo registrado con ContextHub. Para agregar un módulo de interfaz de usuario, debe conocer el nombre del tipo de módulo asociado.

AEM proporciona un tipo de módulo de interfaz de usuario base, así como varios tipos de módulos de interfaz de usuario de ejemplo en los que puede basar un módulo de interfaz de usuario. En la tabla siguiente se proporciona una breve descripción de cada uno. Para obtener información sobre el desarrollo de un módulo de IU personalizado, consulte [Creación de módulos de IU de ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

Las propiedades del módulo de interfaz de usuario incluyen una configuración detallada en la que puede proporcionar valores para propiedades específicas del módulo. Proporcione la configuración detallada en formato JSON. La columna Tipo de módulo de la tabla proporciona vínculos a información sobre el código JSON necesario para cada tipo de módulo de interfaz de usuario.

| Tipo de módulo | Descripción | Almacenar |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | Un tipo de módulo de IU genérico | Configurado en las propiedades del módulo de IU |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | Muestra información sobre el explorador | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | Muestra información de fecha y hora | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | Muestra la latitud y longitud del cliente, así como la ubicación en un mapa. Permite cambiar la ubicación. | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | Muestra la orientación de pantalla del dispositivo (horizontal o vertical) | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | Muestra estadísticas sobre etiquetas de página | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | Muestra la información de perfil del usuario actual, incluyendo `authorizableID`, `displayName` y `familyName`. Puede cambiar el valor de `displayName` y `familyName`. | `profile` |

1. En el carril del Experience Manager, pulse o haga clic en Herramientas > Sitios > ContextHub.
1. Toque o haga clic en el contenedor de configuración al que desea agregar un módulo de interfaz de usuario.
1. Haga clic o escriba la Configuración de ContextHub a la que desea agregar el módulo de interfaz de usuario.
1. Toque o haga clic en el modo de IU al que está agregando el módulo de IU.
1. Pulse o haga clic en el botón Crear y, a continuación, pulse o haga clic en Módulo de IU de ContextHub (genérico).

   ![Módulo de IU de ContextHub](assets/contexthub-ui-module.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del módulo de IU: un título que identifica el módulo de IU
   * Tipo de módulo: el tipo de módulo
   * Habilitado: seleccione esta opción para mostrar el módulo de IU en la barra de herramientas de ContextHub

1. (Opcional) Para anular la configuración de almacén predeterminada, introduzca un objeto JSON para configurar el módulo de interfaz de usuario.
1. Toque o haga clic en Guardar.

## Creación de una tienda de ContextHub {#creating-a-contexthub-store}

Cree un almacén de ContextHub para conservar los datos de usuario y acceder a ellos según sea necesario. Las tiendas de ContextHub se basan en candidatos de tiendas registradas. Cuando cree el almacén, necesitará el valor del storeType con el que se registró el candidato del almacén. (Consulte [Crear candidatos de tienda personalizados](extending-contexthub.md#creating-custom-store-candidates).)

### Configuración detallada de la tienda {#detailed-store-configuration}

Al configurar un almacén, la propiedad Configuración detallada permite proporcionar valores para las propiedades específicas del almacén. El valor se basa en `config` parámetro del almacén `init` función. Por lo tanto, si debe proporcionar este valor y el formato del valor dependen del almacén.

El valor de la propiedad Detail Configuration es un `config` en formato JSON.

### Candidatos de tienda de muestra {#sample-store-candidates}

AEM proporciona los siguientes candidatos de tienda de muestra en los que puede basar una tienda.

| Tipo de tienda | Descripción |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | Almacenar para segmentos de ContextHub resueltos y no resueltos. Recupera automáticamente segmentos del Administrador de segmentos de ContextHub |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | Almacena la latitud y longitud de la ubicación del explorador. |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | Define las propiedades y capacidades de una serie de dispositivos y detecta el dispositivo cliente actual |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | Almacena datos de perfil del usuario actual |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | Almacena información sobre el cliente, como información del dispositivo, tipo de explorador y orientación de la ventana |

1. En el carril del Experience Manager, pulse o haga clic en Herramientas > Sitios > ContextHub.
1. Toque o haga clic en el contenedor de configuración predeterminado.
1. Toque o haga clic en Configuración de Contexthub
1. Para agregar una tienda, toque o haga clic en el icono Crear y, a continuación, toque o haga clic en Configuración de tienda de ContextHub.

   ![Configuración de tienda de ContextHub](assets/contexthub-store-configuration.png)

1. Proporcione valores para las propiedades de configuración básicas y toque o haga clic en Siguiente:

   * **Título de configuración:** El título que identifica la tienda
   * **Tipo de tienda:** Valor de la propiedad storeType del candidato de almacén en el que se va a basar el almacén
   * **Requerido:** Seleccionar
   * **Habilitado:** Seleccione para activar la tienda

1. (Opcional) Para anular la configuración de almacén predeterminada, introduzca un objeto JSON en el cuadro Configuración detallada (JSON).
1. Toque o haga clic en Guardar.

## Ejemplo: Uso de un servicio JSONP  {#example-using-a-jsonp-service}

Este ejemplo ilustra cómo configurar un almacén y mostrar los datos en un módulo de interfaz de usuario. En este ejemplo, el servicio MD5 del sitio jsontest.com se utiliza como fuente de datos para una tienda. El servicio devuelve el código hash MD5 de una cadena determinada, en formato JSON.

Se configura un almacén contexthub.generic-jsonp para que almacene datos para la llamada de servicio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. El servicio devuelve los siguientes datos, que se muestran en un módulo de interfaz de usuario:

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Crear un almacén de contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

El candidato del almacén de muestra contexthub.generic-jsonp permite recuperar datos de un servicio JSONP o un servicio web que devuelve datos JSON. Para este candidato a tienda, utilice la configuración de tienda para proporcionar detalles acerca del servicio JSONP que se va a utilizar.

El [init](contexthub-api.md#init-name-config) función del `ContextHub.Store.JSONPStore` La clase JavaScript define una `config` objeto que inicializa este candidato de almacén. El `config` el objeto contiene un `service` que incluye detalles sobre el servicio JSONP. Para configurar el almacén, proporcione el `service` en formato JSON como valor de la propiedad Detail Configuration.

Para guardar datos del servicio MD5 del sitio jsontest.com, utilice el procedimiento de [Creación de una tienda de ContextHub](#creating-a-contexthub-store) mediante las siguientes propiedades:

* **Título de configuración:** md5
* **Tipo de tienda:** contexthub.generic-jsonp
* **Requerido:** Seleccionar
* **Habilitado:** Seleccionar
* **Configuración detallada (JSON):**

   ```javascript
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Adición de un módulo de IU para los datos md5 {#adding-a-ui-module-for-the-md-data}

Agregue un módulo de interfaz de usuario a la barra de herramientas de ContextHub para mostrar los datos almacenados en el almacén md5 de ejemplo. En este ejemplo, el módulo contexthub.base se utiliza para producir el siguiente módulo de interfaz de usuario:

![Tienda de ContextHub MD5](assets/contexthub-md5-store.png)

Utilice el procedimiento de [Adición de un módulo de IU](#adding-a-ui-module) para agregar el módulo de IU a un modo de IU existente, como el modo de IU personal de ejemplo. Para el módulo de interfaz de usuario, utilice los siguientes valores de propiedad:

* **Título de módulo de IU:** MD5
* **Tipo de módulo:** contexthub.base
* **Configuración detallada (JSON):**

   ```javascript
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Conversion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Depuración de ContextHub {#debugging-contexthub}

Se puede habilitar un modo de depuración para ContextHub para permitir la resolución de problemas. El modo de depuración se puede habilitar mediante la configuración de ContextHub o mediante CRXDE.

### Mediante la configuración {#via-the-configuration}

Edite la configuración de ContextHub y marque la opción **Depurar**

1. En el carril, toque o haga clic en **Herramientas > Sitios > ContextHub**
1. Toque o haga clic en el valor predeterminado **Contenedor de configuración**
1. Seleccione el **Configuración de ContextHub** y toque o haga clic en **Editar elemento seleccionado**
1. Haga clic o toque **Depurar** y toque o haga clic en **Guardar**

### Mediante CRXDE {#via-crxde}

Utilice el CRXDE Lite para establecer la propiedad `debug` hasta **true** en:

* `/conf/global/settings/cloudsettings` o
* `/conf/<site>/settings/cloudsettings`

### Registrar mensajes de depuración para ContextHub {#logging-debug-messages-for-contexthub}

Configuración del servicio OSGi de Adobe Granite ContextHub (PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`) para registrar mensajes de Debug detallados que son útiles al desarrollar.

Para configurar el servicio, puede usar el complemento [Consola web](/help/implementing/deploying/configuring-osgi.md) o utilice un nodo JCR en el repositorio:

* Consola web: para registrar los mensajes de Debug, seleccione la propiedad Debug.
* Nodo JCR: para registrar mensajes de Debug, establezca el valor booleano `com.adobe.granite.contexthub.debug` propiedad a `true`.

### Modo silencioso {#silent-mode}

El modo silencioso suprime toda la información de depuración. A diferencia de la opción de depuración normal, que se puede establecer de forma independiente para cada configuración de ContextHub, el modo silencioso es una configuración global que tiene prioridad sobre cualquier configuración de depuración en el nivel de configuración de ContextHub.

Esto resulta útil en la instancia de publicación, donde no desea ninguna información de depuración. Como es una configuración global, se habilita mediante OSGi.

1. Abra el **Configuración de la consola web Adobe Experience Manager** en `http://<host>:<port>/system/console/configMgr`
1. Buscar por **Adobe Granite ContextHub**
1. Haga clic en la configuración **Adobe Granite ContextHub** para editar sus propiedades
1. Marque la opción **Modo silencioso** y haga clic en **Guardar**

## Desactivación de ContextHub {#disabling-contexthub}

ContextHub se puede deshabilitar para evitar que se cargue js/css y se inicialice. Existen dos opciones para deshabilitar ContextHub:

* Edite la configuración de ContextHub y marque la opción **Desactivar ContextHub**

   1. En el carril, toque o haga clic en **Herramientas > Sitios > ContextHub**
   1. Toque o haga clic en el valor predeterminado **Contenedor de configuración**
   1. Seleccione el **Configuración de ContextHub** y toque o haga clic en **Editar elemento seleccionado**
   1. Haga clic o toque **Desactivar ContextHub** y toque o haga clic en **Guardar**

o

* Utilice el CRXDE Lite para establecer la propiedad `disabled` hasta **true** bajo `/conf/global/settings/cloudsettings/<configName>/contexthub`
