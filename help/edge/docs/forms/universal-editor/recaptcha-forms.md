---
title: Añadir Google reCAPTCHA a formularios en el editor universal
description: Guía para implementar la protección reCAPTCHA de Google en formularios Edge Delivery Services para evitar spam y ataques automatizados
feature: Edge Delivery Services
keywords: reCAPTCHA en formularios, uso de reCAPTCHA en el editor universal, añadir reCAPTCHA en formularios, seguridad de formularios, protección contra spam
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1281'
ht-degree: 100%

---


# Añadir Google reCAPTCHA a formularios en el editor universal

Google reCAPTCHA ayuda a proteger los formularios al distinguir entre usuarios que son humanos y los bots automatizados. En esta guía se explica cómo implementar las versiones de reCAPTCHA Enterprise y Standard en el editor universal.

**Objetivos:**

- Seleccionar la solución reCAPTCHA adecuada
- Configurar reCAPTCHA Enterprise o Standard
- Añadir reCAPTCHA a los formularios
- Validar y probar la implementación
- Monitorizar y optimizar el rendimiento

## Requisitos previos

Antes de empezar, asegúrese de que dispone de lo siguiente:

### Requisitos de acceso

- Acceso de creación a AEM as a Cloud Service
- Acceso al editor universal con permisos de edición de formularios

### Requisitos técnicos

- Cuenta activa de Google
- Para Enterprise: proyecto de Google Cloud Platform con facturación habilitada
- Para Standard: Cuenta reCAPTCHA de Google
- Propiedad de dominio verificada para sus formularios

### Requisitos de conocimientos

- Comprensión básica de AEM Forms y el editor universal
- Familiaridad con las configuraciones de servicios en la nube
- Comprensión de los conceptos de seguridad del formulario

## ¿Por qué debería usar reCAPTCHA en sus formularios?

