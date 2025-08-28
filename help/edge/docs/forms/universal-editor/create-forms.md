---
title: Crear y publicar formularios adaptables con Edge Delivery Services
description: Instrucciones paso a paso para crear, crear y publicar Forms adaptable con plantillas de Edge Delivery Services en AEM, con un enfoque en la precisión y la claridad técnicas.
keywords: formularios adaptables, servicios de envío Edge, editor universal, creación de formularios, formularios AEM, publicación de formularios
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 87%

---


# Crear y publicar formularios adaptables con Edge Delivery Services

Este documento proporciona instrucciones paso a paso para crear, configurar y publicar Forms adaptable con plantillas de Edge Delivery Services en AEM. Abarca todo el flujo de trabajo, desde la creación del formulario a la implementación de producción.

Al final de la guía, aprenderá a hacer lo siguiente:

- Creación de formularios con plantillas de Edge Delivery Services
- Crear formularios con el Editor universal
- Configurar y publicar de formularios en Edge Delivery Services
- Acceder a los formularios publicados y verificar la implementación



## Requisitos previos

Asegúrese de que se cumplen los siguientes requisitos previos para continuar:


- **Formularios de AEM as a Cloud Service**: instancia de autor activa con licencia de Forms.
- **Cuenta de GitHub**: cuenta personal u organizativa para la administración de repositorios.
- **Configuración del repositorio**: elija una de las siguientes opciones:
   - **Nuevo proyecto**: [cree un nuevo proyecto de AEM con el bloque de formularios adaptable](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block). El repositorio está preconfigurado para Edge Delivery Services.
   - **Proyecto existente**: [añada un bloque de formularios adaptables a un repositorio existente](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) y actualice la configuración.

- **Conexión entre AEM y GitHub**: [establezca una conexión](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) entre su instancia de AEM y el repositorio de GitHub.
- **Edge Delivery Services**: asegúrese de que el repositorio esté configurado para la implementación automática.
- **Permisos**: compruebe que dispone de los derechos de acceso necesarios para la creación y publicación de formularios.

- Confirme que el repositorio de GitHub contiene el bloque de formularios adaptables.



## Flujo de trabajo de la creación y publicación de formularios

El proceso consta de tres fases principales:

- **Fase 1:** [Creación de formularios](#step-1-form-creation)
- **Fase 2:** [Creación y diseño de formularios](#step-2-form-authoring-and-design)
- **Fase 3:** [Configuración y publicación](#step-3-configuration-and-publishing)

Cada fase incluye pasos de validación para confirmar la configuración correcta.


### Paso 1: Creación de formularios

1. **Acceder a la creación de formularios**
   - Inicie sesión en su instancia de autor de AEM Forms as a Cloud Service.
   - Vaya a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**.
   - Haga clic en **Crear** > **Formularios adaptables**. 

1. **Seleccionar plantilla**
   - En la pestaña **Fuente**, seleccione una **plantilla basada en Edge Delivery Services**.
   - El botón **Crear** se habilita.

     ![Creación de formularios EDS](/help/edge/assets/create-eds-forms.png)

1. **Configurar opciones (opcional)**
   - **Pestaña Fuente de datos**: seleccione la integración de datos si es necesario.
   - **Pestaña Envío**: elija una acción de envío (se puede configurar más adelante).
   - **Pestaña Entrega**: establezca la programación de publicación/cancelación de publicación.

1. **Completar la configuración del formulario**
   - Haga clic en **Crear** para abrir el Asistente para crear formulario.
   - Escriba lo siguiente:
      - **Nombre**: identificador interno (sin espacios, use guiones).
      - **Título**: nombre para mostrar del formulario.
      - **URL de GitHub**: URL del repositorio (por ejemplo, `https://github.com/your-org/your-repo`).

   ![Asistente para crear formulario](/help/edge/assets/create-form-wizard.png)

1. **Validación**
   - Después de hacer clic en **Crear**, verifique lo siguiente:
      - El formulario se abre en el editor universal. 
      - La URL de GitHub está vinculada correctamente.
      - La paleta de componentes está disponible.
      - El lienzo del formulario es visible.

   ![Interfaz del editor universal](/help/edge/assets/author-form.png)

**Resultado:** el formulario está listo para la creación en el editor universal.

### Paso 2: Creación y diseño de formularios


1. **Acceder a la biblioteca de componentes**
   - Abra el explorador de contenido en el editor universal.
   - Vaya al componente **Formulario adaptable** en el árbol de contenido.

   ![Navegación del árbol de contenido](/help/edge/assets/content-tree.png)

1. **Añadir campos de formulario**
   - Haga clic en el icono **Añadir** para abrir la biblioteca de componentes.
   - Seleccione los componentes en la lista **Componentes de formularios adaptables**.
   - Arrastre y suelte los componentes en el lienzo del formulario.

   ![Añadir componentes](/help/edge/assets/add-component.png)

1. **Diseñar el formulario**
   - Configure las propiedades de campo en el panel Propiedades.
   - Establecer reglas y comportamientos de validación.
   - Ajuste el estilo y el diseño según sea necesario.

   ![Formulario de registro completado](/help/edge/assets/contact-us.png)

#### Validación

- Todos los campos obligatorios están presentes.
- Las propiedades del campo están configuradas correctamente.
- El diseño es adaptable y accesible.
- Las reglas de validación funcionan según lo esperado.

#### Próximos pasos

- [Configure acciones de envío](/help/edge/docs/forms/universal-editor/submit-action.md) para la administración de datos.
- [Guía del editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg) para funciones avanzadas.

### Paso 3: Configuración y publicación

Configure Edge Delivery Services y publique el formulario.

**Configuración:** automática (no se requiere configuración manual).

- La conexión al repositorio de GitHub y la configuración de Edge Delivery Services se crean durante la creación del formulario.
- Los puntos finales de publicación se configuran automáticamente.

**Verificación:**

- Confirme que la configuración aparece en la configuración del formulario.
- Asegúrese de que la dirección URL de GitHub esté vinculada correctamente.

![Configuración automática de EDS](/help/edge/assets/aem-instance-eds-configuration.png)

#### Publicar el formulario

1. En el editor universal, haga clic en el botón **Publicar** (esquina superior derecha).
2. Confirme la publicación correcta en el cuadro de diálogo.
3. Tenga en cuenta las direcciones URL generadas para las versiones ensayadas y activas.

   ![Publicar con el editor universal](/help/edge/assets/publish-form.png)

- [Guía de publicación](/help/edge/docs/forms/universal-editor/publish-forms.md)

## URL de formulario

Los formularios publicados son accesibles a través de las direcciones URL de Edge Delivery Services.

### Estructura de URL

- **Ensayo (vista previa/prueba):**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **Activo (producción):**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### Parámetros de URL

- `<branch>`: nombre de rama de GitHub (por ejemplo, `main`, `develop`)
- `<repo>`: nombre del repositorio de GitHub (por ejemplo, `my-forms-project`)
- `<owner>`: organización de GitHub o nombre de usuario (por ejemplo, `company-name`)
- `<form_name>`: identificador de formulario tal como se define en AEM (por ejemplo, `contact-us`)

#### Ejemplo

Ejemplo del formulario `contact-us` en el repositorio `forms-project` de la organización `acme-corp`:

- **Ensayo:** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **Activo:** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### Diferencias de entorno

- **Ensayo (.page):** cambios más recientes para realizar pruebas.
- **Activo (.live):** contenido publicado para producción.

![Estructura URL](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Desglose de estructura de URL de formularios Edge Delivery Services*

#### Ejemplos visuales

**Plantilla de Edge Delivery Services:**

- Ensayo: ![versión de ensayo de formulario de registro](/help/forms/assets/registration-form-staged-version.png)
- Activo: ![versión activa de formulario de registro](/help/forms/assets/registration-form-live-version.png)

## Resolución de problemas

A continuación, se muestran problemas comunes y soluciones para AEM Forms con Edge Delivery Services.

+++Formulario no cargado

**Problema:** la dirección URL del formulario devuelve 404 o una página en blanco.

**Resolución:**

- Quitar la extensión `.html` de las direcciones URL.
- Compruebe que el formulario esté publicado.
- Compruebe el repositorio de GitHub del bloque de formularios adaptables.
- Asegúrese de que el nombre del formulario coincida con la dirección URL (con distinción entre mayúsculas y minúsculas).

+++

+++Problemas de configuración

**Problema:** la configuración de Edge Delivery Services no funciona.

**Resolución:**

- Asegúrese de que la dirección URL de GitHub esté en formato `https://github.com/owner/repository`.
- Utilice el nombre de rama correcto en la configuración.
- Compruebe el acceso al repositorio (público o autenticado).
- Consulte `fstab.yaml` para obtener los detalles correctos de GitHub.

+++

+++Problemas de publicación

**Problema:** los cambios no aparecen en el sitio activo.

**Resolución:**

- Espere de 2 a 3 minutos para actualizar la caché de la CDN.
- Confirme que el flujo de trabajo de publicación se ha completado.
- Pruebe primero en el entorno de ensayo (.page).
- Asegúrese de que el repositorio de GitHub esté actualizado.

+++

+++Problemas del editor universal

**Problema:** no se puede editar el formulario o los componentes no cargan.

**Resolución:**

- Utilice un navegador compatible (Chrome, Firefox, Safari).
- Borre la caché y las cookies del explorador.
- Compruebe la conectividad de red.
- Confirme los permisos de autor.

+++

+++Errores de envío de formularios

**Problema:** los envíos de formularios no funcionan.

**Resolución:**

- Configure la acción de envío en las propiedades del formulario.
- Pruebe los extremos de envío manualmente.
- Compruebe la configuración de CORS en caso de incrustar formularios.
- Compruebe que los campos obligatorios están configurados.

+++

+++Problemas de rendimiento

**Problema:** carga lenta del formulario o rendimiento deficiente.

**Resolución:**

- Optimizar imágenes.
- Elimine los componentes innecesarios.
- Use la CDN de Edge Delivery Services.
- Minimice el uso de JavaScript/CSS personalizado.

+++

+++Obtención de ayuda

Si los problemas persisten:

1. Compruebe el estado del servicio de Adobe Experience Cloud.
2. Revise la [documentación de Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=es).
3. Visite la [Comunidad de Adobe Experience League](https://experienceleaguecommunities.adobe.com/?profile.language=es).
4. Contacte con el Servicio de atención al cliente de Adobe.

+++

## Próximos pasos

Después de completar la creación y publicación del formulario, tenga en cuenta lo siguiente:

- [Configure acciones de envío](/help/edge/docs/forms/universal-editor/submit-action.md): configure la administración de datos y las integraciones.
- [Modelos de datos de formulario](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md): conecte formularios a orígenes de datos back-end.
- [Prácticas recomendadas de Edge Delivery Services](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html?lang=es): maximice el rendimiento.
- [Form Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html?lang=es): efectúe el seguimiento del rendimiento del formulario y del comportamiento del usuario.

