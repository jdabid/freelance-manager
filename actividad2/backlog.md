# Product Backlog — FreelanceManager

**Proyecto:** Sistema de Gestión de Proyectos Freelance
**Autor:** Jesús David Castro Vanegas
**Curso:** Ingeniería de Sistemas — Universidad de Manizales
**Fecha:** Manizales, abril de 2026
**Total de historias:** 15
**Metodología:** Scrum

---

## Marco Scrum del proyecto

| Elemento Scrum | Definición para FreelanceManager |
|---|---|
| **Product Owner** | Jesús David Castro Vanegas |
| **Scrum Master** | Jesús David Castro Vanegas |
| **Development Team** | Jesús David Castro Vanegas |
| **Duración del Sprint** | 2 semanas (10 días hábiles) |
| **Total de Sprints** | 3 sprints de desarrollo |
| **Velocity estimada** | 18-20 Story Points por sprint |

El Product Backlog es el artefacto central de Scrum: la lista ordenada y priorizada de todo lo que el sistema debe hacer, expresada desde el punto de vista del usuario. El **Product Owner** es responsable de su contenido, orden y disponibilidad. En FreelanceManager, el Product Backlog fue ordenado combinando el criterio de valor (MoSCoW) con la dependencia técnica del sistema — ninguna historia puede implementarse sin que sus dependencias estén completas.

---

## Definition of Done (DoD)

Una historia de usuario está **Done** (Terminada) cuando cumple todos los criterios siguientes:

1. El código está implementado y funcional en el entorno de desarrollo
2. Todos los criterios de aceptación son verificables y pasan manualmente
3. El código no tiene errores de compilación ni warnings críticos
4. La funcionalidad está integrada con los módulos que dependen de ella
5. La tarjeta del tablero fue movida a la columna **Terminado** en GitHub Projects

Ninguna historia puede considerarse Done si alguno de estos puntos no se cumple. Durante el Sprint Review, el equipo verifica cada historia contra esta definición.

---

## Sprint Goals

| Sprint | Meta del Sprint | Historias | Story Points |
|---|---|:---:|:---:|
| **Sprint 1** | El freelancer puede registrarse, iniciar sesión y gestionar su lista de clientes | HU-01 a HU-05 | 19 SP |
| **Sprint 2** | El freelancer puede crear proyectos, gestionar tareas y registrar sus horas de trabajo | HU-06 a HU-10 | 17 SP |
| **Sprint 3** | El freelancer puede generar reportes, facturar sus servicios y ver su dashboard | HU-11 a HU-15 | 31 SP |
| **Total** | 3 sprints — 6 semanas de desarrollo | **15 HU** | **67 SP** |

---

## Criterio de priorización

Se utilizó el método **MoSCoW** combinado con la **dependencia técnica** del sistema para ordenar el Product Backlog, siguiendo la responsabilidad del Product Owner en Scrum:

- **Alta (Must Have):** funcionalidades sin las cuales el sistema no puede operar. Se priorizan primero porque otras historias dependen de ellas técnicamente.
- **Media (Should Have):** funcionalidades importantes que aportan valor directo al freelancer pero que no bloquean el funcionamiento básico.
- **Baja (Could Have):** funcionalidades deseables que mejoran la experiencia pero pueden postergarse sin afectar el núcleo del sistema.

El orden específico sigue esta lógica: **Autenticación → Clientes → Proyectos → Tareas → Tiempo → Facturación → Dashboard → Administración**. No se puede crear un proyecto sin un cliente registrado, no se puede registrar tiempo sin un proyecto activo, y no se puede generar una factura sin horas registradas. Las dependencias de datos determinan la prioridad y, por ende, el Sprint al que pertenece cada historia.

Los **Story Points (SP)** se estimaron usando la escala Fibonacci (1, 2, 3, 5, 8, 13), donde 1 = trivial y 13 = muy complejo. Se usó Planning Poker individual comparando la complejidad relativa entre historias.

---

## Backlog priorizado

