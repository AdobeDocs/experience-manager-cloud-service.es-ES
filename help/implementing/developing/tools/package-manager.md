---
title: El administrador de paquetes
description: Conozca los conceptos básicos de AEM; administración de paquetes con el Administrador de paquetes.
feature: Administering, Developing
role: Admin
exl-id: b5fef273-912d-41f6-a698-0231eedb2b92
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '3772'
ht-degree: 3%

---

# El administrador de paquetes {#working-with-packages}

Los paquetes permiten importar y exportar el contenido del repositorio. Puede utilizar paquetes para instalar contenido nuevo, transferir contenido entre instancias y realizar copias de seguridad del contenido del repositorio.

AEM Con el Administrador de paquetes, puede transferir paquetes entre la instancia de y el sistema de archivos local para fines de desarrollo.

## ¿Qué son los paquetes? {#what-are-packages}

Un paquete es un archivo zip que contiene contenido del repositorio en forma de serialización del sistema de archivos, denominada serialización de Vault, lo que proporciona una representación fácil de usar y editar de archivos y carpetas. El contenido incluido en el paquete se define mediante filtros.

Un paquete también contiene metainformación de Vault, incluidas las definiciones de filtros y la información de configuración de importación. En el paquete se pueden incluir propiedades de contenido adicionales, que no se utilizan para la extracción de paquetes, como una descripción, una imagen visual o un icono. Estas propiedades de contenido adicionales son para el consumidor del paquete de contenido y solo con fines informativos.

>[!NOTE]
>
>Los paquetes representan la versión actual del contenido en el momento en que se crea el paquete. AEM No incluyen ninguna versión anterior del contenido que se mantiene en el repositorio de la que se haya hecho clic en el botón de la barra de herramientas de la aplicación de la aplicación de la aplicación de la.

## Paquetes en AEM as a Cloud Service {#aemaacs-packages}

Los paquetes de contenido creados para las aplicaciones de AEM as a Cloud Service deben tener una separación limpia entre el contenido inmutable y el mutable. Por lo tanto, el Administrador de paquetes solo se puede utilizar para administrar paquetes que contengan contenido. Cualquier código debe implementarse mediante Cloud Manager.

>[!NOTE]
>
>Los paquetes solo pueden contener contenido. Cualquier funcionalidad (por ejemplo, contenido almacenado bajo `/apps`) debe [implementarse usando su canalización de CI/CD en Cloud Manager](/help/implementing/cloud-manager/deploy-code.md).

>[!IMPORTANT]
>
>La interfaz de usuario del Administrador de paquetes puede devolver el mensaje de error **Indefinido** si un paquete tarda más de 10 minutos en instalarse.
>
>Esto no se debe a un error en la instalación, sino a un tiempo de espera que Cloud Service tiene para todas las solicitudes.
>
>No vuelva a intentar realizar la instalación si aparece un error de este tipo. La instalación continúa correctamente en el fondo. Si reinicia la instalación, podrían producirse conflictos debido a varios procesos de importación simultáneos.

Para obtener más información sobre cómo administrar paquetes para AEMaaCS, consulte [Implementación en AEM as a Cloud Service](/help/implementing/deploying/overview.md) en la guía de implementación de usuario.

## Tamaño del paquete {#package-size}

Adobe recomienda no crear paquetes grandes. Esto sirve para evitar problemas de tiempo de espera al cargar y descargar paquetes.

Como regla general, un paquete debe transmitirse en su totalidad en un plazo de 60 segundos. Esto proporciona la siguiente fórmula como guía.

```text
MaxPackageSize (in MB) = ConnectionSpeed (in MB/s) * 60 s
```

Dado que el tráfico de red es variable y siempre es menor que el valor teórico máximo anunciado, intente utilizar una herramienta de prueba de velocidad de conexión a Internet en línea.

