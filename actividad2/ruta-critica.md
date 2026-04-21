# Ruta Crítica — FreelanceManager

**Proyecto:** Sistema de Gestión de Proyectos Freelance
**Autor:** Jesús David Castro Vanegas
**Curso:** Ingeniería de Sistemas — Universidad de Manizales
**Fecha:** Manizales, abril de 2026
**Metodología:** Scrum

---

## Contexto

Esta ruta crítica es una vista de **alto nivel** del proyecto FreelanceManager enmarcada en la metodología **Scrum**. A diferencia del PERT detallado de la Actividad 1 (62 actividades, 130.51 días), aquí se trabaja con los **módulos principales** del sistema y sus dependencias de desarrollo. El objetivo es identificar qué módulo bloquea a cuál, cuál es la cadena de desarrollo más larga, y cómo esas dependencias justifican la secuencia de Sprints.

En Scrum, la ruta crítica determina qué funcionalidades deben completarse (Done) en un Sprint para que el siguiente Sprint pueda comenzar. Las dependencias de datos del sistema mapean directamente en la secuencia de Sprints: el Sprint 2 no puede alcanzar su Sprint Goal si el Sprint 1 no está completo.

---

## Roles Scrum

| Rol | Responsable |
|---|---|
| **Product Owner** | Jesús David Castro Vanegas |
| **Scrum Master** | Jesús David Castro Vanegas |
| **Development Team** | Jesús David Castro Vanegas |

---

## Tabla de actividades, dependencias y Sprint

| # | Actividad | Duración estimada | Predecesoras | Sprint | ¿Crítica? |
|:---:|---|:---:|---|:---:|:---:|
| A1 | Planificación y levantamiento de requerimientos | 5 días | — | Pre-Sprint | ✅ |
| A2 | Diseño de arquitectura y modelo de base de datos | 7 días | A1 | Pre-Sprint | ✅ |
| A3 | Diseño UX/UI — wireframes y prototipo navegable | 8 días | A1 | Pre-Sprint | ❌ |
| A4 | Configuración de infraestructura y entorno de desarrollo | 4 días | A2 | Pre-Sprint | ✅ |
| A5 | Módulo de Autenticación (registro, login, recuperación) | 6 días | A4 | Sprint 1 | ✅ |
| A6 | Módulo de Clientes (CRUD completo) | 5 días | A5 | Sprint 1 | ✅ |
| A7 | Módulo de Proyectos (creación, estados, presupuesto) | 6 días | A6 | Sprint 2 | ✅ |
| A8 | Módulo de Tareas (prioridad, estado, fecha límite) | 5 días | A7 | Sprint 2 | ❌ |
| A9 | Módulo de Registro de Tiempo (time tracking manual) | 5 días | A7 | Sprint 2 | ✅ |
| A10 | Módulo de Facturación (generación y exportación PDF) | 6 días | A9 | Sprint 3 | ✅ |
| A11 | Módulo de Dashboard (métricas y panel de control) | 5 días | A8, A10 | Sprint 3 | ✅ |
| A12 | Integración entre módulos y pruebas de flujo completo | 5 días | A11 | Post-Sprint | ✅ |
| A13 | Pruebas y QA (funcionales, usabilidad, regresión) | 6 días | A12 | Post-Sprint | ✅ |
| A14 | Despliegue, documentación y entrega final | 4 días | A13 | Post-Sprint | ✅ |

**Duración total de la ruta crítica:** 69 días

---

## Sprint Goals y dependencias entre Sprints

| Sprint | Sprint Goal | Módulos que entrega | Prerrequisito para |
|---|---|---|---|
| **Pre-Sprint** | Arquitectura y entorno listos para desarrollar | Planificación, Arquitectura, Infraestructura, UX/UI | Sprint 1 no puede comenzar sin A4 Done |
| **Sprint 1** | El freelancer puede registrarse y gestionar clientes | Autenticación, Clientes | Sprint 2 no puede comenzar sin A6 Done |
| **Sprint 2** | El freelancer puede gestionar proyectos, tareas y tiempo | Proyectos, Tareas, Registro de Tiempo | Sprint 3 no puede comenzar sin A9 Done |
| **Sprint 3** | El freelancer puede facturar y ver su dashboard | Facturación, Dashboard, Administración | Post-Sprint no puede comenzar sin A11 Done |
| **Post-Sprint** | Sistema integrado, probado y desplegado | Integración, QA, Despliegue | Entrega final |

