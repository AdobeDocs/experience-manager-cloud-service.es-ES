---
title: Referencias de desarrollador para  [!DNL Assets]
description: '[!DNL Assets] API y contenido de referencia de desarrollador le permite administrar recursos, incluidos archivos binarios, metadatos, representaciones, comentarios y  [!DNL Content Fragments].'
contentOwner: AG
feature: Assets HTTP API
role: Developer, Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] casos de uso para desarrolladores, API y material de referencia {#assets-cloud-service-apis}

El artículo contiene recomendaciones, materiales de referencia y recursos para desarrolladores de [!DNL Assets] como [!DNL Cloud Service]. Incluye nuevo módulo de carga de recursos, referencia de la API e información sobre la compatibilidad proporcionada en los flujos de trabajo posteriores al procesamiento.

## [!DNL Experience Manager Assets] API y operaciones {#use-cases-and-apis}

[!DNL Assets] as a [!DNL Cloud Service] proporciona varias API para interactuar mediante programación con recursos digitales. Cada API admite casos de uso específicos, como se menciona en la tabla siguiente. La interfaz de usuario [!DNL Assets], la aplicación de escritorio [!DNL Experience Manager] y [!DNL Adobe Asset Link] admiten todas o algunas de las operaciones.

>[!CAUTION]
>
>Algunas API siguen existiendo, pero no son compatibles de forma activa (indicadas con un ×). En la medida de lo posible, no utilice estas API.

| Niveles de soporte | Descripción |
| ------------- | --------------------------- |
| ✓ | Compatible |
| × | No compatible. No utilice. |
| - | No disponible |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) API de Java | [Servicio de cómputo de recursos](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=es) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **binario original** |  |  |  |  |  |  |
| Crear original | ✓ | × | - | × | × | - |
| Leer original | - | × | ✓ | ✓ | ✓ | - |
| Actualizar original | ✓ | × | ✓ | × | × | - |
| Eliminar original | - | ✓ | - | ✓ | ✓ | - |
| Copiar original | - | ✓ | - | ✓ | ✓ | - |
| Mover original | - | ✓ | - | ✓ | ✓ | - |
| **Metadatos** |  |  |  |  |  |  |
| Crear metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Leer metadatos | - | ✓ | - | ✓ | ✓ | - |
| Actualización de los metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Eliminar metadatos | - | ✓ | ✓ | ✓ | ✓ | - |
| Copiar metadatos | - | ✓ | - | ✓ | ✓ | - |
| Mover metadatos | - | ✓ | - | ✓ | ✓ | - |
| **Fragmentos de contenido (CF)** |  |  |  |  |  |  |
| Crear CF | - | ✓ | - | ✓ | - | - |
| Leer CF | - | ✓ | - | ✓ | - | ✓ |
| Actualizar CF | - | ✓ | - | ✓ | - | - |
| Eliminar CF | - | ✓ | - | ✓ | - | - |
| Copiar CF | - | ✓ | - | ✓ | - | - |
| Mover CF | - | ✓ | - | ✓ | - | - |
| **Versiones** |  |  |  |  |  |  |
| Crear versión | ✓ | ✓ | - | - | - | - |
| Versión de lectura | - | ✓ | - | - | - | - |
| Eliminar versión | - | ✓ | - | - | - | - |
| **Carpetas** |  |  |  |  |  |  |
| Crear carpeta | ✓ | ✓ | - | ✓ | - | - |
| Leer carpeta | - | ✓ | - | ✓ | - | - |
| Eliminar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Copiar carpeta | ✓ | ✓ | - | ✓ | - | - |
| Mover carpeta | ✓ | ✓ | - | ✓ | - | - |

## Carga de recursos {#asset-upload}

En [!DNL Experience Manager] como [!DNL Cloud Service], puede cargar directamente los recursos al almacenamiento en la nube mediante la API HTTP. A continuación se indican los pasos para cargar un archivo binario. Ejecute estos pasos en una aplicación externa y no dentro de la JVM [!DNL Experience Manager].

