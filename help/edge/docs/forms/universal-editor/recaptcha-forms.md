---
title: Añadir Google reCAPTCHA a Forms en el editor universal
description: Guía para implementar la protección reCAPTCHA de Google en formularios Edge Delivery Services para evitar spam y ataques automatizados
feature: Edge Delivery Services
keywords: reCAPTCHA en formularios, uso de reCAPTCHA en el editor universal, añadir reCAPTCHA en formularios, seguridad de formularios, protección contra spam
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 5%

---


# Añadir Google reCAPTCHA a Forms en el editor universal

Google reCAPTCHA ayuda a proteger los formularios al distinguir entre usuarios humanos y bots automatizados. En esta guía se explica cómo implementar las versiones de reCAPTCHA Enterprise y Standard en el editor universal.

**Objetivos:**

- Seleccione la solución reCAPTCHA adecuada
- Configuración de reCAPTCHA Enterprise o Standard
- Añadir reCAPTCHA a los formularios
- Validación y prueba de la implementación
- Monitorización y optimización del rendimiento

## Requisitos previos

Antes de empezar, asegúrese de que dispone de lo siguiente:

### Requisitos de acceso

- Acceso de creación de AEM as a Cloud Service
- Acceso al Editor universal con permisos de edición de formularios
- Inscripción en el programa de acceso anticipado para funciones de reCAPTCHA

### Requisitos técnicos

- Cuenta activa de Google
- Para empresas: proyecto de Google Cloud Platform con facturación habilitada
- Para Standard: Cuenta reCAPTCHA de Google
- Propiedad de dominio verificada para sus formularios

### Requisitos de conocimientos

- Comprensión básica de AEM Forms y Universal Editor
- Familiaridad con las configuraciones de servicios en la nube
- Comprensión de los conceptos de seguridad del formulario

## ¿Por qué utilizar reCAPTCHA en su Forms?

