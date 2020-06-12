---
title: Uso del analizador de preparación para la nube
description: Uso del analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: d72f02f76f9be61ef4c3eefd790ff8abbb23a3d8
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# Uso del analizador de preparación para la nube {#using-cloud-readiness-analyzer}

## Consideraciones importantes sobre el uso del analizador de preparación para la nube {#imp-considerations}

Siga la sección siguiente para comprender las consideraciones importantes al ejecutar el analizador de preparación para la nube (CRA):

* El informe de CRA se crea con el resultado del detector [de](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)patrones de Adobe Experience Manager (AEM). La versión del detector de patrones utilizado por CRA se incluye en el paquete de instalación de CRA.

* El CRA solo puede ser ejecutado por el `admin` usuario o un usuario del `Administrators` grupo.

* CRA se admite en instancias de AEM con la versión 6.1 o posterior.

* CRA puede ejecutarse en cualquier entorno, pero es preferible que se ejecute en un entorno de *etapa* .

   >[!NOTE]
   >Para evitar un impacto en instancias críticas del negocio, se recomienda ejecutar CRA en un entorno de ensayo de *creación* que esté lo más cerca posible del entorno de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno *Autor* de producción.

* La generación de informes de CRA puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores.

* Debido al tiempo considerable que se necesita para generar el informe, los resultados se guardan en una caché y están disponibles para su posterior visualización y descarga hasta que caduque la caché o se actualice el informe de forma explícita.

## Disponibilidad {#availability}

El analizador de preparación para la nube se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue el analizador de preparación para la nube del portal de distribución de software *pendiente*.

## Ejecución del analizador de preparación para la nube {#running-tool}

Siga esta sección para obtener información sobre cómo ejecutar el analizador de preparación para la nube:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Una vez que haga clic en el Analizador **de preparación para** la nube, la herramienta inicio la generación del informe y, a los pocos minutos, el informe de resumen estará disponible en la instancia de AEM.

   >[!NOTE]
   >Tendrá que desplazarse hacia abajo por la página para vista del informe completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### AEM 6.3 y posterior {#aem-older-version}

Para AEM 6.3 y versiones posteriores, la forma principal de ejecutar el analizador de preparación para la nube es:

1. Utilice la interfaz de usuario de Adobe Experience Manager para navegar hasta Herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

   >[!NOTE]
   >El CRA iniciará un proceso en segundo plano para generar el informe en cuanto se abra la herramienta. Muestra una indicación de que la generación del informe está en curso hasta que el informe está listo. Puede cerrar la ficha del explorador y regresar más tarde para realizar la vista del informe cuando se haya completado.

Una vez generado y mostrado el informe de CRA, tiene la opción de descargar el informe en formato de valores separados por comas (CSV) haciendo clic en el botón **CSV** en la esquina superior derecha de la página de herramientas.

Puede forzar el CRA para que borre su caché y vuelva a generar el informe haciendo clic en el botón &quot;Actualizar informe&quot; en la esquina superior izquierda.

### AEM 6.2 y 6.1 {#aem-specific-versions}

La interfaz de usuario de CRA está limitada en AEM 6.2 a un vínculo que genera y descarga el informe CSV. En AEM 6.1, la interfaz de usuario no funciona y solo se puede utilizar la interfaz HTTP.

En todas las versiones, el detector de patrones incluido puede ejecutarse de forma independiente.

## Informe de resumen de CRA {#cra-summary-report}

Cuando el CRA se ejecuta en la interfaz de usuario de AEM, el informe se muestra como resultados en la ventana de herramientas. El formato del informe es:

* Información general del informe: Información sobre el propio informe, incluso cuando se generó.
* Información general del sistema: Información sobre el sistema AEM en el que se ejecutó el CRA.
* Búsqueda de Categorías: Varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: Nombre de la Categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción. Los niveles de importancia utilizados son los siguientes:

| Importancia | Descripción |
|--- |--- |
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este hallazgo es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL | Es probable que este hallazgo sea un problema de actualización que se debe abordar. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |

## Informe CSV de CRA {#crs-csv-report}

Cuando se presiona el botón &quot;CSV&quot;, el formato CSV del informe de CRA se crea a partir de la caché de resultados y se devuelve al explorador. Según la configuración del explorador, este informe se descargará automáticamente como archivo con un nombre predeterminado de `results.csv`. Si la caché ha caducado, el informe se regenerará antes de crear y descargar el archivo CSV.

Siga los pasos a continuación para generar un formato CSV del informe de resumen desde la instancia de AEM:

1. 
   1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador** de preparación para la nube.

1. Una vez que el informe esté disponible, haga clic en **CSV** para descargar el informe de resumen completo en formato de valores separados por comas (CSV), como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

El formato CSV del informe incluye información que se genera a partir de la salida del detector de patrones, ordenada y organizada por tipo de categoría, subtipo y nivel de importancia. Su formato es adecuado para visualizarlo y editarlo en una aplicación como Microsoft Excel. Su finalidad es proporcionar toda la información de búsqueda en un formato repetible que pueda resultar útil al comparar los informes con el paso del tiempo para medir el progreso.

Las columnas del informe de formato CSV son:

* **código**: el código de categoría
* **type**: el nombre de la categoría
* **subtipo**: subtipo de categoría
* **importancia**: el nivel de importancia
* **identificador**: el identificador principal de la búsqueda
* **otros**: información adicional sobre la búsqueda
* **mensaje**: el mensaje proporcionado para la búsqueda
* **moreInfo**: un vínculo que puede utilizarse para acceder a la ayuda en línea sobre la categoría
* **contexto**: una cadena JSON de búsqueda de datos

