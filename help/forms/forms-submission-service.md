---
title: Servicio de envío de Forms para Edge Delivery Services
description: Almacene los envíos de formularios directamente en hojas de cálculo utilizando el servicio de envío de Forms alojado en Adobe. Obtenga información sobre la configuración, el uso de API y la configuración para la integración de Google Sheets, OneDrive y SharePoint.
keywords: Servicio de envío de Forms, formularios Edge Delivery Services, integración de hojas de cálculo, formularios Google Sheets, formularios OneDrive, formularios SharePoint, recopilación de datos de formulario
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: ae423010910f66cd5e35ad8bd6b0c077d5bbda97
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 1%

---

# Servicio de envío de Forms para Edge Delivery Services

El servicio de envío de Forms es la solución alojada de Adobe que almacena automáticamente los datos de envío de formularios directamente en sus hojas de cálculo preferidas: Google Sheets, Microsoft OneDrive o SharePoint. Esto elimina la necesidad de una infraestructura backend compleja, a la vez que proporciona recopilación y administración de datos en tiempo real.

## Información general

![servicio de envío de Forms](/help/forms/assets/form-submission-service.png)
*Imagen: flujo de trabajo del servicio de envío de Forms: desde el envío del formulario al almacenamiento de la hoja de cálculo*

+++ ¿Quién Debe Utilizar Este Servicio?

**Perfecto para:**

- **Creadores de contenido** que crean formularios de recopilación de datos simples
- **Pequeñas empresas** que necesitan flujos de trabajo rápidos de formulario a hoja de cálculo
- **Equipos de mercadotecnia** que recopilan información de posibles clientes
- **Organizadores de eventos** administrando registros

**Considerar alternativas para:**

- Flujos de trabajo complejos que requieren lógica personalizada
- Integraciones empresariales con bases de datos
- Forms que necesita validación o procesamiento avanzados

+++

+++ Casos de uso comunes

| Caso práctico | Ejemplos | Beneficio de hoja de cálculo |
|----------|---------|-------------------|
| **Contactar con Forms** | Consultas del sitio web → Hojas de cálculo de Google | Fácil seguimiento e importación de CRM |
| **Registro de eventos** | Suscripciones a la conferencia → Excel Online | Seguimiento de asistentes en tiempo real |
| **Generación de clientes potenciales** | Suscripciones a la newsletter → SharePoint | Análisis de campañas de marketing |
| **Colección de comentarios** | Respuestas de encuesta → hojas de Google | Visualización rápida de datos |

+++

## Principales ventajas

El servicio de envío de Forms ofrece varias ventajas para una recopilación de datos optimizada:

+++ Configuración simplificada

- **No se requiere infraestructura back-end** - Adobe aloja el punto final de envío
- **Integración directa** con plataformas de hoja de cálculo populares
- **Asignación automática de datos** de campos de formulario a columnas de hoja de cálculo

+++


+++ Real-Time Data Management

- **Captura instantánea de datos**: los envíos aparecen inmediatamente en la hoja de cálculo
- **Almacenamiento estructurado**: columnas organizadas para facilitar el análisis
- **Colaboración en vivo**: varios integrantes del equipo pueden acceder a datos y analizarlos

+++

+++ Seguridad y control de acceso integrados

- **Aprovecha los permisos existentes**: usa los controles para compartir de la plataforma de hojas de cálculo
- **Seguridad administrada por Adobe**: extremo de envío seguro con protección de nivel empresarial
- **Propiedad de los datos**: los datos permanecen en la plataforma de hoja de cálculo elegida

+++

## Requisitos previos

Antes de configurar el servicio de envío de Forms, asegúrese de lo siguiente:



+++ Requisitos técnicos

- **Repositorio de GitHub** configurado para su proyecto de Edge Delivery Services con el último bloque de Forms adaptable instalado
- **Aprobación de acceso** - Repositorio agregado a la lista de permitidos

+++

+++ Configuración de plataforma de hoja de cálculo


Elija una de las plataformas compatibles:

- **Hojas de cálculo de Google** - Cuenta de Google con permisos de creación de hojas
- **Microsoft OneDrive** - Cuenta de Microsoft 365 con acceso a Excel Online
- **SharePoint**: acceso a SharePoint con permisos de lista/biblioteca

+++

+++ Permisos y acceso

- **Editar permisos** para la hoja de cálculo de destino
- **Compartir capacidades** para conceder acceso a `forms@adobe.com`
- Permisos de **generación de vínculos** para la plataforma elegida