| ![Seguridad](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protección contra bots](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Experiencia del usuario](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Seguridad mejorada** | **Prevención de bots y spam** | **Experiencia del usuario perfecta** |
| Proteger formularios de actividades y ataques fraudulentos | Impedir que los bots automatizados envíen formularios | reCAPTCHA invisible no interrumpe a los usuarios legítimos |

**Concepto clave:** reCAPTCHA utiliza el aprendizaje automático para analizar el comportamiento del usuario y asigna una puntuación (de 0,0 a 1,0) que indica la probabilidad de interacción humana. Las puntuaciones más altas indican usuarios humanos; las puntuaciones más bajas sugieren bots.

**Ejemplo:** Un formulario de cálculo de impuestos que administra datos confidenciales requiere protección contra ataques automatizados. reCAPTCHA comprueba que los envíos proceden de usuarios reales, no de bots.

## Elija su solución reCAPTCHA

Edge Delivery Services Forms admite dos opciones de Google reCAPTCHA. Utilice los siguientes criterios para seleccionar la solución correcta:

### Guía de decisión rápida

**Usar reCAPTCHA Enterprise si tiene:**

- Formularios de alto tráfico (>10 000 solicitudes al mes)
- Requisitos de cumplimiento estrictos (RGPD, SOX, HIPAA)
- Necesidad de análisis e informes avanzados
- Presupuesto para funciones de seguridad avanzadas
- Implementaciones complejas de varios dominios

**Use reCAPTCHA Standard si tiene:**

- Tráfico de bajo a moderado (&lt;10 000 solicitudes/mes)
- Necesidades de seguridad básicas
- Presupuesto limitado (nivel gratuito)
- Configuración simple de un solo dominio
- Es nuevo en reCAPTCHA

### Comparación detallada

| **Función** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **Costo** | De pago (precios basados en el uso) | Gratis |
| **Límite de solicitudes** | Ilimitado | 1 millones de solicitudes al mes |
| **Análisis avanzado** | Informes detallados | Solo estadísticas básicas |
| **Reglas personalizadas** | Reglas específicas de la cuenta | Solo reglas globales |
| **Compatibilidad con varios dominios** | Administración avanzada | Soporte básico |
| **SLA** | Garantía de tiempo de actividad del 99,9% | Mejor esfuerzo |
| **Asistencia** | Soporte Enterprise | Apoyo comunitario |
| **Cumplimiento** | De categoría empresarial | Cumplimiento estándar |

**Ambas soluciones proporcionan:**

- Detección basada en puntuaciones (escala de 0,0 a 1,0)
- Operación invisible (no se requiere interacción del usuario)
- Detección de bots con tecnología de aprendizaje automático
- Evaluación de riesgos en tiempo real

## Configuración de reCAPTCHA Enterprise


+++ Paso 1: Preparar el entorno de nube de Google

**Requisitos:**

1. Proyecto de Google Cloud con facturación habilitada
2. ID de proyecto (del panel de GCP)
3. Verificación de dominios para sus formularios
4. Acceso de administrador a GCP y AEM

**Configuración:**

1. Cree o seleccione un proyecto de Google Cloud
   - Ir a [Consola de Google Cloud](https://console.cloud.google.com/)
   - Cree un nuevo proyecto o seleccione uno existente
   - Anote su ID de proyecto

2. Habilitar la API de reCAPTCHA Enterprise
   - Vaya a API y servicios > Biblioteca
   - Busque &quot;reCAPTCHA Enterprise API&quot;
   - Haga clic en Habilitar

3. Crear credenciales de API
   - Vaya a API y servicios > Credenciales
   - Haga clic en Crear credenciales > Clave de API
   - Copiar y almacenar la clave de API

4. Crear clave del sitio
   - Vaya a Seguridad > reCAPTCHA Enterprise
   - Haga clic en Crear clave
   - Elija el tipo de clave basada en la puntuación
   - Añadir sus dominios.
   - Establecer puntuación de umbral (recomendado: 0,5)

**Punto de comprobación de validación:** Asegúrese de que dispone de:

- ID del proyecto
- Clave de API
- Clave del sitio
- Dominio verificado en Google Cloud

+++

+++ Paso 2: Configurar el contenedor de configuración de AEM Cloud

![Configuración de nube paso a paso](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Imagen: habilitando configuraciones de nube para el contenedor de formularios*

**Configuración:**

1. Acceder al explorador de configuración
   - Inicie sesión en la instancia de autor de AEM
   - Vaya a Herramientas > General > Explorador de configuración

2. Habilitar configuraciones en la nube
   - Busque el contenedor de configuración del formulario
   - Seleccionar propiedades
   - Comprobar configuraciones de nube
   - Haga clic en Guardar y cerrar

3. Verificar la configuración
   - Confirme que aparece &quot;Configuraciones de nube&quot; en las propiedades del contenedor

**Punto de comprobación de validación:**

- Configuraciones de nube habilitadas para el contenedor
- El contenedor aparece en el Explorador de configuración
- Las propiedades muestran &quot;Configuraciones en la nube&quot; como habilitadas

+++

+++ Paso 3: Configuración del servicio reCAPTCHA Enterprise en AEM

![pantalla de configuración de reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Figura: interfaz de configuración de reCAPTCHA Enterprise en AEM*

**Configuración:**

1. Acceso a configuración de reCAPTCHA
   - Vaya a Herramientas > Cloud Services > reCAPTCHA
   - Seleccione el contenedor de configuración del formulario
   - Haga clic en Crear

2. Configuración de empresa
   - Título: Nombre descriptivo (por ejemplo, &quot;Production reCAPTCHA&quot;)
   - Nombre: Nombre del sistema (generado automáticamente o personalizado)
   - Versión: seleccione ReCAPTCHA Enterprise
   - ID del proyecto: introduzca su ID de proyecto de Google Cloud
   - Clave del sitio: introduzca la clave del sitio desde Google Cloud
   - Clave de API: Introduzca la clave de API de Google Cloud
   - Tipo de clave: seleccione la clave del sitio basada en la puntuación

3. Establecer umbral de seguridad
   - Puntuación de umbral: establezca entre 0,0 y 1,0
   - Valores recomendados:
      - 0.7-0.9: Alta seguridad (puede bloquear a algunos usuarios legítimos)
      - 0,5-0,7: seguridad equilibrada (recomendado)
      - 0.1-0.5: menor seguridad (permite más usuarios)

4. Guardar y publicar
   - Haga clic en Crear para guardar la configuración
   - Haga clic en Publicar para que esté disponible

**Punto de comprobación de validación:**

- Configuración guardada correctamente
- Todos los campos obligatorios completados
- Configuración publicada y visible
- No hay mensajes de error

+++

## Configuración de reCAPTCHA Standard

+++Paso 1: Obtener claves de API reCAPTCHA (Ver detalles)

>[!IMPORTANT]
>
> Edge Delivery Services Forms solo admite reCAPTCHA v2 (basado en puntuación). No utilice la versión de la casilla de verificación.

**Generación de claves:**

1. Acceder a la consola de Google reCAPTCHA

   - Ir a [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - Inicie sesión con su cuenta de Google

2. Crear nuevo sitio

   - Haga clic en + para agregar un nuevo sitio
   - Etiqueta: introduzca un nombre descriptivo
   - Tipo reCAPTCHA: Seleccione reCAPTCHA v2 > &quot;No soy un robot&quot; Invisible
   - Dominios: Agregue los dominios del formulario
   - Acepte los términos y haga clic en Enviar

3. Recopile sus claves

   - Clave del sitio: copie la clave del sitio (clave pública)
   - Clave secreta: copie la clave secreta (clave privada)

**Punto de comprobación de validación:**

- Sitio creado en la consola reCAPTCHA

- Clave de sitio obtenida

- Clave secreta obtenida

- Dominio(s) añadido(s) y verificado

+++

+++Paso 2: Configurar el contenedor de configuración de AEM Cloud (Ver detalles)

Siga el mismo proceso que en la configuración de Enterprise:

1. Habilitar configuraciones de nube en el explorador de configuración

2. Verificar configuración del contenedor

3. Confirmar que se guardaron los ajustes

+++

+++Paso 3: Configuración del servicio reCAPTCHA Standard en AEM (Ver detalles)

![Pantalla de configuración estándar reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Figura: interfaz de configuración estándar reCAPTCHA en AEM*

**Configuración:**

1. Acceso a configuración de reCAPTCHA

   - Vaya a Herramientas > Cloud Services > reCAPTCHA
   - Seleccione el contenedor de configuración del formulario
   - Haga clic en Crear

2. Configuración estándar

   - Título: Nombre descriptivo (por ejemplo, &quot;reCAPTCHA estándar&quot;)
   - Nombre: Nombre del sistema (generado automáticamente o personalizado)
   - Versión: seleccione ReCAPTCHA v2
   - Clave del sitio: introduzca la clave del sitio reCAPTCHA de Google
   - Clave secreta: introduzca la clave secreta reCAPTCHA de Google

3. Guardar y publicar

   - Haga clic en Crear para guardar la configuración
   - Haga clic en Publicar para que esté disponible

**Punto de comprobación de validación:**

- Configuración creada sin errores

- Ambas claves se han introducido correctamente

- Configuración publicada correctamente

- La configuración aparece en la lista

+++

## Agregar reCAPTCHA al formulario

Después de configurar el servicio reCAPTCHA, agregue protección al formulario de la siguiente manera:

![Agregando el componente reCAPTCHA a un formulario](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figura: Agregar el componente Captcha invisible al formulario*

+++1. Abrir formulario en editor universal
Vaya al formulario en AEM Sites y haga clic en Editar para abrirlo en el editor universal. Espere a que se cargue el editor.

- Vaya al formulario en AEM Sites
- Haga clic en Editar para abrir en el editor universal
- Espere a que se cargue el editor
+++

+++2. Busque la estructura del formulario
En el árbol de contenido (panel izquierdo), busque la sección Formulario adaptable y expanda la estructura del formulario para ver los puntos de inserción.

- En el árbol de contenido (panel izquierdo), busque la sección Formulario adaptable
- Expandir la estructura del formulario para ver los puntos de inserción
+++

+++3. Añadir componente reCAPTCHA
Agregue el componente Captcha (invisible) al formulario.

- Haga clic en el icono Agregar (+) de la sección del formulario
- En la lista de componentes, seleccione Captcha (invisible)
- También puede arrastrar y soltar el componente desde el panel Componentes
+++

+++4. Configurar componente (opcional)
Seleccione el componente captcha recién agregado y verifique que utiliza su configuración reCAPTCHA.

- Seleccione el componente captcha recién agregado
- En el panel Propiedades, compruebe que utiliza la configuración de reCAPTCHA
- No se necesita ninguna configuración adicional para la configuración básica
+++

+++5. Publicación de los cambios
Publique los cambios y compruebe que no hay errores.

- Haga clic en Publicar en el editor universal
- Esperar confirmación
- Verificar que no aparezcan errores
+++

### Verificar implementación

Su formulario protegido está ahora disponible en:

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**URL de ejemplo:**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-form
```
