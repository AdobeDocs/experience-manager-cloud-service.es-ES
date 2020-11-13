---
title: Uso del Analizador de optimizaciones
description: Uso del Analizador de optimizaciones
translation-type: tm+mt
source-git-commit: 07180809ff8b4a42a07eb9c691ab7a99262742ec
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 47%

---


# Uso del Analizador de optimizaciones {#using-best-practices-analyzer}

## Consideraciones importantes sobre el uso del Analizador de optimizaciones {#imp-considerations}

Siga la sección siguiente para comprender las consideraciones importantes para ejecutar el Analizador de optimizaciones (BPA):

* The BPA report is built using the output of the Adobe Experience Manager (AEM) [Pattern Detector](https://docs.adobe.com/content/help/es-ES/experience-manager-65/deploying/upgrading/pattern-detector.html). La versión del detector de patrones utilizado por BPA se incluye en el paquete de instalación de BPA.

* BPA may only be run by the **admin** user or a user in the **administrators** group.

* BPA se admite en instancias de AEM con la versión 6.1 o superior.

   >[!NOTE]
   > Please see [Installing on AEM 6.1](#installing-on-aem61) for special requirements for installing BPA on AEM 6.1.

* BPA can run on any environment, but it is preferred to have it run on a *Stage* environment.

   >[!NOTE]
   >In order to avoid an impact on business critical instances, it is recommended that you run BPA on an *Author* environment that is as close as possible to the *Production* environment in the areas of customizations, configurations, content and user applications. Como alternativa, se puede ejecutar en un clon del entorno de *Author* de producción.

* La generación del contenido del informe BPA puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores.

* Debido al tiempo considerable que puede ser necesario para generar el contenido del informe, se generan mediante un proceso en segundo plano y se guardan en la caché. Ver y descargar el informe debería ser relativamente rápido, ya que utiliza la caché de contenido hasta que caduque o hasta que el informe se actualice de forma explícita. Durante la generación del contenido del informe, puede cerrar la pestaña del explorador y regresar más tarde para ver el informe una vez que su contenido esté disponible en la caché.

## Disponibilidad {#availability}

El Analizador de optimizaciones se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Download the Best Practices Analyzer from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html) portal.

## Visualización del informe del Analizador de optimizaciones {#viewing-report}

### Adobe Experience Manager 6.3.0 y versiones posteriores {#aem-later-versions}

Siga esta sección para obtener información sobre la vista del informe del Analizador de optimizaciones:

1. Select Adobe Experience Manager and navigate to tools -> **Operations** -> **Best Practices Analyzer**.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic1.png)

1. Haga clic en **Generar informe** para ejecutar el Analizador de optimizaciones.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic2.png)

1. Mientras el BPA está generando el informe, puede ver el progreso realizado por la herramienta en la pantalla. Muestra el número de elementos analizados y también el número de hallazgos encontrados.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic3.png)


1. Una vez generado el informe BPA, muestra un resumen y el número de hallazgos en un formato de tabla organizado por el tipo de búsqueda y el nivel de importancia. Para obtener más detalles sobre una búsqueda en particular, puede hacer clic en el número que corresponde al tipo de búsqueda en la tabla.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic4.png)

   La acción anterior se desplazará automáticamente a la ubicación de esa búsqueda en el informe.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic5.png)

1. You have the option of downloading the report in a comma-separated values (CSV) format by clicking on **CSV**, as shown in the figure below.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >You may force the BPA to clear its cache and regenerate the report by clicking **Refresh Report**.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >Mientras el informe se está regenerando, muestra el progreso en términos de porcentaje completado como se muestra en la imagen a continuación.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/BPA_pic8.png)


### Adobe Experience Manager 6.2 y 6.1 {#aem-specific-versions}

La herramienta Analizador de optimizaciones está limitada en Adobe Experience Manager 6.2 a un vínculo que genera y descarga el informe CSV.

Para Adobe Experience Manager 6.1, la herramienta no funciona y solo se puede utilizar la interfaz HTTP.

>[!NOTE]
>En todas las versiones, Pattern Detector puede ejecutarse de forma independiente.

## Interpretación del informe del Analizador de optimizaciones {#cra-report}

Cuando la herramienta Analizador de optimizaciones se ejecuta en la instancia de AEM, el informe se muestra como resultados en la ventana de herramientas.

El formato del informe es el siguiente:

* **Información general del informe**: información sobre el informe que incluye lo siguiente:
   * **Hora del informe**: el horario en que se generó el contenido del informe y se puso a disposición por primera vez.
   * **Hora de caducidad**: cuando caduque la caché de contenido del informe.
   * **Período de tiempo de generación**: tiempo empleado por el proceso de generación de contenido del informe.
   * **Recuento de búsqueda**: número total de conclusiones incluidas en el informe.
* **Información general** del sistema: Información sobre el sistema de AEM en el que se ejecutó el BPA.
* **Búsqueda de categorías**: varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: nombre de la categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción.

>[!NOTE]
>Para obtener más información sobre cada Categoría de búsqueda, consulte Categorías [del detector de](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)patrones.

Siga la tabla siguiente para comprender los niveles de importancia:

| Importancia | Descripción |
|--- |--- |
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este resultado es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL | Es probable que este resultado sea un problema de actualización que se deba abordar. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |


## Interpretación del informe CSV del Analizador de optimizaciones {#cra-csv-report}

When you click the **CSV** option from your AEM instance, the CSV format of the Best Practices Analyzer report is built from the content cache and returned to your browser. Según la configuración del explorador, este informe se descargará automáticamente como archivo con un nombre predeterminado de `results.csv`.

Si la caché ha caducado, el informe se regenerará antes de crear y descargar el archivo CSV.

El formato CSV del informe incluye información que se genera a partir de los resultados de Pattern Detector, ordenados y organizados por tipo de categoría, subtipo y nivel de importancia. Su formato es adecuado para visualizarlo y editarlo en una aplicación como Microsoft Excel. Su finalidad es proporcionar toda la información de búsqueda en un formato repetible que pueda resultar útil al comparar los informes con el paso del tiempo para medir el progreso.

Las columnas del informe de formato CSV son las siguientes:

* **Código**: el código de categoría.
* **Tipo**: el nombre de la categoría.
* **Subtipo**: subtipo de categoría.
* **Importancia**: el nivel de importancia.
* **Identificador**: el identificador principal de la búsqueda.
* **Otros**: información adicional sobre la búsqueda.
* **Mensaje**: el mensaje proporcionado para la búsqueda.
* **MoreInfo**: un vínculo que puede utilizarse para acceder a la ayuda en línea sobre la categoría.
* **Contexto**: una cadena JSON de búsqueda de datos.

El valor &quot;\N&quot; en una columna para una búsqueda individual indica que no se proporcionaron datos.

## Interfaz HTTP {#http-interface}

El BPA proporciona una interfaz HTTP que puede utilizarse como alternativa a su interfaz de usuario dentro de AEM. La interfaz admite comandos HEAD y GET. Puede utilizarse para generar el informe BPA y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

The following URLs are available for HTTP access, where `<host>` is the hostname, and port if necessary, of the server on which the BPA is installed:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` para el formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` para el formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` para el formato TSV

### Ejecución de una petición HTTP {#executing-http-request}

La interfaz HTTP puede utilizarse en diversos métodos.

Una forma sencilla es abrir una pestaña en el mismo explorador en el que ya ha iniciado sesión en AEM como administrador. Puede escribir la dirección URL en la pestaña del explorador y mostrar o descargar los resultados.

También puede utilizar una herramienta de línea de comandos como `curl` o `wget` como así también cualquier aplicación cliente HTTP. Cuando no utilice una pestaña de explorador con una sesión autenticada, debe proporcionar el nombre de usuario y la contraseña de administración como parte del comentario.

A continuación se muestra un ejemplo de cómo se puede realizar esto:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Encabezados y parámetros {#http-headers-and-parameters}

Esta interfaz utiliza los siguientes encabezados HTTP:

* `Cache-Control: max-age=<seconds>`:: Especifica la duración de la actualización de la caché en segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`:: Especifica que el servidor debe responder asincrónicamente. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).
* `Prefer: return=minimal`:: Especifica que el servidor debe devolver una respuesta mínima. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)).

Los siguientes parámetros de consulta HTTP están disponibles para determinar cuándo es posible que los encabezados HTTP no se utilicen fácilmente:

* `max-age` (número, opcional): Especifica la duración de la actualización de la caché en segundos. Este número debe ser 0 o más. La duración de la actualización predeterminada es 86400 segundos. Sin este parámetro o el encabezado correspondiente, se utilizará una nueva caché para atender solicitudes durante 24 horas, momento en el cual se deberá volver a generar la caché. El uso `max-age=0` fuerza la eliminación de la caché e inicia una regeneración del informe, usando la duración de actualización anterior distinta de cero para la caché recién generada.
* `respond-async` (booleano, opcional): Especifica que la respuesta debe proporcionarse de forma asíncrona. Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. Si la caché es nueva, este parámetro no tiene ningún efecto. The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` (booleano, opcional): Especifica que el servidor puede actualizar la caché en respuesta a una solicitud si la caché actual está vacía, obsoleta o pronto estará obsoleta. Si `may-refresh-cache=true`o no se especifica, el servidor puede iniciar una tarea en segundo plano que invoque el detector de patrones y actualice la caché. Si `may-refresh-cache=false` entonces el servidor no iniciará ninguna tarea de actualización que de otro modo se hubiera realizado si la caché está vacía o está obsoleta, en cuyo caso el informe estará vacío. Este parámetro no afectará a ninguna tarea de actualización que ya esté en curso.
* `return-minimal` (booleano, opcional): Especifica que la respuesta del servidor solo debe incluir el estado que contiene la indicación de progreso y el estado de caché en el formato JSON. Si `return-minimal=true`, el cuerpo de respuesta se limitará al objeto status. Si `return-minimal=false`o no se especifica, se proporcionará una respuesta completa.
* `log-findings` (booleano, opcional): Especifica que el servidor debe registrar el contenido de la caché cuando se crea o actualiza por primera vez. Cada búsqueda de la caché se registrará como una cadena JSON. Este registro solo se producirá si `log-findings=true` y la solicitud genera una nueva caché.

Cuando están presentes tanto un encabezado HTTP como el parámetro de consulta correspondiente, el parámetro de consulta tendrá prioridad.

Una manera sencilla de iniciar la generación del informe a través de la interfaz HTTP es con el siguiente comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Una vez realizada una solicitud, el cliente no necesita permanecer activo para que se genere el informe. La generación de informes se puede iniciar con un cliente mediante una solicitud de GET HTTP y, una vez generado el informe, se puede ver desde la caché con otro cliente o con la herramienta BPA en la interfaz de usuario de AEM.

### Respuestas {#http-responses}

Los siguientes valores de respuesta son posibles:

* `200 OK`:: Indica que la respuesta contiene los resultados del detector de patrones que se generaron durante la duración de la actualización de la caché.
* `202 Accepted`:: Se utiliza para indicar que la caché está obsoleta. Cuando `respond-async=true` y `may-refresh-cache=true` esta respuesta indica que hay una tarea de actualización en curso. Cuando `may-refresh-cache=false` esta respuesta indica simplemente que la caché está obsoleta.
* `400 Bad Request`: indica que se produjo un error con la solicitud. A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) provides more details.
* `401 Unauthorized`:: Indica que la solicitud no está autorizada.
* `500 Internal Server Error`: indica que se ha producido un error de servidor interno. El mensaje en formato Detalles del problema proporciona más detalles.
* `503 Service Unavailable`: indica que el servidor está ocupado con otra respuesta y no puede atender esta solicitud de forma oportuna. Esto solo es probable cuando se realizan solicitudes sincrónicas. El mensaje en formato Detalles del problema proporciona más detalles.

## Información del administrador

### Ajuste de la duración de caché {#cache-adjustment}

La duración predeterminada de la caché de BPA es de 24 horas. Con la opción para actualizar un informe y regenerar la caché, tanto en la instancia de AEM como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del BPA. Si el tiempo de generación de informes es particularmente largo para la instancia de AEM, puede que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de la caché se almacena como la `maxCacheAge` propiedad en el siguiente nodo de repositorio:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante CRX/DE Lite.

### Instalar en AEM 6.1 {#installing-on-aem61}

BPA utilizes a system service user account named `repository-reader-service` to execute the Pattern Detector. Esta cuenta está disponible en AEM 6.2 y posteriores. On AEM 6.1, this account must be created *prior to* installation of BPA by taking the following steps:

1. Siga las instrucciones en [Crear un nuevo usuario de servicio](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) para crear un usuario. Establezca el UserID en `repository-reader-service` y deje la ruta intermedia vacía y luego haga clic en la marca de verificación verde.

2. Siga las instrucciones en [Administrar usuarios y grupos](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups), específicamente las instrucciones para Añadir usuarios a un grupo para agregar el `repository-reader-service` usuario al `administrators` grupo.

3. Instale el paquete BPA mediante el Administrador de paquetes en la instancia de AEM de origen. (Esto agregará la modificación de configuración necesaria a la configuración de ServiceUserMapper para el usuario del servicio `repository-reader-service` del sistema).
