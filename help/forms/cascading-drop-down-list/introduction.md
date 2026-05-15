---
title: Lista desplegable en cascada
description: Utilice expresiones de formularios adaptables para agregar validación automática, cálculo y activar o desactivar la visibilidad de una sección.
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: cc3cd74ad87f4213a200f36745ab3d335edca02d
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 100%

---

# Descripción del caso de uso

Al crear formularios o aplicaciones, a menudo resulta útil guiar a los usuarios a través de la selección de ubicaciones de forma estructurada. Una lista desplegable en cascada facilita la tarea: primero, el usuario selecciona un país, que filtra la lista de estados o provincias disponibles, y luego realiza una selección final de ciudades según el estado. Este enfoque no solo mantiene los formularios más limpios, sino que también evita combinaciones no válidas (como elegir una ciudad que no existe en un estado elegido).

Se requieren los siguientes pasos para realizar este caso de uso

- Crear integración de API
- Crear un formulario con campos para capturar el país, el estado o la ciudad
- Crear una regla para rellenar las listas desplegables mediante la integración de la API