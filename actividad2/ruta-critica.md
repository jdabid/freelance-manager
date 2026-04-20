# Ruta Crítica — FreelanceManager

**Proyecto:** Sistema de Gestión de Proyectos Freelance
**Autor:** Jesús David Castro Vanegas
**Curso:** Ingeniería del Software — Universidad de Manizales
**Fecha:** Manizales, abril de 2026

---

## Contexto

Esta ruta crítica es una vista de **alto nivel** del proyecto FreelanceManager. A diferencia del PERT detallado de la Actividad 1 (62 actividades, 130.51 días), aquí se trabaja con los **módulos principales** del sistema y sus dependencias de desarrollo. El objetivo es identificar qué módulo bloquea a cuál y cuál es la cadena de desarrollo más larga.

---

## Tabla de actividades y dependencias

| # | Actividad | Duración estimada | Predecesoras | ¿Crítica? |
|:---:|---|:---:|---|:---:|
| A1 | Planificación y levantamiento de requerimientos | 5 días | — | ✅ |
| A2 | Diseño de arquitectura y modelo de base de datos | 7 días | A1 | ✅ |
| A3 | Diseño UX/UI — wireframes y prototipo navegable | 8 días | A1 | ❌ |
| A4 | Configuración de infraestructura y entorno de desarrollo | 4 días | A2 | ✅ |
| A5 | Módulo de Autenticación (registro, login, recuperación) | 6 días | A4 | ✅ |
| A6 | Módulo de Clientes (CRUD completo) | 5 días | A5 | ✅ |
| A7 | Módulo de Proyectos (creación, estados, presupuesto) | 6 días | A6 | ✅ |
| A8 | Módulo de Tareas (prioridad, estado, fecha límite) | 5 días | A7 | ✅ |
| A9 | Módulo de Registro de Tiempo (time tracking manual) | 5 días | A7 | ✅ |
| A10 | Módulo de Facturación (generación y exportación PDF) | 6 días | A9 | ✅ |
| A11 | Módulo de Dashboard (métricas y panel de control) | 5 días | A8, A10 | ✅ |
| A12 | Integración entre módulos y pruebas de flujo completo | 5 días | A11 | ✅ |
| A13 | Pruebas y QA (funcionales, usabilidad, regresión) | 6 días | A12 | ✅ |
| A14 | Despliegue, documentación y entrega final | 4 días | A13 | ✅ |

**Duración total de la ruta crítica:** 69 días

---

## Diagrama de secuencia

```
A1 (Planificación)
├── A2 (Arquitectura) ──── A4 (Infraestructura) ──── A5 (Autenticación)
│                                                           │
│                                                     A6 (Clientes)
│                                                           │
│                                                     A7 (Proyectos)
│                                                      ├──────────┐
│                                                   A8 (Tareas)  A9 (Tiempo)
│                                                      │               │
│                                                      └──────┬────────┘
│                                                         A10 (Facturación)
│                                                              │
│                                                         A11 (Dashboard)
│                                                              │
│                                                         A12 (Integración)
│                                                              │
│                                                         A13 (Pruebas QA)
│                                                              │
└── A3 (UX/UI) ─────────────────────────────────────────A14 (Despliegue)
```

**Ruta crítica (secuencia lineal dominante):**

```
A1 → A2 → A4 → A5 → A6 → A7 → A9 → A10 → A11 → A12 → A13 → A14
```

> **Nota sobre A8 (Tareas) y A9 (Tiempo):** Ambas dependen de A7 (Proyectos) y pueden desarrollarse en paralelo. La ruta más larga pasa por A9 → A10 porque la Facturación depende del Registro de Tiempo, no de las Tareas directamente.

> **Nota sobre A3 (UX/UI):** Se realiza en paralelo con A2 y A4. No es crítica porque termina antes de que los módulos de backend estén listos — el diseño guía el desarrollo pero no lo bloquea.

---

## Ruta crítica identificada

**Secuencia crítica:**
```
A1 → A2 → A4 → A5 → A6 → A7 → A9 → A10 → A11 → A12 → A13 → A14
```

**Duración total:** 5 + 7 + 4 + 6 + 5 + 6 + 5 + 6 + 5 + 5 + 6 + 4 = **69 días**

Cualquier retraso en cualquiera de estas 12 actividades retrasa la entrega final del proyecto. Las actividades no críticas (A3 y A8) tienen holgura y pueden retrasarse sin afectar la fecha de entrega.

---

## Justificación del orden

### Por qué A1 (Planificación) va primero
Sin requerimientos definidos no se puede diseñar ni construir nada. Es el punto de entrada único de todo el proyecto: establece los módulos, el alcance, los usuarios y las restricciones técnicas.

### Por qué A2 (Arquitectura) bloquea A4 (Infraestructura)
El modelo de base de datos y la arquitectura de la aplicación deben definirse antes de configurar el entorno. No tiene sentido levantar un servidor o elegir un ORM sin saber qué tablas y relaciones se van a usar.