1. [Enviar una solicitud HTTP](#initiate-upload). Informa a [!DNL Experience Manage]r implementación de su intención de cargar un nuevo binario.
1. [PUT cambió el contenido del binario](#upload-binary) a uno o más URI proporcionados por la solicitud de inicio.
1. [Envíe una solicitud HTTP](#complete-upload) para informar al servidor de que el contenido del binario se cargó correctamente.

![Descripción general del protocolo de carga binaria directa](assets/add-assets-technical.png)

>[!IMPORTANT]
>
>Ejecute los pasos anteriores en una aplicación externa y no dentro de la JVM [!DNL Experience Manager].

El método ofrece una administración escalable y más eficaz de las cargas de recursos. Las diferencias con respecto a [!DNL Experience Manager] 6.5 son:

* Los binarios no pasan por [!DNL Experience Manager], que ahora simplemente coordina el proceso de carga con el almacenamiento de nube binaria configurado para la implementación.
* El almacenamiento en la nube binario funciona con una red de distribución de contenido (CDN) o una red Edge. Una CDN selecciona un punto final de carga más cercano a un cliente. Cuando los datos viajan a una distancia menor a un punto final cercano, el rendimiento de carga y la experiencia del usuario mejoran, especialmente para equipos distribuidos geográficamente.

>[!NOTE]
>
>Consulte el código de cliente para implementar este método en la [biblioteca de carga de aem](https://github.com/adobe/aem-upload) de código abierto.
>
>[!IMPORTANT]
>
>En determinadas circunstancias, es posible que los cambios no se propaguen completamente entre solicitudes a Experience Manager debido a la naturaleza finalmente coherente del almacenamiento en Cloud Service. Esto provoca que se produzcan respuestas 404 para iniciar o completar llamadas de carga debido a que no se propagan las creaciones de carpetas necesarias. Los clientes deben esperar respuestas 404 y gestionarlas implementando un reintento con una estrategia de back-off.

### Iniciar carga {#initiate-upload}

Envíe una solicitud HTTP POST a la carpeta deseada. Los Assets se crean o actualizan en esta carpeta. Incluya el selector `.initiateUpload.json` para indicar que la solicitud es para iniciar la carga de un archivo binario. Por ejemplo, la ruta a la carpeta donde se debe crear el recurso es `/assets/folder`. La solicitud de POST es `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contengan los campos siguientes:

* `(string) fileName`: obligatorio. Nombre del recurso tal como aparece en [!DNL Experience Manager].
* `(number) fileSize`: obligatorio. El tamaño de archivo, en bytes, del recurso que se carga.

Se puede utilizar una sola solicitud para iniciar cargas para varios binarios, siempre que cada binario contenga los campos obligatorios. Si se realiza correctamente, la solicitud responde con un código de estado `201` y un cuerpo que contiene datos JSON en el siguiente formato:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (cadena): Invoque este URI cuando el binario termine de cargarse. El URI puede ser absoluto o relativo, y los clientes deben poder gestionarlo. Es decir, el valor puede ser `"https://[aem_server]:[port]/content/dam.completeUpload.json"` o `"/content/dam.completeUpload.json"`. Vea [carga completa](#complete-upload).
* `folderPath` (cadena): Ruta de acceso completa a la carpeta en la que se cargó el binario.
* `(files)` (matriz): una lista de elementos cuya longitud y orden coinciden con la longitud y el orden de la lista de información binaria proporcionada en la solicitud de inicio.
* `fileName` (cadena): nombre del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `mimeType` (cadena): el tipo MIME del binario correspondiente, tal como se proporciona en la solicitud de inicio. Este valor debe incluirse en la solicitud completa.
* `uploadToken` (cadena): un token de carga para el binario correspondiente. Este valor debe incluirse en la solicitud completa.
* `uploadURIs` (matriz): una lista de cadenas cuyos valores son URI completos a los que se debe cargar el contenido del binario (consulte [Cargar binario](#upload-binary)).
* `minPartSize` (número): La longitud mínima, en bytes, de datos que se pueden proporcionar a cualquiera de los `uploadURIs`, si hay más de un URI.
* `maxPartSize` (número): Longitud máxima, en bytes, de datos que se pueden proporcionar a cualquiera de los `uploadURIs`, si hay más de un URI.

### Cargar binario {#upload-binary}

La salida del inicio de una carga incluye uno o más valores de URI de carga. Si se proporciona más de un URI, el cliente puede dividir el binario en partes y realizar solicitudes PUT de cada parte a los URI de carga proporcionados, por orden. Si decide dividir el binario en partes, siga las siguientes directrices:

* Cada parte, a excepción de la última, debe tener un tamaño mayor o igual que `minPartSize`.
* Cada parte debe tener un tamaño inferior o igual a `maxPartSize`.
* Si el tamaño del binario supera `maxPartSize`, divida el binario en partes para cargarlo.
* No es necesario que utilice todos los URI.

Si el tamaño del binario es menor o igual que `maxPartSize`, puede cargar el binario completo en un único URI de carga. Si se proporciona más de un URI de carga, utilice el primero e ignore el resto. No es necesario que utilice todos los URI.

Los nodos perimetrales de CDN ayudan a acelerar la carga solicitada de binarios.

La forma más sencilla de conseguir esto es usar el valor de `maxPartSize` como tamaño de pieza. El contrato de API garantiza que haya suficientes URI de carga para cargar el binario si utiliza este valor como tamaño de parte. Para ello, divida el binario en partes de tamaño `maxPartSize`, utilizando un URI para cada parte, en orden. La parte final puede ser de cualquier tamaño inferior o igual a `maxPartSize`. Por ejemplo, suponga que el tamaño total del binario es de 20.000 bytes, `minPartSize` es de 5.000 bytes, `maxPartSize` es de 8.000 bytes y el número de URI de carga es de 5. Ejecute los siguientes pasos:

* Cargue los primeros 8000 bytes del binario con el primer URI de carga.
* Cargue los segundos 8000 bytes del binario mediante el segundo URI de carga.
* Cargue los últimos 4000 bytes del binario con el tercer URI de carga. Como esta es la parte final, no necesita ser mayor que `minPartSize`.
* No es necesario utilizar los dos últimos URI de carga. Puedes ignorarlos.

Un error común es calcular el tamaño de la parte en función del número de URI de carga proporcionados por la API. El contrato de API no garantiza que este enfoque funcione y es posible que en realidad genere tamaños de partes que estén fuera del intervalo entre `minPartSize` y `maxPartSize`. Esto puede provocar errores de carga de archivos binarios.

De nuevo, la forma más fácil y segura es usar simplemente partes de tamaño igual a `maxPartSize`.

Si la carga se realiza correctamente, el servidor responde a cada solicitud con un código de estado `201`.

>[!NOTE]
>
>Para obtener más información sobre el algoritmo de carga, consulte la [documentación oficial de funciones](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) y la [documentación de API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) en el proyecto de Apache Jackrabbit Oak.

### Carga completa {#complete-upload}

Una vez cargadas todas las partes de un archivo binario, envíe una solicitud HTTP POST al URI completo proporcionado por los datos de inicio. El tipo de contenido del cuerpo de la solicitud debe ser `application/x-www-form-urlencoded` datos de formulario, que contengan los campos siguientes.

| Campos | Tipo | Requerido o no | Descripción |
|---|---|---|---|
| `fileName` | Cadena | Necesario | El nombre del recurso, tal como lo proporcionaron los datos de inicio. |
| `mimeType` | Cadena | Necesario | El tipo de contenido HTTP del binario, tal como lo proporcionaron los datos de inicio. |
| `uploadToken` | Cadena | Necesario | Cargue el token para el binario, tal como lo proporcionaron los datos de inicio. |
| `createVersion` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] crea una nueva versión del recurso. |
| `versionLabel` | Cadena | Opcional | Si se crea una nueva versión, la etiqueta asociada a la nueva versión de un recurso |
| `versionComment` | Cadena | Opcional | Si se crea una nueva versión, los comentarios asociados con la versión. |
| `replace` | Booleano | Opcional | Si `True` y existe un recurso con el nombre especificado, [!DNL Experience Manager] elimina el recurso y lo vuelve a crear. |
| `uploadDuration` | Número | Opcional | Tiempo total, en milisegundos, que el archivo se va a cargar en su totalidad. Si se especifica, la duración de la carga se incluye en los archivos de registro del sistema para el análisis de la velocidad de transferencia. |
| `fileSize` | Número | Opcional | El tamaño, en bytes, del archivo. Si se especifica, el tamaño del archivo se incluye en los archivos de registro del sistema para el análisis de velocidad de transferencia. |

>[!NOTE]
>
>Si el recurso existe y no se ha especificado ni `createVersion` ni `replace`, [!DNL Experience Manager] actualiza la versión actual del recurso con el nuevo binario.

Al igual que el proceso de inicio, los datos de solicitud completos pueden contener información de más de un archivo.

El proceso de carga de un binario no termina hasta que se invoca la dirección URL completa del archivo. Una vez completado el proceso de carga, se procesa un recurso. El procesamiento no se inicia aunque el archivo binario del recurso se haya cargado completamente, pero el proceso de carga no se haya completado. Si la carga se realiza correctamente, el servidor responderá con un código de estado `200`.

### Ejemplo de script de shell para cargar recursos en AEM as a Cloud Service {#upload-assets-shell-script}

El proceso de carga de varios pasos para el acceso binario directo en AEM as a Cloud Service se ilustra en el siguiente ejemplo de shell-script `aem-upload.sh`:

```bash
#!/bin/bash

# Check if pv is installed
if ! command -v pv &> /dev/null; then
    echo "Error: 'pv' command not found. Please install it before running the script."
    exit 1
fi

# Check if jq is installed
if ! command -v jq &> /dev/null; then
    echo "Error: 'jq' command not found. Please install it before running the script."
    exit 1
fi

# Set DEBUG to true to enable debug statements
DEBUG=true

# Function for printing debug statements
function debug() {
    if [ "${DEBUG}" = true ]; then
        echo "[DEBUG] $1"
    fi
}

# Function to check if a file exists
function file_exists() {
    [ -e "$1" ]
}

# Function to check if a path is a directory
function is_directory() {
    [ -d "$1" ]
}

# Check if the required number of parameters are provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <aem-url> <asset-folder> <file-to-upload> <bearer-token>"
    exit 1
fi

AEM_URL="$1"
ASSET_FOLDER="$2"
FILE_TO_UPLOAD="$3"
BEARER_TOKEN="$4"

# Extracting file name or folder name from the file path
NAME=$(basename "${FILE_TO_UPLOAD}")

# Step 1: Check if "file-to-upload" is a folder
if is_directory "${FILE_TO_UPLOAD}"; then
    echo "Uploading files from the folder recursively..."
    
    # Recursively upload files in the folder
    find "${FILE_TO_UPLOAD}" -type f | while read -r FILE_PATH; do
        FILE_NAME=$(basename "${FILE_PATH}")
        debug "Uploading file: ${FILE_PATH}"
        
        # You can choose to initiate upload for each file here
        # For simplicity, let's assume you use the same ASSET_FOLDER for all files
        ./aem-upload.sh "${AEM_URL}" "${ASSET_FOLDER}" "${FILE_PATH}" "${BEARER_TOKEN}"
    done
else
    # "file-to-upload" is a single file
    FILE_NAME="${NAME}"

    # Step 2: Calculate File Size
    FILE_SIZE=$(stat -c %s "${FILE_TO_UPLOAD}")

    # Step 3: Initiate Upload
    INITIATE_UPLOAD_ENDPOINT="${AEM_URL}/content/dam/${ASSET_FOLDER}.initiateUpload.json"

    debug "Initiating upload..."
    debug "Initiate Upload Endpoint: ${INITIATE_UPLOAD_ENDPOINT}"
    debug "File Name: ${FILE_NAME}"
    debug "File Size: ${FILE_SIZE}"

    INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
        -d "fileName=${FILE_NAME}" \
        -d "fileSize=${FILE_SIZE}" \
        ${INITIATE_UPLOAD_ENDPOINT})

    # Continue with the rest of the script...
fi


# Check if the response body contains the specified HTML content for a 404 error
if echo "${INITIATE_UPLOAD_RESPONSE}" | grep -q "<title>404 Specified folder not found</title>"; then
    echo "Folder not found. Creating the folder..."

    # Attempt to create the folder
    CREATE_FOLDER_ENDPOINT="${AEM_URL}/api/assets/${ASSET_FOLDER}"

    debug "Creating folder..."
    debug "Create Folder Endpoint: ${CREATE_FOLDER_ENDPOINT}"

    CREATE_FOLDER_RESPONSE=$(curl -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer ${BEARER_TOKEN}" \
        -d '{"class":"'${ASSET_FOLDER}'","properties":{"title":"'${ASSET_FOLDER}'"}}' \
        ${CREATE_FOLDER_ENDPOINT})

    # Check the response code and inform the user accordingly
    STATUS_CODE_CREATE_FOLDER=$(echo "${CREATE_FOLDER_RESPONSE}" | jq -r '.properties."status.code"')
    case ${STATUS_CODE_CREATE_FOLDER} in
        201)
            echo "Folder created successfully. Initiating upload again..."

            # Retry Initiate Upload after creating the folder
            INITIATE_UPLOAD_RESPONSE=$(curl -X POST \
                -H "Authorization: Bearer ${BEARER_TOKEN}" \
                -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
                -d "fileName=${FILE_NAME}" \
                -d "fileSize=${FILE_SIZE}" \
                ${INITIATE_UPLOAD_ENDPOINT})
            ;;
        409)
            echo "Error: Folder already exists."
            ;;
        412)
            echo "Error: Precondition failed. Root collection cannot be found or accessed."
            exit 1
            ;;
        500)
            echo "Error: Internal Server Error. Something went wrong."
            exit 1
            ;;
        *)
            echo "Error: Unexpected response code ${STATUS_CODE_CREATE_FOLDER}"
            exit 1
            ;;
    esac
