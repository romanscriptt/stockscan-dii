#  StockScan SGA (SCAN ALMACÉN)

**Sistema de Gestión de Almacén (SGA) Modular, Escalable y de Alto Rendimiento**

---

##  QUIÉNES SOMOS

Somos un equipo multidisciplinar de desarrolladores e ingenieros de software orientados al diseño de sistemas industriales. Nos especializamos en la optimización de procesos operativos mediante **interfaces de alta usabilidad (UI/UX)**, arquitecturas desacopladas y reducción drástica de la carga cognitiva en entornos de trabajo exigentes.

**Miembros del grupo:**
* **Álvaro López** 
* **Carmen Monge**
* **Elena Sáez**
* **Ángel Luis Sánchez**

---

##  EL PROBLEMA REAL QUE RESOLVEMOS

En la logística industrial actual, la ineficiencia operativa rara vez se debe a la falta de esfuerzo humano; proviene de herramientas de software deficientes:

1. **Interfaces saturadas e ineficientes:** Más del 65% de las pérdidas operativas y errores de stock ocurren por el uso de software anticuado y de difícil lectura.
2. **Pérdida de tiempo operativa:** Hasta un **40% del tiempo de trabajo** de los operarios se desperdicia interactuando con pantallas complejas y confirmando datos manualmente.
3. **Fatiga visual y errores de selección:** Entornos con poco contraste y flujos rígidos provocan errores constantes en las fases de *picking* y *packing*.

---

##  NUESTRA SOLUCIÓN: STOCKSCAN SGA

**StockScan SGA** aborda directamente la raíz del problema mediante:

* **Sistemas de Tokens Semánticos:** Paleta de contraste extremo y retroalimentación cromática inmediata (Verde = Éxito, Rojo = Conflicto, Ámbar = Alerta) calibrados para pantallas industriales (HiDPI / PDA).
* **Minimización de Carga Cognitiva:** Flujos de interacción simplificados que reducen el tiempo de escaneo e identificación a menos de 2 segundos.
* **Confirmación y Validación en Tiempo Real:** Cero margen de error en el control de stock e historial de movimientos.

---

##  QUÉ HEMOS HECHO POR AHORA (SPRINT 1)

Durante el **Sprint 1**, hemos establecido las bases operativas, de diseño y arquitectónicas del proyecto:

### 1. Caracterización de Usuarios y Flujos (UX)
* Definición de *User Personas* clave (*Operario*, *Supervisor*, *Administrador*).
* Mapeo de flujos críticos de trabajo para maximizar la velocidad operativa.

### 2. Prototipado e Interfaz (UI HiDPI)
* **Prototipo Interactivo en Figma:** Maquetación completa de paneles principales, escaneo de inventario y gestión de stock.
* **Sistema de Design Tokens:** Definición estandarizada de colores semánticos, fuentes monoespaciadas para códigos SKU y componentes reutilizables[cite: 17].

### 3. Arquitectura MVC + DAO (Backend Base)
Diseño de una arquitectura limpia y desacoplada estructurada en 4 capas:
* ** VIEW:** Componentes Java Swing optimizados para pantallas táctiles y desktop (Layouts reactivos con `MigLayout`).
* ** CONTROLLER:** Gestión de eventos de usuario (`ActionListeners`) y control del flujo de datos.
* ** MODEL:** POJOs (`Producto`, `Movimiento`, `Usuario`) que encapsulan el estado y la lógica de negocio.
* ** DAO (Data Access Object):** Capa de abstracción para persistencia en base de datos independiente (H2 / SQLite / MySQL).

### 4. Gestión Ágil
* Organización del flujo de trabajo y tareas mediante **GitHub Projects (Tablero Kanban).

---

##  ESTRUCTURA DEL REPOSITORIO

```text
├── docs/
│   ├── MEMORIA.md            # Documentación técnica completa
│   └── architecture_mvc.png  # Diagrama de arquitectura
├── src/
│   ├── controller/           # Controladores del sistema
│   ├── model/                # POJOs y lógica de negocio
│   ├── dao/                  # Interfaces y clases de acceso a datos
│   └── view/                 # Componentes de interfaz Swing
├── README.md                 # Visión general del proyecto
└── pom.xml / build.gradle    # Configuración de dependencias
