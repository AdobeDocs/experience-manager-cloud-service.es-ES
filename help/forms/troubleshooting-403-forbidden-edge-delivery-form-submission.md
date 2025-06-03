---
title: Solución de problemas de errores 403 prohibidos en el envío de formularios Edge Delivery Services
description: Obtenga información sobre cómo diagnosticar y resolver errores prohibidos 403 al enviar formularios de Edge Delivery Services a AEM Publish. Esta guía cubre causas comunes, incluidos CORS, reglas de Dispatcher y problemas del Filtro de referente.
feature: Edge Delivery Services, Forms
role: Admin, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 3%

---


# Solución de problemas de errores 403 prohibidos en el envío de formularios Edge Delivery Services {#troubleshooting-403-forbidden-edge-delivery}

Al enviar formularios desde Edge Delivery Services a AEM Publish, puede encontrar un error **403 Prohibido**. Este error indica que el servidor se niega a procesar la solicitud, normalmente debido a configuraciones de seguridad. Este artículo le ayuda a identificar y resolver las causas más comunes de este problema.

## Descripción del problema

Los usuarios experimentan un error **403 prohibido** al enviar formularios de Edge Delivery Services a AEM Publish. El error se muestra de la siguiente manera:

- Código de estado HTTP: 403
- Mensaje de error: &quot;Prohibido&quot; o &quot;Acceso denegado&quot;
- El envío del formulario falla sin llegar al servlet de envío de AEM

Este problema suele ocurrir en integraciones de Edge Delivery Services en las que formularios alojados en dominios de Edge (`.aem.live`, `.aem.page`, `.hlx.page`, `.hlx.live`) intentan enviar datos a instancias de publicación de AEM.

>[!IMPORTANT]
>
>Con las configuraciones de reprocesamiento, se pueden alojar varios sitios con el mismo repositorio. Cada dominio del sitio debe agregarse individualmente a las listas de permitidos para que los envíos de formularios funcionen correctamente.
>
>**Ejemplo:**
>
>- Repositorio: `https://github.com/adobe/abc`
>- Sitio 1: `main--abc--adobe.aem.live`
>- Sitio 2: `main--abc1--adobe.aem.live`
>
>Ambos dominios necesitan entradas de lista de permitidos independientes para que el envío de formularios funcione desde ambos sitios.

## Causas y soluciones comunes

Un error 403 prohibido en el envío de formularios de Edge Delivery Services puede tener varias causas. Siga estos pasos para solucionar problemas en orden:

### &#x200B;1. Problemas del CORS (Intercambio de Recursos de Origen Cruzado)

**Síntomas:**

- La consola del explorador muestra mensajes de error relacionados con CORS
- La pestaña Red muestra la solicitud bloqueada antes de llegar al servidor
- Mensajes de error que mencionan &quot;Solicitud de origen cruzado bloqueada&quot;

**Diagnóstico:**

1. Abrir herramientas para desarrolladores del explorador (F12)
2. Compruebe la pestaña Consola para ver mensajes de error CORS
3. Buscar mensajes como: `Access to fetch at 'https://publish-xxx.adobeaemcloud.com' from origin 'https://main--repo--owner.aem.live' has been blocked by CORS policy`

**Solución:**
Configure las opciones de CORS en AEM para permitir solicitudes de los dominios de sitio específicos de Edge Delivery:

```apache
# Developer Localhost
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Sites - Add each site domain individually
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc--adobe\.aem\.live$)#" CORSTrusted=true
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://main--abc1--adobe\.aem\.live$)#" CORSTrusted=true

# Legacy Franklin domains (if still in use)
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

>[!NOTE]
>
>Reemplace `main--abc--adobe.aem.live` y `main--abc1--adobe.aem.live` por sus dominios de sitio reales. Cada sitio alojado desde el mismo repositorio requiere una entrada de configuración CORS independiente.

Para obtener información detallada sobre la configuración de CORS, consulte la [Guía de configuración de CORS](https://experienceleague.adobe.com/es/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors).

### &#x200B;2. Reglas de Dispatcher

**Síntomas:**

- El error 403 se produce sin mensajes CORS en la consola del explorador
- La solicitud llega al servidor, pero Dispatcher la ha bloqueado
- Se produce un error antes de alcanzar la capa de aplicación de AEM

**Diagnóstico:**

1. Compruebe si la dirección URL de la solicitud coincide con alguna regla de filtro de Dispatcher
2. Revise la configuración de Dispatcher para `/filter` reglas que podrían bloquear solicitudes POST
3. Compruebe que el punto final de envío del formulario esté permitido en la configuración de Dispatcher

**Solución:**
Actualice la configuración de Dispatcher para permitir las solicitudes de envío de formularios:

1. Asegúrese de que se permiten las solicitudes POST a los extremos de envío de formularios
2. Agregar las reglas de filtro adecuadas para los dominios de Edge Delivery
3. Compruebe que la ruta del servlet de envío no esté bloqueada

Ejemplo de configuración del filtro Dispatcher:

```apache
/filter {
  # Allow POST requests to form submission servlet
  /0100 { /type "allow" /method "POST" /url "/content/forms/af/*" }
  /0101 { /type "allow" /method "POST" /url "/adobe/forms/af/submit/*" }
  /0102 { /type "allow" /method "POST" /url "/content/forms/portal/submit/adaptiveform" }
}
```

### &#x200B;3. Problemas del filtro de referente

**Síntomas:**

- Error 403 sin problemas CORS en la consola del explorador
- La solicitud llega a AEM, pero el filtro de referente de Sling la rechaza
- El error se produce en la capa de aplicación de AEM

**Diagnóstico:**
Compruebe los registros de errores de AEM para ver los mensajes de rechazo del filtro de referente:

1. [Acceder a los registros de AEM Cloud Service a través de Cloud Manager](/help/implementing/cloud-manager/manage-logs.md)
2. Busque entradas en `aemerror.log` que contengan:
   - &quot;Filtro de referente rechazado&quot;
   - &quot;org.apache.sling.security.impl.ReferrerFilter&quot;
   - Mensajes que indican errores de validación del referente

**Ejemplo de entrada de registro:**

```
[ERROR] org.apache.sling.security.impl.ReferrerFilter Referrer filter rejected request with referrer 'https://main--abc--adobe.aem.live' for POST /content/forms/af/submit
```

**Solución:**
Configure el Filtro de referente para permitir los dominios de sitio específicos de Edge Delivery:

1. Crear o actualizar el archivo de configuración de OSGi: `org.apache.sling.security.impl.ReferrerFilter.cfg.json`

2. Agregue la siguiente configuración con los dominios de sitio específicos:

   ```json
   {
     "allow.empty": false,
     "allow.hosts": [
       "main--abc--adobe.aem.live",
       "main--abc1--adobe.aem.live"
     ],
     "allow.hosts.regexp": [
       "https://.*\\.aem\\.live:443",
       "https://.*\\.aem\\.page:443",
       "https://.*\\.hlx\\.page:443",
       "https://.*\\.hlx\\.live:443"
     ],
     "filter.methods": [
       "POST",
       "PUT",
       "DELETE",
       "COPY",
       "MOVE"
     ],
     "exclude.agents.regexp": [
       ""
     ]
   }
   ```

3. Implementar la configuración mediante Cloud Manager

>[!IMPORTANT]
>
>**Configuraciones sin fin:** Debe agregar cada dominio de sitio individualmente a la matriz `allow.hosts`. El uso de solo patrones de regex puede no ser suficiente para todos los escenarios. Incluya dominios específicos y patrones de regex para una cobertura completa.

>[!WARNING]
>
>El filtro de referente de AEM no es una fábrica de configuración OSGi, lo que significa que solo una configuración está activa en un servicio de AEM a la vez. Cuando sea posible, evite añadir configuraciones personalizadas del filtro de referente, ya que esto sobrescribirá las configuraciones nativas de AEM y podría romper la funcionalidad del producto.

## Pasos de diagnóstico

Siga estos pasos para identificar la causa específica del error 403:

### Paso 1: Comprobar la consola del explorador

1. Abrir herramientas para desarrolladores del explorador (F12)
2. Vaya a la pestaña Consola
3. Intentar envío de formulario
4. Buscar mensajes de error relacionados con CORS

**Si hay errores CORS:** Siga la solución CORS indicada arriba.
**Si no hay errores CORS:** Continúe con el paso 2.

### Paso 2: Marque la pestaña Red

1. Abrir herramientas para desarrolladores del explorador (F12)
2. Vaya a la pestaña Red
3. Intentar envío de formulario
4. Comprobación de los detalles de la solicitud fallida
5. Consultar los encabezados de respuesta y el estado

**Si la solicitud no llega al servidor:** Probablemente sea un problema de Dispatcher.
**Si la solicitud llega al servidor pero falla:** Probablemente sea un problema de filtro de referente.

### Paso 3: Comprobación de los registros de AEM

1. Acceder a Cloud Manager
2. Navegar a entornos → su entorno → registros
3. Descargar o ver `aemerror.log`
4. Buscar entradas en el momento del envío del formulario
5. Busque el Filtro de referente o mensajes relacionados con la seguridad

## Prevención y prácticas recomendadas

### &#x200B;1. Configuración correcta durante la instalación

- Configuración de CORS, Dispatcher y Filtro de referente durante la configuración inicial de Edge Delivery Services
- **Para cada nuevo sitio:** Agregue el dominio específico a todas las listas de permitidos (CORS, Filtro de referente)
- Probar los envíos de formularios en el entorno de desarrollo antes de activarse

### &#x200B;2. Configuraciones específicas del entorno

- Utilizar diferentes configuraciones para entornos de desarrollo, ensayo y producción
- Incluir dominios de host local para pruebas de desarrollo local
- **Documentar todos los dominios de sitio** que necesitan acceso de lista de permitidos para su repositorio

### &#x200B;3. Monitoreo y registro

- Configurar la monitorización de registros para los rechazos del filtro de referente
- Implementar el control de errores adecuado en el código de envío del formulario
- Uso de las herramientas para desarrolladores de navegadores durante la prueba

### &#x200B;4. Documentación y conocimiento del equipo

- **Mantener un registro** de todos los dominios de sitio que usan el mismo repositorio
- Formación del equipo de desarrollo en pasos de solución de problemas
- Mantener una lista de comprobación para la configuración de formularios de Edge Delivery Services
- **Actualizar listas de permitidos** cada vez que se creen nuevos sitios a partir de repositorios existentes

## Administración de dominios de sitio para configuraciones de reprocesamiento

Con las arquitecturas Helix-5 y repoless, siga estas directrices:

### Al crear sitios nuevos

1. **Identificar el dominio del sitio** (por ejemplo, `main--newsite--adobe.aem.live`)
2. **Actualice la configuración de CORS** para incluir el nuevo dominio
3. **Actualizar filtro de referente** para incluir el nuevo dominio en `allow.hosts`
4. **Probar envío de formulario** desde el nuevo sitio
5. **Documentar el nuevo dominio** en el registro del sitio

### Patrones de nombres de dominio

- Patrón estándar: `{branch}--{site}--{owner}.aem.live`
- Cada sitio obtiene un dominio único incluso cuando comparte el mismo repositorio
- Se pueden usar los dominios `.aem.live` y `.aem.page`

### Administración de configuración

- Usar entradas de dominio específicas en `allow.hosts` para mejorar la seguridad
- Suplemento con patrones regex para una cobertura más amplia
- Auditar y actualizar regularmente las listas de permitidos a medida que se añaden o eliminan sitios

## Recursos adicionales

- [Configuración del filtro de referente con AEM Headless](/help/headless/deployment/referrer-filter.md)
- [Guía de configuración de CORS](https://experienceleague.adobe.com/es/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Explicación del uso compartido de recursos de origen cruzado](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)
- [Documentación de Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/publish-forms.md)

## Temas relacionados

- [Configuración de acciones de envío](/help/forms/configuring-submit-actions.md)
- [Servicio de envío de Forms](/help/forms/forms-submission-service.md)
- [Información general de Edge Delivery Services](/help/edge/overview.md)


**¿Necesita ayuda adicional?** Si sigue teniendo problemas después de seguir estos pasos, póngase en contacto con el servicio de atención al cliente de Adobe con:

- Sus mensajes de error específicos
- Detalles del entorno de AEM Cloud Service
- **Todos los dominios de sitio de Edge Delivery Services** que necesitan acceso para enviar formularios
- Entradas de registro relevantes desde el momento del error

**¿Necesita ayuda adicional?** Si sigue teniendo problemas después de seguir estos pasos, póngase en contacto con el servicio de atención al cliente de Adobe con:

- Sus mensajes de error específicos
- Detalles del entorno de AEM Cloud Service
- Información del dominio de Edge Delivery Services
- Entradas de registro relevantes desde el momento del error
