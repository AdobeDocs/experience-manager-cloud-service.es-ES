---
title: Publicar Forms adaptable con Edge Delivery Services
description: Obtenga información sobre cómo publicar, configurar y acceder a Forms adaptable mediante Edge Delivery Services para uso en producción.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [Publicación de formularios, Edge Delivery Services, configuración de formularios, CORS, filtro de referente]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 2%

---

# Publicar Forms adaptable con Edge Delivery Services

La publicación de un formulario adaptable hace que esté disponible en Edge Delivery Services para que los usuarios finales accedan y lo envíen. Este proceso implica tres fases principales: publicar el formulario, configurar la seguridad y acceder al formulario activo.

**Lo que va a lograr:**

- Publicación del formulario en Edge Delivery Services
- Configure las opciones de seguridad para enviar formularios
- Acceso y verificación del formulario publicado
- Configurar el enrutamiento de URL y las políticas CORS adecuados

## Requisitos previos

- Formulario adaptable creado con una plantilla de Edge Delivery Services
- Formulario probado y listo para el uso en producción
- Permisos de autor de AEM Forms
- Acceso a Cloud Manager (para la configuración de producción)
- Acceso de desarrollador al código de bloque de formulario (para la configuración del envío)

## Resumen del proceso de publicación

La publicación de formularios en Edge Delivery Services sigue un enfoque de tres fases:

- **Fase 1: publicación de formulario** - Publique el formulario en la red de distribución de contenido (CDN) y compruebe el estado de publicación
- **Fase 2: Configuración de seguridad**: configure directivas CORS y filtros de referente para envíos seguros
- **Fase 3: acceso y validación**: pruebe la funcionalidad del formulario y valide el flujo de trabajo completo

Cada fase se basa en la anterior para garantizar una implementación segura y funcional.

### Fase 1: Publicar el formulario

+++ Paso 1: Inicio de la publicación

1. **Acceda a su formulario**: abra su formulario adaptable en el editor universal
2. **Comenzar a publicar**: Haga clic en el icono **Publicar** de la barra de herramientas

   ![Haga clic en Publicar](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ Paso 2: Revisar y confirmar

1. **Revisar recursos de publicación**: el sistema muestra todos los recursos que se están publicando, incluido el formulario

   ![Publicación al hacer clic](/help/forms/assets/on-click-publish.png)

2. **Confirmar publicación**: Haga clic en **Publicar** para continuar
3. **Verificar éxito**: busque el mensaje de confirmación

   ![Éxito de publicación](/help/forms/assets/publish-success.png)

+++


+++ Paso 3: Verificar el estado de publicación

**Comprobar estado**: vuelve a hacer clic en el icono **Publicar** para ver el estado actual.

![Estado de publicación](/help/forms/assets/publish-status.png)

**Punto de comprobación de validación:**

- El formulario muestra el estado &quot;Publicado&quot; en el editor
- No hay mensajes de error durante el proceso de publicación
- El formulario aparece en la lista de recursos publicados

+++


+++ Administración de Forms publicado

**Para cancelar la publicación de un formulario:**

1. Abra el formulario en el editor
2. Haga clic en el menú de tres puntos (⋯) en la esquina superior derecha
3. Seleccionar **Cancelar publicación**

![Cancelar publicación de formulario](/help/forms/assets/unpublish--form.png)

+++


### Fase 2: Configurar opciones de seguridad

+++ Por qué se requiere la configuración de seguridad

Para habilitar los envíos de formularios seguros, debe configurar opciones de seguridad que:

- Permitir que Edge Delivery Services envíe datos a AEM
- Impedir el acceso no autorizado a la instancia de AEM
- Habilitar CORS (Intercambio de recursos de origen cruzado) para envíos de formularios
- Filtrar solicitudes para permitir solo dominios de Edge Delivery legítimos

>[!IMPORTANT]
>
>**Necesario para producción**: estas configuraciones son obligatorias para que los envíos de formularios funcionen en entornos de producción.

+++



+++ Paso 1: Configurar la URL de envío del formulario

**Propósito**: enviar formularios directamente a su instancia de AEM

**Ubicación de archivo**: `blocks/form/constant.js` en su proyecto de Edge Delivery Services

**Ejemplos de configuración:**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**Punto de comprobación de validación:**

- `constant.js` archivo actualizado con la URL de publicación de AEM correcta
- La dirección URL coincide con su entorno (producción, ensayo o local)
- No hay barra diagonal en la dirección URL

+++



+++ Paso 2: Configuración de CORS

**Propósito**: permitir solicitudes de envío de formularios de dominios de Edge Delivery Services

**Implementación**: agregue la configuración CORS a su configuración de AEM Dispatcher o Apache

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**Punto de comprobación de validación:**

- Reglas CORS aplicadas a la configuración de Dispatcher
- Se incluyen todos los dominios necesarios (localhost, hlx.page, hlx.live)
- Configuración implementada en el entorno de destino

**Documentación de referencia:**

- [Guía de configuración de CORS](https://experienceleague.adobe.com/es/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Documentación del filtro de referente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ Paso 3: Configurar el filtro de referente

**Propósito**: Restringir las operaciones de escritura a dominios de Edge Delivery Services autorizados

**Método de implementación**: configure mediante Cloud Manager en AEM as a Cloud Service

**Archivo de configuración**: Agregue a la configuración OSGi de su proyecto

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
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

**Desglose de configuración:**

- **`allow.empty`**: rechaza solicitudes sin encabezados de referente
- **`allow.hosts.regexp`**: permite solicitudes de dominios de Edge Delivery Services
- **`filter.methods`**: aplica el filtrado a estos métodos HTTP
- **`exclude.agents.regexp`**: agentes de usuario excluidos del filtrado

**Punto de comprobación de validación:**

- Configuración del filtro de referente implementada mediante Cloud Manager
- Configuración activa en la instancia de publicación de AEM
- El envío de formularios de prueba funciona desde el dominio de Edge Delivery Services
- Los dominios no autorizados no pueden enviar formularios

**Documentación de referencia:**

- [Configurar el filtro de referente a través de Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### Fase 3: Acceso Al Formulario Publicado



+++ Estructura URL de Edge Delivery Services

**Formato de dirección URL estándar:**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**Componentes de URL:**

- **`<branch>`**: nombre de rama Git (normalmente `main`)
- **`<repo>`**: nombre del repositorio
- **`<owner>`**: organización de GitHub o nombre de usuario
- **`<form_name>`**: nombre del formulario (en minúsculas, con guiones)

**URL específicas del entorno:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ Pasos finales de validación

**Verificar accesibilidad del formulario:**

1. **Probar la carga del formulario**: Visite la dirección URL del formulario y confirme que se carga correctamente
2. **Probar el envío de formularios**: complete y envíe el formulario para verificar el procesamiento de datos
3. **Comprobar diseño interactivo**: probar el formulario en diferentes dispositivos y tamaños de pantalla
4. **Validar seguridad**: Asegúrese de que CORS y el filtro de referente funcionan correctamente

**Resultados esperados:**

- El formulario se carga sin errores
- Todos los campos de formulario se representan correctamente
- Procesos de envío de formularios correctamente
- Los datos aparecen en el destino configurado (hoja de cálculo, correo electrónico, etc.)
- No hay errores de consola relacionados con CORS o políticas de seguridad

+++


## Próximos pasos


- [Configurar acciones de envío de formularios](/help/edge/docs/forms/universal-editor/submit-action.md)
- [Aplicar estilo y temática a los formularios](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [Crear diseños de formulario adaptables](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [Añadir protección reCAPTCHA](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



