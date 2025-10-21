---
title: Configuración de ContextHub
description: Aprenda a configurar ContextHub, un marco de trabajo para almacenar, manipular y presentar datos de contexto.
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: 79480fc14163b144c76ea33d38cda7c6b84f826b
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 1%

---

# Configuración de ContextHub {#configuring-contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. Para obtener más información sobre ContextHub, consulte [Información general para desarrolladores de ContextHub](contexthub.md).

Puede configurar la barra de herramientas de ContextHub para controlar si aparece en el modo de vista previa, crear tiendas de ContextHub y añadir módulos de interfaz de usuario.

## Mostrar y ocultar la interfaz de usuario de ContextHub {#showing-and-hiding-the-contexthub-ui}

Configure el servicio OSGi de ContextHub de Adobe Granite para mostrar u ocultar la [interfaz de usuario de ContextHub](/help/sites-cloud/authoring/personalization/targeted-content.md) en sus páginas. El PID de este servicio es `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Para configurar el servicio, puede usar la [consola web](/help/implementing/deploying/configuring-osgi.md) o usar un nodo JCR en el repositorio:

* **Consola web:** Para mostrar la interfaz de usuario, seleccione la propiedad Mostrar IU. Para ocultar la interfaz de usuario, borre la propiedad Ocultar interfaz de usuario.
* **Nodo JCR:** Para mostrar la interfaz de usuario, establezca la propiedad booleana `com.adobe.granite.contexthub.show_ui` en `true`. Para ocultar la IU, establezca la propiedad en `false`.

Al mostrar la interfaz de usuario de ContextHub, solo aparece en páginas de instancias de autor de AEM. La interfaz de usuario no aparece en las páginas de instancias de publicación.

## Adición de modos y módulos de IU de ContextHub {#adding-contexthub-ui-modes-and-modules}

Configure los modos y módulos de interfaz de usuario que aparecen en la barra de herramientas de ContextHub en el modo de vista previa:

* Modos de IU: grupos de módulos relacionados
* Módulos: widgets que exponen datos de contexto de un almacén y permiten a los autores manipular el contexto

Los modos de interfaz de usuario aparecen como una serie de iconos en la parte izquierda de la barra de herramientas. Cuando se seleccionan, los módulos de un modo de interfaz de usuario aparecen a la derecha.

![Barra de herramientas de ContextHub](assets/contexthub-toolbar.png)

Los iconos son referencias de la [biblioteca de iconos de la IU de Coral](https://opensource.adobe.com/coral-spectrum/examples/#icon).

### Adición de un modo de IU {#adding-a-ui-mode}

Añada un modo de interfaz de usuario para agrupar módulos de ContextHub relacionados. Al crear el modo de IU, se indica el título y el icono que aparecen en la barra de herramientas de ContextHub.

1. En el carril Experience Manager, seleccione Herramientas > Sitios > Context Hub.
1. Seleccione el contenedor de configuración predeterminado.
1. Seleccione la configuración de Context Hub.
1. Seleccione el botón Crear y, a continuación, seleccione Modo de IU de Context Hub.

   ![Agregar modo de interfaz de usuario](assets/contexthub-ui-mode.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del modo de IU: título que identifica el modo de IU
   * Icono de modo: el selector para que [Coral UI icon](https://opensource.adobe.com/coral-spectrum/examples/#icon) use, por ejemplo, `coral-Icon--user`
   * Habilitado: seleccione esta opción para mostrar el modo de IU en la barra de herramientas de ContextHub

1. Seleccione Guardar.

### Adición de un módulo de IU {#adding-a-ui-module}

Agregue un módulo de IU de ContextHub a un modo de IU para que aparezca en la barra de herramientas de ContextHub para obtener una vista previa del contenido de la página. Al agregar un módulo de IU, se crea una instancia de un tipo de módulo registrado con ContextHub. Para agregar un módulo de interfaz de usuario, debe conocer el nombre del tipo de módulo asociado.

AEM proporciona un tipo de módulo de IU base, así como varios tipos de módulos de IU de ejemplo en los que puede basar un módulo de IU. En la tabla siguiente se proporciona una breve descripción de cada uno. Para obtener información sobre el desarrollo de un módulo de IU personalizado, consulte [Creación de módulos de IU de ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

Las propiedades del módulo de interfaz de usuario incluyen una configuración detallada en la que puede proporcionar valores para propiedades específicas del módulo. Proporcione la configuración detallada en formato JSON. La columna Tipo de módulo de la tabla proporciona vínculos a información sobre el código JSON necesario para cada tipo de módulo de interfaz de usuario.

| Tipo de módulo | Descripción | Almacenar |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | Un tipo de módulo de IU genérico | Configurado en las propiedades del módulo de IU |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | Muestra información sobre el explorador | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | Muestra información de fecha y hora | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | Muestra la latitud y longitud del cliente, así como la ubicación en un mapa. Permite cambiar la ubicación. | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | Muestra la orientación de pantalla del dispositivo (horizontal o vertical) | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | Muestra estadísticas sobre etiquetas de página | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | Muestra la información de perfil del usuario actual, incluidos `authorizableID`, `displayName` y `familyName`. Puede cambiar el valor de `displayName` y `familyName`. | `profile` |

1. En el carril Experience Manager, seleccione Herramientas > Sitios > ContextHub.
1. Seleccione el contenedor de configuración al que desea agregar un módulo de interfaz de usuario.
1. Seleccione o escriba la Configuración de ContextHub a la que desea agregar el módulo de interfaz de usuario.
1. Seleccione el modo de interfaz de usuario al que va a agregar el módulo de interfaz de usuario.
1. Seleccione el botón Crear y, a continuación, seleccione Módulo de IU de ContextHub (genérico).

   ![Módulo de IU de ContextHub](assets/contexthub-ui-module.png)

1. Proporcione valores para las siguientes propiedades:

   * Título del módulo de IU: un título que identifica el módulo de IU
   * Tipo de módulo: el tipo de módulo
   * Habilitado: seleccione esta opción para mostrar el módulo de IU en la barra de herramientas de ContextHub

1. (Opcional) Para anular la configuración de almacén predeterminada, introduzca un objeto JSON para configurar el módulo de interfaz de usuario.
1. Seleccione Guardar.

## Creación de una tienda de ContextHub {#creating-a-contexthub-store}

Cree un almacén de ContextHub para conservar los datos de usuario y acceder a ellos según sea necesario. Las tiendas de ContextHub se basan en candidatos de tiendas registradas. Cuando cree el almacén, necesitará el valor del storeType con el que se registró el candidato del almacén. (Consulte [Creación de candidatos de tienda personalizados](extending-contexthub.md#creating-custom-store-candidates).)

### Configuración detallada de la tienda {#detailed-store-configuration}

Al configurar un almacén, la propiedad Configuración detallada permite proporcionar valores para las propiedades específicas del almacén. El valor se basa en el parámetro `config` de la función `init` del almacén. Por lo tanto, si debe proporcionar este valor y el formato del valor dependen del almacén.

El valor de la propiedad Detail Configuration es un objeto `config` en formato JSON.

### Candidatos de tienda de muestra {#sample-store-candidates}

AEM proporciona los siguientes ejemplos de candidatos a tiendas en los que puede basar una tienda.

| Tipo de tienda | Descripción |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | Almacenar para segmentos de ContextHub resueltos y no resueltos. Recupera automáticamente segmentos del Administrador de segmentos de ContextHub |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | Almacena la latitud y longitud de la ubicación del explorador. |
| [granite.emulators](sample-stores.md#granite-emulators-sample-store-candidate) | Define las propiedades y capacidades de varios dispositivos y detecta el dispositivo cliente actual |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | Almacena datos de perfil del usuario actual |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | Almacena información sobre el cliente, como información del dispositivo, tipo de explorador y orientación de la ventana |

1. En el carril Experience Manager, seleccione Herramientas > Sitios > ContextHub.
1. Seleccione el contenedor de configuración predeterminado.
1. Seleccionar configuración de Contexthub
1. Para añadir una tienda, seleccione el icono Crear y luego seleccione Configuración de tienda de ContextHub.

   ![Configuración de tienda de ContextHub](assets/contexthub-store-configuration.png)

1. Proporcione valores para las propiedades de configuración básicas y seleccione Siguiente:

   * **Título de configuración:** El título que identifica el almacén
   * **Tipo de almacén:** Valor de la propiedad storeType del candidato de almacén en el que se basará el almacén
   * **Requerido:** Seleccionar
   * **Habilitado:** Seleccione esta opción para habilitar el almacén

1. (Opcional) Para anular la configuración de almacén predeterminada, introduzca un objeto JSON en el cuadro Configuración detallada (JSON).
1. Seleccione Guardar.

## Ejemplo: Uso de un servicio JSONP  {#example-using-a-jsonp-service}

Este ejemplo ilustra cómo configurar un almacén y mostrar los datos en un módulo de interfaz de usuario. En este ejemplo, el servicio MD5 del sitio jsontest.com se utiliza como fuente de datos para una tienda. El servicio devuelve el código hash MD5 de una cadena determinada, en formato JSON.

Se ha configurado un almacén contexthub.generic-jsonp para que almacene datos para la llamada de servicio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. El servicio devuelve los siguientes datos, que se muestran en un módulo de interfaz de usuario:

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Crear un almacén de contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

El candidato del almacén de muestra contexthub.generic-jsonp permite recuperar datos de un servicio JSONP o un servicio web que devuelve datos JSON. Para este candidato a tienda, utilice la configuración de tienda para proporcionar detalles acerca del servicio JSONP que se va a utilizar.

La función [init](contexthub-api.md#init-name-config) de la clase JavaScript `ContextHub.Store.JSONPStore` define un objeto `config` que inicializa este candidato de almacén. El objeto `config` contiene un objeto `service` que incluye detalles acerca del servicio JSONP. Para configurar el almacén, proporcione el objeto `service` en formato JSON como valor de la propiedad Detail Configuration.

Para guardar datos del servicio MD5 del sitio jsontest.com, use el procedimiento de [Creación de un almacén de ContextHub](#creating-a-contexthub-store) con las siguientes propiedades:

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

![Almacén ContextHub MD5](assets/contexthub-md5-store.png)

Use el procedimiento de [Agregar un módulo de interfaz de usuario](#adding-a-ui-module) para agregar el módulo de interfaz de usuario a un modo de interfaz de usuario existente, como el modo de interfaz de usuario personal de ejemplo. Para el módulo de interfaz de usuario, utilice los siguientes valores de propiedad:

* **Título del módulo de interfaz de usuario:** MD5
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

Edite la configuración de ContextHub y marque la opción **Debug**

1. En el carril, seleccione **Herramientas > Sitios > ContextHub**
1. Seleccione el **contenedor de configuración** predeterminado
1. Seleccione la **configuración de ContextHub** y seleccione **Editar elemento seleccionado**
1. Seleccione **Depurar** y seleccione **Guardar**

### Mediante CRXDE {#via-crxde}

Use CRXDE Lite para establecer la propiedad `debug` en **true** en:

* `/conf/global/settings/cloudsettings` o
* `/conf/<site>/settings/cloudsettings`

### Registrar mensajes de depuración para ContextHub {#logging-debug-messages-for-contexthub}

Configure el servicio OSGi de ContextHub de Adobe Granite (PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`) para registrar mensajes de depuración detallados que sean útiles al desarrollar.

