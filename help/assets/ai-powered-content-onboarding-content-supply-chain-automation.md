---
title: Integración de contenido con tecnología de IA y automatización de supply chain de contenido
description: Obtenga información sobre cómo automatizar migraciones de contenido únicas y la automatización de supply chain de contenido entre Adobe y repositorios de terceros admitidos.
role: Admin
hide: true
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
source-git-commit: 3985d61b59b610c63f94407a9fdc4860390d7e42
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---


# Integración de contenido con tecnología de IA y automatización de supply chain de contenido {#ai-powered-content-onboarding-content-supply-chain-automation}

Las organizaciones suelen almacenar recursos digitales y metadatos en varios repositorios, como sistemas de administración de recursos digitales (DAM), servicios de almacenamiento en la nube y plataformas de contenido. La migración de contenido a un sistema nuevo o la sincronización de varios repositorios suelen requerir un esfuerzo manual o integraciones personalizadas que pueden ser difíciles de crear y mantener.

Esta capacidad le ayuda a automatizar migraciones de contenido únicas y a realizar sincronizaciones recurrentes entre repositorios admitidos. Un agente con tecnología de IA le guía a través de la configuración de transferencias de contenido, proponiendo conexiones de repositorio, asignaciones de metadatos y configuraciones de transferencia, reduciendo el esfuerzo necesario para mover y sincronizar contenido entre sistemas.

## Ventajas {#benefits-ai-powered-content-onboarding-content-supply-chain-automation}

La automatización de la incorporación y sincronización de contenido ofrece las siguientes ventajas:

- Agilice la incorporación al reducir el tiempo necesario para migrar los recursos y metadatos existentes a un nuevo repositorio.
- Simplifique la sincronización recurrente automatizando las transferencias de contenido programado entre sistemas de registro.
- Reduzca la sobrecarga de mantenimiento reemplazando las integraciones personalizadas con conexiones configurables.
- Compatibilidad con transferencias de contenido entre Adobe y repositorios de terceros.
- Valide la configuración de transferencia antes de mover contenido mediante ejecuciones en seco.

## ¿Cómo funcionan las transferencias de contenido? {#how-content-transfer-work}

El agente con tecnología de IA ayuda a configurar una transferencia de contenido entre un repositorio de origen y un repositorio de destino.

Durante la configuración, el agente:

- Recopila la información necesaria para conectarse a cada repositorio.
- Propone asignaciones entre campos de metadatos y taxonomías.
- Permite revisar y validar las asignaciones propuestas antes de transferir contenido.
- Admite ejecuciones en seco para poder verificar la configuración antes de mover el contenido de producción.
- Configura programaciones de transferencia únicas o recurrentes.

Cada transferencia configurada se denomina **conexión**. Una conexión usa **puertas de enlace** para comunicarse con los repositorios de origen y destino. Cada ejecución de una conexión se denomina **run**.

Las ejecuciones tienen estado. Rastrean los recursos y metadatos transferidos anteriormente para que las ejecuciones posteriores transfieran solo contenido nuevo o modificado en lugar de volver a procesar todo el repositorio.

## Capacidades clave {#key-capabilities-ai-powered-content-onboarding-content-supply-chain-automation}

- **Asignación de identidad**: mantiene la relación entre los recursos de los repositorios de origen y destino en varias ejecuciones.

- **Detección de cambios**: transfiere solo los recursos y metadatos que han cambiado desde la ejecución anterior, lo que reduce el procesamiento innecesario y mejora la eficacia.

- **Asignación de metadatos**: Asigna campos de metadatos y taxonomías entre repositorios como parte del proceso de transferencia de contenido.

- **Ejecución en seco**: valida asignaciones y configuración de transferencia antes de mover contenido al repositorio de destino.

- **Sincronización programada**: ejecuta las transferencias en una programación recurrente, como por hora, diaria o semanal.

- **Transformaciones personalizadas**: admite lógica de transformación adicional cuando es necesario, incluido JavaScript, expresiones regulares, enlaces web y hash de contenido.

## Repositorios admitidos {#supported-repositories}

El contenido se puede transferir entre Adobe y repositorios de terceros a través de puertas de enlace de origen y destino admitidas.

Algunos ejemplos de repositorios admitidos son:

- Adobe Experience Manager Assets
- Adobe Content Platform
- Adobe Commerce
- Amazon S3
- Azure Blob Storage
- Box
- Dropbox
- Google Drive
- OneDrive
- WordPress
- Workfront
- Servidores FTP y SFTP
- Recursos compartidos de archivos SMB

Se han planificado repositorios adicionales para futuras versiones.

## Casos de uso de ejemplo {#example-use-cases}

### Migración de contenido a un nuevo repositorio

Configure una migración única desde un repositorio de DAM heredado o de almacenamiento en la nube a un nuevo sistema de registro. Revise las asignaciones de metadatos con una ejecución seca antes de transferir contenido de producción.

### Sincronización de repositorios

Mantenga el contenido sincronizado entre el almacenamiento en la nube y un DAM configurando una transferencia recurrente que procese solo los recursos recién añadidos o modificados.

### Optimice su supply chain de contenido

Reduzca el movimiento manual del contenido automatizando las transferencias entre repositorios utilizados en todo el ciclo de vida del contenido de su organización.

## Cuándo utilizar esta capacidad {#when-to-use-ai-powered-content-onboarding-content-supply-chain-automation}

Esta capacidad es adecuada para lo siguiente:

- Migraciones de contenido únicas.
- Incorporación de nuevos sistemas de registro.
- Sincronización recurrente entre repositorios.
- Asignación de metadatos y taxonomía durante las transferencias de contenido.
- Automatización del movimiento de contenido en varios repositorios.

## Cuándo no utilizar esta capacidad {#when-not-to-use-ai-powered-content-onboarding-content-supply-chain-automation}

Esta capacidad no está pensada para:

- Flujo de trabajo general o automatización de procesos empresariales.
- Canalizaciones ETL de datos de clientes o Analytics.
- Propagación impulsada por eventos en tiempo real.
- Flujo continuo de bytes entre repositorios.