Un valor de &quot;\N&quot; en una columna para una búsqueda individual indica que no se proporcionaron datos.

## Interfaz HTTP {#http-interface}

El CRA proporciona una interfaz HTTP que puede utilizarse como alternativa a la interfaz de usuario de AEM. La interfaz admite comandos HEAD y GET. Se puede utilizar para generar el informe CRA y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

Las siguientes direcciones URL están disponibles para el acceso HTTP, donde `<host>` es el nombre de host y el puerto, si es necesario, del servidor en el que está instalado CRA:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` para formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` para formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` para formato TSV

### Ejecución de una solicitud HTTP {#executing-http-request}

La interfaz HTTP puede utilizarse en diversos métodos.

Una forma sencilla es abrir una ficha de navegador en el mismo navegador en el que ya ha iniciado sesión en AEM como administrador. Puede introducir la dirección URL en la ficha del explorador y mostrar o descargar los resultados en el explorador.

También puede utilizar una herramienta de línea de comandos como `curl` o `wget` como así también cualquier aplicación cliente HTTP. Cuando no utilice una ficha de explorador con una sesión autenticada, debe proporcionar un nombre de usuario y una contraseña de administración como parte del comentario. A continuación se muestra un ejemplo de cómo se puede realizar esto:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`

### Encabezados y parámetros {#http-headers-and-parameters}

Esta interfaz utiliza los siguientes encabezados HTTP:

* `Cache-Control: max-age=<seconds>`:: Especifique la duración de la actualización de la caché en segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`:: Indica que el servidor debe responder asincrónicamente. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1).)

Los siguientes parámetros de consulta HTTP están disponibles para determinar cuándo es posible que los encabezados HTTP no se utilicen fácilmente:

* `max-age` (número, opcional): Especifique la duración de la actualización de la caché en segundos. Este número debe ser 0 o bueno. La duración de la actualización predeterminada es de 86400 segundos, lo que significa que sin este parámetro o el encabezado correspondiente se utilizará una nueva caché para servir solicitudes durante 24 horas antes de que se deba volver a generar el informe. El uso `max-age=0` fuerza la eliminación de la caché e inicia una regeneración del informe. Inmediatamente después de esta solicitud, la duración de la frescura se restablecerá al valor anterior distinto de cero.
* `respond-async` (booleano, opcional): Especifique que la respuesta se debe proporcionar de forma asíncrona. Si se utiliza `respond-async=true` cuando la caché está obsoleta, el servidor devolverá una respuesta de `202 Accepted, processing cache` sin esperar a que se genere el informe y se actualice la caché. Si la caché está fresca, este parámetro no tiene ningún efecto. El valor predeterminado es `false`, lo que significa que sin este parámetro o el encabezado correspondiente, el servidor responderá sincrónicamente, lo que puede requerir una cantidad de tiempo considerable y un ajuste del tiempo de respuesta máximo para el cliente HTTP.

Cuando están presentes tanto un encabezado HTTP como el parámetro de consulta correspondiente, el parámetro de consulta tendrá prioridad.

Una manera sencilla de iniciar la generación del informe a través de la interfaz HTTP es con el siguiente comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`

Una vez realizada una solicitud, el cliente no necesita permanecer activo para que se genere el informe. La generación de informes se puede iniciar con un cliente mediante una solicitud HTTP GET y, una vez generado el informe, se puede ver desde la caché en otro cliente o desde la herramienta CSV en la interfaz de usuario de AEM.

### Respuestas (#http-response)

Los siguientes valores de respuesta son posibles:

* `200 OK`:: La respuesta contiene los hallazgos del detector de patrones que se generaron durante la duración de frescura de la caché.
* `202 Accepted, processing cache`:: Se proporcionan respuestas asincrónicas para indicar que la caché estaba obsoleta y que se está realizando una actualización.
* `400 Bad Request`:: Indica que se produjo un error con la solicitud. Un mensaje en formato Detalles del problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) proporciona más detalles.
* `401 Unauthorized`:: No se autorizó la solicitud.
* `500 Internal Server Error`:: Indica que se ha producido un error de servidor interno. Un mensaje en formato Detalles del problema proporciona más detalles.
* `503 Service Unavailable`:: Indica que el servidor está ocupado con otra respuesta y no puede atender esta solicitud de forma oportuna. Esto solo sucede cuando se realizan solicitudes sincrónicas. Un mensaje en formato Detalles del problema proporciona más detalles.

## Ajuste de duración de caché {#cache-adjustment}

La duración predeterminada de la caché de CRA es de 24 horas. Con la opción de actualizar un informe y regenerar la caché, tanto en la interfaz de usuario como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del CRA. Si el tiempo de generación de informes es particularmente largo para la instancia de AEM, puede que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de la caché se almacena como la `maxCacheAge` propiedad en el siguiente nodo de repositorio:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante la interfaz CRX/DE Lite a AEM.

## Visualización del informe en instancias de AEM 6.1 {#aem-instances-report}

Siga los pasos a continuación para descargar el informe CSV de Adobe Experience Manager (AEM) 6.1:

1. Vaya a **Adobe Experience Manager Web ConsoleConfiguración** mediante `https://serveraddress:serverport/system/console/configMgr`.

1. Seleccione la ficha **Estado** y busque Detector **de** patrones en la lista desplegable, como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Puede descargar el informe de resumen en una carpeta zip o en formato JSON.