Para configurar el servicio, puede usar la [consola web](/help/implementing/deploying/configuring-osgi.md) o usar un nodo JCR en el repositorio:

* Consola web: para registrar los mensajes de Debug, seleccione la propiedad Debug.
* Nodo JCR: para registrar los mensajes de depuración, establezca la propiedad booleana `com.adobe.granite.contexthub.debug` en `true`.

### Modo silencioso {#silent-mode}

El modo silencioso suprime toda la información de depuración. A diferencia de la opción de depuración normal, que se puede establecer de forma independiente para cada configuración de ContextHub, el modo silencioso es una configuración global que tiene prioridad sobre cualquier configuración de depuración en el nivel de configuración de ContextHub.

Esto resulta útil en la instancia de publicación, donde no desea depurar ninguna información. Como es una configuración global, se habilita mediante OSGi.

1. Abrir la **configuración de la consola web de Adobe Experience Manager** en `http://<host>:<port>/system/console/configMgr`
1. Buscar **Adobe Granite ContextHub**
1. Haga clic en la configuración **Adobe Granite ContextHub** para editar sus propiedades
1. Marque la opción **Modo silencioso** y haga clic en **Guardar**

## Desactivación de ContextHub {#disabling-contexthub}

ContextHub se puede deshabilitar para evitar que se cargue js/css y se inicialice. Existen dos opciones para deshabilitar ContextHub:

* Edite la configuración de ContextHub y marque la opción **Deshabilitar ContextHub**

   1. En el carril, seleccione **Herramientas > Sitios > ContextHub**
   1. Seleccione el **contenedor de configuración** predeterminado
   1. Seleccione la **configuración de ContextHub** y seleccione **Editar elemento seleccionado**
   1. Seleccione **Deshabilitar ContextHub** y seleccione **Guardar**

o

* Use CRXDE Lite para establecer la propiedad `disabled` en **true** en `/conf/global/settings/cloudsettings/<configName>/contexthub`
