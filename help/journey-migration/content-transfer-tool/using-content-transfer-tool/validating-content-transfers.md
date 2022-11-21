---
title: Validación de transferencias de contenido
description: Usar la herramienta de transferencia de contenido para validar transferencias de contenido
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: 99ecf1309b9fa7613bfb9c99de9677700082f128
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Validación de transferencias de contenido {#validating-content-transfers}

## Introducción {#getting-started}

Los usuarios tienen la capacidad de determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se incorporó correctamente a la instancia de destino. Esta función de validación funciona comparando un compendio de las rutas de todos los nodos involucrados durante la extracción con un compendio de las rutas de todos los nodos involucrados durante la ingesta. Si hay rutas de nodos incluidas en el compendio de extracción que no aparecen en el compendio de ingesta, se considera que la validación ha fallado y puede que sea necesaria una validación manual adicional.

>[!INFO]
>
>Esta función estará disponible a partir de la versión 1.8.x de la herramienta de transferencia de contenido (CTT). El entorno de destino de AEM Cloud Service debe estar ejecutando al menos la versión 6158 o buenas. También requiere que el entorno de origen esté configurado para ejecutarse [copia previa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La función de validación busca el archivo azcopy.config en el origen. Si no encuentra este archivo, la validación no se ejecutará. Para obtener más información sobre cómo configurar un archivo azcopy.config, consulte [esta página](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La validación de una transferencia de contenido es una función opcional. La activación de esta función aumentará tanto el tiempo que se tarda en realizar una extracción como la ingesta. Para utilizar la función, actívela en la consola del sistema del entorno de AEM de origen siguiendo estos pasos:

1. Vaya a la consola web de Adobe Experience Manager en la instancia de origen, yendo a **Herramientas - Operaciones - Consola Web** o directamente a la dirección URL en *https://serveraddress:serverport/system/console/configMgr*
1. Buscar **Configuración del servicio de extracción de la herramienta de transferencia de contenido**
1. Utilice el botón de icono de lápiz para editar sus valores de configuración
1. Active la variable **Habilitar la validación de migración durante la extracción** configuración y, a continuación, pulse **Guardar**:

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Con esta configuración habilitada, y el entorno de AEM Cloud Service de destino que ejecute una versión compatible, la validación de la migración se producirá durante todas las extracciones y entregas posteriores.

Para obtener más información sobre cómo instalar la herramienta de transferencia de contenido, consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Validación de una transferencia de contenido {#how-to-validate-a-content-transfer}

Con la validación de migración habilitada en el entorno de AEM de origen, inicie una extracción.

If **Sobrescribir el contenedor de ensayo durante la extracción** está activada, todos los nodos implicados en la extracción se registrarán en el compendio de ruta de extracción. Cuando se utiliza esta configuración, es importante habilitar la variable **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** durante la ingesta, de lo contrario, puede parecer que faltan nodos en el compendio de ingesta. Estos son los nodos que ya están presentes en el destino en ingestas anteriores.

Para ver una ilustración gráfica de esto, consulte los ejemplos siguientes:

### Ejemplo 1 {#example-1}

* **Extracción (sobrescritura)**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Ingesta (Borrar)**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

   Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes, incluso para ingestas repetidas.

### Ejemplo 2 {#example-2}

* **Extracción**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

   Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes para la ingesta inicial.

   Si se repite la ingesta, el compendio de ingesta estará vacío y la validación parecerá haber fallado. El compendio de ingesta estará vacío porque todos los nodos de esta extracción ya estarán presentes en el destino.

Una vez finalizada la extracción, comience la ingesta.

La parte superior del registro de ingesta contiene una entrada, similar a `aem-ethos/tools:1.2.438`. Asegúrese de que este número de versión **1,2,438** o bueno, de lo contrario, la validación no se admite en la versión de AEM as a Cloud Service que esté utilizando.

Una vez finalizada la ingesta y que comience la validación, se anotará la siguiente entrada de registro en el registro de ingesta:

```
Gathering artifacts for migration validation...  
```

Los detalles de la validación seguirán esta entrada. Encuentre un ejemplo de una migración grande a continuación:

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

Este es un ejemplo de una validación que se ha realizado correctamente, ya que no faltaban entradas en el compendio de ingesta que estuvieran presentes en el compendio de extracción.

Para comparar, el aspecto de un informe de validación sería el siguiente si la validación hubiera fallado:

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

El ejemplo de error anterior se logró ejecutando una ingesta y luego ejecutando de nuevo la misma ingesta con Wipe desactivado, de modo que no había nodos involucrados durante la ingesta — todo ya estaba presente en el destino.

Además de incluirse en el registro de ingesta, también se puede acceder al informe de validación desde el **Trabajos de Ingesta** interfaz de usuario en Cloud Acceleration Manager. Para ello, haga clic en los tres puntos (**...**) y haga clic en **Informe de validación** en la lista desplegable para ver el informe de validación.


![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Solución de problemas {#troubleshooting}

### Error de validación. ¿Y ahora qué?  {#validation-fail}

El primer paso es determinar si la ingesta realmente falló o si el contenido extraído ya está presente en el entorno de destino. Esto puede ocurrir si se repite una ingesta con el **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** está desactivada.

Para verificarlo, elija una ruta del informe de validación y compruebe si está presente en el entorno de destino. Si se trata de un entorno de publicación, puede limitarse a comprobar las páginas y los recursos directamente. Abra un ticket con el Servicio de atención al cliente si necesita ayuda con este paso.

### El recuento de nodos es inferior al esperado. ¿Por qué? {#node-count-lower-than-expected}

Algunas rutas de los compendios de extracción e ingesta se excluyen intencionadamente para mantener el tamaño de estos archivos manejable, con el objetivo de poder calcular el resultado de la validación de migración dentro de las dos horas siguientes a la finalización de la ingesta.

Las rutas que excluimos actualmente de los compendios incluyen: `cqdam.text.txt` representaciones, nodos dentro de `/home`y nodos dentro de `/jcr:system`.
