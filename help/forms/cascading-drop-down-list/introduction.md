---
title: Lista desplegable en cascada
description: Utilice expresiones de formularios adaptables para agregar validación automática, cálculo y activar o desactivar la visibilidad de una sección.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 15%

---

# Descripción del caso de uso

Al crear formularios o aplicaciones, a menudo resulta útil guiar a los usuarios a través de la selección de ubicaciones de forma estructurada. Una lista desplegable en cascada lo hace simple y fácil de usar: el usuario primero selecciona un país, que filtra la lista de estados/provincias disponibles, y luego una elección final de ciudades según el estado. Este enfoque no solo mantiene los formularios más limpios, sino que también evita combinaciones no válidas (como elegir una ciudad que no existe en un estado elegido).

Se requieren los siguientes pasos para realizar este caso de uso

- Crear integración de API
- Cree un formulario con campos para capturar el país, el estado o la ciudad
- Cree una regla para rellenar las listas desplegables mediante la integración de la API