+++

>[!TIP]
>
>**¿Es nuevo en Edge Delivery Services?** Comience con el [Tutorial de introducción](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) para configurar la base de su proyecto.

## Métodos de configuración

El servicio de envío de Forms ofrece dos métodos de configuración. Elija el método que mejor se adapte a su flujo de trabajo:


+++ Elija el método de configuración

| Método | Ideal para | Tiempo necesario | Nivel técnico |
|--------|----------|---------------|-----------------|
| **[Configuración manual](#manual-configuration)** | Creadores de contenido, configuración única | 10-15 minutos | Principiante |
| **[Configuración de API](#api-configuration)** | Desarrolladores, flujos de trabajo automatizados | 5-10 minutos | Intermedio |

+++

+++ Configuración del proyecto

Antes de configurar cualquiera de los métodos, asegúrese de que la base del proyecto de AEM está lista:

1. **Cree o actualice su proyecto de AEM** con el último bloque de Forms adaptable ([Tutorial de introducción](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial))

2. **Actualización`fstab.yaml`** en la raíz del proyecto:

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **Compartir la carpeta del proyecto** con `forms@adobe.com` (se requieren permisos de edición)

+++

+++

## Configuración manual

![Flujo de trabajo para el servicio de envío de formularios](/help/forms/assets/forms-submission-service-workflow.png)
*Imagen: flujo de trabajo completo para la configuración manual del servicio de envío de Forms*

Siga estas instrucciones paso a paso para configurar el formulario con envío de hoja de cálculo:



+++ Paso 1: Crear la definición del formulario

Cree la estructura del formulario con Hojas de cálculo de Google o Microsoft Excel.

**Pasos de creación de formularios:**

1. **Abra la plataforma de hoja de cálculo** (Hojas de cálculo de Google o Excel de Microsoft)
2. **Cree una nueva hoja de cálculo** para su proyecto de formulario
3. **Asigne un nombre a la hoja** (debe ser `helix-default` o `shared-aem`)
4. **Defina la estructura del formulario** mediante la [guía de creación de formularios](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![Definición de formulario](/help/forms/assets/form-submission-definition.png)
*Ejemplo: definición de formulario con tipos de campo, etiquetas y reglas de validación*

>[!IMPORTANT]
>
>**Requisitos de nomenclatura de hojas**
>
>La hoja de definición del formulario debe tener uno de los siguientes nombres:
>
>- `helix-default` (recomendado para formularios únicos)
>- `shared-aem` (para proyectos de varios formularios)
>
>El sistema no reconocerá otros nombres de hoja.

**Punto de comprobación de validación:**

- La estructura del formulario se completa con todos los campos obligatorios
- La hoja tiene el nombre correcto (`helix-default` o `shared-aem`)
- Los tipos de campo y las reglas de validación están correctamente configurados

+++

+++ Paso 2: Crear la hoja de recopilación de datos

Configure una hoja dedicada para recibir los datos de envío de formularios.

**Configuración de hoja de datos:**

1. **Agregar una hoja nueva** a la hoja de cálculo existente
2. **Asigne un nombre a la hoja exactamente`incoming`** (distingue mayúsculas de minúsculas)
3. **Configurar encabezados de columna** que coincidan con los campos de formulario
4. **Guarde la hoja de cálculo** para asegurarse de que se conservan los cambios

![Hoja entrante](/help/forms/assets/form-submission-incoming-sheet.png)
*Ejemplo: hoja entrante con encabezados de columna que coinciden con campos de formulario*

>[!WARNING]
>
>**Requisito crítico**
>
>La hoja debe tener exactamente el nombre `incoming` (en minúsculas). Sin esta hoja:
>
>- Los envíos de formularios se rechazarán
>- No se almacenarán datos
>- Los usuarios verán los errores de envío

**Punto de comprobación de validación:**

- La hoja `incoming` existe en su hoja de cálculo
- Los encabezados de columna coinciden con los nombres de los campos de formulario
- La hoja se ha guardado correctamente y es accesible

>[!TIP]
>
>**Sugerencia profesional:** copie los nombres de campo exactos de su definición de formulario para garantizar la perfecta coincidencia entre los campos de formulario y las columnas de la hoja de cálculo.

+++

+++ Paso 3: Compartir una hoja de cálculo con el servicio de Adobe

Conceda acceso al servicio de envío de Adobe Forms a su hoja de cálculo.

**Proceso de uso compartido:**

1. **Haga clic en el botón Compartir** en la esquina superior derecha de la hoja de cálculo
2. **Agregar la cuenta de servicio de Adobe:**
   - Correo electrónico: `forms@adobe.com`
   - Nivel de permiso: **Editor** (requerido para la escritura de datos)
3. **Enviar la invitación para compartir**
4. **Copie el vínculo de la hoja de cálculo** para el paso siguiente

   ![Compartir hoja entrante](/help/forms/assets/form-submission-share-incoming.png)
   *Proceso de uso compartido paso a paso para conceder acceso al servicio de Adobe*

**Instrucciones específicas de la plataforma:**

**Hojas de cálculo Google:**

- Agregar `forms@adobe.com` como editor
- Asegúrese de que &quot;Cualquier persona que tenga el vínculo que puede ver&quot; esté habilitado
- Copiar el vínculo que se puede compartir

**Microsoft Excel (OneDrive/SharePoint):**

- Agregar `forms@adobe.com` con permisos de edición
- Configure el uso compartido de vínculos como &quot;Cualquier persona que tenga el vínculo puede editarlo&quot;
- Copiar la URL para compartir

  ![Copiar vínculo de la hoja entrante](/help/forms/assets/form-submission-copy-link.png)
  *Ejemplo: copiando el vínculo que se puede compartir para la configuración del formulario*

**Punto de comprobación de validación:**

- `forms@adobe.com` tiene acceso de editor a su hoja de cálculo
- El vínculo de hoja de cálculo se ha copiado y está listo para usarse
- Los permisos de uso compartido permiten acceso externo

+++

+++ Paso 4: Conectar el formulario a la hoja de cálculo

Vincule la definición del formulario a la hoja de cálculo de envío.

**Conexión de hoja de cálculo de formulario:**

1. **Abra la hoja de cálculo de definición de formulario** (la que tiene `helix-default` o `shared-aem` hoja)
2. **Busque la fila del campo de envío** en su definición de formulario
3. **Pegue el vínculo de hoja de cálculo copiado** en la columna **Acción** para el campo Enviar
4. **Guardar los cambios** en su definición de formulario

   ![Vincular una hoja de cálculo](/help/forms/assets/form-submission-sheet-linking.png)

*Ejemplo: conectar la acción de envío a la hoja de cálculo de recopilación de datos*

**Publicando Su Formulario:**

1. **Abrir AEM Sidekick** en el explorador
2. **Previsualice el formulario** para probar la configuración
3. **Publicar el formulario** para activarlo

**Validación final:**

- El vínculo de hoja de cálculo se agrega correctamente a la acción Enviar campo
- La definición del formulario se guarda y publica
- La vista previa del formulario muestra todos los campos correctamente
- El botón Enviar está configurado correctamente

>[!SUCCESS]
>
>**Configuración completada.** El formulario ahora está conectado al servicio de envío de Forms. Pruébelo enviando datos de ejemplo y comprobando su hoja `incoming`.

**Materiales de referencia:**

- [Hoja de cálculo de ejemplo completa](/help/forms/assets/spreadsheet.xlsx) con la configuración adecuada
- [Documentación de AEM Sidekick](https://www.aem.live/docs/sidekick) para instrucciones de publicación

+++

## Configuración de la API

El método API permite a los desarrolladores enviar datos mediante programación al servicio de envío de Forms, lo que resulta ideal para flujos de trabajo automatizados e integraciones personalizadas.


+++ Cuándo usar la API

**Perfecto para:**

- Sistemas automatizados de recopilación de datos
- Implementaciones de formularios personalizados
- Integración con aplicaciones existentes
- Flujos de trabajo de envío masivo de datos

+++

+++ Requisitos previos de API

Antes de usar la API, asegúrese de lo siguiente:

- **Configuración de hoja de cálculo** completada (incluida `incoming` hoja)
- Se concedió acceso al servicio **Adobe** a `forms@adobe.com`
- **ID de formulario** de su formulario publicado
- **Información del repositorio** (organización y nombre del sitio)

>[!IMPORTANT]
>
>**Pasos de configuración necesarios**
>
>La API requiere la misma configuración de hoja de cálculo que la configuración manual:
>
>- La hoja `incoming` debe existir
>- `forms@adobe.com` debe tener acceso de editor
>- La hoja debe publicarse mediante AEM Sidekick

+++

+++ Extremo y autenticación de API

**URL básica:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**Encabezados requeridos:**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**Documentación de API:** [Referencia de API completa](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ Uso de Postman

Postman proporciona una interfaz fácil de usar para probar los envíos de API.

**Instrucciones de instalación:**

1. **Crear una nueva solicitud POST** en Postman
2. **Configurar el extremo:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **Reemplazar marcadores de posición:**
   - `{id}` → su ID de formulario real
   - `[repository]` → el nombre de su repositorio de GitHub
   - `[organization]` → su organización/nombre de usuario de GitHub

**Configuración de solicitud:**

```json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Headers:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main--your-repo--your-org

Body (JSON):
{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Mary",
            "age": "35",
            "subscribe": null,
            "email": "mary@gmail.com"
                }
}
```

**Respuesta esperada:**

- **Código de estado:** `201 Created`
- **Los datos aparecen** inmediatamente en su hoja de cálculo de `incoming`

![pantalla de postman](/help/forms/assets/postman-api.png)
*Ejemplo: envío correcto de la API mediante la interfaz de Postman*

+++

+++ Uso de la línea de comandos (curl)

Para los desarrolladores que prefieren terminal/símbolo del sistema, utilice curl para enviar datos mediante programación.

**Configuración de línea de comandos:**

Reemplace los siguientes marcadores de posición en los comandos siguientes:

- `{id}` → su ID de formulario real
- `[repository]` → el nombre de su repositorio de GitHub
- `[organization]` → su organización/nombre de usuario de GitHub

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
```

>[!TAB Símbolo del sistema de Windows]

```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
```

>[!ENDTABS]

+++

+++ Respuesta y verificación de API

**Respuesta correcta:**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**Verificación de datos:**

Después de un envío correcto, compruebe que los datos aparecen en la hoja de cálculo:

![hoja actualizada](/help/forms/assets/updated-sheet.png)
*Ejemplo: datos escritos correctamente en la hoja entrante a través de la API*

**Validación de respuesta:**

- **Estado HTTP:** `201 Created` indica envío correcto
- **X-Request-Id:** Identificador único para rastrear el envío
- **Los datos aparecen** en su hoja de `incoming` en cuestión de segundos
- **Todos los campos de formulario** están asignados correctamente a las columnas de la hoja de cálculo

+++

## Resolución de problemas



+++ Problemas y soluciones comunes

**Problema: Error 403 prohibido**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**Problema: Error 404 No Encontrado**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**Problema: Los datos no aparecen en la hoja de cálculo**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**Problema: Error de formato JSON no válido**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


+++

+++ Obtención de ayuda

**Canales de soporte:**

- **Problemas de acceso anticipado:** Correo electrónico [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **Documentación de la API:** [Referencia del desarrollador](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **Soporte de la comunidad:** [Comunidad de Adobe Experience League](https://experienceleaguecommunities.adobe.com/?profile.language=es)

+++

## Próximos pasos

Ahora que tiene configurado el servicio de envío de Forms, explore estos temas relacionados:


+++ Mejore su Forms

- **[Crear Forms avanzado](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)**: agregue validación, lógica condicional y estilo personalizado
- **[Guía de componentes de formulario](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)**: explore los tipos de campos de formulario disponibles

+++

+++ Métodos de envío alternativos

- **[Envíos de publicación de AEM](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)**: para flujos de trabajo complejos e integraciones empresariales
- **[Acciones de envío personalizadas](/help/forms/configure-submit-actions-core-components.md)** - Administración avanzada del envío

+++

+++ Administración de datos

- **[Form Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)**: haga un seguimiento del rendimiento y el uso del formulario
- **[Integración de datos](/help/forms/configure-data-sources.md)** - Conectar formularios a bases de datos y sistemas CRM

+++

## Resumen

El servicio de envío de Forms proporciona una solución potente y sin código para recopilar datos de formulario directamente en hojas de cálculo. Las ventajas principales incluyen:

- **Configuración rápida**: no se requiere infraestructura back-end
- **Datos en tiempo real**: captura de envío inmediata
- **Plataformas flexibles**: Hojas de cálculo de Google, OneDrive o SharePoint
- **Acceso a la API** - Funciones de envío mediante programación
- **Seguridad empresarial**: extremos administrados por Adobe con controles de acceso

**¿Listo para comenzar?** Siga la guía de [configuración manual](#manual-configuration) para obtener una configuración visual o vaya a [configuración de API](#api-configuration) para la integración mediante programación.