---

## Diagrama de secuencia

```
A1 (Planificación) — PRE-SPRINT
├── A2 (Arquitectura) ──── A4 (Infraestructura) ──── [SPRINT 1]
│                                                     A5 (Autenticación)
│                                                           │
│                                                     A6 (Clientes)
│                                                           │
│                                                     [SPRINT 2]
│                                                     A7 (Proyectos)
│                                                      ├──────────┐
│                                                  A8 (Tareas)  A9 (Tiempo)
│                                                      │               │
│                                                      │         [SPRINT 3]
│                                                      └──────┬──A10 (Facturación)
│                                                             │
│                                                        A11 (Dashboard)
│                                                             │
│                                                     [POST-SPRINT]
│                                                        A12 (Integración)
│                                                             │
│                                                        A13 (Pruebas QA)
│                                                             │
└── A3 (UX/UI) ──────────────────────────────────────── A14 (Despliegue)
```

**Ruta crítica (secuencia lineal dominante):**

```
A1 → A2 → A4 → A5 → A6 → A7 → A9 → A10 → A11 → A12 → A13 → A14
```

> **Nota sobre A8 (Tareas) y A9 (Tiempo):** Ambas dependen de A7 (Proyectos) y pueden desarrollarse en paralelo dentro del Sprint 2. La ruta más larga pasa por A9 → A10 porque la Facturación depende del Registro de Tiempo, no de las Tareas directamente.

> **Nota sobre A3 (UX/UI):** Se realiza en paralelo con A2 y A4 durante el Pre-Sprint. No es crítica porque termina antes de que los módulos de backend estén listos — el diseño guía el desarrollo pero no lo bloquea.

---

## Ruta crítica identificada

**Secuencia crítica:**
```
A1 → A2 → A4 → A5 → A6 → A7 → A9 → A10 → A11 → A12 → A13 → A14
```

**Duración total:** 5 + 7 + 4 + 6 + 5 + 6 + 5 + 6 + 5 + 5 + 6 + 4 = **69 días**

Cualquier retraso en cualquiera de estas 12 actividades retrasa la entrega final del proyecto. En términos Scrum: si un Sprint no alcanza su Sprint Goal, el siguiente Sprint no puede comenzar con todas sus dependencias satisfechas, lo que retrasa el Release.

Las actividades no críticas (A3 y A8) tienen holgura — pueden retrasarse sin afectar la fecha de entrega ni los Sprint Goals.

---

## Justificación del orden

### Por qué A1 (Planificación) va primero
Sin requerimientos definidos no se puede diseñar ni construir nada. Es el punto de entrada único del proyecto. En Scrum, esta actividad equivale a la creación inicial del Product Backlog — sin el backlog no hay Sprint Planning posible.

### Por qué A2 (Arquitectura) bloquea A4 (Infraestructura)
El modelo de base de datos y la arquitectura deben definirse antes de configurar el entorno. No tiene sentido levantar un servidor sin saber qué tablas y relaciones se van a usar.

### Por qué A3 (UX/UI) no es crítica
El diseño de interfaces puede hacerse en paralelo con la arquitectura. Los wireframes guían el desarrollo pero los módulos del backend no dependen del prototipo visual. En el contexto Scrum, el diseño UX/UI alimenta la Definición de Listo (Definition of Ready) de las historias, pero no bloquea el inicio de los Sprints.

### Por qué A5 (Autenticación) es el primer módulo de código — Sprint 1
Todos los módulos requieren un usuario autenticado. Sin login no hay sesión, sin sesión no hay contexto de usuario, y sin contexto no se pueden vincular clientes, proyectos ni registros de tiempo. Es la puerta de entrada al sistema y el bloqueador más crítico del Sprint 1.

### Por qué A6 (Clientes) cierra el Sprint 1
En el modelo de datos, un proyecto siempre pertenece a un cliente (`proyecto.cliente_id` es FK obligatoria). El Sprint 2 no puede construir la pantalla "Nuevo proyecto" si no existe la lista de clientes. El Sprint 1 debe terminar con Autenticación y Clientes Done.

### Por qué A7 (Proyectos) abre el Sprint 2
Las tareas pertenecen a proyectos (`tarea.proyecto_id`). Los registros de tiempo se vinculan a proyectos o tareas (`registro.proyecto_id`). Proyectos es el pivot del Sprint 2 — debe implementarse primero dentro de la iteración.

