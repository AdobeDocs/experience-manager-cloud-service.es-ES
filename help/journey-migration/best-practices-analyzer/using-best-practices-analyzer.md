---
title: Uso del analizador de prácticas recomendadas
description: Aprenda a utilizar el Analizador de prácticas recomendadas para comprender la preparación de la actualización.
exl-id: e8498e17-f55a-4600-87d7-60584d947897
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 45%

---

# Uso del analizador de prácticas recomendadas {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="Uso de Best Practices Analyzer"
>abstract="Revise la documentación para utilizar Best Practices Analyzer (anteriormente Cloud Readiness Analyzer) y el informe generado. El informe de Best Practices Analyzer se utiliza para obtener una comprensión de alto nivel de la preparación general para la actualización."
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Seminario web] Presentación de las herramientas para acelerar el recorrido a Adobe Experience Manager as a Cloud Service"

## Consideraciones importantes sobre el uso del Analizador de prácticas recomendadas {#imp-considerations}

En la sección siguiente se comprenden las consideraciones importantes al ejecutar el Analizador de prácticas recomendadas (BPA):

* El informe de BPA se crea con los resultados de Adobe Experience Manager AEM () [Detector de patrones](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). La versión de Pattern Detector utilizada por BPA se incluye en el paquete de instalación de BPA.

* BPA solo puede ser ejecutado por el **administrador** o un usuario en el **administradores** grupo.

* AEM BPA es compatible con instancias de con la versión 6.1 y posteriores.

  >[!NOTE]
  >Consulte [AEM Instalación en.1](#installing-on-aem61) AEM para los requisitos especiales para la instalación de BPA en la versión 6.1 del.

* BPA puede ejecutarse en cualquier entorno, pero se prefiere que sea en un *Fase* entorno.

  >[!NOTE]
  >Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar BPA en un *Autor* entorno lo más cercano posible al entorno de *Producción* en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de *Author* de producción.

* La generación del contenido de los informes de BPA puede llevar una cantidad de tiempo considerable, de varios minutos a pocas horas. La cantidad de tiempo necesaria depende en gran medida del tamaño y la naturaleza del contenido del repositorio de AEM, la versión de AEM y otros factores.

* Debido al tiempo considerable que puede ser necesario para generar el contenido del informe, se generan mediante un proceso en segundo plano y se guardan en la caché. Ver y descargar el informe debería ser relativamente rápido, ya que utiliza la caché de contenido hasta que caduque o hasta que el informe se actualice de forma explícita. Durante la generación del contenido del informe, puede cerrar la pestaña del explorador y regresar más tarde para ver el informe una vez que su contenido esté disponible en la caché.

## Disponibilidad {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="Descargar Best Practices Analyzer"
>abstract="Best Practices Analyzer se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM)."

Best Practices Analyzer se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en la instancia de origen de Adobe Experience Manager AEM ().

>[!NOTE]
>Descargue el Analizador de prácticas recomendadas de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) portal.

## Visualización del informe del Analizador de prácticas recomendadas {#viewing-report}

### Adobe Experience Manager 6.3.0 y versiones posteriores {#aem-later-versions}

Siga esta sección para obtener información sobre la vista del informe Analizador de prácticas recomendadas:

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Analizador de prácticas recomendadas**.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. Haga clic en **Generar informe** para ejecutar el Analizador de prácticas recomendadas.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. Mientras el BPA genera el informe, puede ver el progreso realizado por la herramienta en la pantalla. Muestra el número de elementos analizados y también el número de conclusiones encontradas.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)

1. Una vez generado el informe de BPA, muestra un resumen y la cantidad de conclusiones en un formato de tabla organizado por el tipo de búsqueda y el nivel de importancia. Para obtener más detalles sobre un hallazgo particular, puede hacer clic en el número que corresponde al tipo de hallazgo en la tabla.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   La acción anterior se desplazará automáticamente a la ubicación de esa búsqueda en el informe.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. Tiene la opción de descargar el informe en formato de valores separados por comas (CSV) haciendo clic en **Exportar a CSV**, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >Puede forzar el BPA para que borre su caché y vuelva a generar el informe haciendo clic en **Actualizar informe**.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >Mientras se regenera el informe, muestra el progreso en términos de porcentaje completado como se muestra en la siguiente imagen.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)

#### Uso de filtros en el informe del Analizador de prácticas recomendadas {#bpa-filters}

Para filtrar los resultados relacionados con [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), siga los pasos a continuación:

1. Haga clic en el icono del carril izquierdo en el lado izquierdo de la página. Se mostrará el **Filtro ACS Commons**. Haga clic en **Filtro ACS Commons** para mostrar la casilla de verificación interactiva como se muestra en la siguiente imagen.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >El icono del carril izquierdo solo aparecerá si el BPA detecta el uso de ACS Commons.