fi

# Extracting values from the response
FOLDER_PATH=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.folderPath')
UPLOAD_URIS=($(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadURIs[]'))
UPLOAD_TOKEN=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].uploadToken')
MIME_TYPE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].mimeType')
MIN_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].minPartSize')
MAX_PART_SIZE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.files[0].maxPartSize')
COMPLETE_URI=$(echo "${INITIATE_UPLOAD_RESPONSE}" | jq -r '.completeURI')

# Extracting "Affinity-cookie" from the response headers
AFFINITY_COOKIE=$(echo "${INITIATE_UPLOAD_RESPONSE}" | grep -i 'Affinity-cookie' | awk '{print $2}')

debug "Folder Path: ${FOLDER_PATH}"
debug "Upload Token: ${UPLOAD_TOKEN}"
debug "MIME Type: ${MIME_TYPE}"
debug "Min Part Size: ${MIN_PART_SIZE}"
debug "Max Part Size: ${MAX_PART_SIZE}"
debug "Complete URI: ${COMPLETE_URI}"
debug "Affinity Cookie: ${AFFINITY_COOKIE}"
if $DEBUG; then
    i=1
    for UPLOAD_URI in "${UPLOAD_URIS[@]}"; do
        debug "Upload URI $i: "$UPLOAD_URI
        i=$((i+1))
    done