| # | Historia de Usuario | Módulo | Prioridad | SP | Sprint | Criterios de Aceptación |
|:---:|---|---|:---:|:---:|:---:|---|
| HU-01 | Como **freelancer**, quiero registrarme con mi correo y contraseña para acceder al sistema de forma segura | Autenticación | **Alta** | 5 | Sprint 1 | 1. Dado que el freelancer ingresa un correo válido y una contraseña de mínimo 8 caracteres, cuando hace clic en "Registrarse", entonces el sistema crea su cuenta y lo redirige al dashboard. 2. Dado que el freelancer ingresa un correo ya registrado, cuando intenta registrarse, entonces el sistema muestra el mensaje "Este correo ya está en uso". |
| HU-02 | Como **freelancer**, quiero iniciar y cerrar sesión con mis credenciales para proteger el acceso a mi información | Autenticación | **Alta** | 3 | Sprint 1 | 1. Dado que el freelancer ingresa su correo y contraseña correctos, cuando hace clic en "Iniciar sesión", entonces el sistema lo redirige al dashboard en menos de 2 segundos. 2. Dado que el freelancer hace clic en "Cerrar sesión", entonces el sistema invalida su sesión y lo redirige a la pantalla de login. |
| HU-03 | Como **freelancer**, quiero recuperar mi contraseña mediante mi correo para no perder acceso a mi cuenta | Autenticación | **Alta** | 5 | Sprint 1 | 1. Dado que el freelancer ingresa su correo registrado en el formulario de recuperación, cuando hace clic en "Enviar", entonces el sistema genera un enlace de restablecimiento válido por 24 horas. 2. Dado que el freelancer accede al enlace de restablecimiento, cuando ingresa y confirma su nueva contraseña, entonces el sistema la actualiza y le permite iniciar sesión. |
| HU-04 | Como **freelancer**, quiero registrar la información de mis clientes para tener todos sus datos en un solo lugar | Clientes | **Alta** | 3 | Sprint 1 | 1. Dado que el freelancer completa los campos obligatorios (nombre, correo, teléfono), cuando guarda el cliente, entonces el sistema lo agrega a su lista de clientes y confirma el registro. 2. Dado que el freelancer intenta guardar un cliente sin nombre, cuando hace clic en guardar, entonces el sistema muestra el mensaje "El nombre del cliente es obligatorio". |
| HU-05 | Como **freelancer**, quiero editar y eliminar clientes para mantener mi información actualizada | Clientes | **Alta** | 3 | Sprint 1 | 1. Dado que el freelancer modifica los datos de un cliente existente, cuando guarda los cambios, entonces el sistema actualiza la información y muestra una confirmación. 2. Dado que el freelancer elimina un cliente, cuando confirma la acción, entonces el sistema elimina el registro y lo quita de la lista. |
| HU-06 | Como **freelancer**, quiero crear proyectos con nombre, descripción, cliente, fechas y presupuesto para organizar mi trabajo | Proyectos | **Alta** | 5 | Sprint 2 | 1. Dado que el freelancer completa los campos obligatorios del proyecto (nombre, cliente, fecha de entrega), cuando lo guarda, entonces el sistema crea el proyecto con estado "Activo" por defecto. 2. Dado que el freelancer intenta crear un proyecto sin fecha de entrega, cuando hace clic en guardar, entonces el sistema indica que la fecha de entrega es obligatoria. |
| HU-07 | Como **freelancer**, quiero cambiar el estado de mis proyectos (activo, pausado, completado, cancelado) para reflejar su avance real | Proyectos | **Alta** | 2 | Sprint 2 | 1. Dado que el freelancer selecciona un nuevo estado para un proyecto, cuando confirma el cambio, entonces el sistema actualiza el estado y registra la fecha del cambio. 2. Dado que el freelancer accede a la lista de proyectos, entonces el sistema muestra el estado actual de cada proyecto con un indicador visual diferenciado por color. |
| HU-08 | Como **freelancer**, quiero crear tareas dentro de mis proyectos con prioridad y fecha límite para no perder el control del trabajo | Tareas | **Alta** | 3 | Sprint 2 | 1. Dado que el freelancer crea una tarea con nombre, proyecto asociado y fecha límite, cuando la guarda, entonces el sistema la agrega al listado de tareas del proyecto con estado "Pendiente". 2. Dado que la fecha límite de una tarea es anterior a la fecha actual, entonces el sistema muestra la tarea marcada visualmente como vencida. |
| HU-09 | Como **freelancer**, quiero actualizar el estado de mis tareas (pendiente, en progreso, completada) para hacer seguimiento real del avance | Tareas | **Alta** | 2 | Sprint 2 | 1. Dado que el freelancer cambia el estado de una tarea, cuando confirma el cambio, entonces el sistema actualiza el estado inmediatamente y lo refleja en el proyecto asociado. 2. Dado que el freelancer filtra las tareas por estado, entonces el sistema muestra únicamente las tareas que coinciden con el filtro seleccionado. |
| HU-10 | Como **freelancer**, quiero registrar manualmente las horas trabajadas en un proyecto o tarea para tener un control preciso de mi tiempo | Registro de tiempo | **Alta** | 5 | Sprint 2 | 1. Dado que el freelancer ingresa la cantidad de horas, el proyecto, la tarea y una descripción, cuando guarda el registro, entonces el sistema lo agrega al historial de tiempo del proyecto. 2. Dado que el freelancer intenta registrar 0 horas o un valor negativo, cuando intenta guardar, entonces el sistema muestra el mensaje "El tiempo registrado debe ser mayor a cero". |
| HU-11 | Como **freelancer**, quiero ver un resumen de horas trabajadas por proyecto y por período para conocer mi inversión de tiempo real | Registro de tiempo | **Media** | 5 | Sprint 3 | 1. Dado que el freelancer accede al reporte de tiempo de un proyecto, entonces el sistema muestra el total de horas registradas agrupadas por semana y por tarea. 2. Dado que el freelancer filtra el reporte por rango de fechas, entonces el sistema muestra únicamente los registros dentro del período seleccionado. |
| HU-12 | Como **freelancer**, quiero generar una factura a partir de las horas registradas en un proyecto para cobrar mis servicios de forma organizada | Facturación | **Media** | 8 | Sprint 3 | 1. Dado que el freelancer selecciona un proyecto y hace clic en "Generar factura", entonces el sistema calcula el monto total (horas × tarifa del proyecto) y muestra la vista previa de la factura. 2. Dado que la vista previa de la factura se despliega, entonces el sistema incluye los datos del cliente, el desglose de horas y el monto total a cobrar. |
| HU-13 | Como **freelancer**, quiero exportar mis facturas en formato PDF para enviarlas a mis clientes | Facturación | **Media** | 5 | Sprint 3 | 1. Dado que el freelancer hace clic en "Exportar PDF" desde la vista previa de una factura, entonces el sistema genera y descarga el archivo PDF en menos de 3 segundos. 2. El PDF generado incluye: nombre y datos del cliente, nombre del proyecto, desglose de horas trabajadas, tarifa aplicada y monto total. |
| HU-14 | Como **freelancer**, quiero ver un dashboard con mis proyectos activos, tareas pendientes y horas registradas para tener una visión general de mi negocio | Dashboard | **Baja** | 8 | Sprint 3 | 1. Dado que el freelancer accede al dashboard, entonces el sistema muestra el número de proyectos activos, tareas pendientes y total de horas registradas en el mes actual. 2. Dado que el freelancer tiene proyectos con tareas vencidas, entonces el dashboard las resalta con un indicador visual de alerta. |
| HU-15 | Como **administrador**, quiero gestionar las cuentas de usuario (activar, desactivar) para mantener el control de acceso a la plataforma | Administración | **Baja** | 5 | Sprint 3 | 1. Dado que el administrador accede al panel de gestión de usuarios, entonces el sistema muestra la lista de cuentas registradas con su estado (activa/inactiva). 2. Dado que el administrador desactiva una cuenta, cuando confirma la acción, entonces el sistema bloquea el acceso de ese usuario y registra la fecha de desactivación. |

