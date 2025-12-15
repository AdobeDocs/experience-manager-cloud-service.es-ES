---
title: ¿Cómo se configuran las API sincrónicas de comunicaciones interactivas?
description: Configurar el entorno de desarrollo para las API sincrónicas de comunicaciones interactivas para Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: 9401d96bcf5375dc20c33055343a5b895b4e9107
workflow-type: tm+mt
source-wordcount: '2573'
ht-degree: 2%

---


# Procesamiento de API sincrónicas de comunicaciones de AEM Forms as a Cloud Service

Esta guía proporciona instrucciones completas para configurar y utilizar las API sincrónicas de comunicaciones de AEM Forms.

Obtenga información sobre cómo configurar el entorno de AEM as a Cloud Service, habilitar el acceso a la API e invocar las API de comunicaciones mediante la autenticación de servidor a servidor OAuth.

## Requisitos previos

Para configurar un entorno para ejecutar y probar las API de comunicaciones de AEM Forms, asegúrese de que dispone de lo siguiente:

### Acceso y permisos

Asegúrese de tener los derechos de acceso y los permisos necesarios antes de empezar a configurar las API de comunicaciones.

**Permisos de usuario y función**

- Adobe ID creado en [https://account.adobe.com/](https://account.adobe.com/)
- Adobe ID asociado al correo electrónico de su organización
- Contexto de producto de Adobe Managed Services asignado
- Función de desarrollador asignada en Adobe Admin Console
- Permiso para crear proyectos en Adobe Developer Console

>[!NOTE]
>
> Para obtener más información sobre la asignación de funciones y la concesión de acceso a los usuarios, consulte el artículo [Agregar usuarios y funciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

**Acceso a Cloud Manager**

- Credenciales de inicio de sesión para [Cloud Manager](https://my.cloudmanager.adobe.com)
- Acceso para ver y administrar los entornos del programa
- Permiso para crear y ejecutar canalizaciones de CI/CD
- Acceso a los detalles y la configuración del entorno

**Acceso al repositorio Git**

- Acceso al repositorio de Git de Cloud Manager
- Credenciales de Git para clonar y transferir cambios

### Herramientas de desarrollo

- **Node.js** para ejecutar aplicaciones de ejemplo
- Última versión de **Git**
- Acceso a **Terminal/Línea de comandos**
- **Editor de texto o IDE** para editar archivos de configuración (código VS, IntelliJ, etc.)
- **Postman** o una herramienta similar para las pruebas de API

>[!NOTE]
>
> Este es un proceso único por entorno que debe completarse antes de continuar con la configuración de las API de comunicaciones de AEM Forms.

Ahora vamos a entender cada paso en detalle.

### Paso 1: Actualizar la instancia de AEM

Para actualizar la instancia de AEM:

1. **Iniciar sesión en Adobe Cloud Manager**
   1. Vaya a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Inicie sesión con su Adobe ID

2. **Ir a la descripción general del programa**
   1. Seleccione el programa en la lista. Se le redirigirá a la página Información general del programa

3. **Buscar detalles del entorno**
   1. Seleccione el icono `ellipsis`(...) junto al nombre del entorno y haga clic en **Actualizar**
   2. Haga clic en el botón **Enviar** y ejecute la canalización de pila completa sugerida.

      ![Actualizar entorno](/help/forms/assets/update-env.png)

### Paso 2: Clonar el repositorio de Git

Clone el repositorio Git de Cloud Manager para administrar sus archivos de configuración de API.

1. **Busque la sección del repositorio**
   1. En la página **Resumen del programa**, haga clic en la ficha **Repositorios**
   2. Busque el nombre del repositorio y haga clic en el menú de puntos suspensivos (...).
   3. Copiar la URL del repositorio

      >[!NOTE]
      >
      > El formato de dirección URL suele ser `https://git.cloudmanager.adobe.com/<org>/<program>/`

2. **Clonar con el comando Git**

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
      https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-p43162-uk59167/
      ```

      ![Clonando el repositorio Git](/help/forms/assets/repo-clone.png)


**Opciones de integración del repositorio Git**

Adobe Cloud Manager admite ambas opciones de repositorio:

- **Uso directo del repositorio Git de Cloud Manager**
   - Uso del repositorio de Git nativo de Cloud Manager
   - Integración integrada con canalizaciones

- **Integración con el repositorio Git administrado por el cliente**
   - Conecte su propio repositorio de Git (GitHub, GitLab, Bitbucket, etc.)
   - Configuración de la sincronización con Adobe Cloud Manager

Para obtener más información sobre cómo integrar Adobe Cloud Manager y Adobe Cloud Manager, consulte [Documentación de integración de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Paso 3: Acceso al entorno de AEM Cloud Service y al extremo de AEM Forms

Acceda a los detalles del entorno de AEM Cloud Service para obtener las direcciones URL y los identificadores necesarios para la configuración de la API.

1. **Iniciar sesión en Adobe Cloud Manager**
   1. Vaya a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
   2. Inicie sesión con su Adobe ID

2. **Ir a la descripción general del programa**
Seleccione el programa en la lista. Se le redirigirá a la página Información general del programa

3. **Acceder y ver el entorno de AEM Cloud Service**

   Puede ver o acceder a los detalles del entorno de AEM Cloud Service mediante cualquiera de las dos opciones:

   - **Opción 1: desde la página de información general**

      1. En la página **Resumen del programa**
      2. Haga clic en **&quot;Entornos&quot;** en el menú del lado izquierdo.  Puede ver una lista de todos los entornos

         ![Ver todos los entornos](/help/forms/assets/all-env.png)

      3. Haga clic en el nombre de entorno específico para ver los detalles

         ![Detalles de Opción1-Entorno](/help/forms/assets/option1-env.png)

   - **Opción 2: desde la sección Entornos**

      1. En la página Información general del programa
      2. Busque la sección **Entornos**
      3. Haga clic en **&quot;Mostrar todo&quot;** para ver todos los entornos
      4. Haga clic en el menú de **puntos suspensivos (...)** que está junto al entorno
         ![Detalles de Opción1-Entorno](/help/forms/assets/option2-env-details.png)
      5. Seleccionar **&quot;Ver detalles&quot;**

         ![Detalles de Opción1-Entorno](/help/forms/assets/option1-env.png)

4. **Buscar el extremo de AEM Forms**

   En la página de detalles de **Entorno**, tenga en cuenta los siguientes detalles:

   **URL del servicio de creación**

   - URL: `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Cubo: author-pXXXXX-eYYYY
Ejemplo: `https://author-p43162-e177398.adobeaemcloud.com`

   **URL del servicio de publicación**

   - URL: `https://publish-pXXXXX-eYYYYY.adobeaemcloud.com`
   - Contenedor: publish-pXXXXX-eYYYY
Ejemplo: `https://publish-p43162-e177398.adobeaemcloud.com`

>[!NOTE]
>
> Para ver cómo acceder al entorno de acceso a AEM Cloud Service y al extremo de AEM Forms, consulte [Documentación sobre la administración de entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=es).

### Paso 4: Configuración del acceso a API

Siga estos pasos para configurar las API de comunicaciones de AEM Forms:

#### 4.1 Configuración del proyecto de Adobe Developer Console

1. **Acceder a Adobe Developer Console**
   1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console)
   2. Inicie sesión con su Adobe ID

2. **Crear nuevo proyecto**
   1. En la sección **Inicio rápido**, haga clic en **Crear nuevo proyecto**
   2. Se crea un nuevo proyecto con un nombre predeterminado

      ![Crear proyecto ADC](/help/forms/assets/adc-home.png)

   3. Haga clic en **Editar proyecto** en la esquina superior derecha

      ![Editar proyecto](/help/forms/assets/adc-edit-project.png)

   4. Proporcione un nombre significativo (por ejemplo, &quot;formsproject&quot;)
   5. Haga clic en **Guardar**.

      ![Editar nombre de proyecto](/help/forms/assets/adc-edit-projectname.png)

#### 4.2 Añadir API de comunicación de Forms

Puede agregar diferentes API de comunicaciones de AEM Forms según sus necesidades.

**A. Para las API de servicios de documentos**

1. Haga clic en **Agregar API**

   ![Agregar API](/help/forms/assets/adc-add-api.png)

2. Seleccionar **API de comunicación de Forms**
   1. En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
   2. Seleccione **&quot;API de comunicación de Forms&quot;**

   ![Agregar API de comunicación de Forms](/help/forms/assets/adc-add-forms-api.png)


3. Seleccione el método de autenticación **OAuth Server-to-Server**

   ![Seleccionar método de autenticación](/help/forms/assets/adc-add-authentication-method.png)

**B. Para las API de tiempo de ejecución de Forms**

1. **Haga clic en Agregar API**
   - En su proyecto, haga clic en el botón **Agregar API**

   ![Agregar API](/help/forms/assets/adc-add-api.png)

2. **Seleccionar API de tiempo de ejecución y entrega de AEM Forms**
   - En el cuadro de diálogo _Agregar API_, filtrar por **Experience Cloud**
   - Seleccione **&quot;API de tiempo de ejecución y entrega de AEM Forms&quot;**
   - Haga clic en **Siguiente**

   ![Agregar API de tiempo de ejecución](/help/forms/assets/add-runtime-api.png)


3. **Método de autenticación**
   - Seleccione el método de autenticación **OAuth Server-to-Server**.


   ![Seleccionar método de autenticación](/help/forms/assets/add-authentication-for-runtime-apis.png)

#### 4.3 Añadir perfil de producto

Siga estos pasos para agregar el perfil de producto:

1. Seleccione el **perfil de producto** apropiado según el nivel de acceso requerido:

   | Tipo de acceso | Perfil del producto |
   |------------------|----------------------|
   | Acceso de solo lectura | `AEM Users - author - Program XXX - Environment XXX` |
   | Acceso de lectura y escritura | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
   | Acceso administrativo completo | `AEM Administrators - author - Program XXX - Environment XXX` |

2. Seleccione el **perfil de producto** que coincida con la dirección URL del servicio de creación (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Por ejemplo: seleccione `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

3. Haga clic en **Guardar API configurada**. La API y el perfil de producto se añaden al proyecto

   ![Seleccionar configuración del proyecto](/help/forms/assets/adc-add-product-profile.png)

#### 4.4 Generar y guardar credenciales

1. **Acceder a sus credenciales**

   1. Vaya al proyecto en Adobe Developer Console
   2. Haga clic en la credencial **OAuth de servidor a servidor**
   3. Ver la sección **Detalles de credenciales**

   ![Ver credenciales](/help/forms/assets/adc-view-credential.png)

2. **Registrar credenciales de API**

   ```text
   API Credentials:
   ================
   Client ID: <your_client_id>
   Client Secret: <your_client_secret>
   Technical Account ID: <tech_account_id>
   Organization ID: <org_id>
   Scopes: AdobeID,openid,read_organizations
   ```

#### 4.5 Generación de tokens de acceso

**A. Para pruebas**

Genere los tokens de acceso manualmente en Adobe Developer Console:

1. **Vaya a su proyecto**
   1. En Adobe Developer Console, abra el proyecto
   2. Haga clic en **Servidor a servidor de OAuth**

2. **Generar token de acceso**
   1. Haga clic en el botón **&quot;Generar token de acceso&quot;** en la sección de API del proyecto
   2. Copiar el token de acceso generado

   ![Generar token de acceso](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > El token de acceso es válido durante **24 horas**

**B. Para producción**

Genere tokens mediante programación utilizando el comando cURL:

**Credenciales requeridas:**

- ID del cliente
- Secreto de cliente
- Ámbitos (normalmente: `AdobeID,openid,read_organizations`)

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

#### 4.6 Registro del ID de cliente con el entorno de AEM

Para permitir que el ID de cliente del proyecto ADC se comunique con la instancia de AEM, debe registrarla con un archivo de configuración YAML e implementarla mediante una canalización de configuración.

1. **Localizar o crear directorio de configuración**

   1. Vaya al repositorio clonado de AEM Project y luego a la carpeta `config`
   2. Si no existe, créela en el nivel raíz del proyecto:

   ```bash
   mkdir config
   ```

2. Cree un nuevo archivo con el nombre `api.yaml` en el directorio `config`:

   ```bash
   touch config/api.yaml
   ```

3. Agregue el siguiente código al archivo `api.yaml`:

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

   Por ejemplo, agregue `allowedClientIDs` como `6bc4589785e246eda29a545d3ca55980` y envTypes como `dev`:

   ![Agregando archivo de configuración](/help/forms/assets/create-api-yaml-file.png)

4. **Cambios de confirmación y inserción**

   1. Vaya a la carpeta raíz del repositorio clonado y ejecute los siguientes comandos:


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Cambios de Git push](/help/forms/assets/push-yaml-changes-in-git.png)


5. **Configurar canalización de configuración**

   1. **Iniciar sesión en Cloud Manager**
      1. Vaya a [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
      2. Inicie sesión con su Adobe ID

   2. **Vaya a su programa**
Seleccione el programa de la lista y se le redirigirá a la página Información general del programa

   3. **Localizar la tarjeta de canalizaciones**
      1. Busque la tarjeta **Canalizaciones** en la página Información general del programa
      1. Haga clic en el botón **&quot;Agregar&quot;**

   4. **Seleccionar tipo de canalización**

      - **Para Entornos De Desarrollo**: Seleccione **&quot;Agregar Canalización Que No Sea De Producción&quot;**. Las canalizaciones que no son de producción son para entornos de desarrollo y ensayo

      - **Para Entornos De Producción**: Seleccione **&quot;Agregar Canalización De Producción&quot;**. Las canalizaciones de producción requieren aprobaciones adicionales

        >[!NOTE]
        >
        > En este caso, cree una canalización que no sea de producción, ya que hay un entorno de desarrollo disponible.

   5. **Configurar canalización: ficha Configuración**

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

   6. **Configurar canalización: ficha Código Source**

      En la ficha **Código Source**:

      a. **Tipo de implementación**
      - Seleccione **&quot;Implementación de destino&quot;**

      b. **Opciones de implementación**
      - Seleccione **&quot;Config&quot;** (implementar solo archivos de configuración). Indica a Cloud Manager que se trata de una implementación de configuración.

      c. **Seleccionar entorno de implementación elegible**
      - Elija el entorno en el que desea implementar la configuración. En este caso, es un entorno `dev`.

      d. **Definir detalles de código Source**

      - **Repositorio**: seleccione el repositorio que contiene el archivo `api.yaml`. Por ejemplo, seleccione el repositorio `AEMFormsInternal-ReleaseSanity-p43162-uk59167`.
      - **Rama Git**: Seleccione su rama. Por ejemplo, en este caso nuestro código se implementa en la rama `main`.
      - **Ubicación del código**: escriba la ruta de acceso al directorio `config`. Como `api.yaml` se encuentra en la carpeta `config` en la raíz, escriba `/config`

      e. Haga clic en **&quot;Guardar&quot;** para crear la canalización

      ![Configurar canalización](/help/forms/assets/confirm-pipeline-1.png)

6. **Implementar configuración**

   Ahora que se ha creado la canalización, implemente la configuración de `api.yaml`:

   1. **De la descripción general de canalizaciones**
      1. En la página Información general del programa, busque la tarjeta **Canalizaciones**
      2. Vaya a la canalización de configuración recién creada en la lista. Por ejemplo, busque el nombre de la canalización que ha creado (por ejemplo, &quot;api-config-pipeline&quot;). Puede ver los detalles de la canalización, incluido el estado y la última ejecución.

   2. **Iniciar la implementación**
      1. Haga clic en el botón **&quot;Generar&quot;** (o en el icono de reproducción ▶) que se encuentra junto a la canalización
      2. Confirme la implementación si se le solicita y comienza la ejecución de la canalización

      ![ejecutar la canalización](/help/forms/assets/run-config-pipeline.png)

   3. **Verificar implementación correcta**
      - Espere a que se complete la canalización.
         - Si tiene éxito, el estado cambia a &quot;Correcto&quot; (marca de verificación verde ✓).
         - Si falla, el estado cambia a &quot;Fail&quot; (Cruz roja ✗). Haga clic en **Descargar registros** para ver los detalles del error.

           ![Canalización correcta](/help/forms/assets/pipeline-suceess.png)

      Ahora puede empezar a probar las API de comunicaciones de Forms. Para realizar pruebas, puede utilizar Postman, curl o cualquier otro cliente REST para invocar las API.

### Paso 5: Especificaciones y pruebas de la API

Ahora que su entorno está configurado, puede empezar a probar las API de comunicación de AEM Forms usando [Swagger UI](#a-using-swagger-ui-for-api-testing) o programáticamente desarrollando la aplicación NodeJS.

En este ejemplo, generemos un PDF con las API de servicios de documentos que utilizan la plantilla y el archivo XDP.

#### A. Usar la interfaz de usuario de Swagger para las pruebas de API

La interfaz de usuario de Swagger proporciona una interfaz interactiva para probar las API sin escribir código. Use la característica **Probarla** para invocar y probar la API del servicio de documentos [generate PDF](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).

1. Vaya a la documentación de API
   - API de Forms: [Referencia de API de Forms](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
   - Servicios de documentos: [Referencia de API de servicios de documentos](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)
Abra la documentación de [API de servicios de documentos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) en su explorador.
2. Expanda la sección **Generación de documentos** y seleccione [Genera un formulario PDF que se puede rellenar a partir de una plantilla XDP o PDF, opcionalmente con la combinación de datos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).
3. En el panel derecho, haga clic en **Probar**.

   ![Prueba de Swagger para API](/help/forms/assets/api-doc-generation.png)
4. Introduzca los siguientes valores:

   | **Sección** | **Parámetro** | **Valor** |
   |--------------|---------------|------------|
   | cubo | Instancia de AEM | Nombre de instancia de AEM sin el nombre de dominio de Adobe (`.adobeaemcloud.com`). Por ejemplo, use `p43162-e177398` como contenedor. |
   | Seguridad | Token de portador | Utilice el token de acceso de la credencial de servidor a servidor OAuth del proyecto de Adobe Developer Console |
   | Cuerpo | plantilla | Cargue un XDP para generar el formulario de PDF. Por ejemplo, puede usar [este XDP](/help/forms/assets/ClosingForm.xdp) para generar un PDF. |
   | Cuerpo | data | Un archivo XML opcional que contiene los datos que se van a combinar con la plantilla para generar un formulario PDF rellenado previamente. Por ejemplo, puede usar [este XML](/help/forms/assets/ClosingForm.xml) para generar un PDF. |
   | Parámetros | X-Adobe-Accept-Experimental | 1 |

5. Haga clic en **Enviar** para invocar la API

   ![Enviar API](/help/forms/assets/api-send.png)

6. Compruebe la respuesta en la ficha **Respuesta**:
   - Si el código de respuesta es `200`, significa que PDF se ha creado correctamente.
   - Si el código de respuesta es `400`, significa que los parámetros de la solicitud no son válidos o tienen un formato incorrecto.
   - Si el código de respuesta es `500`, significa que hay un error interno del servidor.

   En este caso, el código de respuesta es `200`, lo que significa que PDF se ha generado correctamente:

   ![Respuesta de revisión](/help/forms/assets/api-success.png)

   Ahora puedes descargar el [PDF](/help/forms/assets/create-pdf.pdf) creado con el botón **Descargar** y verlo en el visor de PDF:

   ![Ver PDF](/help/forms/assets/create-pdf.png)

>[!NOTE]
>
> Para hacer pruebas, también puede usar [Postman](https://www.postman.com/), [curl](https://curl.se/) o cualquier otro cliente REST para invocar las API de AEM.

#### B. Mediante programación, desarrollando la aplicación NodeJS

Desarrolle una aplicación Node.js para generar un formulario PDF que se pueda rellenar a partir de una plantilla **XDP** y un archivo de datos **XML** mediante la **API de servicios de documentos**

##### Requisitos previos

- Node.js instalado en el sistema
- Instancia de AEM as a Cloud Service activa
- Token de portador para la autenticación de API desde Adobe Developer Console
- Archivo XDP de muestra: [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- Archivo XML de ejemplo: [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Para desarrollar la aplicación Node.js, siga el desarrollo paso a paso:

##### Paso 1: Crear un nuevo proyecto de Node.js

Abra cmd/terminal y ejecute los siguientes comandos:

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![Crear nuevo proyecto js de nodo](/help/forms/assets/api-1.png)

##### Paso 2: Instalar las dependencias necesarias

Instale las bibliotecas **node-fetch**, **dotenv** y **form-data** para realizar solicitudes HTTP, leer variables de entorno y administrar datos de formulario respectivamente.

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![instalar dependencias de npm](/help/forms/assets/api-2.png)

##### Paso 3: Actualización de package.json

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

##### Paso 4: Crear un archivo .env

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

##### Paso 5: Crear src/index.js

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

##### Paso 6: Ejecutar la aplicación

```bash
node src/index.js
```

![ejecutar aplicación](/help/forms/assets/api-7.png)

El PDF se crea en la carpeta `demo-nodejs-generate-pdf`. Vaya a la carpeta para buscar el archivo generado denominado `generatedForm.pdf`.

![ver pdf creado](/help/forms/assets/api-8.png)

Puede abrir el [PDF generado](/help/forms/assets/create-pdf.png) para verlo.

## Resolución de problemas

### Problemas comunes y posibles causas

#### Problema 1: Error 403 prohibido

**Síntomas:**

- Las solicitudes de API devuelven `403 Forbidden`
- Mensaje de error: *Acceso denegado* o *Permisos insuficientes*
- Se produce incluso con un token de acceso válido

**Posibles causas:**

- Permisos insuficientes en el perfil de producto vinculado a la credencial de servidor a servidor de OAuth
- El grupo de usuarios de servicio del Autor de AEM carece de los permisos necesarios en las rutas de contenido requeridas

#### Problema 2: Error 401 no autorizado

**Síntomas:**

- Las solicitudes de API devuelven `401 Unauthorized`
- Mensaje de error: *Token inválido o caducado*

**Posibles causas:**

- Token de acceso caducado (solo válido durante 24 horas)
- ID de cliente y secreto de cliente incorrectos o no coincidentes
- Faltan encabezados de autenticación o tienen un formato incorrecto en la solicitud de API

#### Problema 3: Error 404 Not Found

**Síntomas:**

- Las solicitudes de API devuelven `404 Not Found`
- Mensaje de error: *No se encontró el recurso* o no se encontró el extremo de la API *3&rbrace;*

**Posibles causas:**

- El ID de cliente no se ha registrado en la configuración `api.yaml` de la instancia de AEM
- Parámetro de bloque incorrecto (no coincide con el identificador de instancia de AEM)
- ID de recurso no válido o inexistente (formulario o recurso)

#### Problema 4: Opción de autenticación de servidor a servidor no disponible

**Síntomas:**

- Falta la opción de servidor a servidor OAuth o está deshabilitada en Adobe Developer Console

**Causa posible:**

- El usuario que crea la integración no se agrega como **desarrollador** en el perfil de producto asociado

#### Problema 5: Error de implementación de canalización

**Síntomas:**

- Error de ejecución de configuración de canalización
- Los registros de implementación muestran errores relacionados con `api.yaml`

**Posibles causas:**

- Sintaxis YAML no válida (problemas de sangría, comillas o formato de matriz)
- `api.yaml` se colocó en un directorio incorrecto
- ID de cliente incorrecto o mal formado en la configuración


## Artículos relacionados

Para obtener información sobre cómo configurar el entorno para el procesamiento por lotes (API asincrónicas), consulte [Procesamiento por lotes de comunicaciones de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md).
