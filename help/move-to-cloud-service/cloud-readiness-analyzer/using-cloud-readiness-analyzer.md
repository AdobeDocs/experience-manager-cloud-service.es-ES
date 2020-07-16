---
title: Uso de Cloud Readiness Analyzer
description: Uso de Cloud Readiness Analyzer
translation-type: ht
source-git-commit: a0e58c626f94b778017f700426e960428b657806
workflow-type: ht
source-wordcount: '1871'
ht-degree: 100%

---


# Uso de Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## Consideraciones importantes sobre el uso de Cloud Readiness Analyzer {#imp-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar el Cloud Readiness Analyzer (CRA):

* El informe de CRA se crea con los resultados de [Pattern Detector](https://docs.adobe.com/content/help/es-ES/experience-manager-65/deploying/upgrading/pattern-detector.html) de Adobe Experience Manager (AEM). La versión de Pattern Detector utilizada por CRA se incluye en el paquete de instalación de CRA.

* Solo el usuario **administrador** o un usuario del grupo de **administradores** pueden ejecutar el CRA.

* CRA se admite en instancias de AEM con la versión 6.1 o posterior.

   >[!NOTE]
   > Consulte [Instalar en AEM 6.1](#installing-on-aem61) para conocer los requisitos especiales para instalar CRA en AEM 6.1.

* CRA puede ejecutarse en cualquier entorno, pero se prefiere que sea en un entorno de *ensayo*.

   >[!NOTE]
   >Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar el CRA en un entorno de *Author* lo más cercano posible al entorno de *producción* en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de *Author* de producción.

* La generación del contenido de los informes CRA puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores.

* Debido al tiempo considerable que puede ser necesario para generar el contenido del informe, se generan mediante un proceso en segundo plano y se guardan en la caché. Ver y descargar el informe debería ser relativamente rápido, ya que utiliza la caché de contenido hasta que caduque o hasta que el informe se actualice de forma explícita. Durante la generación del contenido del informe, puede cerrar la pestaña del explorador y regresar más tarde para ver el informe una vez que su contenido esté disponible en la caché.

## Disponibilidad {#availability}

Cloud Readiness Analyzer se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue Cloud Readiness Analyzer del portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html).

## Visualización del informe de Cloud Readiness Analyzer {#viewing-report}

### Adobe Experience Manager 6.3.0 y versiones posteriores {#aem-later-versions}

Siga esta sección para obtener información sobre la vista del informe de Cloud Readiness Analyzer:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Cloud Readiness Analyzer**.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Una vez que haga clic en **Cloud Readiness Analyzer**, la herramienta inicia la generación del informe y lo muestra cuando está disponible.

   >[!NOTE]
   >Se tiene que desplazar hacia abajo de la página para ver el informe completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. Una vez generado y mostrado el informe de CRA, tiene la opción de descargarlo en formato de valores separados por comas (CSV) haciendo clic en **CSV**, como se muestra en la imagen siguiente.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >Puede forzar el CRA para que borre su caché y vuelva a generar el informe haciendo clic en **Actualizar informe**.

### Adobe Experience Manager 6.2 y 6.1 {#aem-specific-versions}

La herramienta Cloud Readiness Analyzer está limitada en Adobe Experience Manager 6.2 a un vínculo que genera y descarga el informe CSV.

Para Adobe Experience Manager 6.1, la herramienta no funciona y solo se puede utilizar la interfaz HTTP.

>[!NOTE]
>En todas las versiones, Pattern Detector puede ejecutarse de forma independiente.

## Interpretación del informe de Cloud Readiness Analyzer {#cra-report}

Cuando la herramienta Cloud Readiness Analyzer se ejecuta en la instancia de AEM, el informe se muestra en los resultados de la ventana de las herramientas.

El formato del informe es el siguiente:

* **Información general del informe**: información sobre el informe que incluye lo siguiente:
   * **Hora del informe**: el horario en que se generó el contenido del informe y se puso a disposición por primera vez.
   * **Hora de caducidad**: cuando caduque la caché de contenido del informe.
   * **Período de tiempo de generación**: tiempo empleado por el proceso de generación de contenido del informe.
   * **Recuento de búsqueda**: número total de conclusiones incluidas en el informe.
* **Información general del sistema**: datos sobre el sistema AEM en el que se ejecutó el CRA.
* **Búsqueda de categorías**: varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: nombre de la categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción.

Siga la tabla siguiente para comprender los niveles de importancia:

| Importancia | Descripción |
|--- |--- |
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este resultado es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL | Es probable que este resultado sea un problema de actualización que se deba abordar. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |


## Interpretación del informe CSV de Cloud Readiness Analyzer {#cra-csv-report}

Al hacer clic en la opción **CSV** desde la instancia de AEM, el formato CSV de Cloud Readiness Analyzer se crea desde la caché de contenido y se devuelve al explorador. Según la configuración del explorador, este informe se descargará automáticamente como archivo con un nombre predeterminado de `results.csv`.

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

El CRA proporciona una interfaz HTTP que puede utilizarse como alternativa a su interfaz de usuario en AEM. La interfaz admite comandos HEAD y GET. Se puede utilizar para generar el informe CRA y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

Las siguientes direcciones URL están disponibles para el acceso HTTP, donde `<host>` es el nombre de host y el puerto, si es necesario, del servidor en el que está instalado CRA:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` para el formato JSON
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` para el formato CSV
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` para el formato TSV

### Ejecución de una petición HTTP {#executing-http-request}

La interfaz HTTP puede utilizarse en diversos métodos.

Una forma sencilla es abrir una pestaña en el mismo explorador en el que ya ha iniciado sesión en AEM como administrador. Puede escribir la dirección URL en la pestaña del explorador y mostrar o descargar los resultados.

También puede utilizar una herramienta de línea de comandos como `curl` o `wget` como así también cualquier aplicación cliente HTTP. Cuando no utilice una pestaña de explorador con una sesión autenticada, debe proporcionar el nombre de usuario y la contraseña de administración como parte del comentario.

A continuación se muestra un ejemplo de cómo se puede realizar esto:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`.

### Encabezados y parámetros {#http-headers-and-parameters}

Esta interfaz utiliza los siguientes encabezados HTTP:

* `Cache-Control: max-age=<seconds>`: especifica la duración de la actualización de la caché en segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: indica que el servidor debe responder asincrónicamente. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).