| ![Seguridad](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protección contra bots](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Experiencia del usuario](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Seguridad mejorada** | **Prevención de bots y spam** | **Experiencia del usuario perfecta** |
| Proteger los formularios de actividades y ataques fraudulentos | Impedir que los bots automatizados envíen formularios | El reCAPTCHA invisible no interfiere con los usuarios legítimos. |

**Concepto clave:** el reCAPTCHA utiliza el aprendizaje automático para analizar el comportamiento del usuario y asigna una puntuación (de 0,0 a 1,0) que indica la probabilidad de interacción humana. Las puntuaciones más altas indican usuarios humanos; las puntuaciones más bajas sugieren que se trata de un bot.

**Ejemplo:** un formulario de cálculo de impuestos que administra datos confidenciales requiere protección contra ataques automatizados. reCAPTCHA comprueba que los envíos proceden de usuarios reales, no de bots.

## Elija su solución reCAPTCHA

Los formularios de Edge Delivery Services admiten dos opciones de Google reCAPTCHA. Utilice los siguientes criterios para seleccionar la solución adecuada:

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
| **Costo** | De pago (precios según el uso) | Gratis |
| **Límite de solicitudes** | Ilimitado | 1 millón de solicitudes al mes |
| **Análisis avanzado** | Creación de informes detallados | Solo estadísticas básicas |
| **Reglas personalizadas** | Reglas específicas de la cuenta | Solo reglas globales |
| **Compatibilidad con varios dominios** | Gestión avanzada | Asistencia básica |
| **SLA** | Garantía de tiempo de actividad del 99,9 % | Mejor esfuerzo |
| **Soporte** | Asistencia técnica para empresas | Asistencia para la comunidad |
| **Cumplimiento** | Categoría empresarial | Cumplimiento estándar |

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
   - Vaya a la [Consola de Google Cloud](https://console.cloud.google.com/)
   - Cree un nuevo proyecto o seleccione uno existente
   - Tenga en cuenta su ID de proyecto

2. Habilite la API de reCAPTCHA Enterprise
   - Vaya a API y servicios > Biblioteca
   - Busque &quot;API de reCAPTCHA Enterprise&quot;
   - Haga clic en Habilitar

3. Crear credenciales de la API
   - Vaya a API y servicios > Credenciales
   - Haga clic en Crear credenciales > Clave de la API
   - Copie y guarde la clave de la API

4. Cree clave del sitio
   - Vaya a Seguridad > reCAPTCHA Enterprise
   - Haga clic en Crear clave
   - Elija el tipo de clave basada en la puntuación
   - Añadir sus dominios
   - Establezca umbral de puntuación (recomendado: 0,5)

**Punto de comprobación de validación:** asegúrese de que dispone de:

- ID del proyecto
- Clave API
- Clave del sitio
- Dominio verificado en Google Cloud

+++

+++ Paso 2: Configurar contenedor de configuración de AEM Cloud

![Configuración de nube paso a paso](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Imagen: habilitando configuraciones de nube para el contenedor de formularios*

**Configuración:**

1. Acceda al explorador de configuración
   - Inicie sesión en la instancia de autor de AEM
   - Vaya a Herramientas > General > Explorador de configuración

2. Habilite configuraciones de la nube
   - Busque el contenedor de configuración del formulario
   - Seleccione Propiedades
   - Compruebe configuraciones de la nube
   - Haga clic en Guardar y cerrar

3. Verificar la configuración
   - Confirme que &quot;Configuraciones de nube&quot; aparece en las propiedades del contenedor

**Punto de comprobación de validación:**

- Configuraciones de nube habilitadas para el contenedor
- El contenedor aparece en el explorador de configuración
- Las propiedades muestran &quot;Configuraciones en la nube&quot; como habilitadas

+++

+++ Paso 3: Configurar el servicio reCAPTCHA Enterprise en AEM

![pantalla de configuración de reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Figura: interfaz de configuración de reCAPTCHA Enterprise en AEM*

**Configuración:**

1. Acceso a la configuración de reCAPTCHA
   - Vaya a Herramientas > Servicios de nube > reCAPTCHA
   - Seleccione el contenedor de configuración del formulario
   - Haga clic en Crear

2. Establezca la configuración de empresa
   - Título: Nombre descriptivo (por ejemplo, &quot;Production reCAPTCHA&quot;)
   - Nombre: Nombre del sistema (generado automáticamente o personalizado)
   - Versión: seleccione ReCAPTCHA Enterprise
   - ID del proyecto: introduzca su ID de proyecto de Google Cloud
   - Clave del sitio: introduzca la clave del sitio desde Google Cloud
   - Clave de API: Introduzca la clave de API de Google Cloud
   - Tipo de clave: seleccione clave de sitio basada en la puntuación

3. Establezca umbral de seguridad
   - Puntuación de umbral: establezca entre 0,0 y 1,0
   - Valores recomendados:
      - 0,7-0,9: Alta seguridad (puede bloquear a algunos usuarios legítimos)
      - 0,5-0,7: seguridad equilibrada (recomendado)
      - 0,1-0,5: menor seguridad (permite más usuarios)

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
> Los formularios de Edge Delivery Services solo admiten servicios reCAPTCHA v2 (basados en puntuación). No utilice la versión de la casilla de verificación.

**Generación de clave:**

1. Acceda a la consola de Google reCAPTCHA

   - Vaya a [la Admin Console de Google reCAPTCHA](https://www.google.com/recaptcha/admin)
   - Inicie sesión con su cuenta de Google

2. Cree nuevo sitio

   - Haga clic en “+” para añadir nuevo sitio
   - Etiqueta: introduzca un nombre descriptivo
   - Tipo de reCAPTCHA: seleccione reCAPTCHA v2 > &quot;No soy un robot&quot; invisible
   - Dominios: agregue los dominios del formulario
   - Acepte los términos y haga clic en Enviar

3. Consiga sus claves

   - Clave del sitio: copie la clave del sitio (clave pública)
   - Clave secreta: copie la clave secreta (clave privada)

**Punto de comprobación de validación:**

- Sitio creado en la consola reCAPTCHA

- Clave de sitio obtenida

- Clave secreta obtenida

- Dominio(s) añadido(s) y verificado(s)

+++

+++Paso 2: Configurar el contenedor de configuración de AEM Cloud (Ver detalles)

Siga el mismo proceso que en la configuración de Enterprise:

1. Habilite Configuraciones de nube en el explorador de configuración

2. Verifique la configuración del contenedor

3. Confirme que se guardaron los ajustes

+++

+++Paso 3: Configuración del servicio reCAPTCHA Standard en AEM (Ver detalles)

![Pantalla de configuración estándar reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Figura: interfaz de configuración estándar reCAPTCHA en AEM*

**Configuración:**

1. Acceso a la configuración de reCAPTCHA

   - Vaya a Herramientas > Servicios de nube > reCAPTCHA
   - Seleccione el contenedor de configuración del formulario
   - Haga clic en Crear

2. Establezca la configuración estándar

   - Título: Nombre descriptivo (por ejemplo, &quot;reCAPTCHA estándar&quot;)
   - Nombre: Nombre del sistema (generado automáticamente o personalizado)
   - Versión: seleccione ReCAPTCHA v2
   - Clave del sitio: introduzca la clave del sitio reCAPTCHA de Google
   - Clave secreta: introduzca la clave secreta de reCAPTCHA de Google

3. Guardar y publicar

   - Haga clic en Crear para guardar la configuración
   - Haga clic en Publicar para que esté disponible

**Punto de comprobación de validación:**

- Configuración creada sin errores

- Ambas claves se han introducido correctamente

- Configuración publicada correctamente

- La configuración aparece en la lista

+++

## Añadir reCAPTCHA al formulario

Después de configurar el servicio reCAPTCHA, agregue la protección al formulario de la siguiente manera:

![Agregando el componente reCAPTCHA a un formulario](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figura: agregar el componente Captcha invisible al formulario*

+++&#x200B;1. Abrir el formulario en el editor universal
Vaya al formulario en AEM Sites y haga clic en Editar para abrirlo en el editor universal. Espere a que se cargue el editor.

- Vaya al formulario en AEM Sites
- Haga clic en Editar para abrir en el editor universal
- Espere a que se cargue el editor
+++

+++&#x200B;2. Buscar la estructura del formulario
En el árbol de contenido (panel izquierdo), busque la sección Formulario adaptable y expanda la estructura del formulario para ver los puntos de inserción.

- En el árbol de contenido (panel izquierdo), busque la sección Formulario adaptable
- Expanda la estructura del formulario para ver los puntos de inserción
+++

+++&#x200B;3. Añadir el componente reCAPTCHA
Añada el componente Captcha (invisible) a al formulario.

- Haga clic en el icono Añadir (+) de la sección del formulario
- En la lista de componentes, seleccione Captcha (invisible)
- También puede arrastrar y soltar el componente desde el panel Componentes
+++

+++&#x200B;4. Configurar el componente (opcional)
Seleccione el componente captcha recién añadido y verifique que utiliza su configuración reCAPTCHA.

- Seleccione el componente captcha recién agregado
- En el panel Propiedades, compruebe que utiliza la configuración de reCAPTCHA
- No se necesita ninguna configuración adicional para la configuración básica
+++

+++&#x200B;5. Publicar los cambios
Publique los cambios y compruebe que no hay errores.

- Haga clic en Publicar en el editor universal
- Espere la confirmación
- Verifique que no aparezcan errores
+++

### Verifique la implementación

Su formulario protegido está ahora disponible en:

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**URL de ejemplo:**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
