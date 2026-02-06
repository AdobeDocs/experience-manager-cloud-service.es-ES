---
title: Integrar la interfaz de usuario asociada para las comunicaciones interactivas en tiempo de ejecución
description: Aprenda a integrar la interfaz de usuario de AEM Forms Associate con su aplicación para permitir a los profesionales del lado del cliente generar comunicaciones interactivas personalizadas en tiempo real en instancias de publicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: b76f6dfe2462cec187d549234e9050f8ca9a8cdf
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 2%

---


# Integración de la interfaz de usuario asociada en la aplicación

<span>: la capacidad de comunicación interactiva está disponible en el programa de usuarios que la adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.</span>

Este artículo explica cómo integrar la interfaz de usuario de Associate con la aplicación, lo que permite a los profesionales de cara al cliente, como los asociados de campo y los agentes de servicio, generar comunicaciones interactivas personalizadas en tiempo real en instancias de publicación.

## Requisitos previos

Antes de integrar la interfaz de usuario de Associate con su aplicación, asegúrese de lo siguiente:

- Comunicación interactiva creada y publicada
- Explorador con compatibilidad emergente habilitada
- Los usuarios de la asociación [deben formar parte del grupo de asociados de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-roles#assign-a-role-to-users-and-groups)
- Autenticación configurada utilizando cualquier mecanismo de autenticación [admitido por AEM](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/authentication/authentication) (por ejemplo, SAML 2.0, OAuth o controladores de autenticación personalizados)

>[!NOTE]
>
>- Este artículo muestra la configuración de autenticación usando SAML 2.0 con [Microsoft Entra ID (Azure AD) como proveedor de identidad](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings).
>- Para la interfaz de usuario asociada, se requieren configuraciones de SAML adicionales más allá de la configuración estándar explicada en el artículo [Autenticación SAML 2.0](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Consulte la sección [Configuraciones adicionales de SAML para la interfaz de usuario asociada](#additional-saml-configurations-for-associate-ui) para obtener más información.

### Configuraciones adicionales de SAML para la IU asociada

Al configurar la autenticación SAML 2.0 para la interfaz de usuario asociada, debe aplicar la siguiente configuración específica en los archivos de configuración OSGi.

#### Controlador de autenticación SAML

El controlador de autenticación SAML es una configuración de fábrica de OSGi que permite varias configuraciones SAML para diferentes árboles de recursos. Esto habilita las implementaciones de AEM en varios sitios y le permite agregar recursos de la IU asociada a la configuración de SAML existente.

Crear el archivo `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` en `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login"
    "idpUrl": "https://login.microsoftonline.com/{azure-tenant-id}/saml2",
    "idpCertAlias": "{your-certificate-alias}",
    "idpIdentifier": "https://sts.windows.net/{azure-tenant-id}/",
    "userIDAttribute": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
    "createUser": true,
    "userIntermediatePath": "saml",
    "synchronizeAttributes": [
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname=profile/givenName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname=profile/familyName",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress=profile/email"
      ],
      "addGroupMemberships": true,
      "defaultGroups": ["forms-associates"],
      "defaultRedirectUrl": "/libs/fd/associate/ui.html",
      "idpHttpRedirect": false,
      "service.ranking": 5002
  }
```

| Propiedad | Descripción |
|----------|-------------|
| `path` | Debe establecerse en `/libs/fd/associate` para la interfaz de usuario asociada |
| `defaultGroups` | Establezca `forms-associates` para asignar automáticamente usuarios al grupo requerido |
| `defaultRedirectUrl` | Redirige a los usuarios autenticados a la interfaz de usuario asociada |
| `idpHttpRedirect` | Debe ser `false` para el flujo iniciado por SP |
| `idpCertAlias` | Debe coincidir exactamente con el alias del certificado en el almacén de confianza (distingue mayúsculas de minúsculas) |

#### Sling Authenticator

El autenticador de Sling aplica la autenticación para acceder a los recursos de la IU asociada en la publicación.

Actualizar el archivo `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` en `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Filtro de Dispatcher

Añada las siguientes reglas para asegurarse de que las API de comunicaciones interactivas y la interfaz de usuario asociada funcionan correctamente en la instancia de publicación.

Si aún no lo está, agregue las siguientes reglas al archivo `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

```json
  # Allow Interactive Communications APIs and Associate UI
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/adobe/communications" }
  /XXXX { /type "allow" /method '(GET|POST|OPTIONS)' /url "/adobe/communications/*" }
  /XXXX { /type "allow" /method "GET" /url "/content/dam/fd:fonts/*" }
  /XXXX { /type "allow" /method '(GET|OPTIONS)' /url "/libs/fd/associate/*" }
```

>[!NOTE]
>
> Reemplazar `XXXX` con la secuencia numérica adecuada usada en el archivo `filters.any` existente.

## Invocando la IU asociada en la instancia de publicación

Esta sección le guiará a través del inicio de la interfaz de usuario de Associate desde su propia aplicación. Siga estos pasos para empezar rápidamente: empiece con una página de muestra de HTML lista para usar y, a continuación, configúrela para su entorno.

### Paso 1: Comience con la Página de HTML de muestra

Para probar y comprender rápidamente cómo funciona la integración de la interfaz de usuario de Associate, utilice la siguiente página de muestra de HTML. Copie este código en un archivo de HTML y ábralo en su explorador.

Este ejemplo proporciona una interfaz de formulario sencilla en la que puede introducir los detalles de la comunicación interactiva e iniciar la interfaz de usuario de Associate con un solo clic.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Associate UI Integration</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
    }
    .form-group {
      margin: 20px 0;
    }
    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    textarea {
      height: 80px;
      font-family: monospace;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      border-radius: 4px;
    }
    .btn-primary {
      background: #007bff;
      color: white;
      border: none;
    }
    .btn-primary:hover {
      background: #0056b3;
    }
    .error {
      color: red;
      font-size: 12px;
      display: none;
    }
  </style>
</head>
<body>
  <h1>Launch Associate UI</h1>

  <form id="form">
    <div class="form-group">
      <label>IC ID *</label>
      <input type="text" id="icId" placeholder="Enter Interactive Communication ID" required>
    </div>

    <div class="form-group">
      <label>Prefill Service</label>
      <input type="text" id="serviceName" placeholder="e.g., CustomerDataService">
    </div>

    <div class="form-group">
      <label>Service Parameters (JSON)</label>
      <textarea id="serviceParams" placeholder='{"customerId": "12345"}'>{}</textarea>
      <span id="paramsError" class="error">Invalid JSON format</span>
    </div>

    <div class="form-group">
      <label>Options (JSON)</label>
      <textarea id="options" placeholder='{"mode": "edit", "locale": "en_US"}'>{}</textarea>
      <span id="optionsError" class="error">Invalid JSON format</span>
    </div>

    <button type="button" onclick="reset()">Reset</button>
    <button type="button" class="btn-primary" onclick="launch()">Launch Associate UI</button>
  </form>

  <script>
    // Replace with your AEM Publish instance URL
    const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';

    function validateJSON(str, errorId) {
      const err = document.getElementById(errorId);
      try {
        const obj = JSON.parse(str || '{}');
        err.style.display = 'none';
        return obj;
      } catch (e) {
        err.style.display = 'block';
        return null;
      }
    }

    function launch() {
      const icId = document.getElementById('icId').value.trim();
      if (!icId) {
        alert('IC ID is required');
        return;
      }

      const params = validateJSON(document.getElementById('serviceParams').value, 'paramsError');
      const opts = validateJSON(document.getElementById('options').value, 'optionsError');

      if (!params || !opts) {
        alert('Please fix JSON errors before launching');
        return;
      }

      const data = {
        id: icId,
        prefill: {
          serviceName: document.getElementById('serviceName').value.trim(),
          serviceParams: params
        },
        options: opts
      };

      const win = window.open(AEM_URL, '_blank');
      if (!win) {
        alert('Pop-up blocked. Please enable pop-ups for this site.');
        return;
      }

      const handler = (e) => {
        if (e.data && e.data.type === 'READY' && e.data.source === 'APP') {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      };

      window.addEventListener('message', handler);

      // Fallback timeout in case READY message is missed
      setTimeout(() => {
        if (win && !win.closed) {
          win.postMessage({ type: 'INIT', source: 'PORTAL', data }, '*');
          window.removeEventListener('message', handler);
        }
      }, 1000);
    }

    function reset() {
      document.getElementById('form').reset();
      document.getElementById('serviceParams').value = '{}';
      document.getElementById('options').value = '{}';
      document.getElementById('paramsError').style.display = 'none';
      document.getElementById('optionsError').style.display = 'none';
    }
  </script>
</body>
</html>
```

### Paso 2: Configuración de la URL de instancia de publicación

Para poder iniciar la interfaz de usuario de Associate, debe apuntar el ejemplo a la instancia de publicación de AEM Forms Cloud Service.

En el ejemplo de HTML anterior, busque la línea siguiente en la sección `<script>`:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Reemplace los valores de marcador de posición con los detalles del entorno real:
- `{program-id}`: Su ID de programa de AEM Cloud Service
- `{env-id}`: su ID de entorno

Por ejemplo, si el identificador de programa es `12345` y el identificador de entorno es `67890`, la dirección URL pasa a ser:

```javascript
const AEM_URL = 'https://publish-p12345`-e67890.adobeaemcloud.com/libs/fd/associate/ui.html';
```

>[!NOTE]
>
> Por motivos de seguridad, los parámetros como el ID de comunicación interactiva, el servicio de relleno previo y los parámetros de servicio no se pasan a través de la dirección URL. En su lugar, estos parámetros se pasan de forma segura mediante la API `postMessage` de JavaScript.

### Paso 3: Comprender la función de integración de JavaScript

El HTML de ejemplo utiliza la siguiente función de JavaScript para iniciar la interfaz de usuario de Associate. Esta función valida el ID de CI, construye la carga útil de datos, abre la interfaz de usuario asociada en una nueva ventana del explorador y envía los datos mediante la API `postMessage` del explorador.

```javascript
function launchAssociateUI(icId, prefillService, prefillParams, options) {
  if (!icId) {
    console.error('IC ID required');
    return;
  }

  const data = {
    id: icId,
    prefill: {
      serviceName: prefillService || '',
      serviceParams: prefillParams || {}
    },
    options: options || {}
  };

  const AEM_URL = 'https://your-aem.adobeaemcloud.com/libs/fd/associate/ui.html';
  const win = window.open(AEM_URL, '_blank');

  if (!win) {
    alert('Please enable pop-ups for this site');
    return;
  }

  const readyHandler = (event) => {
    if (event.data && event.data.type === 'READY' && event.data.source === 'APP') {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  };

  window.addEventListener('message', readyHandler);

  // Fallback timeout in case READY message is missed
  setTimeout(() => {
    if (win && !win.closed) {
      win.postMessage({ type: 'INIT', source: 'PORTAL', data: data }, '*');
      window.removeEventListener('message', readyHandler);
    }
  }, 1000);
}
```

La función acepta cuatro parámetros: el ID de CI (obligatorio), el nombre del servicio de relleno previo, los parámetros del servicio de relleno previo y las opciones adicionales. Estos parámetros se estructuran en la carga útil de datos como se describe a continuación.

### Paso 4: Comprender la estructura de carga útil de datos

**Formato de carga útil:**

```javascript
const data = {
  id: "your-ic-id",              // Required: Interactive Communication ID
  prefill: {                      // Optional: Data to prefill the IC
    serviceName: "YourService",
    serviceParams: { key: "value" }
  },
  options: {}                     // Optional: Additional configuration options
};
```

**Componentes de carga útil:**

| Componente | Requerido | Descripción |
|-----------|----------|-------------|
| `id` | Sí | El identificador de la comunicación interactiva (CI) que se va a cargar |
| `prefill` | Opcional | Contiene la configuración de servicio para rellenar previamente los datos |
| `prefill.serviceName` | Opcional | Nombre del servicio del modelo de datos de formulario que se invocará para rellenar previamente los datos |
| `prefill.serviceParams` | Opcional | Pares de clave-valor pasados al servicio de relleno previo |
| `options` | Opcional | Propiedades adicionales admitidas para el procesamiento en PDF: locale, includeAttachments, embedFonts, makeAccessible |

#### Ejemplos de carga útil de datos

**Carga útil mínima (solo ID de CI)**

Utilice esta opción cuando no se requieran datos de relleno previo:

```json
{
  "id": "12345",
  "prefill": { 
    "serviceName": "", 
    "serviceParams": {} 
  },
  "options": {}
}
```

**Con Datos De Relleno Previo**

Use esto para rellenar dinámicamente la CI con datos del cliente:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

**Con Opciones De Procesamiento De PDF**

Utilice esto para especificar opciones de renderización adicionales:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "IC_FDM",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": { 
      "locale": "en_US",
      "includeAttachments": "true",
      "webOptimized": "false",
      "embedFonts": "false",
      "makeAccessible": "false"
  }
}
```

### Paso 5: Introduzca el ID de CI e inicie la interfaz de usuario asociada

Ahora está listo para iniciar la interfaz de usuario de Associate mediante la página de HTML de ejemplo:

1. **Escriba el Id. de CI**: en el campo **Id. de CI**, escriba el identificador de la comunicación interactiva publicada. Este es el único campo obligatorio.

2. **Configurar servicio de relleno previo** (opcional): si desea rellenar previamente la CI con datos dinámicos, escriba el nombre del servicio del modelo de datos de formulario en el campo **Servicio de relleno previo**. Por ejemplo, use `FdmTestData` para datos de ejemplo o `IC-FDM` para datos de prueba.

3. **Agregar parámetros de servicio** (opcional): en el campo **Parámetros de servicio (JSON)**, escriba un objeto JSON con los parámetros que requiere su servicio de relleno previo. Por ejemplo:

   ```json
   {"customerId": "101", "accountNumber": "ACC-98765"}
   ```

4. **Establecer opciones de PDF** (opcional): en el campo **Opciones (JSON)**, configure opciones de procesamiento como configuración regional, archivos adjuntos o de accesibilidad.

5. **Haga clic en Iniciar la interfaz de usuario asociada**: Haga clic en el botón **Iniciar la interfaz de usuario asociada**. Se abrirá una nueva ventana del explorador con la interfaz de usuario de Associate, precargada con la comunicación interactiva.

>[!NOTE]
>
> Si la ventana no se abre, compruebe que el explorador permite ventanas emergentes para este sitio.

## Solución de problemas

### Ventana emergente bloqueada

**Problema**: La ventana Asociar interfaz de usuario no se abre.

**Solución**:
- Habilitar ventanas emergentes para su dominio en la configuración del explorador
- Asegúrese de que se llame a `window.open()` desde una acción del usuario (por ejemplo, hacer clic en un botón)
- Realizar pruebas con distintos exploradores para identificar el comportamiento de bloqueo

### Datos que no se cargan

**Problema**: la comunicación interactiva se abre pero los datos no se rellenan.

**Solución**:
- Verificar que el ID de CI es correcto y que se ha publicado el IC
- Busque errores de JavaScript en la consola del explorador
- Asegúrese de que la estructura `postMessage` coincida exactamente con la especificación
- Compruebe que el servicio del modelo de datos de formulario está configurado correctamente

### Error de autenticación

**Problema**: el usuario recibe un error de autenticación cuando se abre la interfaz de usuario asociada.

**Solución**:
- Configurar la autenticación SAML 2.0 en la instancia de publicación
- Compruebe que el usuario forma parte del grupo **forms-associates**
- Comprobar configuración de tiempo de espera de sesión

### Errores de CORS

**Problema**: Errores de uso compartido de recursos de origen cruzado en la consola.

**Solución**:
- Para desarrollo: usar `'*'` como origen de destino en `postMessage`
- Para producción: especifique la dirección URL de origen exacta de la aplicación
- Asegúrese de que la configuración de CORS de instancia de publicación permite el dominio de aplicación

<!--## Best Practices

When implementing the Associate UI integration, follow these best practices:

1. **Validation**: Always validate the IC ID and JSON payload before sending
2. **Error Handling**: Implement proper error handling for `window.open()` failures
3. **User Experience**: Display a loading indicator while the Associate UI initializes
4. **Memory Management**: Remove event listeners after initialization to prevent memory leaks
5. **Testing**: Test the integration with popup blockers enabled to ensure graceful handling
6. **User Permissions**: Verify users have appropriate access to the forms-associates group-->

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Comunicaciones interactivas en la nube](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [Funciones de acceso anticipado](/help/forms/early-access-ea-features.md)