---

## Justificación de priorización

### Por qué Autenticación va primero — Sprint 1 (HU-01, HU-02, HU-03)
Sin un sistema de login funcional, ninguna otra historia puede implementarse. El sistema completo depende de que exista un usuario autenticado — los clientes, proyectos, tareas y registros de tiempo pertenecen a una cuenta específica. En Scrum, el Sprint 1 no puede completar su Sprint Goal sin estas tres historias. Técnicamente es el punto de entrada obligatorio del sistema.

### Por qué Clientes va antes que Proyectos — Sprint 1 (HU-04, HU-05)
En el modelo de datos del sistema, un proyecto siempre está vinculado a un cliente. No es posible construir la pantalla "nuevo proyecto" sin que exista la lista de clientes para seleccionar. La dependencia de datos determina que Clientes debe estar Done dentro del mismo Sprint 1, antes de que el Sprint 2 comience.

### Por qué Proyectos va antes que Tareas y Tiempo — Sprint 2 (HU-06, HU-07)
Las tareas pertenecen a un proyecto y los registros de tiempo se vinculan a un proyecto o tarea. Sin proyectos creados, ambas funcionalidades no tienen contexto donde operar. El Sprint Goal del Sprint 2 requiere que los proyectos se implementen primero dentro de la misma iteración.

