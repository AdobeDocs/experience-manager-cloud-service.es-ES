---
title: Invocar una interfaz de usuario asociada en una instancia de publicación
description: Aprenda a integrar e invocar la IU asociada de AEM Forms en instancias de publicación para permitir a los profesionales del lado del cliente generar comunicaciones interactivas personalizadas en tiempo real.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
hidefromtoc: true
source-git-commit: 6b90e8f2d26d6bfd22fbd94af0d6c68466c69bbb
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---


# Generar comunicaciones personalizadas con la interfaz de usuario asociada

<span>: la capacidad de comunicación interactiva está disponible en el programa de usuarios que la adoptaron por primera vez. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.</span>

La IU asociada se puede invocar directamente en las instancias de publicación, lo que permite a los profesionales de cara al cliente, como los asociados de campo y los agentes de servicio, generar comunicaciones personalizadas en tiempo real durante las interacciones con los clientes.

La siguiente tabla muestra los distintos escenarios reales en los que la interfaz de usuario de Associate se puede utilizar para enviar mensajes personalizados a los clientes:

| Industria | Caso práctico |
|----------|----------|
| **Servicios financieros** | Generar cartas de confirmación de préstamo en tiempo real, extractos de cuentas y resúmenes de perfil de riesgo durante las reuniones con los clientes |
| **Seguro** | Produzca tarjetas de prueba de seguro instantáneas y resúmenes de disposición de reclamaciones en los mostradores de servicio |
| **Atención sanitaria** | Crear resúmenes de planes de tratamiento de pacientes con importes y horarios de copago calculados |
| **Gobierno** | Generar informes de verificación policial, recibos de servicio ciudadano y resúmenes de actualización de casos en el lugar |

## Requisitos previos

Antes de integrar la interfaz de usuario de Associate con su aplicación, asegúrese de lo siguiente:

- Instancia de publicación de AEM Forms Cloud Service
- Comunicación interactiva creada y publicada en AEM
- Explorador con compatibilidad emergente habilitada
- Los usuarios asociados deben formar parte del grupo **forms-associates**
- Autenticación configurada - [SAML 2.0](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)