fi


# Calculate the number of parts needed
NUM_PARTS=$(( (FILE_SIZE + MAX_PART_SIZE - 1) / MAX_PART_SIZE ))
debug "Number of Parts: $NUM_PARTS"

# Calculate the part size for the last chunk
LAST_PART_SIZE=$(( FILE_SIZE % MAX_PART_SIZE ))
if [ "${LAST_PART_SIZE}" -eq 0 ]; then
    LAST_PART_SIZE=${MAX_PART_SIZE}
fi

# Step 4: Upload binary to the blob store in parts
PART_NUMBER=1
for i in $(seq 1 $NUM_PARTS); do
    PART_SIZE=${MAX_PART_SIZE}
    if [ ${PART_NUMBER} -eq ${NUM_PARTS} ]; then
        PART_SIZE=${LAST_PART_SIZE}
        debug "Last part size: ${PART_SIZE}"
    fi

    PART_FILE="/tmp/${FILE_NAME}_part${PART_NUMBER}"

    # Creating part file 
    SKIP=$((PART_NUMBER - 1))
    SKIP=$((MAX_PART_SIZE * SKIP))
    dd if="${FILE_TO_UPLOAD}" of="${PART_FILE}"  bs="${PART_SIZE}" skip="${SKIP}" count="${PART_SIZE}" iflag=skip_bytes,count_bytes  > /dev/null 2>&1
    debug "Creating part file: ${PART_FILE} with size ${PART_SIZE}, skipping first ${SKIP} bytes."

    
    UPLOAD_URI=${UPLOAD_URIS[$PART_NUMBER-1]}

    debug "Uploading part ${PART_NUMBER}..."
    debug "Part Size: $PART_SIZE"
    debug "Part File: ${PART_FILE}"
    debug "Part File Size: $(stat -c %s "${PART_FILE}")"
    debug "Upload URI: ${UPLOAD_URI}"

    # Upload the part in the background
    if command -v pv &> /dev/null; then
        pv "${PART_FILE}" | curl --progress-bar -X PUT --data-binary "@-" "${UPLOAD_URI}" &
    else
        curl -# -X PUT --data-binary "@${PART_FILE}" "${UPLOAD_URI}" &
    fi

    PART_NUMBER=$((PART_NUMBER + 1))