### Por qué A8 (Tareas) y A9 (Tiempo) pueden ir en paralelo dentro del Sprint 2
Ambas dependen solo de A7, no entre sí. Las tareas y los registros de tiempo son entidades independientes — un registro de tiempo puede vincularse directamente a un proyecto sin pasar por una tarea (`registro.tarea_id` es nullable). Desarrollarlas en paralelo es la decisión óptima dentro del Sprint 2.

### Por qué A9 (Tiempo) → A10 (Facturación) es la ruta y no A8 → A10
La factura se genera calculando `horas_registradas × tarifa_del_proyecto`. El módulo de Facturación depende directamente de los datos del Registro de Tiempo (A9). Las tareas (A8) no alimentan la factura. Por eso la ruta crítica pasa por A9, y A10 abre el Sprint 3.

### Por qué A11 (Dashboard) va al final de los módulos — Sprint 3
El dashboard agrega métricas de todos los módulos: proyectos activos (A7), tareas pendientes (A8), horas registradas (A9), facturación (A10). Construirlo antes sería construir un panel vacío. En Scrum, esto significa que el Sprint 3 debe terminar con Facturación Done antes de que el Dashboard pueda implementarse.

### Por qué A12 (Integración) y A13 (QA) van en el Post-Sprint
En Scrum, cada Sprint debe entregar un Incremento potencialmente entregable. La integración formal y el QA de regresión completo son actividades post-desarrollo que verifican que todos los Sprints funcionen como sistema unificado.

---

## Decisiones tomadas

### Decisión 1 — A8 (Tareas) y A9 (Tiempo) en paralelo dentro del Sprint 2

**Opción considerada:** Poner A8 antes de A9 en secuencia dentro del Sprint 2.

**Decisión tomada:** Paralelizar A8 y A9 porque son independientes en el modelo de datos. Un registro de tiempo puede vincularse directamente a un proyecto sin pasar por una tarea — `registro.tarea_id` es nullable. Forzar la secuencia habría alargado el Sprint 2 innecesariamente. En Scrum, esto se llama **paralelización dentro del Sprint**: el equipo puede trabajar simultáneamente en historias que no tienen dependencias entre sí.

### Decisión 2 — La ruta crítica pasa por A9 (Tiempo) y no por A8 (Tareas)

**Razonamiento:** Cuando A8 y A9 se desarrollan en paralelo a partir de A7, ambas convergen en A11 (Dashboard). Pero A10 (Facturación) solo depende de A9. Esto crea un camino A7 → A9 → A10 → A11 más largo que A7 → A8 → A11. En Scrum, esto implica que el **Sprint 3 depende del Sprint 2 completando A9**, no A8. Si A9 no está Done al final del Sprint 2, el Sprint Goal del Sprint 3 no puede alcanzarse.

---

## Resumen visual por módulo

| Módulo | Actividad | Duración | Sprint | Holgura | Posición en ruta |
|---|---|:---:|:---:|:---:|---|
| Planificación | A1 | 5 días | Pre-Sprint | 0 | Crítica — inicio |
| Arquitectura | A2 | 7 días | Pre-Sprint | 0 | Crítica |
| UX/UI | A3 | 8 días | Pre-Sprint | ~8 días | No crítica |
| Infraestructura | A4 | 4 días | Pre-Sprint | 0 | Crítica |
| Autenticación | A5 | 6 días | Sprint 1 | 0 | Crítica — primer módulo |
| Clientes | A6 | 5 días | Sprint 1 | 0 | Crítica |
| Proyectos | A7 | 6 días | Sprint 2 | 0 | Crítica — núcleo |
| Tareas | A8 | 5 días | Sprint 2 | ~5 días | No crítica |
| Registro de Tiempo | A9 | 5 días | Sprint 2 | 0 | Crítica |
| Facturación | A10 | 6 días | Sprint 3 | 0 | Crítica |
| Dashboard | A11 | 5 días | Sprint 3 | 0 | Crítica |
| Integración | A12 | 5 días | Post-Sprint | 0 | Crítica |
| Pruebas QA | A13 | 6 días | Post-Sprint | 0 | Crítica |
| Despliegue | A14 | 4 días | Post-Sprint | 0 | Crítica — cierre |

**Actividades críticas:** 12 de 14
**Actividades con holgura:** A3 (UX/UI), A8 (Tareas)
**Duración mínima del proyecto:** 69 días
**Sprints de desarrollo:** 3 sprints × 2 semanas = 6 semanas