>[!NOTE]
>
> Para la interfaz de usuario asociada, se requieren configuraciones de SAML adicionales más allá de la configuración estándar explicada en el artículo [Autenticación SAML 2.0](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/authentication/saml-2-0). Consulte la sección [Configuraciones adicionales de SAML para la interfaz de usuario asociada](#additional-saml-configurations-for-associate-ui) para obtener más información.

### Configuraciones adicionales de SAML para la IU asociada

Al configurar la autenticación SAML 2.0 para la interfaz de usuario asociada, debe aplicar la siguiente configuración específica en los archivos de configuración OSGi.

#### Controlador de autenticación SAML

Crear el archivo `com.adobe.granite.auth.saml.SamlAuthenticationHandler~saml.cfg.json` en `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
  {
    "path": ["/libs/fd/associate"],
    "serviceProviderEntityId": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com",
    "assertionConsumerServiceURL": "https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/saml_login",
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

Actualizar el archivo `org.apache.sling.engine.impl.auth.SlingAuthenticator~saml.cfg.json` en `ui.config/src/main/content/jcr_root/apps/<project-name>/osgiconfig/config.publish`:

```json
{
  "sling.auth.requirements": ["+/libs/fd/associate/ui.html"],
  "sling.auth.anonymous": false
}
```

#### Filtro de Dispatcher

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

Para invocar la IU asociada desde la aplicación, configure la URL de instancia de publicación, prepare la carga útil de datos y utilice la función de integración para iniciar la IU asociada en una nueva ventana del explorador.

### Paso 1: Configurar la URL de instancia de publicación

Se accede a la interfaz de usuario asociada a través de un punto final específico en la instancia de publicación de AEM Forms Cloud Service:

```javascript
const AEM_URL = 'https://publish-p{program-id}-e{env-id}.adobeaemcloud.com/libs/fd/associate/ui.html';
```

Reemplace `{program-id}` y `{env-id}` por sus valores de entorno reales.

### Paso 2: Preparar la carga útil de datos

Estructurar la carga útil de datos con el siguiente formato:

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
| `prefill` | No | Contiene la configuración de servicio para el prerrellenado de datos. |
| `prefill.serviceName` | No | Nombre del servicio del modelo de datos de formulario que se invocará para rellenar previamente los datos |
| `prefill.serviceParams` | No | Pares de clave-valor pasados al servicio de relleno previo |
| `options` | No | Propiedades adicionales admitidas para el procesamiento en PDF: locale, includeAttachments, embedFonts, makeAccessible |

### Paso 3: Implementar la función de integración

Cree una función de JavaScript para iniciar la interfaz de usuario de Associate y gestionar la comunicación de mensajes:

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

### Paso 4: Invocar la función

Llame a la función con los parámetros adecuados:

```javascript
// Basic invocation with IC ID only
launchAssociateUI('12345', '', {}, {});

// With prefill service
launchAssociateUI('12345', 'FdmTestData', 
  { customerId: '101'}, {});

// With all parameters
launchAssociateUI('12345', 'FdmTestData', 
  { policyNumber: 'POL-123' }, 
  { locale: 'en', acrobatVersion: 'Acrobat_11' });
```

## Prueba de la integración con una página de HTML de muestra

Para observar cómo aparece la interfaz de usuario de Associate en el front-end y probar la integración, aquí tiene un ejemplo sencillo de HTML. Esta página de ejemplo le permite introducir el ID de CI, configurar los parámetros del servicio de relleno previo, establecer las opciones de PDF e iniciar la interfaz de usuario de asociación en la instancia de publicación.

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

### Cómo funciona el ejemplo

1. **Campo de ID de CI**: escriba el identificador de la comunicación interactiva (obligatorio)
2. **Servicio de relleno previo**: especifique el nombre del servicio del modelo de datos de formulario para rellenar previamente los datos
3. **Parámetros de servicio**: escriba un objeto JSON con parámetros para pasar al servicio de relleno previo
4. **Opciones**: escriba las opciones de configuración de PDF, por ejemplo, locale, includeAttachments, embedFonts, makeAccessible
5. **Botón de inicio**: abre la interfaz de usuario asociada en una nueva ventana y envía los datos de inicialización

## Ejemplos de carga útil de datos

### Carga útil mínima (solo IC)

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

### Con datos de relleno previo

Use esto para rellenar dinámicamente la CI con datos del cliente:

```json
{
  "id": "12345",
  "prefill": {
    "serviceName": "FdmTestData",
    "serviceParams": {
      "customerId": "101",
      "accountNumber": "ACC-98765"
    }
  },
  "options": {}
}
```

### Con configuración de opciones

Utilice esto para especificar opciones de renderización adicionales:

```json
{
  "id": "12345ß",
  "prefill": {
    "serviceName": "FdmTestData",
    "serviceParams": { 
      "policyNumber": "POL-123" 
    }
  },
  "options": { 
      locale: "en_US",
      includeAttachments: "true",
      webOptimized: "false",
      embedFonts: "false",
      makeAccessible: "false"
  }
}
```

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

## Prácticas recomendadas

Al implementar la integración de la interfaz de usuario asociada, siga estas prácticas recomendadas:

1. **Validación**: Valide siempre el ID de CI y la carga útil JSON antes de enviar
2. **Control de errores**: Implemente el control de errores adecuado para `window.open()` errores
3. **Experiencia del usuario**: Mostrar un indicador de carga mientras se inicializa la interfaz de usuario asociada
4. **Administración de memoria**: quite detectores de eventos después de la inicialización para evitar pérdidas de memoria
5. **Pruebas**: pruebe la integración con bloqueadores de ventanas emergentes habilitados para garantizar una administración correcta
6. **Permisos de usuario**: compruebe que los usuarios tengan acceso adecuado al grupo de asociados de formularios

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Comunicaciones interactivas en la nube](/help/forms/early-access-ea-features.md#interactive-communications-on-cloud)
- [Funciones de acceso anticipado](/help/forms/early-access-ea-features.md)