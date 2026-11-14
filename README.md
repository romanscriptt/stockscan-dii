<div align="center">

# StockScan SGA (SCAN ALMACÉN)

**Sistema de Gestión de Almacén (SGA) Modular, Escalable y de Alto Rendimiento**

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Swing](https://img.shields.io/badge/UI-Java_Swing-007396?style=for-the-badge&logo=java&logoColor=white)
![NetBeans](https://img.shields.io/badge/IDE-Apache_NetBeans-1B6AC6?style=for-the-badge&logo=apachenetbeanside&logoColor=white)
![Estado](https://img.shields.io/badge/Sprint_1-Completado-27AE60?style=for-the-badge)

</div>

---

## QUIÉNES SOMOS

Somos un equipo multidisciplinar de desarrolladores e ingenieros de software orientados al diseño de sistemas industriales. Nos especializamos en la optimización de procesos operativos mediante **interfaces de alta usabilidad (UI/UX)**, arquitecturas desacopladas y reducción drástica de la carga cognitiva en entornos de trabajo exigentes[cite: 4].

| Miembro del Equipo | Perfil en GitHub |
| :--- | :--- |
| **Álvaro López** | [@romanscriptt](https://github.com/romanscriptt)[cite: 4] |
| **Carmen Monge** | [@carmenmonge25](https://github.com/carmenmonge25)[cite: 4] |
| **Elena Sáez** | [@elenasaez25](https://github.com/elenasaez25)[cite: 4] |
| **Ángel Luis Sánchez** | [@angelluissanchez25](https://github.com/angelluissanchez25)[cite: 4] |

---

## EL PROBLEMA REAL QUE RESOLVEMOS

En la logística industrial actual, la ineficiencia operativa rara vez se debe a la falta de esfuerzo humano; proviene de herramientas de software deficientes:

1. **Interfaces saturadas e ineficientes:** Más del 65% de las pérdidas operativas y errores de stock ocurren por el uso de software anticuado y de difícil lectura[cite: 4].
2. **Pérdida de tiempo operativa:** Hasta un **40% del tiempo de trabajo** de los operarios se desperdicia interactuando con pantallas complejas y confirmando datos manualmente.
3. **Fatiga visual y errores de selección:** Entornos con poco contraste y flujos rígidos provocan errores constantes en las fases de *picking* y *packing*.

---

## NUESTRA SOLUCIÓN: STOCKSCAN SGA

**StockScan SGA** aborda directamente la raíz del problema mediante:

- **Sistemas de Tokens Semánticos:** Paleta de contraste extremo y retroalimentación cromática inmediata (Verde = Éxito, Rojo = Conflicto, Ámbar = Alerta) calibrados para pantallas industriales (HiDPI / PDA).
- **Minimización de Carga Cognitiva:** Flujos de interacción simplificados que reducen el tiempo de escaneo e identificación a menos de 2 segundos.
- **Confirmación y Validación en Tiempo Real:** Cero margen de error en el control de stock e historial de movimientos, con respuesta instantánea mediante eventos de ratón, foco y teclado.

---

## QUÉ HEMOS HECHO POR AHORA (SPRINT 1)

Durante el **Sprint 1**, hemos establecido las bases operativas, de diseño y arquitectónicas del proyecto:

### 1. Caracterización de Usuarios y Flujos (UX)
- Definición de *User Personas* clave (*Operario*, *Supervisor*, *Administrador*).
- Mapeo de flujos críticos de trabajo para maximizar la velocidad operativa.

### 2. Prototipado e Interfaz (UI HiDPI)
- **Prototipo Interactivo en Figma:** Maquetación completa de paneles principales (`Dashboard`, `Mapa de Almacén`, `Stock`, `Etiquetas`, `Trazabilidad`, `Alertas`, `Equipo`, `Agenda` y `Chat`).
- **Sistema de Design Tokens:** Definición estandarizada de colores semánticos, fuentes claras para códigos SKU y componentes reutilizables.

### 3. Arquitectura MVC + DAO e Interactividad Avanzada
Diseño de una arquitectura limpia y desacoplada estructurada en 4 capas:
- **VIEW (`com.stockscan.view.pages`):** Componentes Java Swing desarrollados en Apache NetBeans con gestión de **eventos de bajo nivel** (`MouseAdapter`, `FocusAdapter` y `KeyAdapter`) para filtrado en tiempo real, validación de clics sin duplicidad y navegación accesible por teclado.
- **CONTROLLER:** Gestión de eventos de usuario y control del flujo de datos entre vistas.
- **MODEL:** POJOs (`Producto`, `Movimiento`, `Usuario`) que encapsulan el estado y la lógica de negocio.
- **DAO (Data Access Object):** Capa de abstracción preparada para persistencia en base de datos relacional (H2 / SQLite / MySQL).

### 4. Gestión Ágil
- Organización del flujo de trabajo y trazabilidad de tareas mediante **GitHub Projects (Tablero Kanban)** y documentación técnica por sprint.

---

## ESTRUCTURA DEL REPOSITORIO

```text
Grupo4-DII-Proyecto/
├── StockScanE/                        # Proyecto principal Java Swing (Apache NetBeans)
│   ├── src/
│   │   └── com/stockscan/
│   │       └── view/pages/            # Vistas modulares y listeners de bajo nivel
│   ├── build.xml                      # Script de compilación Ant[cite: 4]
│   └── nbproject/                     # Configuración del proyecto NetBeans
├── docs/                              # Documentación técnica del proyecto[cite: 2]
│   ├── sprints/                       # Memorias detalladas de cada Sprint[cite: 2]
│   ├── analisis_y_backlog.md          # Análisis funcional y backlog[cite: 2]
│   └── desarrollo_mvc.md              # Especificación de arquitectura MVC[cite: 2]
├── .gitignore                         # Exclusión de archivos temporales y compilados[cite: 2]
└── README.md                          # Visión general del proyecto[cite: 2]