Las velocidades de Internet son casi siempre diferentes para las cargas y descargas. Suponiendo que debe cargar y descargar paquetes, debe utilizar el valor más bajo (normalmente velocidad de carga) en el cálculo.

### Ejemplos {#example}

Utilizando una herramienta de prueba de velocidad de Internet, veo que mi velocidad de carga actual es de unos 100 Mbps.

```text
100 Mbps = 12.5 MB/s
12.5 MB/s * 60 s = 750 MB
```

Por lo tanto, cualquier paquete que cree debe ser menor que 750 MB.

>[!NOTE]
>
>Las velocidades de la red están sujetas a las condiciones locales actuales. Incluso con una prueba de velocidad reciente, el rendimiento real puede variar.
>
>Por lo tanto, la fórmula proporcionada es solo una guía y el tamaño máximo real del envase recomendado puede variar.

## El administrador de paquetes {#package-manager}

AEM El Administrador de paquetes administra los paquetes en la instalación de la. Una vez que [haya asignado los permisos necesarios](#permissions-needed-for-using-the-package-manager), podrá usar el Administrador de paquetes para diversas acciones, como configurar, generar, descargar e instalar los paquetes.

### Permisos necesarios {#required-permissions}

Para crear, modificar, cargar e instalar paquetes, los usuarios deben tener los permisos adecuados en los siguientes nodos:

* Derechos completos excluyendo eliminación en `/etc/packages`
* El nodo que contiene el contenido del paquete

>[!CAUTION]
>
>La concesión de permisos para paquetes puede dar lugar a la divulgación de información confidencial y a la pérdida de datos.
>
>Para limitar estos riesgos, es muy recomendable conceder permisos de grupo específicos solo sobre subárboles dedicados.

### Acceso al Administrador de paquetes {#accessing}

Puede acceder al Administrador de paquetes de tres formas:

1. AEM Desde el menú principal de la > **Herramientas** > **Implementación** > **Paquetes**
1. De [CRXDE Lite](crxde.md) mediante la barra de conmutación superior
1. Accediendo directamente a `http://<host>:<port>/crx/packmgr/`

### IU del Administrador de paquetes {#ui}

El Administrador de paquetes se divide en cuatro áreas funcionales principales:

* **Panel de navegación izquierdo**: este panel le permite filtrar y ordenar la lista de paquetes.
* **Lista de paquetes**: esta es la lista de paquetes de su instancia filtrados y ordenados por selecciones en el panel de navegación izquierdo.
* **Registro de actividad**: este panel se minimiza al principio y se amplía para detallar la actividad del Administrador de paquetes, como cuándo se crea o instala un paquete. Hay botones adicionales en la pestaña Registro de actividad para:
   * **Borrar registro**
   * **Mostrar/Ocultar**
* **Barra de herramientas**: La barra de herramientas contiene botones de actualización para el panel de navegación izquierdo y la lista de paquetes, así como botones para buscar, crear y cargar paquetes.

![IU del Administrador de paquetes](assets/package-manager-ui.png)

Al hacer clic en una opción del panel de navegación izquierdo, se filtra inmediatamente la lista de paquetes.

Al hacer clic en el nombre de un paquete, se expande la entrada en la Lista de paquetes para mostrar más detalles sobre el paquete.

![Detalles del paquete ampliado](assets/package-expand.png)

Existen varias acciones que se pueden realizar en un paquete a través de los botones de la barra de herramientas disponibles cuando se expanden los detalles del paquete.

* [Editar](#edit-package)
* [Generar](#building-a-package)
* [Reinstalar](#reinstalling-packages)
* [Descargar](#downloading-packages-to-your-file-system)

Hay más acciones disponibles debajo del botón **Más**.

* [Eliminar](#deleting-packages)
* [Cobertura](#package-coverage)
* [Contenido](#viewing-package-contents-and-testing-installation)
* [Volver a empaquetar](#rewrapping-a-package)
* [Otras versiones](#other-versions)
* [Desinstalar](#uninstalling-packages)
* [Probar instalación](#viewing-package-contents-and-testing-installation)
* [Validate](#validating-packages)
* [Replicar](#replicating-packages)

### Estado del paquete {#package-status}

Cada entrada en la lista de paquetes tiene un indicador de estado para permitirle conocer de un vistazo el estado del paquete. Al pasar el ratón por encima del estado, se muestra información del objeto con el detalle del estado.

![Estado del paquete](assets/package-status.png)

Si el paquete se ha cambiado o nunca se ha creado, el estado se presenta como un vínculo para realizar acciones rápidas para reconstruir o instalar el paquete.

## Configuración de paquetes {#package-settings}

Un paquete es esencialmente un conjunto de filtros y los datos del repositorio basados en esos filtros. Con la interfaz de usuario del Administrador de paquetes, puede hacer clic en un paquete y luego en el botón **Editar** para ver los detalles de un paquete, incluida la siguiente configuración.

* [Configuración general](#general-settings)
* [Filtros de paquetes](#package-filters)
* [Dependencias del paquete](#package-dependencies)
* [Configuración avanzada](#advanced-settings)
* [Capturas de pantalla de paquetes](#package-screenshots)

### Configuración general {#general-settings}

Puede editar una variedad de configuraciones de paquetes para definir información como la descripción del paquete, las dependencias y los detalles del proveedor.

El cuadro de diálogo **Configuración del paquete** está disponible a través del botón **Editar** al [crear](#creating-a-new-package) o [editar](#viewing-and-editing-package-information) un paquete. Una vez que haya realizado cambios, haga clic en **Guardar**.

![Cuadro de diálogo Editar paquete, configuración general](assets/general-settings.png)

| Campo | Descripción |
|---|---|
| Nombre | El nombre del paquete |
| Grupo | Para organizar paquetes, puede escribir el nombre de un grupo nuevo o seleccionar uno existente |
| Versión | Texto que se utilizará para la versión |
| Descripción | Una breve descripción del paquete que permite el marcado del HTML para el formato |
| Miniatura    | El icono que aparece con la lista de paquetes |

### Filtros de paquetes {#package-filters}

Los filtros identifican los nodos del repositorio que se van a incluir en el paquete. Una **definición de filtro** especifica la siguiente información:

* **Ruta raíz** del contenido que se va a incluir
* **Reglas** que incluyen o excluyen nodos específicos debajo de la ruta raíz

Agregar reglas utilizando el botón **+**. Quitar reglas con el botón **-**.

Las reglas se aplican según su orden, así que colóquelas según sea necesario utilizando los botones de flecha **Arriba** y **Abajo**.

Los filtros pueden incluir cero o más reglas. Cuando no se define ninguna regla, el paquete contiene todo el contenido por debajo de la ruta raíz.

Puede definir una o más definiciones de filtro para un paquete. Utilice más de un filtro para incluir contenido de varias rutas raíz.

![Ficha Filtros](assets/edit-filter.png)

Al crear reglas, defina una expresión regular (también conocida como regex, regexp o expresión racional) para especificar todos los nodos que desee incluir o excluir.

| Tipo de regla | Descripción |
|---|---|
| include | Include incluirá todos los archivos y carpetas del directorio especificado que coincidan con la expresión regular. Incluir **no** incluirá otros archivos o carpetas de la ruta raíz especificada. |
| excluir | Excluir excluirá todos los archivos y carpetas que coincidan con la expresión regular. |

Los filtros de paquetes se definen con mayor frecuencia la primera vez que [crea el paquete](#creating-a-new-package). Sin embargo, también se pueden editar más adelante, después de lo cual el paquete debe volver a crearse para actualizar su contenido en función de las nuevas definiciones de filtro.

>[!TIP]
>
>Un paquete puede contener varias definiciones de filtros para que los nodos de diferentes ubicaciones se puedan combinar fácilmente en un paquete.

>[!TIP]
>
>Para obtener información básica, consulte la [Documentación de Apache Jackrabbit - Workspace Filter](https://jackrabbit.apache.org/filevault/filter.html).

### Dependencias {#dependencies}

![Ficha Dependencias](assets/dependencies.png)

| Campo | Descripción | Ejemplo/Detalles |
|---|---|---|
| Probado con | El nombre y la versión del producto a los que se dirige este paquete o con los que es compatible. | `AEMaaCS` |
| Problemas solucionados | Un campo de texto que permite enumerar los detalles de los errores corregidos con este paquete, un error por línea | - |
| Depende de | Enumera otros paquetes necesarios para que el paquete actual se ejecute según lo esperado cuando se instale | `groupId:name:version` |
| Reemplaza | Una lista de paquetes obsoletos a los que reemplaza este paquete | `groupId:name:version` |

### Configuración avanzada {#advanced-settings}

![Ficha Configuración avanzada](assets/advanced-settings.png)

| Campo | Descripción | Ejemplo/Detalles |
|---|---|---|
| Nombre | El nombre del proveedor del paquete | `WKND Media Group` |
| URL | URL del proveedor | `https://wknd.site` |
| Vínculo | Vínculo específico del paquete a una página de proveedor | `https://wknd.site/package/` |
| Requiere | Define si hay alguna restricción al instalar el paquete | AEM **Administrador** - El paquete solo debe instalarse con privilegios de administrador <br>**Reiniciar** - se debe reiniciar después de instalar el paquete, por lo que se requiere un reinicio de la instalación del paquete. |
| Administración de AC | Especifica cómo se administra la información de control de acceso definida en el paquete cuando se importa el paquete | **Ignorar** - Conservar ACL en el repositorio <br>**Sobrescribir** - Sobrescribir ACL en el repositorio <br>**Combinar** - Combinar ambos conjuntos de ACL <br>**MergePreserve** - Combinar el control de acceso en el contenido con el proporcionado con el paquete agregando las entradas de control de acceso de las principales que no están presentes en el contenido <br>**Borrar** - Borrar ACL |

### Capturas de pantalla de paquetes {#package-screenshots}

Puede adjuntar varias capturas de pantalla al paquete para proporcionar una representación visual del aspecto del contenido.

![Ficha Capturas de pantalla](assets/screenshots.png)

## Acciones de paquete {#package-actions}

Se pueden realizar muchas acciones en un paquete.

### Creación de un paquete {#creating-a-new-package}

1. [Acceder al Administrador de paquetes](#accessing).

1. Haga clic en **Crear paquete**.

   >[!TIP]
   >
   >Si la instancia tiene muchos paquetes, puede haber una estructura de carpetas configurada. En estos casos, es más fácil navegar a la carpeta de destino requerida antes de crear el nuevo paquete.

1. En el cuadro de diálogo **Nuevo paquete**, introduzca los campos siguientes:

   ![Cuadro de diálogo Nuevo paquete](assets/new-package-dialog.png)

   * **Nombre del paquete**: seleccione un nombre descriptivo para ayudarle (y a otros) a identificar fácilmente el contenido del paquete.

   * **Versión**: este es un campo de texto para que usted indique una versión. Se anexa al nombre del paquete para formar el nombre del archivo zip.

   * **Grupo**: este es el nombre del grupo de destino (o carpeta). Los grupos le ayudan a organizar sus paquetes. Se crea una carpeta para el grupo si aún no existe. Si deja el nombre del grupo en blanco, se creará el paquete en la lista de paquetes principal.

1. Haga clic en **Aceptar** para crear el paquete.

1. AEM La lista de paquetes nuevos se encuentra en la parte superior de la lista de paquetes.

   ![Nuevo paquete](assets/new-package.png)

1. Haga clic en **Editar** para definir el [contenido del paquete](#package-contents). Haga clic en **Guardar** cuando termine de editar la configuración.

1. Ahora puede [compilar](#building-a-package) su paquete.

No es obligatorio crear inmediatamente el paquete después de crearlo. Un paquete sin compilar no contiene contenido y consiste únicamente en los datos de filtro y otros metadatos del paquete.

>[!TIP]
>
>Para evitar tiempos de espera, el Adobe recomienda [no crear paquetes grandes](#package-size).

### Creación de un paquete {#building-a-package}

Un paquete se crea a menudo al mismo tiempo que [crea el paquete](#creating-a-new-package), pero puede volver más tarde para compilarlo o reconstruirlo. Esto puede resultar útil si el contenido del repositorio ha cambiado o los filtros del paquete han cambiado.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Generar**. Un cuadro de diálogo le pedirá que confirme que desea crear el paquete, ya que se sobrescribirá el contenido existente.

1. Haga clic en **Aceptar**. AEM crea el paquete, enumerando todo el contenido añadido al paquete tal y como lo hace en la lista de actividad. AEM Cuando se completa, muestra una confirmación de que el paquete se ha creado y (al cerrar el cuadro de diálogo) actualiza la información de la lista de paquetes.

>[!TIP]
>
>Para evitar tiempos de espera, el Adobe recomienda [no crear paquetes grandes](#package-size).

### Edición de un paquete {#edit-package}

AEM Una vez cargado un paquete en el repositorio de, puede modificar su configuración.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Editar** y actualice **[Configuración del paquete](#package-settings)** según sea necesario.

1. Haga clic en **Guardar** para guardar.

Es posible que tenga que [reconstruir el paquete](#building-a-package) para actualizar su contenido en función de los cambios que ha realizado.

### Reajuste de un paquete {#rewrapping-a-package}

Una vez que se ha creado un paquete, se puede volver a empaquetar. Al volver a ajustar, se cambia la información del paquete sin incluir miniaturas, descripciones, etc., sin cambiar el contenido del paquete.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Editar** y actualice **[Configuración del paquete](#package-settings)** según sea necesario.

1. Haga clic en **Guardar** para guardar.

1. Haga clic en **Más** > **Reajustar** y un cuadro de diálogo solicitará confirmación.

### Visualización de otras versiones de paquetes {#other-versions}

Dado que cada versión de un paquete aparece en la lista como cualquier otro paquete, el Administrador de paquetes puede encontrar otras versiones de un paquete seleccionado.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Más** > **Otras versiones** y se abrirá un cuadro de diálogo con una lista de otras versiones del mismo paquete con información de estado.

### Visualización del contenido del paquete y prueba de la instalación {#viewing-package-contents-and-testing-installation}

Una vez creado un paquete, puede ver su contenido.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Para ver el contenido, haga clic en **Más** > **Contenido** y el Administrador de paquetes mostrará todo el contenido del paquete en el registro de actividades.

   ![Contenido del paquete](assets/package-contents.png)

1. Para realizar una ejecución en seco de la instalación, haga clic en **Más** > **Probar la instalación** y en los informes del Administrador de paquetes del registro de actividad para ver los resultados como si se hubiera realizado la instalación.

   ![Probar instalación](assets/test-install.png)

### Descarga de paquetes en el sistema de archivos {#downloading-packages-to-your-file-system}

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en el botón **Descargar** o en el nombre de archivo vinculado del paquete en el área de detalles del paquete.

1. AEM Descarga el paquete en su equipo.

>[!TIP]
>
>Para evitar tiempos de espera, el Adobe recomienda [no crear paquetes grandes](#package-size).

### Carga de paquetes desde el sistema de archivos {#uploading-packages-from-your-file-system}

1. [Acceder al Administrador de paquetes](#accessing).

1. Seleccione la carpeta del grupo en la que desea cargar el paquete.

1. Haga clic en el botón **Cargar paquete**.

1. Proporcione la información necesaria sobre el paquete cargado.

   ![Cuadro de diálogo de carga de paquetes.](assets/package-upload-dialog.png)

   * **Paquete** - Utilice el botón **Examinar...** para seleccionar el paquete requerido de su sistema de archivos local.
   * **Forzar carga**: si ya existe un paquete con este nombre, esta opción fuerza la carga y sobrescribe el paquete existente.

1. Haga clic en **Aceptar**, el paquete seleccionado se cargará y la lista de paquetes se actualizará en consecuencia.

AEM El contenido del paquete ahora existe en la, pero para que el contenido esté disponible para su uso, asegúrese de [instalar el paquete](#installing-packages).

>[!TIP]
>
>Para evitar tiempos de espera, el Adobe recomienda [no crear paquetes grandes](#package-size).

### Validación de paquetes {#validating-packages}

Dado que los paquetes pueden modificar el contenido existente, a menudo resulta útil validar estos cambios antes de instalar.

#### Opciones de validación {#validation-options}

El Administrador de paquetes puede realizar las siguientes validaciones:

* [Importaciones de paquetes OSGi](#osgi-package-imports)
* [Superposiciones](#overlays)
* [ACL](#acls)

##### Validar importaciones de paquetes OSGi {#osgi-package-imports}

>[!NOTE]
>
>Como los paquetes no se pueden usar para implementar código en AEMaaCS, la validación **Importaciones de paquetes OSGi** no es necesaria.

**Comprobaciones**

AEM Esta validación inspecciona el paquete para todos los archivos JAR (paquetes OSGi), extrae sus `manifest.xml` (que contienen las dependencias con versiones de las que depende dicho paquete OSGi) y verifica la instancia que exporta las exportaciones de las instancias mencionadas dependencias con las versiones correctas.

**Cómo se informa**

AEM Cualquier dependencia con versiones que la instancia de la instancia de la aplicación no pueda satisfacer se enumera en el registro de actividad del administrador de paquetes.

**Estados de error**

Si las dependencias no están satisfechas, los paquetes OSGi del paquete con esas dependencias no se iniciarán. Esto resulta en una implementación de aplicación dañada, ya que todo lo que dependa del paquete OSGi no iniciado a su vez no funcionará correctamente.

**Resolución de errores**

Para resolver errores debido a paquetes OSGi no satisfechos, se debe ajustar la versión de dependencia en el paquete con importaciones no satisfechas.

##### Validar capas {#overlays}

>[!NOTE]
>
>Como los paquetes no se pueden usar para implementar código en AEMaaCS, la validación **Superposiciones** es innecesaria.

**Comprobaciones**

AEM Esta validación determina si el paquete que se está instalando contiene un archivo que ya se superpone en la instancia de destino de la.

Por ejemplo, dada una superposición existente en `/apps/sling/servlet/errorhandler/404.jsp`, un paquete que contiene `/libs/sling/servlet/errorhandler/404.jsp`, de forma que cambiará el archivo existente en `/libs/sling/servlet/errorhandler/404.jsp`.

**Cómo se informa**

Cualquier superposición de este tipo se describe en el registro de actividad del administrador de paquetes.

**Estados de error**

Un estado de error significa que el paquete intenta implementar un archivo que ya está superpuesto, por lo que los cambios en el paquete se anularán (y, por lo tanto, &quot;ocultarán&quot;) por la superposición y no surtirán efecto.

**Resolución de errores**

Para resolver este problema, el mantenedor del archivo de superposición en `/apps` debe revisar los cambios del archivo superpuesto en `/libs` e incorporar los cambios según sea necesario en la superposición ( `/apps`), y volver a implementar el archivo superpuesto.

>[!NOTE]
>
>El mecanismo de validación no tiene forma de conciliar si el contenido superpuesto se ha incorporado correctamente al archivo de superposición. Por lo tanto, esta validación seguirá informando sobre los conflictos incluso después de realizar los cambios necesarios.

##### Validar ACL {#acls}

**Comprobaciones**

Esta validación comprueba qué permisos se agregan, cómo se administran (combinar/reemplazar) y si los permisos actuales se ven afectados.

**Cómo se informa**

Los permisos se describen en el registro de actividad del administrador de paquetes.

**Estados de error**

No se pueden proporcionar errores explícitos. La validación simplemente indica si se agregan o afectan nuevos permisos ACL al instalar el paquete.

**Resolución de errores**

Con la información proporcionada por la validación, los nodos afectados se pueden revisar en CRXDE y las ACL se pueden ajustar en el paquete según sea necesario.

>[!CAUTION]
>
>AEM Como práctica recomendada, se recomienda que los paquetes no afecten a las ACL proporcionadas por el usuario, ya que esto puede provocar un comportamiento inesperado.

#### Realización de validación {#performing-validation}

La validación de paquetes se puede realizar de dos formas diferentes:

* [A través de la IU del Administrador de paquetes](#via-package-manager).
* [Mediante una solicitud de POST HTTP como con cURL](#via-post-request).

La validación siempre debe producirse después de cargar el paquete, pero antes de instalarlo.

##### Validación De Paquetes Mediante El Administrador De Paquetes {#via-package-manager}

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Para validar el paquete, haga clic en **Más** > **Validar**,

1. En el cuadro de diálogo modal que aparece a continuación, utilice las casillas de verificación para seleccionar los tipos de validación y comience la validación haciendo clic en **Validar**.

1. Las validaciones seleccionadas se ejecutan y los resultados se muestran en el registro de actividad del administrador de paquetes.

##### Validación de paquetes mediante solicitud de POST HTTP {#via-post-request}

La solicitud del POST tiene la siguiente forma.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

El parámetro `type` puede ser cualquier lista desordenada separada por comas que consista en:

* `osgiPackageImports`
* `overlays`
* `acls`

El valor predeterminado de `type` es `osgiPackageImports` si no se pasa explícitamente.

Cuando utilice cURL, ejecute una instrucción similar a la siguiente:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Al validar mediante una solicitud de POST, la respuesta se devuelve como un objeto JSON.

### Visualización de cobertura del paquete {#package-coverage}

Los paquetes se definen mediante sus filtros. Puede hacer que el Administrador de paquetes aplique filtros de un paquete al contenido del repositorio existente para mostrar qué contenido del repositorio está cubierto por la definición del filtro del paquete.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Más** > **Cobertura**.

1. Los detalles de cobertura se enumeran en el registro de actividad.

### Instalación de paquetes {#installing-packages}

Al cargar un paquete, solo se añade el contenido del paquete al repositorio, pero no se puede acceder a él. Debe instalar el paquete cargado para utilizar el contenido del paquete.

>[!CAUTION]
>
>La instalación de un paquete puede sobrescribir o eliminar contenido existente. Cargue un paquete únicamente si está seguro de que no elimina ni sobrescribe el contenido que necesita.

Antes de la instalación del paquete, el Administrador de paquetes crea automáticamente un paquete de instantáneas que contiene el contenido que se sobrescribe. Esta instantánea se vuelve a instalar si desinstala el paquete.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete que desee instalar en la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en el botón **Instalar** en los detalles del elemento o en el vínculo **Instalar** en el estado del paquete.

1. Un cuadro de diálogo solicitará confirmación y permitirá que se especifiquen opciones adicionales.

   * **Extraer solo**: extraiga el paquete solamente para que no se cree ninguna instantánea y, por lo tanto, no sea posible realizar la desinstalación
   * **Guardar umbral**: número de nodos transitorios hasta que se activa el guardado automático (aumente si se producen excepciones de modificación simultáneas)
   * **Extraer subpaquetes** - Habilitar la extracción automática de subpaquetes
   * **Control de acceso**: especifica cómo se administra la información de control de acceso definida en el paquete cuando se instala el paquete (las opciones son las mismas que la [configuración avanzada del paquete](#advanced-settings))
   * **Administración de dependencias**: especifique cómo se administran las dependencias durante la instalación

1. Haga clic en **Instalar**.

1. El registro de actividad detalla el progreso de la instalación.

Una vez completada y completada la instalación, se actualiza la lista de paquetes y aparece la palabra **Instalado** en el estado del paquete.

### Reinstalación de paquetes {#reinstalling-packages}

La reinstalación de paquetes realiza los mismos pasos en un paquete ya instalado que se procesan al [instalar inicialmente el paquete](#installing-packages).

### Carga e instalación basadas en el sistema de archivos {#file-system-based-upload-and-installation}

Puede renunciar por completo al Administrador de paquetes al instalar paquetes. AEM Puede detectar paquetes colocados en una ubicación específica del sistema de archivos local del equipo host y cargarlos e instalarlos automáticamente.

1. AEM En la carpeta de instalación de la, hay una carpeta `crx-quicksart` junto al archivo jar y `license.properties`. Cree una carpeta con el nombre `install` en `crx-quickstart`, dando como resultado la ruta de acceso `<aem-home>/crx-quickstart/install`.

1. En esta carpeta, añada los paquetes. Se cargarán e instalarán automáticamente en su instancia.

1. Una vez completada la carga y la instalación, puede ver los paquetes en el Administrador de paquetes como si hubiera utilizado la interfaz de usuario del Administrador de paquetes para instalarlos.

Si la instancia se está ejecutando, la carga y la instalación comienzan inmediatamente cuando la agrega al paquete en la carpeta `install`

Si la instancia no se está ejecutando, los paquetes colocados en la carpeta `install` se instalan al inicio en orden alfabético.

### Desinstalación de paquetes {#uninstalling-packages}

Al desinstalar un paquete, el contenido del repositorio se revierte a la instantánea realizada automáticamente por el Administrador de paquetes antes de la instalación.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete que desee desinstalar de la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Más** > **Desinstalar** para quitar el contenido de este paquete del repositorio.

1. Un cuadro de diálogo solicitará confirmación y enumerará todos los cambios que se realizan.

1. El paquete se elimina y se aplica la instantánea. El progreso del proceso se muestra en el registro de actividad.

### Eliminación de paquetes {#deleting-packages}

Al eliminar un paquete, solo se eliminan sus detalles del Administrador de paquetes. Si este paquete ya estaba instalado, el contenido instalado no se eliminará.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete que desee eliminar de la lista de paquetes haciendo clic en el nombre del paquete.

1. AEM La solicita confirmación para eliminar el paquete. Haga clic en **Aceptar** para confirmar la eliminación.

1. La información del paquete se elimina y los detalles se incluyen en el registro de actividad.

### Duplicación de paquetes {#replicating-packages}

Repita el contenido de un paquete para instalarlo en la instancia de publicación.

1. [Acceder al Administrador de paquetes](#accessing).

1. Abra los detalles del paquete que desee duplicar desde la lista de paquetes haciendo clic en el nombre del paquete.

1. Haga clic en **Más** > **Replicar**.

1. El paquete se duplica y los detalles se incluyen en el registro de actividad.

## Distribución de software {#software-distribution}

AEM Los paquetes de se pueden utilizar para crear y compartir contenido en entornos AEMaaCS.

AEM AEM [La distribución de software](https://downloads.experiencecloud.adobe.com) proporciona paquetes de para su uso en el desarrollo local de SDK. AEM Los paquetes proporcionados en la distribución de software no deben instalarse en entornos de nube AEMaaCS a menos que el soporte de Adobe los apruebe expresamente.

Para obtener más información, consulte la [documentación de distribución de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=es).