1. Anule la selección del cuadro para filtrar todos los resultados relacionados con ACS Commons. Debería ver una **Recuento de búsqueda filtrada** en el informe como se muestra en la imagen siguiente. El filtro también se aplica al informe cuando se exporta en formato de valores separados por comas (CSV).

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >No se deben ignorar los hallazgos de ACS Commons. Consulte [documentación](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) AEM para determinar la compatibilidad con el as a Cloud Service de la.

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## Interpretación del informe de Best Practices Analyzer {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="Interpretación del informe de Best Practices Analyzer"
>abstract="Existen dos opciones para ver los resultados de los informes de BPA: IU y CSV. Cuando la herramienta Best Practices Analyzer se ejecuta en la instancia de AEM, el informe IU se muestra en los resultados de la ventana de las herramientas. El formato CSV del informe incluye información que se genera a partir de los resultados de Pattern Detector, ordenados y organizados por tipo de categoría, subtipo y nivel de importancia."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=es#analysis-report" text="Revisar el informe de Best Practices Analyzer"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=es" text="Explicación de las categorías del informe de Best Practices Analyzer"

AEM Cuando la herramienta Analizador de prácticas recomendadas se ejecuta en la instancia de la, el informe se muestra en los resultados de la ventana de herramientas.

El formato del informe es el siguiente:

* **Información general del informe**: información sobre el informe que incluye lo siguiente:
   * **Hora del informe**: el horario en que se generó el contenido del informe y se puso a disposición por primera vez.
   * **Hora de caducidad**: cuando caduque la caché de contenido del informe.
   * **Período de tiempo de generación**: tiempo empleado por el proceso de generación de contenido del informe.
   * **Recuento de búsqueda**: número total de conclusiones incluidas en el informe.
* **Información general del sistema** AEM : información sobre el sistema de la en el que se ejecutó el BPA.
* **Búsqueda de categorías**: varias secciones en las que cada una de ellas aborda uno o más resultados de la misma categoría. Cada sección incluye lo siguiente: nombre de la categoría, subtipos, número de búsquedas e importancia, resumen, vínculo a la documentación de la categoría e información de búsqueda individual.

Se asigna un nivel de importancia a cada resultado para indicar una prioridad aproximada para la acción.