### Por qué Registro de tiempo va antes que Facturación — Sprint 2 antes que Sprint 3 (HU-10, HU-11)
La factura se genera calculando horas registradas × tarifa. Si no hay registros de tiempo, no hay datos para calcular el monto de la factura. HU-12 depende directamente de HU-10 — por eso HU-10 está en el Sprint 2 y HU-12 en el Sprint 3.

### Por qué Dashboard y Administración son prioridad Baja — Sprint 3 (HU-14, HU-15)
El dashboard agrega información de todos los módulos anteriores — construirlo primero sería construir un panel vacío. La administración de usuarios es un módulo de soporte que no afecta el flujo principal del freelancer. Ambas van al final del Sprint 3, cuando todos los datos que necesitan ya existen.

---

## Ceremonias Scrum por Sprint

| Ceremonia | Momento | Duración | Propósito |
|---|---|:---:|---|
| **Sprint Planning** | Inicio de cada sprint | 2h | Seleccionar historias del Product Backlog y crear el Sprint Backlog |
| **Daily Scrum** | Cada día del sprint | 15 min | Sincronizar avance e identificar impedimentos |
| **Sprint Review** | Final de cada sprint | 1h | Demostrar el Incremento y verificar el Sprint Goal |
| **Sprint Retrospective** | Final de cada sprint | 45 min | Inspeccionar y adaptar el proceso del equipo |

---

## Resumen por Sprint

| Sprint | Historias | Story Points | Sprint Goal |
|---|:---:|:---:|---|
| Sprint 1 | HU-01 a HU-05 | 19 SP | El freelancer puede registrarse y gestionar clientes |
| Sprint 2 | HU-06 a HU-10 | 17 SP | El freelancer puede gestionar proyectos, tareas y tiempo |
| Sprint 3 | HU-11 a HU-15 | 31 SP | El freelancer puede facturar y ver su dashboard |
| **Total** | **15** | **67 SP** | **3 sprints — 6 semanas de desarrollo** |

---

## Resumen por prioridad MoSCoW

| Prioridad | Historias | Story Points | Módulos cubiertos |
|---|:---:|:---:|---|
| Alta | HU-01 al HU-10 | 36 SP | Autenticación, Clientes, Proyectos, Tareas, Tiempo |
| Media | HU-11 al HU-13 | 18 SP | Reportes de tiempo, Facturación |
| Baja | HU-14 al HU-15 | 13 SP | Dashboard, Administración |
| **Total** | **15** | **67 SP** | **7 módulos** |
