---
title: Portal de obtención de recursos para AEM Assets
description: Obtenga información sobre cómo crear el portal de abastecimiento de Assets, que proporciona una experiencia de autoservicio segura para recopilar recursos de colaboradores externos sin concederles acceso a Adobe Experience Manager Assets.
role: Admin
hide: true
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
source-git-commit: c2a7e7ab0b3c8c336343036af105a827cd77f3c2
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 4%

---


# Portal de obtención de recursos para AEM Assets {#asset-sourcing-portal-aem-assets}

Las organizaciones suelen depender de fotógrafos, agencias creativas y otros colaboradores externos para proporcionar recursos digitales. La recopilación de estos recursos mediante correo electrónico, unidades compartidas o servicios de uso compartido de archivos puede generar metadatos incoherentes, procesamiento manual y esfuerzo administrativo adicional. Proporcionar a los colaboradores externos acceso directo a un sistema de administración de activos digitales (DAM) también puede requerir licencias adicionales y exponer el contenido interno.

El portal de abastecimiento de Assets ofrece una experiencia de autoservicio segura para recopilar recursos de colaboradores externos sin concederles acceso a Adobe Experience Manager Assets. Los colaboradores pueden cargar recursos, proporcionar los metadatos necesarios y enviar contenido directamente a una ubicación de entrada designada, mientras que los administradores mantienen el control de la organización y el control de los recursos.

>[!IMPORTANT]
>
>Esta función está disponible como función de disponibilidad limitada. Puede [crear y enviar un caso de asistencia al cliente de Adobe](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para habilitarlo para su implementación.

## Ventajas {#benefits-asset-sourcing-aem-assets}

El uso del portal de abastecimiento de Assets ofrece las siguientes ventajas:

- Permita que los colaboradores externos carguen recursos sin necesidad de una licencia para AEM Assets.
- Simplifique la ingesta de recursos mediante una experiencia de carga dedicada.
- Reduzca el procesamiento manual mediante la aplicación automática de políticas de ingesta y metadatos.
- Mejore la gobernanza controlando dónde se almacenan los recursos cargados y qué aportan los colaboradores de metadatos.
- Escalar la incorporación para varios colaboradores sin crear soluciones de carga personalizadas.

## ¿Cómo funciona la fuente de recursos? {#how-asset-sourcing-works-in-aem-assets}

Un administrador configura un portal de abastecimiento para un colaborador externo definiendo:

- Ubicación de entrada de destino para los recursos cargados.
- Los colaboradores de los campos de metadatos deben completarlos.
- Políticas de ingesta opcionales, como convenciones de nomenclatura y notificaciones.

Los colaboradores reciben una experiencia de carga especializada en la que pueden:

- Cargue uno o varios recursos.
- Complete los campos de metadatos requeridos.
- Envíe recursos para su ingesta en Adobe Experience Manager Assets.

Durante la ingesta, los recursos cargados se procesan según las directivas configuradas antes de almacenarse en la ubicación de entrada designada.

## Métodos de carga {#upload-methods-asset-sourcing-aem-assets}

El portal de abastecimiento de Assets admite varios métodos de carga para que los colaboradores puedan trabajar dentro de sus flujos de trabajo preferidos.

- **Portal del explorador:** Proporciona una experiencia de carga basada en la web en la que los colaboradores pueden arrastrar y soltar archivos y completar los metadatos requeridos antes de enviar los recursos.

- **API de REST:** permite a las organizaciones integrar cargas de recursos en sistemas de producción existentes o flujos de trabajo automatizados.

- **MCP del proveedor:** permite a los colaboradores que trabajan en entornos asistidos por IA cargar recursos a través de flujos de trabajo conversacionales admitidos.

Todos los métodos de carga proporcionan las mismas capacidades principales de ingesta de recursos.

## Capacidades clave {#key-capabilities-asset-sourcing-aem-assets}

- **Acceso seguro a colaboradores:** Los colaboradores externos pueden cargar recursos sin tener acceso a DAM, explorar repositorios o ver otros recursos.

- **Colección de metadatos configurable:** Los administradores seleccionan campos de metadatos del esquema de metadatos AEM Assets. El portal genera automáticamente el formulario de envío del colaborador en función de los campos seleccionados.

- **Ingesta automatizada de recursos:** Los recursos cargados se enrutan a una ubicación de entrada designada con metadatos configurados aplicados durante la ingesta.

- **Directivas de ingesta configurables:** Los administradores pueden definir reglas de ingesta para cada colaborador, incluidos los campos de metadatos opcionales y requeridos, los valores rellenados previamente, los identificadores por lotes, las convenciones de nomenclatura de recursos, las rutas de destino, las dimensiones de recursos mínimas y las notificaciones del administrador.

- **Incorporación de colaboradores escalables:** Configure varios colaboradores con diferentes destinos de carga, requisitos de metadatos y políticas de ingesta sin desarrollar aplicaciones de carga personalizadas.

## Casos de uso de ejemplo {#example-use-cases-asset-sourcing}

- **Recopilar recursos de agencias creativas:** Permitir que las agencias envíen recursos de campaña a través de un portal de carga dedicado sin conceder acceso al DAM de la organización.

- **Recibir envíos de fotografías:** Proporcionar a los fotógrafos una experiencia de carga sencilla que capture automáticamente los metadatos necesarios y almacene los recursos en la ubicación de admisión adecuada.

- **Integrar sistemas de producción externos:** Utilice la API de REST para enviar automáticamente recursos desde sistemas de producción o creación de contenido de terceros.

## Cuándo utilizar esta capacidad {#when-to-use-this-capability}

Utilice el portal de abastecimiento de Assets cuando necesite:

- Recopile recursos de fotógrafos, agencias y proveedores externos.
- Estandarizar la recopilación de metadatos durante la entrada de recursos.
- Envíos de recursos seguros sin proporcionar acceso a DAM.
- Automatice la ingesta de recursos en ubicaciones de entrada designadas.
- Admitir un gran número de colaboradores externos.

## Cuándo no utilizar esta capacidad {#when-not-to-use-this-capability}

El portal de abastecimiento de Assets no está diseñado para:

- Administración de recursos dentro de DAM después de la ingesta.
- Proporcionar a los colaboradores acceso para examinar, buscar o descargar recursos DAM.
- Flujos de trabajo de colaboración internos que requieren la funcionalidad completa de DAM.