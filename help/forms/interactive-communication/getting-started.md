---
title: Introducción al editor de comunicaciones interactivas (CI)
description: La comunicación interactiva permite a las organizaciones diseñar y ofrecer comunicaciones personalizadas basadas en datos.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 11%

---


# Introducción al editor de comunicaciones interactivas (CI)

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

El editor de **comunicaciones interactivas (CI)** de Adobe Experience Manager (AEM) Forms permite a las organizaciones diseñar y entregar comunicaciones personalizadas basadas en datos, como extractos, facturas y cartas, en canales digitales e impresos. Esta guía proporciona información general sobre cómo empezar, desde la incorporación hasta la navegación por la interfaz del editor de CI.


## Incorporación y acceso

### Requisitos de acceso

Para usar la comunicación interactiva, asegúrate de que tu entorno de AEM Forms as a Cloud Service incluya el **complemento de AEM Forms** y de que tu cuenta tenga los permisos apropiados.

### Verifique su explorador

Para conocer los exploradores y las plataformas de cliente compatibles, siga el artículo vinculado [Plataformas de cliente compatibles](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/supported-platforms)

>[!NOTE]
>
> **Compatibilidad con exploradores con ciclos de lanzamiento rápidos:**
> Firefox, Chrome y Edge lanzan actualizaciones con regularidad. Adobe se compromete a mantener el nivel de compatibilidad indicado anteriormente para las próximas versiones de estos exploradores.

### Configurar roles y permisos de usuario

El acceso a las características del Editor IC está regido por [roles de usuario dentro de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions). A continuación se indican las funciones clave que intervienen en la creación y administración de las comunicaciones interactivas:

| **Función** | **Descripción** | **Permisos de clave** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **Autor de formularios** | Crea y edita comunicaciones interactivas. | Crear, editar, previsualizar y publicar CI. |
| **Autor de plantillas** | Diseña plantillas reutilizables para comunicaciones interactivas. | Cree y bloquee plantillas, y defina diseños. |
| **Administrador** | Administra el acceso de los usuarios, los permisos y las configuraciones. | Asigne funciones, administre plantillas y publique CI. |
| **Autor de FDM** | [Crea y administra modelos de datos de formulario (FDM)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models) para la integración de datos. | Crear, editar y configurar fuentes de datos y modelos. |

>[!NOTE]
>
> Asegúrese de que los usuarios formen parte de los grupos de AEM adecuados (por ejemplo, `forms-user`, `fdm-author`, `template-authors`) para acceder a las funciones correspondientes.

## Acceso al Editor IC

1. Inicie sesión en su instancia de **AEM Forms as a Cloud Service**.
2. Vaya a **Forms > Comunicaciones interactivas**.
3. Haga clic en **Crear** → **Comunicación interactiva**.
4. Elija una **plantilla**, configure las fuentes de datos y haga clic en **Crear** para abrir el **Editor de comunicaciones interactivas**.

El editor proporciona un entorno unificado para diseñar, previsualizar y administrar las versiones impresa y web de las comunicaciones.

## Navegación por la interfaz

La interfaz de **Editor de comunicaciones interactivas** se ha diseñado para que los autores tengan acceso intuitivo a todas las herramientas de diseño y opciones de configuración.

![Buscar documento CI](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### &#x200B;1. Barra de herramientas superior

![Buscar documento CI](/help/forms/interactive-communication/assets/tool-bar.png)

**Ubicación:** sección superior

**Propósito:** Proporciona acceso al entorno y acciones globales.

**Incluye:**

Muestra el **entorno de Adobe Experience Cloud** (por ejemplo, Ensayo), junto con el **título del proyecto**, **comentarios de Beta**, **notificaciones** y **controles de perfil** para administrar la configuración de usuario y el acceso al entorno.

### &#x200B;2. Barra de fichas (fichas Diseño/Patrón y controles de archivo)

![Buscar documento CI](/help/forms/interactive-communication/assets/tab-bar.png)

**Ubicación:** debajo del encabezado superior

**Propósito:** Administrar vistas y archivos de comunicación.

**Incluye:**

**Fichas:** Cambiar entre **Vista de diseño** y **Vista de página maestra** para el diseño y el diseño de elementos reutilizables

**Nombre de archivo:** Muestra el título de la comunicación actual (por ejemplo, ic-11)

**Controles de vista:** Opciones como regla, creación, zoom (85%), Deshacer/Rehacer, Eliminar, Vista previa de PDF y Guardar

### &#x200B;3. Panel izquierdo (navegación y herramientas de componentes)

![Buscar documento CI](/help/forms/interactive-communication/assets/left-panel.png)

**Ubicación:** lado izquierdo de la interfaz

**Propósito:** acceder a la estructura del proyecto, los recursos reutilizables y los enlaces de datos.

**Incluye:**

* **Página principal:** Lleva al usuario a la pantalla principal de la comunicación interactiva (CI), donde puede ver y administrar las CI y carpetas existentes.

* **Panel de menú:** muestra opciones relacionadas con la vista como Reglas, Límites de objeto, Ajustar a cuadrícula, Ajustar a objeto de característica y la característica Importar XDP.

* **Vista de jerarquía:** Muestra la estructura de componentes de la comunicación, mostrando la organización de páginas, paneles y subformularios.

* **Biblioteca de componentes:** Contiene elementos de diseño como texto, imagen, subformulario y código de barras que se pueden arrastrar al lienzo.

* **Fragmentos:** Permite la reutilización de bloques de contenido y diseño predefinidos en varias comunicaciones.

* **Modelo de datos:** Conecta la comunicación con los modelos de datos de formulario (FDM) subyacentes para enlazar datos dinámicos.

### &#x200B;4. Workspace central (lienzo de diseño)

![Buscar documento CI](/help/forms/interactive-communication/assets/canvas.png)

**Ubicación:** Centro de la interfaz

**Propósito:** área de trabajo principal para diseñar comunicaciones interactivas.

**Características:**

* Arrastrar y soltar componentes de la biblioteca

* Organizar y dar formato al diseño visual

* Agregar o editar páginas, subformularios y campos

* Navegue entre páginas (por ejemplo, &quot;1 de 1&quot;) utilizando los controles en la parte inferior izquierda

* Previsualización del diseño final antes de publicar

### &#x200B;5. Panel derecho (panel de propiedades)

![Buscar documento CI](/help/forms/interactive-communication/assets/right-panel.png)

**Ubicación:** lado derecho de la pantalla

**Propósito:** personalizar el comportamiento y el estilo del componente.

**Incluye:**

* Configuración general (nombre, tipo, posición/posición variable)

* Opciones de diseño y apariencia

* Controles de paginación, posición, presencia y enlace de datos