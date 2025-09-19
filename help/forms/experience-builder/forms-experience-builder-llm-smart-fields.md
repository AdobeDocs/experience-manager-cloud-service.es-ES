---
title: Campos inteligentes mejorados con LLM en Forms Experience Builder
description: Aprenda a crear campos de formulario inteligentes con opciones rellenadas previamente mediante la base de conocimiento de IA para datos geográficos, clasificaciones comerciales y estándares del sector.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---


# Campos inteligentes mejorados con LLM en Forms Experience Builder {#llm-enhanced-smart-fields}

Forms Experience Builder aprovecha la potencia de los modelos de lenguaje grande (LLM) para crear campos de formulario inteligentes con opciones rellenadas previamente que se basan en bases de conocimiento completas. Esta capacidad elimina la necesidad de buscar e introducir manualmente grandes conjuntos de datos, lo que mejora considerablemente la precisión y la eficacia de la creación de formularios.

## ¿Qué son los campos inteligentes mejorados con LLM? {#what-are-llm-smart-fields}

Los campos inteligentes mejorados con LLM son campos de formulario que se rellenan automáticamente con datos completos y precisos mediante la base de conocimiento integrada de la IA. En lugar de crear manualmente listas desplegables o conjuntos de opciones, puede solicitar campos que requieran conjuntos de datos extensos y la API generará automáticamente las opciones adecuadas.

**Principales ventajas:**

* **Conjuntos de datos completos**: acceso a información extensa y actualizada en varios dominios
* **Población automática**: no es necesario buscar ni introducir datos manualmente
* **Formatos estandarizados**: Utiliza códigos estándar del sector, clasificaciones y convenciones de nomenclatura
* **Opciones según el contexto**: los campos se pueden adaptar según otras selecciones de formularios
* **Ahorro de tiempo**: reduce el tiempo de creación de formularios de horas a minutos

## Cuándo utilizar campos inteligentes mejorados con LLM {#when-to-use-smart-fields}

Utilice campos inteligentes mejorados con LLM cuando necesite:

* **Conjuntos de datos completos**: campos que requieren información extensa y estandarizada
* **Estándares del sector**: clasificaciones, códigos o datos reglamentarios
* **Información geográfica**: ubicaciones, regiones o divisiones administrativas
* **Datos profesionales** - Títulos de trabajo, certificaciones o clasificaciones del sector
* **Estándares técnicos**: formatos de archivo, protocolos o especificaciones del sistema

## Campos geográficos y de ubicación {#geographic-location-fields}

Cree campos basados en la ubicación con datos geográficos completos e información administrativa.

### Aeropuertos y transporte

**Aeropuertos internacionales con códigos IATA:**

    Agregue un menú desplegable para los aeropuertos de salida con todos los aeropuertos internacionales principales
    Agregue un campo de aeropuerto de llegada con códigos IATA y nombres completos
    Cree un campo para el aeropuerto más cercano a la ubicación del usuario
    Agregue una selección de estaciones de tren para las ciudades europeas

**Mensajes de ejemplo:**

* &quot;Agregue un campo de aeropuerto de salida con todos los principales aeropuertos del mundo, incluidos los códigos IATA y los nombres de las ciudades&quot;
* &quot;Crear un menú desplegable de aeropuertos de llegada con aeropuertos internacionales organizados por continente&quot;
* &quot;Incluir una selección de estaciones de tren para las principales ciudades europeas con códigos de estación&quot;

### Regiones administrativas

**Países, estados y provincias:**

    Agregar una lista completa de estados de EE. UU. con abreviaturas
    Crear un menú desplegable de países con códigos ISO y nombres completos
    Agregar un campo para las principales ciudades del mundo con husos horarios
    Incluir un menú desplegable de provincias y territorios canadienses
    Agregar un campo para los condados y áreas postales del Reino Unido

**Mensajes de ejemplo:**

* &quot;Crear un campo de selección de país con códigos de país ISO y nombres completos&quot;
* &quot;Agregue un menú desplegable de estados de EE. UU. con abreviaciones de estado y nombres completos&quot;
* &quot;Incluir un campo de provincia de Canadá con territorios y códigos postales&quot;
* &quot;Crear un campo de ciudades del mundo con las principales áreas metropolitanas y zonas horarias&quot;

## Datos empresariales e industriales {#business-industry-data}

Aproveche las clasificaciones comerciales completas y los datos profesionales para los formularios corporativos.

### Clasificaciones de empresa

**Tipos de entidades empresariales y del sector:**

    Agregue un campo para la clasificación del sector con códigos NAICS
    Cree un menú desplegable de tipos de entidades comerciales (LLC, Corporation, Partnership, etc.)
    Agregar un campo para categorías de tamaño de compañía (inicio, PYMES, empresa)
    Incluir la selección de departamentos para organizaciones grandes
    Agregar un campo para tipos de servicios profesionales

