---
title: Uso del analizador de prácticas recomendadas
description: Aprenda a utilizar el Analizador de prácticas recomendadas para comprender la preparación de la actualización.
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: 951f7fb56d1d8a3285973fda945cbc21f310925f
workflow-type: tm+mt
source-wordcount: '2796'
ht-degree: 37%

---

# Uso del analizador de prácticas recomendadas {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Uso de Best Practices Analyzer"
>abstract="Revise la documentación para utilizar Best Practices Analyzer (anteriormente Cloud Readiness Analyzer) y el informe generado. El informe del Analizador de prácticas recomendadas se utiliza para obtener una comprensión de alto nivel de la preparación general para la actualización."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Seminario web] Presentación de las herramientas para acelerar el recorrido a Adobe Experience Manager as a Cloud Service"

## Consideraciones importantes sobre el uso del Analizador de prácticas recomendadas {#imp-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar el Analizador de prácticas recomendadas (BPA):

* El informe de BPA se ha creado a partir de los resultados de [Pattern Detector](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html) de Adobe Experience Manager (AEM). La versión de Pattern Detector utilizada por BPA se incluye en el paquete de instalación de BPA.

* Solo el usuario **admin** o un usuario del grupo **administradores** pueden ejecutar BPA.

* BPA es compatible con instancias de AEM con la versión 6.1 y posteriores.

  >[!NOTE]
  >Consulte [Instalar en AEM 6.1](#installing-on-aem61) para conocer los requisitos especiales para instalar BPA en AEM 6.1.

* BPA se puede ejecutar en cualquier entorno, pero se prefiere que se ejecute en un entorno *Stage*.

  >[!NOTE]
  >Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar el BPA en un entorno *Stage* lo más cercano posible al entorno *Production* en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de *Author* de producción.

* La generación del contenido de los informes de BPA puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores.

* Debido al tiempo considerable que puede ser necesario para generar el contenido del informe, se generan mediante un proceso en segundo plano y se guardan en la caché. Ver y descargar el informe debería ser relativamente rápido, ya que utiliza la caché de contenido hasta que caduque o hasta que el informe se actualice de forma explícita. Durante la generación del contenido del informe, puede cerrar la pestaña del explorador y regresar más tarde para ver el informe una vez que su contenido esté disponible en la caché.

## Disponibilidad {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Descargar Best Practices Analyzer"
>abstract="Best Practices Analyzer se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM)."

Best Practices Analyzer se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en la instancia de origen de Adobe Experience Manager (AEM).

>[!NOTE]
>Descargue el Analizador de prácticas recomendadas desde el portal [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividad del entorno de Source {#source-environment-connectivity}

Es posible que la instancia de AEM de origen se esté ejecutando detrás de un cortafuegos donde solo puede llegar a ciertos hosts que se han añadido a una Lista de permitidos. Para cargar correctamente el informe generado por BPA en Cloud Acceleration Manager, es necesario poder acceder a los siguientes extremos desde la instancia que ejecuta AEM:

* El servicio de almacenamiento del blob de Azure: `casstorageprod.blob.core.windows.net`


## Visualización del informe del Analizador de prácticas recomendadas {#viewing-report}

### Adobe Experience Manager 6.3.0 y versiones posteriores {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="Carga automática del informe del Analizador de prácticas recomendadas en CAM"
>abstract="Proporcione la clave de carga de BPA para cargar automáticamente el informe de BPA generado en Cloud Acceleration Manager (CAM)."

Siga esta sección para obtener información sobre la vista del informe Analizador de prácticas recomendadas:

1. Seleccione Adobe Experience Manager y vaya a herramientas > **Operaciones** > **Analizador de prácticas recomendadas**.

   ![Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Haga clic en **Generar informe** para ejecutar el Analizador de prácticas recomendadas.

   ![Generar informe](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

>[!NOTE]
> A partir de la versión 2.1.54 de BPA, se ha introducido una nueva función para obtener la puntuación de Lighthouse.


1. Después de hacer clic en **Generar informe**, aparecerá una ventana emergente solicitando la URL del sitio público de AEM para la puntuación de Lighthouse. El usuario debe introducir una URL válida en el campo proporcionado.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/bpa_popup_url.png)

   1. Si la dirección URL es válida, se mostrará un mensaje de éxito.

      ![imagen](/help/journey-migration/best-practices-analyzer/assets/valid_url.png)

   1. Si la dirección URL no es válida, se mostrará un mensaje de error.

      ![imagen](/help/journey-migration/best-practices-analyzer/assets/invalid_url.png)

1. Proporcione la clave de carga de BPA para cargar automáticamente el informe de BPA generado en [Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md). Para obtener la clave de carga, vaya al [Análisis de prácticas recomendadas en CAM](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

   ![Establecer clave de carga de BPA](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>Tiene la opción de omitir la carga automática a CAM al seleccionar **Omitir la carga automática de informe a CAM**. Si decide omitir, deberá descargar manualmente el informe de BPA como archivo de valor separado por comas y, a continuación, cargar el archivo en CAM. Se recomienda utilizar la opción de clave de carga, ya que optimiza la operación.

>[!IMPORTANT]
>Cuando se carga manualmente en CAM, el tamaño de los informes está restringido a aproximadamente 200 MB. Para informes más grandes, deberá aprovechar la carga automática.

1. El botón **Generate** se activa cuando se proporciona una clave válida. Haga clic en **Generar** para iniciar la generación del informe.

   ![Generar informe](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. Mientras el BPA genera el informe, puede ver el progreso realizado por la herramienta en la pantalla. Muestra el progreso en términos de porcentaje completado. También muestra el número de elementos analizados y el número de conclusiones encontradas.

   ![Generando informe](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>La marca de tiempo de caducidad de la clave de carga de BPA se muestra en la esquina superior derecha. Debe renovar la clave de carga de BPA cuando esté cerca de expirar. Para renovar la clave, puede hacer clic en **Renovar** para ir a CAM y renovar la clave.

1. Una vez generado el informe de BPA, muestra un resumen y la cantidad de conclusiones en un formato de tabla organizado por el tipo de búsqueda y el nivel de importancia. Para obtener más detalles sobre una búsqueda determinada, puede hacer clic en el número que corresponda al tipo de búsqueda de la tabla.

   ![Resumen del informe](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Tiene la opción de descargar el informe en formato de valores separados por comas (CSV) haciendo clic en **Exportar a CSV**. También tiene la opción de ver el informe en CAM haciendo clic en **Ir a CAM**. Esto lo llevará a la página [Análisis de prácticas recomendadas](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis) en CAM.

Puede forzar al BPA a borrar su caché y regenerar el informe haciendo clic en **Actualizar informe**.

![Actualizar informe](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. Si la caché caduca, tiene la opción de ver el último informe generado en CAM haciendo clic en **Ver el último informe generado en CAM** o iniciar una nueva generación de informes haciendo clic en **Generar nuevo informe**.

![Ningún informe](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### Uso de filtros en el informe del Analizador de prácticas recomendadas {#bpa-filters}

Para filtrar los hallazgos relacionados con [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), siga los pasos a continuación:

1. Haga clic en el icono del carril izquierdo en el lado izquierdo de la página. Se mostrará el **filtro ACS Commons**. Haga clic en **ACS Commons Filter** para mostrar la casilla de verificación interactiva como se muestra en la imagen siguiente.

   ![Filtro ACS Commons](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >El icono del carril izquierdo solo aparecerá si el BPA detecta el uso de ACS Commons.

1. Anule la selección del cuadro para filtrar todos los resultados relacionados con ACS Commons. Debería ver **Recuento de búsquedas filtradas** en el informe como se muestra en la siguiente imagen. El filtro también se aplica al informe cuando se exporta en formato de valores separados por comas (CSV).

   ![Recuento de búsquedas filtradas](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >No se deben ignorar los hallazgos de ACS Commons. Consulte [documentación](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) para determinar la compatibilidad con AEM as a Cloud Service.

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Interpretación del informe del Analizador de prácticas recomendadas {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Interpretación del informe del Analizador de prácticas recomendadas"
>abstract="Existen dos opciones para ver los resultados de los informes de BPA: IU y CSV. Cuando la herramienta Best Practices Analyzer se ejecuta en la instancia de AEM, el informe IU se muestra en los resultados de la ventana de las herramientas. El formato CSV del informe incluye información que se genera a partir de los resultados de Pattern Detector, ordenados y organizados por tipo de categoría, subtipo y nivel de importancia."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=es#analysis-report" text="Revisar el informe de Best Practices Analyzer"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=es" text="Explicación de las categorías del informe del Analizador de prácticas recomendadas"

Cuando la herramienta Analizador de prácticas recomendadas se ejecuta en la instancia de AEM, el informe se muestra en los resultados de la ventana de herramientas.

El formato del informe es el siguiente:

* **Información general del informe**: información sobre el informe que incluye lo siguiente:
   * **Hora del informe**: el horario en que se generó el contenido del informe y se puso a disposición por primera vez.
   * **Hora de caducidad**: cuando caduque la caché de contenido del informe.
   * **Período de tiempo de generación**: tiempo empleado por el proceso de generación de contenido del informe.
   * **Recuento de búsqueda**: número total de conclusiones incluidas en el informe.
* **Información general del sistema**: Información sobre el sistema AEM en el que se ejecutó el BPA.
* **Búsqueda de categorías**: varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: nombre de la categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción.

>[!NOTE]
>Para obtener más información sobre cada categoría de búsqueda, consulte [Categorías de Pattern Detector](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=es).

Siga la tabla siguiente para comprender los niveles de importancia:

| Importancia | Descripción |
|--- |--- |
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este resultado es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL | Es probable que este resultado sea un problema de actualización que se deba abordar. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |

## Interpretación del informe CSV del analizador de prácticas recomendadas {#cra-csv-report}

Al hacer clic en la opción **CSV** desde la instancia de AEM, el formato CSV del informe Analizador de prácticas recomendadas se crea desde la caché de contenido y se devuelve al explorador. Según la configuración del explorador, este informe se descarga automáticamente como archivo con el nombre predeterminado `results.csv`.

Si la caché ha caducado, el informe se regenera antes de crear y descargar el archivo CSV.

El formato CSV del informe incluye información que se genera a partir de los resultados de Pattern Detector, ordenados y organizados por tipo de categoría, subtipo y nivel de importancia. Su formato es adecuado para visualizarlo y editarlo en una aplicación como Microsoft Excel. Su finalidad es proporcionar toda la información de búsqueda en un formato repetible que pueda resultar útil al comparar los informes a lo largo del tiempo para medir el progreso.

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

El BPA proporciona una interfaz HTTP que puede utilizarse como alternativa a su interfaz de usuario en AEM. La interfaz admite comandos HEAD y GET. Se puede utilizar para generar el informe de BPA y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

Las siguientes direcciones URL están disponibles para el acceso HTTP, donde `<host>` es el nombre de host y el puerto, si es necesario, del servidor en el que está instalado el BPA:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` para el formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` para el formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` para el formato TSV

### Ejecución de una solicitud HTTP {#executing-http-request}

La interfaz HTTP puede utilizarse en diversos métodos.

Una forma sencilla es abrir una pestaña en el mismo explorador en el que ya ha iniciado sesión en AEM como administrador. Puede escribir la dirección URL en la pestaña del explorador y mostrar o descargar los resultados.

También puede utilizar una herramienta de línea de comandos como `curl` o `wget` y cualquier aplicación cliente HTTP. Cuando no utilice una pestaña de explorador con una sesión autenticada, debe proporcionar el nombre de usuario y la contraseña de administración como parte del comentario.

A continuación se muestra un ejemplo de cómo se puede realizar esto:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`.

### Encabezados y parámetros {#http-headers-and-parameters}

Esta interfaz utiliza los siguientes encabezados HTTP:

* `Cache-Control: max-age=<seconds>`: especifica la duración de la actualización de la caché en segundos. (Consulte [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8).)
* `Prefer: respond-async`: especifica que el servidor debe responder asincrónicamente. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)).
* `Prefer: return=minimal`: especifica que el servidor debe devolver una respuesta mínima. (Consulte [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)).

Los siguientes parámetros de consulta HTTP están disponibles para determinar cuándo es posible que los encabezados HTTP no se utilicen fácilmente:

* `max-age` (número, opcional): especifica la duración de la actualización de la caché en segundos. Este número debe ser 0 o más. La duración de la actualización predeterminada es de 86400 segundos. Sin este parámetro o el encabezado correspondiente, se utiliza una nueva caché para servir solicitudes durante 24 horas, momento en el que se debe volver a generar la caché. Si se utiliza `max-age=0`, se forzará la eliminación de la caché e se iniciará una regeneración del informe, utilizando la duración de actualización anterior distinta de cero para la caché recién generada.
* `respond-async` (booleano, opcional): especifica que la respuesta se debe proporcionar asincrónicamente. Si se usa `respond-async=true` cuando la caché está obsoleta, el servidor devolverá una respuesta de `202 Accepted` sin esperar a que se actualice la caché y se genere el informe. Si la caché es nueva, este parámetro no tiene ningún efecto. El valor predeterminado es `false`. Sin este parámetro o el encabezado correspondiente, el servidor responderá sincrónicamente, lo que puede requerir una cantidad de tiempo considerable y un ajuste del tiempo de respuesta máximo para el cliente HTTP.
* `may-refresh-cache` (booleano, opcional): especifica que el servidor puede actualizar la caché en respuesta a una solicitud si la caché actual está vacía, obsoleta o pronto estará obsoleta. Si `may-refresh-cache=true`, o si no se especifica, el servidor puede iniciar una tarea en segundo plano que invocará Pattern Detector y actualizará la caché. Si `may-refresh-cache=false`, el servidor no iniciará ninguna tarea de actualización que de otra manera se habría realizado si la caché está vacía o obsoleta, en cuyo caso el informe está vacío. Este parámetro no afectará a ninguna tarea de actualización que ya esté en proceso.
* `return-minimal` (booleano, opcional): especifica que la respuesta del servidor solo debe incluir el estado que contiene la indicación de progreso y el estado de caché en formato JSON. Si es `return-minimal=true`, el cuerpo de la respuesta se limita al objeto de estado. Si `return-minimal=false`, o si no se especifica, se proporciona una respuesta completa.
* `log-findings` (booleano, opcional): especifica que el servidor debe registrar el contenido de la caché cuando se genere o actualice por primera vez. Cada hallazgo de la caché de se registra como una cadena JSON. Este registro se producirá solamente si `log-findings=true` y la solicitud genera una nueva caché.

Cuando están presentes tanto un encabezado HTTP como el parámetro de consulta correspondiente, el parámetro de consulta tendrá prioridad.

Una manera sencilla de iniciar la generación del informe a través de la interfaz HTTP es con el siguiente comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Una vez realizada una solicitud, el cliente no necesita permanecer activo para que se genere el informe. La generación de informes se puede iniciar con un cliente mediante una petición HTTP GET y, una vez generado el informe, se puede ver desde la caché con otro cliente o con la herramienta BPA en la interfaz de usuario de AEM.

### Respuestas {#http-responses}

Los siguientes valores de respuesta son posibles:

* `200 OK`: indica que la respuesta contiene los resultados del detector de patrones que se generaron durante la duración de la actualización de la caché.
* `202 Accepted`: se usa para indicar que la caché está obsoleta. Cuando `respond-async=true` y `may-refresh-cache=true` esta respuesta indica que hay una tarea de actualización en curso. Cuando `may-refresh-cache=false` esta respuesta simplemente indica que la caché está obsoleta.
* `400 Bad Request`: indica que se produjo un error con la solicitud. Un mensaje en formato Detalles del problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) proporciona más detalles.
* `401 Unauthorized`: indica que la solicitud no se autorizó.
* `500 Internal Server Error`: indica que se ha producido un error de servidor interno. El mensaje en formato Detalles del problema proporciona más detalles.
* `503 Service Unavailable`: indica que el servidor está ocupado con otra respuesta y no puede atender esta solicitud de forma oportuna. Esto solo es probable cuando se realizan solicitudes sincrónicas. El mensaje en formato Detalles del problema proporciona más detalles.

## Información del administrador

### Ajuste de duración de caché {#cache-adjustment}

La duración predeterminada de la caché de BPA es de 24 horas. Con la opción para actualizar un informe y regenerar la caché, tanto en la instancia de AEM como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del BPA. Si el tiempo de generación de informes es especialmente largo para la instancia de AEM, es posible que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de la caché se almacena como la `maxCacheAge` propiedad en el siguiente nodo de repositorio:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante CRX/DE Lite.

### Instalación en AEM 6.1 {#installing-on-aem61}

BPA utiliza una cuenta de usuario de servicio del sistema denominada `repository-reader-service` para ejecutar Pattern Detector. Esta cuenta está disponible en AEM 6.2 y posteriores. En AEM 6.1, esta cuenta debe crearse *antes de* la instalación de BPA siguiendo los pasos siguientes:

1. Siga las instrucciones en [Crear un nuevo usuario de servicio](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) para crear un usuario. Establezca el UserID en `repository-reader-service` y deje la ruta intermedia vacía y luego haga clic en la marca de verificación verde.

2. Siga las instrucciones en [Administrar usuarios y grupos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups), específicamente las instrucciones para Añadir usuarios a un grupo para agregar el `repository-reader-service` usuario al `administrators` grupo.

3. Instale el paquete BPA mediante el Administrador de paquetes en la instancia de origen de AEM. (Esto agregará la modificación de configuración necesaria a la configuración de ServiceUserMapper para el usuario del servicio `repository-reader-service` del sistema).
