---
title: ¿Cómo se configuran las API sincrónicas de comunicaciones de Forms?
description: Configurar el entorno de desarrollo para las API sincrónicas de comunicaciones interactivas para Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 77da2f4ddcd9074a79883f18a33b6fe50e32b266
workflow-type: tm+mt
source-wordcount: '2396'
ht-degree: 2%

---


# Configuración del acceso de servidor a servidor OAuth para las API sincrónicas de comunicaciones de AEM Forms

Esta guía proporciona instrucciones para configurar e invocar las API sincrónicas de comunicaciones de AEM Forms a las que se accede a través de Adobe Developer Console mediante la autenticación de servidor a servidor OAuth.

## Requisitos previos

Para configurar un entorno para ejecutar y probar las API de comunicaciones de AEM Forms, asegúrese de que dispone de lo siguiente:

### Acceso y permisos

Asegúrese de tener los derechos de acceso y los permisos necesarios antes de empezar a configurar las API de comunicaciones.

**Permisos de usuario y función**

- Función de desarrollador asignada en Adobe Admin Console
- Permiso para crear proyectos en Adobe Developer Console

>[!NOTE]
>
> Para obtener más información sobre la asignación de funciones y la concesión de acceso a los usuarios, consulte el artículo [Agregar usuarios y funciones](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

**Acceso al repositorio Git**

- Acceso al repositorio de Git de Cloud Manager
- Credenciales de Git para clonar y transferir cambios

>[!NOTE]
>
> Para obtener más información sobre cómo integrar Adobe Cloud Manager y Adobe Cloud Manager, consulte [Documentación de integración de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Generar token de acceso mediante Adobe Developer Console (ADC)

- Genere un token de acceso a través de Adobe Developer Console mediante la autenticación de servidor a servidor OAuth.
- Recuperación del ID de cliente desde Adobe Developer Console

>[!NOTE]
>
> Para obtener más información sobre la autenticación de servidor a servidor OAuth mediante Adobe Developer Console, [haga clic aquí](/help/forms/oauth-api-authetication.md).

### Herramientas de desarrollo

- **Node.js** para ejecutar aplicaciones de ejemplo
- Última versión de **Git**
- Acceso a **Terminal/Línea de comandos**
- **Editor de texto o IDE** para editar archivos de configuración (código VS, IntelliJ, etc.)
- **Postman** o una herramienta similar para las pruebas de API

>[!NOTE]
>
> Este es un proceso único por entorno que debe completarse antes de continuar con la configuración de las API de comunicaciones de AEM Forms.

## Configuración de las API sincrónicas de AEM Forms Communications

Se accede a las API de comunicación de AEM Forms a través de Adobe Developer Console mediante la autenticación de servidor a servidor OAuth.

Siga los pasos para explicar cómo configurar las API sincrónicas de comunicación de Forms para generar PDF mediante la plantilla y el archivo XDP:

### Paso 1: Acceso al entorno de AEM Cloud Service y al extremo de AEM Forms

Acceda a los detalles del entorno de AEM Cloud Service para obtener las direcciones URL y los identificadores necesarios para la configuración de la API.

#### 1.1 Iniciar sesión en Adobe Cloud Manager

1. Vaya a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
2. Inicie sesión con su Adobe ID

#### 1.2 Vaya a la Descripción general del programa

Seleccione el programa en la lista. Se le redirigirá a la página **Resumen del programa**

![Página de información general del programa](/help/forms/assets/program-overview.png)

#### 1.3 Acceso y visualización del entorno de AEM Cloud Service

Puede ver o acceder a los detalles del entorno de AEM Cloud Service mediante cualquiera de las dos opciones:

>[!BEGINTABS]

>[!TAB Opción 1: desde la página de información general]

1. En la página **Resumen del programa**
2. Haga clic en **&quot;Entornos&quot;** en el menú del lado izquierdo.  Puede ver una lista de todos los entornos
3. Haga clic en el nombre de entorno específico para ver los detalles

   ![Ver todos los entornos](/help/forms/assets/all-env.png)

>[!TAB Opción 2: desde la sección Entornos]

1. En la página **Resumen del programa**
2. Busque la sección **Entornos**
3. Haga clic en **&quot;Mostrar todo&quot;** para ver todos los entornos
4. Haga clic en el menú de **puntos suspensivos (...)** que está junto al entorno
5. Seleccionar **&quot;Ver detalles&quot;**

   ![Detalles de Opción1-Entorno](/help/forms/assets/option2-env-details.png)

>[!ENDTABS]

#### 1.4. Encontrar el punto final de AEM Forms

En la página de detalles de **Entorno**, observe su instancia de URL de AEM.

![Detalles de Opción1-Entorno](/help/forms/assets/option1-env.png)

>[!NOTE]
>
> Para ver cómo acceder al entorno de acceso a AEM Cloud Service y al extremo de AEM Forms, consulte [Documentación sobre la administración de entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=es).

### Paso 2: Clonar el repositorio de Git

Clone el repositorio Git de Cloud Manager para administrar sus archivos de configuración de API.

#### 2.1 Busque la sección Repositorio

1. En la página **Resumen del programa**, haga clic en la ficha **Repositorios**
2. Busque el nombre del repositorio y haga clic en el menú de puntos suspensivos (...).
3. Copiar la URL del repositorio

   ![Copiar URL del repositorio](/help/forms/assets/copy-repo-url.png)

>[!NOTE]
>
> El formato de dirección URL suele ser `https://git.cloudmanager.adobe.com/<org>/<program>/`

#### 2.2 Clonar usando el comando Git

1. Abra el símbolo del sistema o el terminal
2. Ejecute el comando `git clone` para clonar el repositorio Git.

   ```bash
   git clone [repository-url]
   ```

>[!NOTE]
>
> Para clonar el repositorio Git, utilice las credenciales proporcionadas por Adobe Cloud Manager.

Por ejemplo, para clonar el repositorio Git, ejecute el siguiente comando:

```bash
https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-pXXX-ukYYYY/
```

![Clonando el repositorio Git](/help/forms/assets/repo-clone.png)

Para obtener más información sobre cómo integrar Adobe Cloud Manager y Adobe Cloud Manager, consulte [Documentación de integración de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Paso 3: Configuración del proyecto de Adobe Developer Console

#### 3.1 Acceso a Adobe Developer Console

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console)
2. Inicie sesión con su Adobe ID
3. Cree un nuevo proyecto o vaya al proyecto existente

>[!BEGINTABS]

>[!TAB Para crear un nuevo proyecto]

1. En la sección **Inicio rápido**, haga clic en **Crear nuevo proyecto**
2. Se crea un nuevo proyecto con un nombre predeterminado

   ![Crear proyecto ADC](/help/forms/assets/adc-home.png)

3. Haga clic en **Editar proyecto** en la esquina superior derecha

   ![Editar proyecto](/help/forms/assets/adc-edit-project.png)

4. Proporcione un nombre significativo (por ejemplo, &quot;formsproject&quot;)
5. Haga clic en **Guardar**.

   ![Editar nombre de proyecto](/help/forms/assets/adc-edit-projectname.png)

>[!TAB Para navegar a su proyecto existente]

1. Haga clic en **Todos los proyectos** desde Adobe Developer Console

   ![Buscar proyectos](/help/forms/assets/search-adc-project.png)

2. Busque el proyecto y haga clic en para abrirlo.

   ![Localizar proyectos](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

#### 3.2 Añadir API de comunicación de Forms

1. Haga clic en **Agregar API**

   ![Agregar API](/help/forms/assets/adc-add-api.png)

2. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
3. Seleccione **&quot;API de comunicación de Forms&quot;**

   ![Agregar API de comunicación de Forms](/help/forms/assets/adc-add-forms-api.png)

4. Haga clic en **Siguiente**
5. Seleccione el método de autenticación **OAuth Server-to-Server**

   ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)
6. Haga clic en **Siguiente**

#### 3.3 Añadir perfil de producto

1. Seleccione el **perfil de producto** que coincida con la dirección URL de la instancia de AEM (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

2. Haga clic en **Guardar API configurada**. La API y el perfil de producto se añaden al proyecto

   ![Seleccionar configuración del proyecto](/help/forms/assets/adc-add-product-profile.png)

3. Ver la sección **Detalles de credenciales**

   ![Ver credenciales](/help/forms/assets/adc-view-credential.png)

**Registrar credenciales de API**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

#### 3.4 Generación del acceso

>[!BEGINTABS]

>[!TAB Para Pruebas]

Genere los tokens de acceso manualmente en Adobe Developer Console:

1. Haga clic en el botón **&quot;Generar token de acceso&quot;** en la sección de API del proyecto
2. Copiar el token de acceso generado

   ![Generar token de acceso](/help/forms/assets/adc-access-token.png)

>[!NOTE]
>
> El token de acceso es válido solamente por **24 horas**

>[!TAB Para Producción]

Generar tokens mediante programación usando la API [Adobe IMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service):

**Credenciales requeridas:**

- ID del cliente
- Secreto de cliente
- Ámbitos (normalmente: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

**Extremo de token:**

```
    https://ims-na1.adobelogin.com/ims/token/v3
```

**Solicitud de ejemplo (curl):**

```bash
    curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d 'grant_type=client_credentials' \
    -d 'client_id=<YOUR_CLIENT_ID>' \
    -d 'client_secret=<YOUR_CLIENT_SECRET>' \
    -d 'scope=AdobeID,openid,read_organizations'
```

**Respuesta:**

```json
        {
        "access_token": "eyJhbGciOiJSUz...",
        "token_type": "bearer",
        "expires_in": 86399
        }
```

>[!ENDTABS]

Ahora puede utilizar el token de acceso generado para hacer una llamada de API a entornos de desarrollo, fase o producción.

>[!NOTE]
>
> Para obtener más información sobre la autenticación de servidor a servidor OAuth a través de Adobe Developer Console, consulte el artículo [Autenticación de servidor a servidor OAuth](/help/forms/oauth-api-authetication.md).

### Paso 4: Registro del ID de cliente con el entorno de AEM

Para permitir que el ID de cliente del proyecto ADC se comunique con la instancia de AEM, debe registrarla con un archivo de configuración YAML e implementarla mediante una canalización de configuración.

#### 4.1 Localizar o crear directorio de configuración

1. Vaya al repositorio clonado de AEM Project y busque la carpeta `config`
2. Si no existe, créela en el nivel raíz del proyecto:

   ```bash
   mkdir config
   ```

3. Cree un nuevo archivo con el nombre `api.yaml` en el directorio `config`:

   ```bash
   touch config/api.yaml
   ```

4. Agregue el siguiente código al archivo `api.yaml`:

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

A continuación se explican los parámetros de configuración:

- **kind**: siempre se establece en `"API"` (lo identifica como una configuración de API)
- **versión**: versión de API, normalmente `"1"` o `"1.0"`
- **envTypes**: matriz de tipos de entorno donde se aplica esta configuración
   - `["dev"]`: solo entornos de desarrollo
   - `["stage"]`: solo entornos de ensayo
   - `["prod"]` - Solo entornos de producción
- **allowedClientID**: Los ID de cliente pueden acceder a su instancia de AEM
   - **author**: ID de cliente para el nivel de author
   - **publicar**: ID de cliente para el nivel de publicación
   - **vista previa**: ID de cliente para el nivel de vista previa

![Agregando archivo de configuración](/help/forms/assets/create-api-yaml-file.png)

#### 4.2 Confirmar y enviar cambios

1. Vaya a la carpeta raíz del repositorio clonado y ejecute los siguientes comandos:


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Cambios de Git push](/help/forms/assets/push-yaml-changes-in-git.png)


### Paso 5: Configuración de la canalización

#### 5.1 Iniciar sesión en Adobe Cloud Manager

1. Vaya a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
2. Inicie sesión con su Adobe ID

#### 5.1 Localización de la tarjeta Canalizaciones

1. Busque la tarjeta **Canalizaciones** en la página Información general del programa
2. Haga clic en el botón **&quot;Agregar&quot;**

   ![Agregar canalización](/help/forms/assets/add-pipeline.png)

#### 5.2 Seleccionar tipo de canalización

- **Para Entornos De Desarrollo**: Seleccione **&quot;Agregar Canalización Que No Sea De Producción&quot;**. Las canalizaciones que no son de producción son para entornos de desarrollo y ensayo

- **Para Entornos De Producción**: Seleccione **&quot;Agregar Canalización De Producción&quot;**. Las canalizaciones de producción requieren aprobaciones adicionales

>[!NOTE]
>
> En este caso, cree una canalización que no sea de producción, ya que hay un entorno de desarrollo disponible.

**1. Configurar canalización: ficha Configuración**

En la ficha **Configuración**:

a. **Tipo de canalización**

- Seleccionar **&quot;Canalización de implementación&quot;**

b. **Nombre de canalización**

- Proporcione un nombre descriptivo. Por ejemplo, asigne a la canalización el nombre `api-config-pipieline`

c. **Déclencheur de implementación**

- **Manual**: Implementar solo cuando se activa manualmente (recomendado para la configuración inicial)
- **Cambios en Git**: Implementar automáticamente cuando los cambios se inserten en la rama

d. **Comportamiento de errores de métricas importantes**

- **Preguntar cada vez**: Pedir acción si se producen errores (predeterminado)
- **Error inmediato**: Error automático de canalización en caso de errores de métricas
- **Continuar inmediatamente**: Continuar a pesar de los errores

e. Haga clic en **&quot;Continuar&quot;** para continuar con la ficha **Código Source**

![Configurar canalización](/help/forms/assets/add-config-pipeline.png)

**2. Configurar canalización: ficha Código Source**

En la ficha **Código Source**:

a. **Tipo de implementación**

- Seleccione **&quot;Implementación de destino&quot;**

b. **Opciones de implementación**

- Seleccione **&quot;Config&quot;** (implementar solo archivos de configuración). Indica a Cloud Manager que se trata de una implementación de configuración.

c. **Seleccionar entorno de implementación elegible**

- Elija el entorno en el que desea implementar la configuración. En este caso, es un entorno `dev`.

d. **Definir detalles de código Source**

- **Repositorio**: seleccione el repositorio que contiene el archivo `api.yaml`. Por ejemplo, seleccione el repositorio `AEMFormsInternal-ReleaseSanity-pXXXXX-ukYYYYY`.
- **Rama Git**: Seleccione su rama. Por ejemplo, en este caso nuestro código se implementa en la rama `main`.
- **Ubicación del código**: escriba la ruta de acceso al directorio `config`. Como `api.yaml` se encuentra en la carpeta `config` en la raíz, escriba `/config`

e. Haga clic en **&quot;Guardar&quot;** para crear la canalización

![Configurar canalización](/help/forms/assets/confirm-pipeline-1.png)

### Paso 6: Implementar la configuración

Ahora que se ha creado la canalización, implemente la configuración de `api.yaml`

#### 6.1 Desde la información general de las canalizaciones

1. En la página Información general del programa, busque la tarjeta **Canalizaciones**
2. Vaya a la canalización de configuración recién creada en la lista. Por ejemplo, busque el nombre de la canalización que ha creado (por ejemplo, &quot;api-config-pipeline&quot;). Puede ver los detalles de la canalización, incluido el estado y la última ejecución.

#### 6.2 Iniciar la implementación**

1. Haga clic en el botón **&quot;Generar&quot;** (o en el icono de reproducción ▶) que se encuentra junto a la canalización
2. Confirme la implementación si se le solicita y comienza la ejecución de la canalización

![ejecutar la canalización](/help/forms/assets/run-config-pipeline.png)

#### 6.3 Verificar la implementación correcta

- Espere a que se complete la canalización.
   - Si tiene éxito, el estado cambia a &quot;Correcto&quot; (marca de verificación verde ✓).
   - Si falla, el estado cambia a &quot;Fail&quot; (Cruz roja ✗). Haga clic en **Descargar registros** para ver los detalles del error.

     ![Canalización correcta](/help/forms/assets/pipeline-suceess.png)

Ahora puede empezar a probar las API de comunicaciones de Forms. Para realizar pruebas, puede utilizar Postman, curl o cualquier otro cliente REST para invocar las API.

### Paso 7: Especificaciones y pruebas de la API

Ahora que su entorno está configurado, puede empezar a probar las API de comunicación de AEM Forms mediante la interfaz de usuario de Swagger o mediante programación desarrollando la aplicación NodeJS.

>[!BEGINTABS]

>[!TAB A. Usando la interfaz de usuario de Swagger para las pruebas de API]

La interfaz de usuario de Swagger proporciona una interfaz interactiva para probar las API sin escribir código. Use la característica **Probarla** para invocar y probar la API de comunicación de Forms [generate PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).

1. Vaya a [Referencia de la API de comunicación de Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) y abra la documentación de la [API de comunicación de Forms](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) en su explorador.
2. Expanda la sección **Generación de documentos** y seleccione [Genera un formulario PDF que se puede rellenar a partir de una plantilla XDP o PDF, opcionalmente con la combinación de datos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).
3. En el panel derecho, haga clic en **Probar**.

   ![Prueba de Swagger para API](/help/forms/assets/api-doc-generation.png)
4. Introduzca los siguientes valores:

   | **Sección** | **Parámetro** | **Valor** |
   |--------------|---------------|------------|
   | cubo | Instancia de AEM | Nombre de instancia de AEM sin el nombre de dominio de Adobe (`.adobeaemcloud.com`). Por ejemplo, use `pXXXXX-eYYYYY` como contenedor. |
   | Seguridad | Token de portador | Utilice el token de acceso [de la credencial de servidor a servidor OAuth del proyecto de Adobe Developer Console](/help/forms/oauth-api-authetication.md#how-to-generate-an-access-token-using-oauth-server-to-server-authentication) |
   | Cuerpo | plantilla | Cargue un XDP para generar el formulario de PDF. Por ejemplo, puede usar [este XDP](/help/forms/assets/ClosingForm.xdp) para generar un PDF. |
   | Cuerpo | data | Un archivo XML opcional que contiene los datos que se van a combinar con la plantilla para generar un formulario PDF rellenado previamente. Por ejemplo, puede usar [este XML](/help/forms/assets/ClosingForm.xml) para generar un PDF. |
   | Parámetros | X-Adobe-Accept-Experimental | 1 |

5. Haga clic en **Enviar** para invocar la API

   ![Enviar API](/help/forms/assets/api-send.png)

6. Compruebe la respuesta en la ficha **Respuesta**:
   - Si el código de respuesta es `200`, significa que PDF se ha creado correctamente.
   - Si el código de respuesta es `400`, significa que los parámetros de la solicitud no son válidos o tienen un formato incorrecto.
   - Si el código de respuesta es `500`, significa que hay un error interno del servidor.
   - Si el código de respuesta es `403`, significa que hay un error de autorización.

   En este caso, el código de respuesta es `200`, lo que significa que PDF se ha generado correctamente:

   ![Respuesta de revisión](/help/forms/assets/api-success.png)

   Ahora puedes descargar el [PDF](/help/forms/assets/create-pdf.pdf) creado con el botón **Descargar** y verlo en el visor de PDF:

   ![Ver PDF](/help/forms/assets/create-pdf.png)

   >[!NOTE]
   >
   > Para hacer pruebas, también puede usar [Postman](https://www.postman.com/), [curl](https://curl.se/) o cualquier otro cliente REST para invocar las API de AEM.

>[!TAB B. Desarrollando la aplicación NodeJS mediante programación]

Desarrolle una aplicación Node.js para generar un formulario PDF que se pueda rellenar a partir de una plantilla **XDP** y un archivo de datos **XML** mediante la **API de servicios de documentos**

**Requisitos previos**

- Node.js instalado en el sistema
- Instancia de AEM as a Cloud Service activa
- Token de portador para la autenticación de API desde Adobe Developer Console
- Archivo XDP de muestra: [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- Archivo XML de ejemplo: [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Para desarrollar la aplicación Node.js, siga el desarrollo paso a paso:

**Paso 1: Crear un nuevo proyecto de Node.js**

Abra cmd/terminal y ejecute los siguientes comandos:

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![Crear nuevo proyecto js de nodo](/help/forms/assets/api-1.png)

**Paso 2: Instalar Dependencias Necesarias**

Instale las bibliotecas **node-fetch**, **dotenv** y **form-data** para realizar solicitudes HTTP, leer variables de entorno y administrar datos de formulario respectivamente.

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![instalar dependencias de npm](/help/forms/assets/api-2.png)

**Paso 3: actualizar package.json**

1. Abra cmd/terminal y ejecute el comando:

   ```bash
   code .
   ```

   ![abrir proyecto en el editor](/help/forms/assets/api-3.png)

   Se abre el proyecto en el editor de código.

2. Actualice el archivo `package.json` para agregar `type` a `module`.

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![actualizar archivo de paquete](/help/forms/assets/api-4.png)

**Paso 4: Crear un archivo .env**

1. Crear archivo .env en el nivel raíz de un proyecto
2. Agregue la siguiente configuración y reemplace los marcadores de posición con los valores reales de la credencial de servidor a servidor OAuth del proyecto ADC.

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![crear archivo env](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > Puede copiar `CLIENT_ID`, `CLIENT_SECRET` y `SCOPES` del proyecto de Adobe Developer Console.

**Paso 5: Crear src/index.js**

1. Crear `index.js` archivo en el nivel raíz del proyecto
2. Agregue el siguiente código y reemplace los marcadores de posición por los valores reales:

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![crear index.js](/help/forms/assets/api-6.png)

**Paso 6: Ejecute la aplicación**

```bash
node src/index.js
```

![ejecutar aplicación](/help/forms/assets/api-7.png)

El PDF se crea en la carpeta `demo-nodejs-generate-pdf`. Vaya a la carpeta para buscar el archivo generado denominado `generatedForm.pdf`.

![ver pdf creado](/help/forms/assets/api-8.png)

![Ver PDF](/help/forms/assets/create-pdf.png)

>[!ENDTABS]

Puede abrir el [PDF generado](/help/forms/assets/create-pdf.png) para verlo.

## Resolución de problemas

### Problemas comunes y posibles causas

#### Problema 1: Error 403 prohibido

**Síntomas:**

- Las solicitudes de API devuelven `403 Forbidden`
- Mensaje de error: *Acceso no autorizado*

**Causa posible:**

- El ID de cliente no se ha registrado en la configuración `api.yaml` de la instancia de AEM

#### Problema 2: Error 401 no autorizado

**Síntomas:**

- Las solicitudes de API devuelven `401 Unauthorized`
- Mensaje de error: *Token inválido o caducado*

**Posibles causas:**

- Token de acceso caducado (solo válido durante 24 horas)
- ID de cliente y secreto de cliente incorrectos o no coincidentes

#### Problema 3: Error 404 Not Found

**Síntomas:**

- Las solicitudes de API devuelven `404 Not Found`
- Mensaje de error: *No se encontró el recurso* o no se encontró el extremo de la API *3&rbrace;*

**Causa posible:**

- Parámetro de bloque incorrecto (no coincide con el identificador de instancia de AEM)

#### Problema 4: Error de implementación de canalización

**Síntomas:**

- Error de ejecución de configuración de canalización
- Los registros de implementación muestran errores relacionados con `api.yaml`

**Posibles causas:**

- Sintaxis YAML no válida (problemas de sangría, comillas o formato de matriz)
- `api.yaml` se colocó en un directorio incorrecto
- ID de cliente incorrecto o mal formado en la configuración
- Secreto de cliente no válido

#### Problema 5: Las API de comunicación de Forms no se pueden ejecutar

**Síntomas:**

- Las solicitudes de API devuelven errores que indican funciones no admitidas o no disponibles.
- La generación de PDF mediante XDP y XML no funciona.
- La implementación de la canalización se completa correctamente, pero las llamadas de API de tiempo de ejecución fallan.

**Causa posible:**

El entorno de AEM ejecuta una versión lanzada antes de que se introdujeran o admitieran las API de comunicación de Forms.
Para actualizar el entorno de AEM, consulte la sección [Actualizar la instancia de AEM](#update-aem-instance).

## Actualizar instancia de AEM

Para actualizar la instancia de AEM para localizar los detalles del entorno:

1. Seleccione el icono `ellipsis`(...) junto al nombre del entorno y haga clic en **Actualizar**
2. Haga clic en el botón **Enviar** y ejecute la canalización de pila completa sugerida.

   ![Actualizar entorno](/help/forms/assets/update-env.png)

## Artículos relacionados

- Para obtener información sobre cómo configurar el entorno para el procesamiento por lotes (API asincrónicas), consulte [Procesamiento por lotes de comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md).