Los siguientes parámetros de consulta HTTP están disponibles para determinar cuándo es posible que los encabezados HTTP no se utilicen fácilmente:

* `max-age` (número, opcional): especifica la duración de la actualización de la caché en segundos. Este número debe ser 0 o más. La duración de la actualización predeterminada es de 86400 segundos, lo que significa que sin este parámetro o el encabezado correspondiente se utilizará una nueva caché para servir solicitudes durante 24 horas antes de que se deba volver a generar el informe. El uso de `max-age=0` fuerza a la eliminación de la caché e inicia una regeneración del informe. Inmediatamente después de esta solicitud, la duración se restablecerá al valor anterior distinto de cero.
* `respond-async` (booleano, opcional): especifique que la respuesta se debe proporcionar de forma asíncrona. Si se utiliza `respond-async=true` cuando la caché está obsoleta, el servidor devolverá una respuesta de `202 Accepted, processing cache` sin esperar a que se genere el informe y se actualice la caché. Si la caché es nueva, este parámetro no tiene ningún efecto. El valor predeterminado es `false`, lo que significa que sin este parámetro o el encabezado correspondiente, el servidor responderá sincrónicamente, lo que puede requerir una cantidad de tiempo considerable y un ajuste del tiempo de respuesta máximo para el cliente HTTP.

Cuando están presentes tanto un encabezado HTTP como el parámetro de consulta correspondiente, el parámetro de consulta tendrá prioridad.

Una manera sencilla de iniciar la generación del informe a través de la interfaz HTTP es con el siguiente comando:
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`.

Una vez realizada una solicitud, el cliente no necesita permanecer activo para que se genere el informe. La generación de informes se puede iniciar con un cliente mediante una petición HTTP GET y, una vez generado el informe, se puede ver desde la caché de otro cliente o desde la herramienta CSV en la interfaz de usuario en AEM.

### Respuestas {#http-responses}

Los siguientes valores de respuesta son posibles:

* `200 OK`: la respuesta contiene los resultados del detector de patrones que se generaron durante la duración de la actualización de la caché.
* `202 Accepted, processing cache`: se proporcionan respuestas asincrónicas para indicar que la caché estaba obsoleta y que se está realizando una actualización.
* `400 Bad Request`: indica que se produjo un error con la solicitud. Un mensaje en formato Detalles del problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) para obtener más información.
* `401 Unauthorized`: no se autorizó la solicitud.
* `500 Internal Server Error`: indica que se ha producido un error de servidor interno. El mensaje en formato Detalles del problema proporciona más detalles.
* `503 Service Unavailable`: indica que el servidor está ocupado con otra respuesta y no puede atender esta solicitud de forma oportuna. Esto solo es probable cuando se realizan solicitudes sincrónicas. El mensaje en formato Detalles del problema proporciona más detalles.

## Información del administrador

### Ajuste de la duración de caché {#cache-adjustment}

La duración predeterminada de la caché de CRA es de 24 horas. Con la opción para actualizar un informe y regenerar la caché, tanto en la instancia de AEM como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del CRA. Si el tiempo de generación de informes es particularmente largo para la instancia de AEM, puede que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de la caché se almacena como la `maxCacheAge` propiedad en el siguiente nodo de repositorio:
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante CRX/DE Lite.

### Instalar en AEM 6.1 {#installing-on-aem61}

CRA utiliza una cuenta de usuario de servicio del sistema llamada `repository-reader-service` para ejecutar el detector de patrones. Esta cuenta está disponible en AEM 6.2 y posteriores. En AEM 6.1, esta cuenta debe crearse *antes* de la instalación de CRA siguiendo los pasos siguientes:

1. Siga las instrucciones en [Crear un nuevo usuario de servicio](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) para crear un usuario. Establezca el UserID en `repository-reader-service` y deje la ruta intermedia vacía y luego haga clic en la marca de verificación verde.

2. Siga las instrucciones en [Administrar usuarios y grupos](https://docs.adobe.com/content/help/en/experience-manager-65/administering/security/security.html#managing-users-and-groups), específicamente las instrucciones para Añadir usuarios a un grupo para agregar el `repository-reader-service` usuario al `administrators` grupo.

3. Instale el paquete de CRA mediante el Administrador de paquetes en la instancia de AEM de origen. (Esto agregará la modificación de configuración necesaria a la configuración de ServiceUserMapper para el usuario del servicio `repository-reader-service` del sistema).