**Mensajes de ejemplo:**

* &quot;Crear un campo completo de la industria utilizando la clasificación estándar de NAICS con subcategorías de tecnología&quot;
* &quot;Agregar un menú desplegable de tipo de entidad empresarial con estructuras legales y descripciones&quot;
* &quot;Incluir un campo de tamaño de empresa con intervalos de recuento de empleados y tramos de ingresos&quot;

### Clasificaciones profesionales

**Títulos y certificaciones de trabajo:**

    Agregue un campo para los puestos con funciones comunes en el sector
    Cree un menú desplegable de certificaciones profesionales por campo
    Incluya niveles de educación con tipos de títulos
    Agregue un campo para rangos de años de experiencia
    Cree una selección de lenguajes y marcos de trabajo de programación

**Mensajes de ejemplo:**

* &quot;Incluya un menú desplegable de certificación profesional que se adapte en función del campo de trabajo seleccionado&quot;
* &quot;Cree un campo de cargo con funciones comunes en tecnología, atención médica y finanzas&quot;
* &quot;Agregar un campo de nivel educativo con tipos de grados y especializaciones&quot;

## Normas y datos reglamentarios {#standards-regulatory-data}

Acceda a códigos, clasificaciones e información reglamentaria estandarizados para formularios centrados en el cumplimiento.

### Financiero y legal

**Información de moneda, impuestos y pagos:**

    Agregue un campo para códigos de moneda con símbolos y tipos de cambio
    Cree un menú desplegable de tipos de identificación fiscal por país
    Incluya un campo para tipos de documentos legales
    Agregue opciones de métodos de pago con características de seguridad
    Cree una selección para instituciones bancarias por país

**Mensajes de ejemplo:**

* &quot;Crear un campo de selección de moneda con códigos ISO, símbolos y tipos de cambio principales&quot;
* &quot;Agregar un campo de tipo de identificación fiscal con formatos de identificación fiscal específicos del país&quot;
* &quot;Incluir un menú desplegable de métodos de pago con funciones de seguridad y tiempos de procesamiento&quot;

### Normas técnicas

**Formatos de archivo y protocolos:**

    Agregar un menú desplegable de tipos de formato de archivo con extensiones
    Incluir opciones de protocolo de red
    Agregar un campo para tipos y versiones de base de datos
    Crear una selección para métodos de autenticación de API

**Mensajes de ejemplo:**

* &quot;Cree un menú desplegable de formato de archivo con extensiones comunes y tipos MIME&quot;
* &quot;Agregar un campo de selección de base de datos con versiones y comparaciones de características&quot;
* &quot;Incluir un campo de método de autenticación de API con niveles de seguridad&quot;

## Sanidad y medicina {#healthcare-medical-fields}

Datos médicos y sanitarios especializados para formularios específicos de la industria.

### Clasificaciones médicas

**Datos médicos y especialidades:**

    Agregue un campo para especialidades médicas
    Cree un menú desplegable de medicamentos comunes con nombres genéricos
    Incluya un campo para los tipos de proveedores de seguros
    Agregue una selección para las relaciones de contacto de emergencia médica
    Cree un campo para las restricciones dietéticas y las alergias

**Mensajes de ejemplo:**

* &quot;Crear un campo de especialidad médica con subespecialidades y certificaciones de la junta&quot;
* &quot;Agregue un campo de medicación con nombres genéricos, marcas y formas farmacéuticas&quot;
* &quot;Incluir un campo de proveedor de seguros con los principales operadores y tipos de plan&quot;

## Inteligencia de tiempo y calendario {#time-calendar-intelligence}

Campos de fecha y hora inteligentes con inteligencia de contexto empresarial y programación.

### Campos de fecha y hora

**Horario de trabajo y programación:**

    Agregue un campo para el horario laboral con administración de husos horarios
    Cree un menú desplegable de días festivos por país
    Incluya opciones de temporada con intervalos de fechas
    Agregue un campo para la reserva de salas de conferencias con disponibilidad
    Cree una selección para patrones de reuniones recurrentes

**Mensajes de ejemplo:**

* &quot;Crear un campo de horario laboral con zonas horarias y excepciones de días festivos&quot;
* &quot;Agregar una selección de días festivos con celebraciones específicas por país&quot;
* &quot;Incluir un campo de patrón de reunión recurrente con opciones de frecuencia&quot;

## Categorías de productos y servicios {#product-service-categories}

Campos de comercio electrónico y orientados a servicios con una categorización completa.

