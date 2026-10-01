# Product Backlog de StockScan

Definición, estructuración y priorización del Product Backlog para el sistema de gestión de almacenes **StockScan**.

Se recopilan las historias de usuario y requisitos funcionales necesarios para la operativa diaria del almacén, clasificados por prioridad según el valor aportado al usuario final y la viabilidad técnica en Java Swing, Web y Móvil.

---

## 1. Objetivo del producto

Que cualquier operario del almacén pueda controlar el stock en tiempo real (entradas, salidas y traspasos) desde Swing, Web o móvil, incluso sin conexión, con menos errores y menos tiempo por operación.

---

## 2. Épicas

| ID | Épica | Qué cubre del prototipo |
|----|-------|-------------------------|
| E1 | Acceso | Login con correo electrónico y contraseña |
| E2 | Consulta de stock | Pantalla principal, buscador de productos/códigos, stock por zona (ferretería / electrónica) y stock general |
| E3 | Entrada de mercancía | Escaneo de código QR o de barras |
| E4 | Salida y picking | Escaneo de salida, identificación del tipo de artículo (tornillo, cinta de embalaje, caja de cartón…) y lista de picking |
| E5 | Traspasos | Mover stock entre estanterías |
| E6 | Modo sin conexión | Guardado local de escaneos y sincronización automática al recuperar la conexión |
| E7 | Comunicación | Chat de grupo con compañeros de la empresa |
| E8 | Agenda | Turno activo, próximos turnos y tareas asignadas |

---

## 3. Backlog ordenado

El orden combina **valor de negocio** (lo decide el Product Owner) y **esfuerzo** (lo estima el equipo). Los puntos de historia (SP) son una propuesta inicial que el equipo debe validar.

| Ord. | ID | Historia de usuario | Prioridad | Valor | Esfuerzo (SP) | Plataformas |
|------|----|---------------------|-----------|-------|---------------|-------------|
| 1 | US-01 | Como operario, quiero iniciar sesión con mi correo y contraseña para acceder a mis funciones. | Must | Alto | 3 | Swing, Web, Móvil |
| 2 | US-02 | Como operario, quiero ver el stock general para saber qué hay en el almacén. | Must | Alto | 5 | Swing, Web, Móvil |
| 3 | US-03 | Como operario, quiero buscar productos por nombre o código para localizarlos rápido. | Must | Alto | 3 | Swing, Web, Móvil |
| 4 | US-04 | Como operario, quiero escanear un código QR o de barras en una entrada para registrar la mercancía sin teclear. | Must | Alto | 8 | Móvil, Web, Swing (lector USB) |
| 5 | US-05 | Como operario, quiero escanear una salida y que el sistema identifique el tipo de artículo (tornillo, cinta, caja de cartón…) para descontar el stock correcto. | Must | Alto | 8 | Móvil, Web, Swing |
| 6 | US-06 | Como operario, quiero que mis escaneos se guarden localmente si no hay conexión para no perder trabajo. | Must | Alto | 8 | Móvil, Swing, Web |
| 7 | US-07 | Como operario, quiero que los escaneos pendientes se sincronicen solos al recuperar la conexión. | Must | Alto | 5 | Móvil, Swing, Web |
| 8 | US-08 | Como operario, quiero ver el stock separado por ferretería y electrónica para consultar cada zona. | Should | Medio-alto | 3 | Swing, Web, Móvil |
| 9 | US-09 | Como operario, quiero seguir una lista de picking en las salidas para preparar pedidos sin olvidar artículos. | Should | Alto | 8 | Móvil, Web |
| 10 | US-10 | Como operario, quiero traspasar stock entre estanterías para mantener la ubicación real actualizada. | Should | Medio-alto | 5 | Móvil, Web, Swing |
| 11 | US-11 | Como operario, quiero ver mi turno activo y los próximos para organizarme. | Should | Medio | 5 | Móvil, Web |
| 12 | US-12 | Como operario, quiero ver las tareas asignadas a mi turno para saber qué hacer. | Should | Medio | 5 | Móvil, Web |
| 13 | US-13 | Como operario, quiero un chat de grupo con mis compañeros para coordinarnos. | Could | Medio-bajo | 8 | Móvil, Web |
| 14 | US-14 | Como operario, quiero un indicador visible del estado de conexión y de escaneos pendientes. | Could | Medio | 2 | Todas |

---

## 4. Justificación del orden

- **Primero lo que da valor desde el día uno:** acceso, consulta y escaneo. Sin eso no hay producto utilizable.
- **El modo sin conexión sube a Must** porque los escaneos son la operación crítica. Es mejor construirlo junto al escaneo que añadirlo después, ya que condiciona cómo se guardan los datos.
- **Traspasos, picking y agenda** aportan eficiencia, pero el almacén puede operar sin ellos al principio.
- **El chat va al final:** tiene valor de comunicación, pero ya existen alternativas externas y su coste es alto (servidor, notificaciones).

---

## 5. Viabilidad técnica por plataforma

| Plataforma | Escaneo | Modo sin conexión |
|------------|---------|-------------------|
| **Java Swing** | La cámara no es lo habitual; lo viable es un lector USB que actúa como teclado. | Base de datos local (SQLite o H2). |
| **Web** | Cámara del navegador (requiere HTTPS). | Posible con Service Workers e IndexedDB, con más complejidad. |
| **Móvil** | La mejor opción para escanear. | SQLite local; la más adecuada para offline. |

> El móvil es la principal candidata para el MVP.

---

## 6. Propuesta de sprints

| Sprint | Historias | Foco |
|--------|-----------|------|
| 1 | US-01, US-02, US-03 | Acceso y consulta |
| 2 | US-04, US-05 | Escaneo de entrada y salida |
| 3 | US-06, US-07, US-08 | Modo sin conexión y zonas |
| 4 | US-09, US-10 | Picking y traspasos |
| 5+ | US-11, US-12, US-13, US-14 | Agenda, chat e indicadores |

Los elementos de los sprints 4 en adelante están menos definidos a propósito y se irán refinando a medida que se acerquen a su ejecución.

---

## 7. Ejemplo de criterios de aceptación

**US-06 – Guardado local sin conexión**

- **Dado que** no hay conexión a internet,
- **cuando** escaneo un código de producto,
- **entonces** el registro se guarda localmente y aparece marcado como "pendiente de sincronizar".

**US-07 – Sincronización automática**

- **Dado que** hay escaneos pendientes y se recupera la conexión,
- **cuando** la app detecta la red,
- **entonces** los registros se envían automáticamente y pasan a estado "sincronizado".

---

## 8. Definición de "Ready"

Una historia puede entrar en un Sprint cuando:

- Tiene criterios de aceptación claros.
- Está estimada por el equipo.
- Tiene el valor de negocio confirmado por el Product Owner.
- Sus dependencias técnicas están resueltas.

## 9. Referencias

[1] alyssa, «The Product Backlog: A Complete Guide | Scrum Inc.» Accedido: 30 de septiembre de 2026. [En línea]. Disponible en: https://www.scruminc.com/product-backlog/
