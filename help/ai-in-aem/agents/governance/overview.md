---
title: Introducción al agente de gobernanza
description: Descubra cómo AEM Governance Agent protege la integridad de la marca y el cumplimiento de las normas en AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 9b26cd1f30ad6fa23e28c9f36fe48091e069962e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Introducción al agente de gobernanza {#governance-agent}

**Governance Agent** es una solución diseñada para salvaguardar la integridad y el cumplimiento de la marca en todo Adobe Experience Manager. Aplica políticas de seguridad, normativas y de marca para garantizar que cada interacción y activación se adhiera a los estándares establecidos. El agente de administración está totalmente integrado en el asistente de IA y está diseñado para funcionar sin problemas en entornos empresariales al aprovechar las herramientas **A2A (Agente a Agente)** y **MCP (Protocolo de control de modelos)**. Estas integraciones permiten al agente conectarse con orquestadores de IA avanzados como ChatGPT, Claude y otros sistemas de IA externos, lo que garantiza una inteligencia flexible y escalable en todas las plataformas.

Las funciones clave incluyen:

* **Gobernanza de la marca:** Mantenga la coherencia de la marca y reduzca la revisión manual automatizando las comprobaciones de marca en el contenido y los recursos
* **Permisos y Digital Rights Management (DRM):** Garantiza una colaboración segura y compatible mediante el control de permisos y derechos de uso en recursos digitales.

Al combinar estas funciones, el agente de gobernanza reduce el riesgo y permite una entrega rápida, segura y a escala de la marca.

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Aptitudes en AEM Governance Agent {#skills-in-aem-governance-agent}

### Gobernanza de marca {#brand-governance}

El agente de gobernanza puede validar el contenido con respecto a las directrices de marca para garantizar la coherencia en todas las experiencias digitales. Utiliza reglas de marca preingeridas, como tono, reclamaciones, uso del logotipo, tipografía e imágenes. Funciona en tiempo real dentro del modo de chat, editores y por lotes en Experience Hub, lo que lo hace ideal para contenido generado por IA, migraciones de sitios y creación de sitios breve.

![Información general sobre Brand Governance](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**Ejemplos de mensajes:**

* *¿Esta página está alineada con mi marca?`https://www.website/en.html`*
* *¿Sigue este(a) `https://www.website/en.html` las directrices de mensajería de marca?*
* *Comprobar si `https://www.website/homepage` sigue las directrices de marca*
* *Mostrarme las directrices de marca*

### Permiso y Digital Rights Management {#permission-and-digital-rights-management}

#### Administración de permisos en Content Hub {#permission-management-in-content-hub}

En Content Hub, el agente de gobernanza garantiza que solo las personas adecuadas accedan a los recursos adecuados en el momento adecuado. Al aplicar controles granulares basados en atributos y derechos de uso, protege el contenido confidencial y, al mismo tiempo, permite la colaboración segura. Esto significa menos riesgo de conformidad, una integridad de marca más sólida y flujos de trabajo más rápidos, los equipos pueden compartir y reutilizar recursos con seguridad sin tener que preocuparse por el acceso no autorizado o el uso indebido. Este equilibrio entre seguridad y flexibilidad se traduce en una mayor eficiencia operativa y confianza en toda la organización.

![Información general sobre administración de permisos](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**Ejemplos de mensajes:**

* *Mostrar todas las reglas ABAC de Content Hub existentes.*
* *Cree una regla que conceda al grupo &quot;Marketing&quot; acceso a todos los recursos.*
* *Dar acceso al grupo de ventas a recursos donde marketing:segment es igual que EMEA.*
* *Eliminar todas las reglas que dan acceso a la agencia externa*
* *¿Qué es ABAC en Content Hub y qué puede ayudarme a hacer?*

#### Assets Digital Rights Management {#assets-digital-rights-management}

Con el agente, puede administrar los derechos digitales de Assets en todo el ecosistema de contenido. Controla los permisos y derechos de uso a nivel granular, lo que garantiza que solo se acceda a los recursos y se utilicen dentro de los límites de conformidad definidos. Esto ofrece tranquilidad, protección de la propiedad intelectual, reducción del riesgo regulatorio y mantenimiento de la integridad de la marca. Al automatizar la aplicación de los derechos, los equipos pueden colaborar de forma segura y segura, lo que acelera la distribución de contenido sin poner en riesgo la seguridad ni el cumplimiento normativo.

![Información general de administración de DRM](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**Ejemplos de mensajes:**

* *¿Alguno de mis recursos caducará pronto?*
* *Encuéntrame todos los activos de la bicicleta que caducaron el mes pasado.*
* *¿Qué recursos caducaron recientemente?*
* *Encontrarme recursos sin fecha de caducidad*
* *Mostrarme todos los recursos en /content/dam/products que están a punto de caducar en los próximos 14 días*