>[!NOTE]
>Para obtener más información sobre cada categoría de búsqueda, consulte [Categorías de Pattern Detector](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

Siga la tabla siguiente para comprender los niveles de importancia:

| Importancia | Descripción |
|--- |--- |
| INFORMACIÓN | Esta conclusión se proporciona con fines informativos. |
| CONSEJO | Este resultado es potencialmente un problema de actualización. Se recomienda una investigación más a fondo. |
| PRINCIPAL | Es probable que este resultado sea un problema de actualización que se deba abordar. |
| CRÍTICO | Es muy probable que este hallazgo sea un problema de actualización que debe solucionarse para evitar la pérdida de funciones o rendimiento. |

## Interpretación del informe CSV del analizador de prácticas recomendadas {#cra-csv-report}

Al hacer clic en **CSV** AEM desde la instancia de la, el formato CSV del informe Analizador de prácticas recomendadas se crea desde la caché de contenido y se devuelve al explorador. Según la configuración del explorador, este informe se descarga automáticamente como archivo con un nombre predeterminado de `results.csv`.

Si la caché ha caducado, el informe se regenera antes de crear y descargar el archivo CSV.

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

AEM El BPA proporciona una interfaz HTTP que puede utilizarse como alternativa a su interfaz de usuario dentro de los entornos de trabajo de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de usuario de la interfaz de. La interfaz admite comandos HEAD y GET. Se puede utilizar para generar el informe de BPA y devolverlo en uno de los tres formatos siguientes: JSON, CSV y valores separados por tabuladores (TSV).

Las siguientes direcciones URL están disponibles para el acceso HTTP, donde `<host>` es el nombre de host y el puerto, si es necesario, del servidor en el que está instalado el BPA:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json` para el formato JSON
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv` para el formato CSV
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv` para el formato TSV

### Ejecución de una petición HTTP {#executing-http-request}

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

* `max-age` (número, opcional): especifica la duración de la actualización de la caché en segundos. Este número debe ser 0 o más. La duración de la actualización predeterminada es de 86400 segundos. Sin este parámetro o el encabezado correspondiente, se utiliza una nueva caché para servir solicitudes durante 24 horas, momento en el que se debe volver a generar la caché. Uso de `max-age=0` forzará la eliminación de la caché e iniciará una regeneración del informe utilizando la duración de actualización anterior distinta de cero para la caché recién generada.
* `respond-async` (booleano, opcional): especifica que la respuesta se debe proporcionar de forma asíncrona. Uso de `respond-async=true` si la caché está obsoleta, el servidor devolverá una respuesta de `202 Accepted` sin esperar a que se actualice la caché y se genere el informe. Si la caché es nueva, este parámetro no tiene ningún efecto. El valor predeterminado es `false`. Sin este parámetro o el encabezado correspondiente, el servidor responderá sincrónicamente, lo que puede requerir una cantidad de tiempo considerable y un ajuste del tiempo de respuesta máximo para el cliente HTTP.
* `may-refresh-cache` (booleano, opcional): Especifica que el servidor puede actualizar la caché en respuesta a una solicitud si la caché actual está vacía, obsoleta o pronto estará obsoleta. If `may-refresh-cache=true`, o si no se especifica, el servidor puede iniciar una tarea en segundo plano que invocará Pattern Detector y actualizará la caché. If `may-refresh-cache=false` a continuación, el servidor no iniciará ninguna tarea de actualización que, de lo contrario, se habría realizado si la caché está vacía o anticuada, en cuyo caso el informe estará vacío. Este parámetro no afectará a ninguna tarea de actualización que ya esté en proceso.
* `return-minimal` (booleano, opcional): especifica que la respuesta del servidor solo debe incluir el estado que contiene la indicación de progreso y el estado de caché en formato JSON. If `return-minimal=true`, el cuerpo de la respuesta se limita al objeto de estado. If `return-minimal=false`, o si no se especifica, se proporciona una respuesta completa.
* `log-findings` (booleano, opcional): Especifica que el servidor debe registrar el contenido de la caché cuando se crea o actualiza por primera vez. Cada hallazgo de la caché de se registra como una cadena JSON. Este registro solo se producirá si `log-findings=true` y la solicitud genera una nueva caché.

Cuando están presentes tanto un encabezado HTTP como el parámetro de consulta correspondiente, el parámetro de consulta tendrá prioridad.

Una manera sencilla de iniciar la generación del informe a través de la interfaz HTTP es con el siguiente comando:
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`.

Una vez realizada una solicitud, el cliente no necesita permanecer activo para que se genere el informe. La generación de informes se puede iniciar con un cliente mediante una solicitud HTTP y, una vez generado el informe, se puede ver desde la GET AEM con otro cliente o con la herramienta BPA en la interfaz de usuario de la interfaz de usuario de la aplicación de configuración de etiquetas de datos (BPA, por sus siglas en inglés).

### Respuestas {#http-responses}

Los siguientes valores de respuesta son posibles:

* `200 OK`: indica que la respuesta contiene los resultados del detector de patrones que se generaron durante la duración de la actualización de la caché.
* `202 Accepted`: se utiliza para indicar que la caché está obsoleta. Cuándo `respond-async=true` y `may-refresh-cache=true` esta respuesta indica que hay una tarea de actualización en curso. Cuándo `may-refresh-cache=false` esta respuesta simplemente indica que la caché está obsoleta.
* `400 Bad Request`: indica que se produjo un error con la solicitud. Un mensaje en formato Detalles del problema (consulte [RFC 7807](https://tools.ietf.org/html/rfc7807)) proporciona más detalles.
* `401 Unauthorized`: indica que la solicitud no se autorizó.
* `500 Internal Server Error`: indica que se ha producido un error de servidor interno. El mensaje en formato Detalles del problema proporciona más detalles.
* `503 Service Unavailable`: indica que el servidor está ocupado con otra respuesta y no puede atender esta solicitud de forma oportuna. Esto solo es probable cuando se realizan solicitudes sincrónicas. El mensaje en formato Detalles del problema proporciona más detalles.

## Información del administrador

### Ajuste de la duración de caché {#cache-adjustment}

La duración predeterminada de la caché de BPA es de 24 horas. AEM Con la opción para actualizar un informe y volver a generar la caché, tanto en la instancia de como en la interfaz HTTP, es probable que este valor predeterminado sea adecuado para la mayoría de los usos del BPA. AEM Si el tiempo de generación de informes es particularmente largo para la instancia de la, es posible que desee ajustar la duración de la caché para minimizar la regeneración del informe.

El valor de duración de la caché se almacena como la `maxCacheAge` propiedad en el siguiente nodo de repositorio:
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

El valor de esta propiedad es la duración de la caché en segundos. Un administrador puede ajustar la duración de la caché mediante CRX/DE Lite.

### Instalar en AEM 6.1 {#installing-on-aem61}

BPA utiliza una cuenta de usuario de servicio del sistema denominada `repository-reader-service` para ejecutar Pattern Detector. Esta cuenta está disponible en AEM 6.2 y posteriores. AEM En la versión 6.1, se debe crear esta cuenta *antes de* Instalación de BPA siguiendo los pasos siguientes:

1. Siga las instrucciones en [Crear un nuevo usuario de servicio](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user) para crear un usuario. Establezca el UserID en `repository-reader-service` y deje la ruta intermedia vacía y luego haga clic en la marca de verificación verde.

2. Siga las instrucciones en [Administrar usuarios y grupos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups), específicamente las instrucciones para Añadir usuarios a un grupo para agregar el `repository-reader-service` usuario al `administrators` grupo.

3. AEM Instale el paquete BPA mediante el Administrador de paquetes en la instancia de origen de la instancia de la. (Esto agregará la modificación de configuración necesaria a la configuración de ServiceUserMapper para el usuario del servicio `repository-reader-service` del sistema).