### Por qué A3 (UX/UI) no es crítica
El diseño de interfaces puede hacerse en paralelo con la arquitectura. Los wireframes guían el desarrollo pero los módulos del backend no dependen del prototipo visual — pueden construirse con la lógica de datos y conectar la UI después.

### Por qué A5 (Autenticación) es el primer módulo de código
Todos los módulos del sistema requieren un usuario autenticado para operar. Sin login no hay sesión, sin sesión no hay contexto de usuario, y sin contexto de usuario no se pueden vincular clientes, proyectos ni registros de tiempo a nadie. Es la puerta de entrada al sistema.

### Por qué A6 (Clientes) va antes que A7 (Proyectos)
En el modelo de datos de FreelanceManager, un proyecto siempre pertenece a un cliente (`proyecto.cliente_id` es una FK obligatoria). No se puede construir la pantalla de "nuevo proyecto" sin que exista la lista de clientes para seleccionar.

### Por qué A7 (Proyectos) va antes que A8 (Tareas) y A9 (Tiempo)
Las tareas pertenecen a proyectos (`tarea.proyecto_id`). Los registros de tiempo se vinculan a proyectos o tareas (`registro.proyecto_id`). Sin un proyecto activo en la base de datos, ambas funcionalidades no tienen contexto donde operar.

### Por qué A8 (Tareas) y A9 (Tiempo) pueden ir en paralelo
Ambas dependen solo de A7 (Proyectos), no entre sí. Las tareas y los registros de tiempo son entidades independientes — un registro de tiempo puede vincularse directamente a un proyecto sin pasar por una tarea. Se desarrollan en paralelo para ganar tiempo, pero la ruta crítica toma el camino más largo: A9 → A10.

### Por qué A9 (Tiempo) → A10 (Facturación) es la ruta y no A8 → A10
La factura se genera calculando `horas_registradas × tarifa_del_proyecto`. El módulo de Facturación depende directamente de los datos del Registro de Tiempo (A9). Las tareas (A8) no alimentan la factura — solo muestran el avance. Por eso la ruta crítica pasa por A9, no por A8.

### Por qué A11 (Dashboard) va al final de los módulos
El dashboard agrega métricas de todos los módulos anteriores: proyectos activos (A7), tareas pendientes (A8), horas registradas (A9), facturación (A10). Construirlo antes sería construir un panel vacío sin datos reales que mostrar.

### Por qué A12 (Integración) va antes que A13 (Pruebas)
La integración verifica que los módulos funcionen juntos como sistema completo — que el flujo cliente → proyecto → tarea → tiempo → factura sea coherente de extremo a extremo. Solo después de validar ese flujo tiene sentido hacer pruebas formales de QA.

---

## Decisiones tomadas

### Decisión 1 — A8 (Tareas) y A9 (Tiempo) en paralelo, no en secuencia

**Opción considerada:** Poner A8 antes de A9 porque intuitivamente se crean tareas antes de registrar tiempo.

**Decisión tomada:** Paralelizar A8 y A9 porque son independientes en el modelo de datos. Un registro de tiempo puede vincularse directamente a un proyecto sin pasar por una tarea — es un campo opcional (`registro.tarea_id` es nullable). Forzar la secuencia habría alargado el cronograma 5 días innecesariamente.

### Decisión 2 — La ruta crítica pasa por A9 (Tiempo) y no por A8 (Tareas)

**Razonamiento:** Cuando A8 y A9 se desarrollan en paralelo a partir de A7, ambas convergen en A11 (Dashboard). Pero A10 (Facturación) solo depende de A9 — las tareas no alimentan la factura. Esto crea un camino A7 → A9 → A10 → A11 que es más largo que A7 → A8 → A11. La ruta crítica elige siempre el camino más largo, por lo tanto pasa por A9.

---

## Resumen visual por módulo

| Módulo | Actividad | Duración | Holgura | Posición en ruta |
|---|---|:---:|:---:|---|
| Planificación | A1 | 5 días | 0 | Crítica — inicio |
| Arquitectura | A2 | 7 días | 0 | Crítica |
| UX/UI | A3 | 8 días | ~8 días | No crítica |
| Infraestructura | A4 | 4 días | 0 | Crítica |
| Autenticación | A5 | 6 días | 0 | Crítica — primer módulo |
| Clientes | A6 | 5 días | 0 | Crítica |
| Proyectos | A7 | 6 días | 0 | Crítica — núcleo |
| Tareas | A8 | 5 días | ~5 días | No crítica |
| Registro de Tiempo | A9 | 5 días | 0 | Crítica |
| Facturación | A10 | 6 días | 0 | Crítica |
| Dashboard | A11 | 5 días | 0 | Crítica |
| Integración | A12 | 5 días | 0 | Crítica |
| Pruebas QA | A13 | 6 días | 0 | Crítica |
| Despliegue | A14 | 4 días | 0 | Crítica — cierre |

**Actividades críticas:** 12 de 14
**Actividades con holgura:** A3 (UX/UI), A8 (Tareas)
**Duración mínima del proyecto:** 69 días