done

# Wait for all background processes to finish
wait

# Step 5: Complete the upload in AEM
COMPLETE_UPLOAD_ENDPOINT="${AEM_URL}${COMPLETE_URI}"

debug "Completing the upload..."
debug "Complete Upload Endpoint: ${COMPLETE_UPLOAD_ENDPOINT}"

RESPONSE=$(curl -X POST \
    -H "Authorization: Bearer ${BEARER_TOKEN}" \
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" \
    -H "Affinity-cookie: ${AFFINITY_COOKIE}" \
    --data-urlencode "uploadToken=${UPLOAD_TOKEN}" \
    --data-urlencode "fileName=${FILE_NAME}" \
    --data-urlencode "mimeType=${MIME_TYPE}" \
    "${COMPLETE_UPLOAD_ENDPOINT}")
    
debug $RESPONSE

echo "File upload completed successfully."
```

### Biblioteca de carga de código abierto {#open-source-upload-library}

Para obtener más información sobre los algoritmos de carga o para crear sus propios scripts y herramientas de carga, Adobe proporciona bibliotecas y herramientas de código abierto:

* [Biblioteca de código abierto aem-upload](https://github.com/adobe/aem-upload).
* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
>
>Tanto la biblioteca de carga de aem como la herramienta de línea de comandos utilizan la [biblioteca node-httptransfer](https://github.com/adobe/node-httptransfer/)

### API de carga de recursos obsoletas {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

El nuevo método de carga solo es compatible con [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. Las API de [!DNL Adobe Experience Manager] 6.5 están en desuso. Los métodos relacionados con la carga o actualización de recursos o representaciones (cualquier carga binaria) están en desuso en las siguientes API:

* [API HTTP de Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API de Java, como `AssetManager.createAsset(..)`, `AssetManager.createAssetForBinary(..)`, `AssetManager.getAssetForBinary(..)`, `AssetManager.removeAssetForBinary(..)`, `AssetManager.createOrUpdateAsset(..)`, `AssetManager.createOrReplaceAsset(..)`

>[!MORELIKETHIS]
>
>* [Biblioteca de código abierto aem-upload](https://github.com/adobe/aem-upload).
>* [Herramienta de línea de comandos de código abierto](https://github.com/adobe/aio-cli-plugin-aem).
>* [Documentación de Apache Jackrabbit Oak para carga directa](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).

## Flujos de trabajo de procesamiento de recursos y posprocesamiento {#post-processing-workflows}

En [!DNL Experience Manager], el procesamiento de recursos se basa en la configuración de **[!UICONTROL Perfiles de procesamiento]** que usa [microservicios de recursos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). El procesamiento no requiere extensiones de desarrollador.

Para la configuración del flujo de trabajo posterior al procesamiento, utilice los flujos de trabajo estándar con extensiones con pasos personalizados.

## Compatibilidad con los pasos del flujo de trabajo en el flujo de trabajo posterior al procesamiento {#post-processing-workflows-steps}

Si actualiza desde una versión anterior de [!DNL Experience Manager], puede utilizar los microservicios de recursos para procesar recursos. Los microservicios de recursos nativos de la nube son más fáciles de configurar y utilizar. No se admiten algunos pasos de flujo de trabajo utilizados en el flujo de trabajo [!UICONTROL DAM Update Asset] de la versión anterior. Para obtener más información acerca de las clases compatibles, consulte la [Referencia de la API de Java o Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Los siguientes modelos de flujo de trabajo técnico se han sustituido por microservicios de recursos o la compatibilidad no está disponible:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).