### Clasificaciones de comercio electrónico

**Datos de productos y servicios:**

    Agregue un campo para las categorías de productos con subcategorías
    Cree un menú desplegable de métodos de envío con estimaciones de entrega
    Incluya un campo para opciones de directivas de devolución
    Agregue una selección para los niveles de prioridad de los clientes
    Cree un campo para los ciclos de facturación de suscripción

**Mensajes de ejemplo:**

* &quot;Crear un campo de categoría de producto con subcategorías de comercio electrónico y patrones de SKU&quot;
* &quot;Añade un menú desplegable de métodos de envío con plazos de entrega y estimaciones de costes&quot;
* &quot;Incluir un campo de ciclo de facturación de suscripción con frecuencias de pago&quot;

## Prácticas recomendadas para campos inteligentes mejorados con LLM {#best-practices-smart-fields}

### Sea específico en sus solicitudes

**Buenos ejemplos:**

* &quot;Añada un menú desplegable de país con códigos ISO, nombres completos e información de moneda&quot;
* &quot;Crear un campo de especialidad médica con certificaciones y subespecialidades de la junta directiva&quot;
* &quot;Incluir un campo de lenguaje de programación con marcos y niveles de habilidad&quot;

**Evitar solicitudes vagas:**

* &quot;Agregar un campo de país&quot;
* &quot;Menú desplegable Crear un puesto de trabajo&quot;
* &quot;Incluir un campo de categoría de producto&quot;

### Combinación con lógica condicional

Los campos inteligentes funcionan excepcionalmente bien con reglas condicionales:

    Crea un campo de certificación profesional que muestre opciones relevantes basadas en la industria seleccionada
    Agrega un campo de ciudad que filtre según el país seleccionado
    Incluye un campo universitario que se adapte según el campo de estudio elegido

### Validación y personalización

Aunque los campos mejorados con LLM proporcionan datos completos, siempre:

* **Revise las opciones generadas** para comprobar su precisión y relevancia
* **Agregar opciones personalizadas** específicas a su organización
* **Quitar opciones irrelevantes** para optimizar la experiencia del usuario
* **Realizar pruebas con usuarios reales** para asegurar la usabilidad

## Técnicas avanzadas de campo inteligente {#advanced-smart-field-techniques}

### Campos según el contexto

Cree campos que se adapten en función de otras selecciones de formulario:

    Agregue un campo de selección de universidad con las principales instituciones organizadas por país y rango
    Cree un menú desplegable de certificación profesional que muestre opciones relevantes basadas en el puesto
    Incluya un campo de ciudad que filtre según el país y la región seleccionados

### Clasificaciones de varios niveles

Crear estructuras de datos jerárquicas:

    Crear un campo de categoría de producto con categorías principales, subcategorías y tipos de producto
    Agregar un campo geográfico con los niveles de país, estado/provincia y ciudad
    Incluir un campo de evaluación de habilidades con categorías, subcategorías y niveles de competencia

### Integración con datos externos

Combine el conocimiento de LLM con los datos de su organización:

    Agregue un campo de departamento que incluya departamentos corporativos estándar y divisiones específicas de su organización
    Cree un campo de producto que combine categorías estándar del sector con su catálogo de productos
    Incluya un campo de ubicación que combine datos geográficos con las ubicaciones de su oficina

## Solución de problemas de campos inteligentes {#troubleshooting-smart-fields}

### Problemas y soluciones comunes

**Problema: Demasiadas opciones generadas**

* **Solución**: Sea más específico en su solicitud o agregue criterios de filtrado
* **Ejemplo**: En lugar de &quot;todos los países&quot;, solicite &quot;los principales países socios comerciales&quot;

**Problema: faltan opciones específicas**

* **Solución**: agregue opciones personalizadas o perfeccione el mensaje
* **Ejemplo**: &quot;Incluir los países principales más [sus países específicos]&quot;

**Problema: Información obsoleta**

* **Solución**: solicite datos actuales o especifique intervalos de fechas
* **Ejemplo**: &quot;Agregar festivos actuales para 2024&quot;

### Optimización de rendimiento

* **Opciones de límite**: utilice filtros para reducir el número de opciones generadas
* **Divulgación progresiva**: primero muestre las opciones básicas y luego permita la expansión
* **Almacenamiento en caché**: considere la posibilidad de almacenar en caché los datos de campos inteligentes usados frecuentemente

## Artículos relacionados

* [Introducción a Forms Experience Builder](forms-experience-builder-getting-started.md)
* [Creación de formularios con tecnología de IA](forms-experience-builder-prompt-examples-library.md)
* [Creación de reglas y lógica empresarial](forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)
* [Envío e integración de formularios](form-submission-integration.md)

