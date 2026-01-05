---
title: Asociar interfaz de usuario en el editor de comunicaciones interactivas
description: Descubra la interfaz de usuario asociada en el Editor de comunicaciones interactivas habilitando el agente orientado al cliente para generar comunicaciones personalizadas y compatibles.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 234b6dc747bbba21e9249d526bf894860572dfe5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 3%

---


# Asociar interfaz de usuario en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

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

Diseña y administra la comunicación interactiva mediante la IU asociada. ß

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
> La asociación debe formar parte del grupo **forms-associates**.

## Casos de uso dinámicos

La interfaz de usuario asociada admite la generación instantánea y personalizada de documentos, crucial para los sectores con necesidades de servicio en tiempo real.

| Industria | Casos de uso de ejemplo |
|----------|-------------------|
| **Servicios financieros** | Generar cartas de confirmación de préstamo en tiempo real, resúmenes de perfil de riesgo y creación de cuentas. |
| **Seguro** | Produzca al instante tarjetas de prueba de seguro o resúmenes de disposición de reclamaciones. |
| **Atención sanitaria** | Crear resúmenes de planes de tratamiento de pacientes con copago calculado y horarios. |
| **Sector Público** | Generar informes de verificación policial, recibos de servicio ciudadano, cartas de confirmación de quejas y resúmenes de actualización de casos in situ. |
| **Gobierno** | Cree resúmenes del estado de la solicitud, cartas de aprobación del servicio y comunicación en tiempo real para las inscripciones en planes de bienestar. |

## Activación del flujo de trabajo Asociar IU

El autor puede seguir los pasos a continuación para configurar y publicar una comunicación interactiva (CI) para el acceso a la IU asociada:

>[!NOTE]
>
> Componentes admitidos para asociados: Campo de fecha, campo numérico, campo de texto, DateTimeField, DateField, casilla de verificación, botón de opción, desplegable.

### Creación de la CI

Diseñe y configure la comunicación interactiva, asegurándose de que la marca, los enlaces de datos, las reglas de conformidad y las integraciones estén correctamente configuradas.

### Habilitar la interfaz de usuario asociada

En la barra de acciones superior, habilite la opción Asociar interfaz de usuario para que la CI esté disponible para las actividades dirigidas por asociados.

### Habilitar la interfaz de usuario asociada en el componente

### Configurar campos editables

En la sección de campos obligatorios, habilite los campos que los asociados pueden editar.
Configure validaciones para garantizar una entrada de datos precisa y controlada.

### Publicación de la CI

Después de finalizar todas las configuraciones, publique la comunicación interactiva para obtener acceso seguro.

### Compartir la CI publicada con los asociados

Proporcione el vínculo de CI publicado al asociado, lo que le permite autenticarse, introducir información específica del cliente y generar la comunicación final con entradas válidas.

La **interfaz de usuario asociada** reduce la brecha entre la creación de contenido estructurado y la participación de clientes en tiempo real.\
Combinando un diseño intuitivo, una configuración back-end sólida y estrictos controles de cumplimiento, las organizaciones pueden ofrecer **comunicaciones rápidas, precisas y personalizadas** a escala.
