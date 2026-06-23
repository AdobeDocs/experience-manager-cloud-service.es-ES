---
title: Asociar interfaz de usuario en el editor de comunicaciones interactivas
description: Descubra la interfaz de usuario asociada en el Editor de comunicaciones interactivas habilitando el agente orientado al cliente para generar comunicaciones personalizadas y compatibles.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: 9ba58659-b14c-4ebc-a6d9-e56a4b6aa48b
source-git-commit: 53ff71c82d35b9ec9b20b521ef469d3f0abd79df
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---

# Asociar interfaz de usuario en el editor de comunicaciones interactivas


La **interfaz de usuario asociada** es una interfaz simplificada y especializada creada sobre el editor de comunicaciones interactivas (CI). Está diseñado para profesionales que trabajan de cara al cliente, como socios de campo y agentes de servicio, para generar comunicaciones personalizadas, compatibles y precisas en tiempo real durante las interacciones en directo.

![Buscar documento CI](/help/forms/interactive-communication/assets/associate-ui-preview.png)

## Asociar interfaz de usuario

La interfaz de usuario de Associate proporciona un espacio de trabajo limpio con dos paneles que permite generar comunicaciones de forma rápida y segura:

### Panel izquierdo: entrada de datos

- Los asociados introducen o confirman información específica del cliente.
- Las validaciones, los textos de ayuda y los campos obligatorios guían la entrada precisa.

### Panel derecho: vista previa en tiempo real

- Muestra una vista previa instantánea del documento final.
- Se actualiza automáticamente a medida que el asociado rellena los datos.

### Generación instantánea de documentos

- Generar o descargar la comunicación finalizada.

## Personas y responsabilidades del usuario

La interfaz de usuario asociada se rige por tres funciones principales, cada una con responsabilidades distintas:

### &#x200B;1. Administrador

Responsable de la configuración del sistema, la gobernanza, las integraciones back-end y el acceso de los usuarios.

| Responsabilidad | Concentrar |
|---------------|-------|
| Configuración del sistema | Configura la infraestructura principal, los grupos de usuarios, los modelos de datos de formulario (FDM) y la salida |
| Gobernanza y seguridad | Gestiona los permisos de usuario y garantiza el cumplimiento del sistema. |
| Administración de integración | Mantiene integraciones back-end y conexiones de datos de clientes activas. |

### &#x200B;2. Autor

Diseña y administra la comunicación interactiva y la configura para la interfaz de usuario asociada (incluida la activación de la vista asociada y el flujo de trabajo opcional).

| Responsabilidad | Concentrar |
|---------------|-------|
| Creación y diseño de CI | Crea el diseño, la personalización de marca y la estructura de documento compatible. |
| Configuración de campo | Asigna campos de datos y define campos editables, obligatorios y de solo lectura. |
| Publicación y activación | Publica el IC y comparte el vínculo para el acceso de asociados. |

### &#x200B;3. Asociar

Utiliza la interfaz de usuario asociada para ayudar a los clientes, actualizar la información y generar comunicaciones compatibles.


| Responsabilidad | Concentrar |
|---------------|-------|
| Confirmación de datos | Rellena o valida los datos del cliente mediante el panel de entrada izquierdo. |
| Previsualización y validación | Garantiza la precisión mediante el panel de vista previa en tiempo real. |
| Entrega | Genera el PDF/correo electrónico y lo envía a través de canales aprobados. |

>[!NOTE]
>
> Asociados debe formar parte del grupo **forms-associates**. Para los autores que también envíen contenido desde la IU asociada en la instancia de autor, agréguelos también a **workflow-users**.

## Casos de uso dinámicos

La interfaz de usuario asociada admite la generación instantánea y personalizada de documentos, crucial para los sectores con necesidades de servicio en tiempo real.

| Industria | Casos de uso de ejemplo |
|----------|-------------------|
| **Servicios financieros** | Generar cartas de confirmación de préstamo en tiempo real, resúmenes de perfil de riesgo y creación de cuentas. |
| **Seguro** | Produzca al instante tarjetas de prueba de seguro o resúmenes de disposición de reclamaciones. |
| **Atención sanitaria** | Crear resúmenes de planes de tratamiento de pacientes con copago calculado y horarios. |
| **Sector Público** | Generar informes de verificación policial, recibos de servicio ciudadano, cartas de confirmación de quejas y resúmenes de actualización de casos in situ. |
| **Gobierno** | Cree resúmenes del estado de la solicitud, cartas de aprobación del servicio y comunicación en tiempo real para las inscripciones en planes de bienestar. |

## Activación de la IU asociada

Los autores habilitan la interfaz de usuario asociada y, opcionalmente, configuran un flujo de trabajo para los envíos en **Configuración de la comunicación interactiva**:

1. **Habilitar vista asociada** — En **Propiedades asociadas**, marque **Habilitar edición de vista asociada**, luego haga clic en **Aplicar cambios** y guarde el documento.
2. **Configurar flujo de trabajo (opcional)**: en **Flujo de trabajo**, active **Configurar flujo de trabajo para actualización**, seleccione un modelo de flujo de trabajo y, opcionalmente, establezca un mensaje de éxito y una URL de redirección.
3. **Configurar campos editables**: habilite los campos que los asociados pueden editar y establecer validaciones.
4. **Publicar y compartir**: publique la CI y comparta el vínculo con los asociados.

Para obtener instrucciones paso a paso con capturas de pantalla y el comportamiento del envío/flujo de trabajo (Autor en Autor vs Asociar en Publicación), consulte [Habilitar y configurar la IU asociada para comunicaciones interactivas](/help/forms/interactive-communication/enable-configure-associate-ui.md). Para generar un flujo de trabajo que genere PDF a partir de los envíos de CI, consulte [Flujo de trabajo de envío para la interfaz de usuario asociada — IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md).

La **interfaz de usuario asociada** reduce la brecha entre la creación de contenido estructurado y la participación de clientes en tiempo real.\
Combinando un diseño intuitivo, una configuración back-end sólida y estrictos controles de cumplimiento, las organizaciones pueden ofrecer **comunicaciones rápidas, precisas y personalizadas** a escala.

## Ver también

- [Habilitar y configurar la interfaz de usuario asociada para comunicaciones interactivas](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Configurar las opciones desplegables de la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-dropdown-options-binding.md)
- [Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-bound-unbound-variables-associate-ui.md)
- [Integración de la interfaz de usuario asociada en la aplicación](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Flujo de trabajo de envío para la IU asociada: IC Generar salida de PDF](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)

