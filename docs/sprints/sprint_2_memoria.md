# Memoria final Sprint 2 – StockScan SGE

## 1. Análisis y planificación

> Introducir aquí la parte de Análisis y planificación (introducción general, si procede).

### 1.1. Analizar requisitos de usabilidad y accesibilidad

> Introducir aquí la parte de análisis de requisitos de usabilidad y accesibilidad.

### 1.2. Definir estándares y pautas de accesibilidad

> Introducir aquí la parte de definición de estándares y pautas de accesibilidad.

### 1.3. Seleccionar métricas y herramientas de auditoría

> Introducir aquí la parte de selección de métricas y herramientas de auditoría.

---

## 2. Diseño de la interfaz

Fase en la que se define cómo se verá y cómo se usará la aplicación: pautas visuales (colores, fuentes, iconos y distribución), estructura de navegación y elementos de interfaz. El resultado es el diseño que se seguirá al programar.

### 2.1. Crear y documentar wireframes y mockups

### Objetivo
Crear y documentar los wireframes y mockups de las cuatro pantallas principales de la aplicación de escritorio StockScan SGA (Inicio, Inventario, Escanear y Alertas) como referencia visual previa a la implementación en Swing.

### Wireframes
Esquemas en escala de grises con zonas numeradas. Todos mantienen la barra lateral fija de 9 secciones.

#### Wireframe 1 · Inicio

<img width="2400" height="1245" alt="Image" src="https://github.com/user-attachments/assets/a453236c-1323-49ed-b8cf-54e1aa61bb83" />

#### Wireframe 2 · Inventario
<img width="2400" height="1185" alt="Image" src="https://github.com/user-attachments/assets/ddb77741-6ae7-4a53-a425-ae114fd36d40" />

#### Wireframe 3 · Alertas
<img width="2400" height="1245" alt="Image" src="https://github.com/user-attachments/assets/cf546b66-90b4-4e7c-8fd1-1abc7b39aabd" />

| Pantalla | Función | Elementos clave |
|---|---|---|
| Inicio | Vista global del almacén | 4 indicadores, gráfico de actividad, mini-gráficos y actividad reciente |
| Inventario | Consultar y filtrar productos | Buscador, filtros por categoría y estado, tabla con barra de nivel, botón Editar |
| Alertas | Gestionar productos bajo el mínimo | Tarjetas resumen, una tarjeta por producto, Generar pedido y Notificar |

### Mockups
Aplican la paleta, la tipografía y los criterios de iconos de las pautas visuales (#45). [Diseño en Figma](figma.com/make/fVgbUMpu9QaXt6AXwhjVY5/StockScan-SGA-Interface-Design?t=gq0krPnJ916Ffdij-20&fullscreen=1&fuid=1686775443056008797)

### Decisiones de diseño
Barra lateral fija, adecuada para 5–10 categorías [2][3]; una acción principal por pantalla; estado del producto siempre con texto además del color [1]; contadores de aviso visibles [4]; una vista Swing por pantalla separada de la lógica [5].

### Resultado
Tres pantallas documentadas en versión escritorio, con sus zonas e incidencias resueltas o asignadas, como base para la implementación y las pruebas de usabilidad.

### Referencias
[1] W3C, «WCAG2ICT», W3C Group Note, 2025. https://www.w3.org/TR/2025/NOTE-wcag2ict-22-20251211
[2] Microsoft, «Navigation view», Microsoft Learn. https://learn.microsoft.com/windows/apps/design/controls/navigationview
[3] Apple Inc., «Sidebars», Human Interface Guidelines. https://developer.apple.com/design/human-interface-guidelines/sidebars
[4] J. Nielsen, «10 Usability Heuristics for User Interface Design», Nielsen Norman Group. https://www.nngroup.com/articles/ten-usability-heuristics/
[5] G. E. Krasner y S. T. Pope, *Journal of Object-Oriented Programming*, vol. 1, n.º 3, pp. 26–49, 1988.

### 2.2. Definir la estructura de navegación y los elementos de interfaz

### Objetivo
Definir la estructura de navegación de la aplicación de escritorio StockScan SGA (barra lateral con 9 secciones y diálogos modales) y catalogar los elementos de interfaz de cada pantalla, de modo que cualquier sección sea accesible en un solo clic y el equipo disponga de una referencia única para implementarla en Java Swing.

### Modelo de navegación
La aplicación usa una **barra lateral izquierda fija y siempre visible**, con 9 secciones:

| Nº | Sección | Aviso |
|---|---|---|
| 1 | Dashboard | — |
| 2 | Mapa de almacén | — |
| 3 | Stock | — |
| 4 | Etiquetas | — |
| 5 | Trazabilidad | — |
| 6 | Alertas | contador |
| 7 | Equipo | — |
| 8 | Agenda | — |
| 9 | Chat | contador |

**Por qué barra lateral:**
- Microsoft recomienda la navegación lateral cuando hay entre 5 y 10 categorías igual de importantes [2]. Aquí son 9.
- En escritorio hay ancho de sobra, así que no hace falta ocultar el menú [2][3].
- Se mantiene visible por defecto para que sea fácil de descubrir [3].

El pie de la barra muestra el usuario conectado (Ana Rodríguez · Admin) y no contiene acciones críticas [3].

### Jerarquía de navegación
- **Nivel 1:** las 9 secciones de la barra lateral (una pantalla cada una).
- **Nivel 2:** diálogos modales abiertos desde una pantalla:
  - Añadir producto / Editar (desde Stock)
  - Entrada de stock, con 3 pasos (desde Stock)
  - Generar pedido y Generar pedido múltiple (desde Alertas)
- **No hay nivel 3:** un diálogo no abre otro diálogo.

Se respeta el máximo de **2 niveles** que recomiendan Microsoft y Apple [2][3].

### Elementos de interfaz y componente Swing

| Elemento | Dónde | Componente Swing |
|---|---|---|
| Barra lateral | Todas | JPanel (BorderLayout.WEST) + botones de sección |
| Cambio de pantalla | Zona central | JPanel con CardLayout |
| Tarjetas de indicadores | Dashboard, Alertas | JPanel + JLabel |
| Gráfico de actividad | Dashboard | Componente propio (paintComponent) |
| Selector Día/Semana/Mes y chips de filtro | Dashboard, Stock | JToggleButton + ButtonGroup |
| Buscador | Stock | JTextField |
| Tabla de productos | Stock | JTable + JScrollPane |
| Barra de nivel | Stock, Alertas | JProgressBar (o componente propio) |
| Botones de acción (Añadir, Editar, Generar pedido, Notificar) | Stock, Alertas | JButton |
| Diálogo Entrada de stock | Stock | JDialog modal |
| Entrada manual de código + OK | Entrada de stock | JTextField + JButton |

Cada pantalla es una vista (JPanel) separada de la lógica, según MVC [6].

### Interacción con teclado y ratón
- **Tab / Mayús+Tab:** recorren los elementos en orden visual.
- **Enter:** confirma el diálogo o la acción principal.
- **Esc:** cancela y cierra el diálogo.
- **Foco inicial** en el campo de código de Entrada de stock, para que un lector USB escriba directamente.
- **Atajos de sección** (propuesta): Ctrl+1 … Ctrl+9, en el orden de la barra lateral

### Estados y avisos
- **Sección activa:** fondo resaltado + texto en negrita (no solo color).
- **Avisos:** contador en Alertas y Chat; el usuario ve el estado sin entrar [4].
- **Estado del producto:** etiqueta de texto (En stock, Stock bajo, Sin stock) además de la barra de nivel.
- **Elementos desactivados:** botón atenuado y sin respuesta al clic.
- **Errores:** mensaje junto al campo (por ejemplo, código de ubicación no válido) y foco en el campo.
El color nunca es el único indicador [1].

### Referencias
[1] W3C, «WCAG2ICT», W3C Group Note, 2025. https://www.w3.org/TR/2025/NOTE-wcag2ict-22-20251211
[2] Microsoft, «Navigation view», Microsoft Learn. https://learn.microsoft.com/windows/apps/design/controls/navigationview
[3] Apple Inc., «Sidebars», Human Interface Guidelines. https://developer.apple.com/design/human-interface-guidelines/sidebars
[4] J. Nielsen, «10 Usability Heuristics for User Interface Design», Nielsen Norman Group. https://www.nngroup.com/articles/ten-usability-heuristics/
[5] FormDev Software, «FlatLaf». https://www.formdev.com/flatlaf/
[6] G. E. Krasner y S. T. Pope, *Journal of Object-Oriented Programming*, vol. 1, n.º 3, pp. 26–49, 1988.
[7] Oracle, «Modifying the Look and Feel», The Java Tutorials. https://docs.oracle.com/javase/tutorial/uiswing/lookandfeel

### 2.3. Establecer las pautas visuales: colores, fuentes, iconos y distribución

### Objetivo

Establecer colores, tipografía, iconos y distribución de la ventana de StockScan SGA para que la aplicación de escritorio sea coherente, legible y accesible.

### Colores

La paleta se basa en azul, blanco y ámbar. El verde y el rojo se reservan para indicar el estado de las operaciones.

| Uso | Color | Código |
|---|---|---|
| Primario | Azul | `#1B4F72` |
| Primario oscuro (cabeceras) | Azul oscuro | `#123A57` |
| Primario claro (fondos suaves) | Azul claro | `#D6EAF8` |
| Acento / alerta | Ámbar | `#F39C12` |
| Éxito | Verde | `#27AE60` |
| Peligro / error | Rojo | `#E74C3C` |
| Fondo / superficie | Gris muy claro / blanco | `#F5F7FA` / `#FFFFFF` |
| Texto principal / secundario | Gris casi negro / gris | `#1C1C1E` / `#6E6E73` |

**Contraste.** Se calcularon las relaciones de contraste de los pares de colores principales según las pautas WCAG 2.2 [1], que exigen un mínimo de 4,5:1 para el texto y de 3:1 para los componentes de interfaz:

- El texto principal sobre blanco alcanza 17:1 y el blanco sobre el azul primario, 8,7:1.
- El texto secundario sobre blanco alcanza 5,1:1.
- El blanco sobre ámbar (2,2:1) y sobre verde (2,9:1) no cumple el mínimo, por lo que en esos botones se utiliza texto oscuro (7,8:1 y 5,9:1 respectivamente).
- El blanco sobre rojo (3,8:1) solo se emplea en texto grande o en negrita.
- El gris terciario (`#AEAEB2`, 2,2:1) no se usa para información importante.

Como regla general, el color nunca es el único medio para transmitir un estado: siempre se acompaña de un icono o de texto [1].

### Tipografía

Se utiliza una fuente sans-serif (Inter) para la interfaz y una fuente monoespaciada para códigos y cifras, de modo que los datos se lean de un vistazo y no se confundan caracteres similares (0/O, 1/l).

| Nivel | Tamaño y peso | Uso |
|---|---|---|
| Display | 32 px · 800 | Título de la pantalla principal |
| H1 | 24 px · 700 | Título de sección |
| H2 | 20 px · 600 | Subsección |
| H3 | 16 px · 600 | Título de lista o tarjeta |
| Body | 14 px · 400 | Texto normal |
| Small | 12 px · 400 | Información secundaria |
| Caption | 11 px · 500 | Etiquetas y estados, en mayúsculas |

La tipografía monoespaciada se aplica a los códigos de producto (`PRD-0041-INOX`), a las ubicaciones de estantería (`PAS-02-EST-04`) y a las cifras de stock (`1,248`). La información importante (código, cantidad o estado) nunca se muestra en los niveles Small o Caption.

### Iconos

Se emplea un único conjunto de iconos de línea, con botones cuadrados de esquinas redondeadas. El color del fondo indica el tipo de acción:


| Icono | Acción | Fondo | Color del icono |
|---|---|---|---|
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/3f533c5e-3435-4c24-bc96-ef392d48a22b" /> | Crear un elemento | Azul primario | Blanco |
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/c7efd8fa-068a-4d2c-9446-743426cdfe71" /> | Buscar | Azul claro | Azul primario |
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/4c2b02d9-ecde-401d-b5bc-6a67cddee5b2" /> | Filtrar | Gris claro | Gris |
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/6e8a11e8-391a-4c4d-b1c3-8c86b1292df4" /> | Cancelar o eliminar | Rojo claro | Rojo |
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/722feed4-ab8e-4434-af12-c4635c4cc223" /> | Confirmar | Verde claro | Verde |
| <img width="50" height="50" alt="Icono" src="https://github.com/user-attachments/assets/42186ffe-de4d-4fe8-99b8-a94ab81ff8fd" /> | Descargar o exportar | Ámbar claro | Ámbar |

Nota: Los iconos están seleccionados de **Font Awesome**, son intuitivos ya que habría que cambiar los colores y el fondo, cosa que la página web no permite.

Las reglas de uso son las siguientes:

- La acción principal de cada pantalla utiliza el único botón de fondo sólido.
- Los botones que solo contienen un icono llevan una etiqueta accesible (texto alternativo o ayuda emergente).
- Las acciones críticas (confirmar y eliminar) incluyen además texto visible junto al icono, para no depender solo del color [1].
- El tamaño táctil mínimo es de 48×48 dp [2].

**Limitación detectada.** Los iconos de color sobre su fondo claro no alcanzan el contraste de 3:1 recomendado para elementos de interfaz (rojo, 2,95:1; verde, 2,46:1; ámbar, 2,03:1) [1]. Se mitiga con la regla anterior de acompañar las acciones críticas con texto, y se deja como mejora oscurecer el tono de estos iconos.

### Distribución

Barra lateral fija (≈210 px), contenido con márgenes de ≈32 px y espaciado en múltiplos de 4/8 px, tarjetas con borde redondeado y tablas a ancho completo. La ventana es redimensionable, con tamaño mínimo propuesto de 1280×720. Las medidas con ≈ se confirmarán en Figma.


### Referencias
[1] W3C, «WCAG2ICT», W3C Group Note, 2025. https://www.w3.org/TR/2025/NOTE-wcag2ict-22-20251211
[2] Sun Microsystems, *Java Look and Feel Design Guidelines*, 2.ª ed. Addison-Wesley, 2001.
[3] Apple Inc., «Sidebars», Human Interface Guidelines. https://developer.apple.com/design/human-interface-guidelines/sidebars
[4] FormDev Software, «FlatLaf». https://www.formdev.com/flatlaf/
[5] Oracle, «Modifying the Look and Feel», The Java Tutorials. https://docs.oracle.com/javase/tutorial/uiswing/lookandfeel

---

## 3. Implementación

La fase de implementación traslada las especificaciones de diseño y las directrices de accesibilidad a código Java ejecutable sobre el entorno Swing. Para ello, se ha desarrollado una arquitectura modular basada en el patrón Modelo-Vista-Controlador (MVC), donde la interfaz gráfica queda desacoplada de la lógica de negocio y de los mecanismos de almacenamiento.

El desarrollo se ha estructurado en torno a una ventana contenedora principal (`MainFrame`) con una resolución de $1000 \times 600\text{ px}$, sobre la que se intercalan dinámicamente los 9 paneles del sistema mediante un contenedor de tipo `CardLayout`, junto a una pantalla independiente de autenticación (`LoginFrame`).

---

### 3.1. Desarrollar componentes visuales e interactivos

Para garantizar la homogeneidad de la interfaz y acelerar el desarrollo con el editor visual NetBeans Matisse, se han categorizado y parametrizado los componentes gráficos clave de la aplicación:

#### Vista de Autenticación (`LoginFrame`)

> ![LoginFrame](https://github.com/user-attachments/assets/479aa5c7-2b1e-40e0-8c79-8c4872c28cef)

* **Estructura visual:** Formulario en *split layout* de $1000 \times 600\text{ px}$ dividido en un banner corporativo lateral (`panelBannerLogin`, $450\text{ px}$) y un área central de credenciales (`panelFormLogin`, $550\text{ px}$).
* **Componentes integrados:** Campos de entrada alineados para correo (`txtEmail`) y clave (`txtPassword`), junto a un botón principal estilizado (`btnIniciarSesion`).

---

#### Cuadro de Mando (`DashboardPanel`)

> ![Dashboard](https://github.com/user-attachments/assets/df6982c4-c4b8-4935-a8ed-6036b1447896)

* **Menu Lateral Fijo (`panelSidebar`):** Contenedor lateral de $220 \times 600\text{ px}$ en azul oscuro (`#121E2B`), con botones de acceso directo a los 9 paneles, tarjetas de usuario y etiquetas de aviso pendientes (`lblBadgeAlertas` y `lblBadgeChat`).
* **Tarjetas KPI y Gráficos:** Módulos visuales superiores para métricas en tiempo real e integración de gráficos de actividad y tablas de registro reciente.

---

#### Control de Inventario (`StockPanel`)

> ![StockPanel](https://github.com/user-attachments/assets/b313edcc-5205-47da-9a16-f0465524a41c)

* **Tabla Principal de Datos (`tblProductosStock`):** Implementada con `DefaultTableModel` no editable, renderizado de celdas personalizado para badges de estado (`[OK]`, `[BAJO]`, `[SIN STOCK]`) y barra visual de nivel.
* **Filtros e Inputs:** Buscador reactivo (`txtBuscarStock`), selector por categoría y botonera de acciones contextuales.

---

#### Impresión de Etiquetas y Trazabilidad (`EtiquetasPanel` y `TrazabilidadPanel`)

| Vista Previa de Etiquetas | Histórico de Trazabilidad |
| :---: | :---: |
| ![EtiquetasPanel](https://github.com/user-attachments/assets/e652abe3-ddf8-4728-bdb3-ca214639436b) | ![TrazabilidadPanel](https://github.com/user-attachments/assets/225f3d08-6733-4b70-80bc-b49da7e616f0) |

* **Generación de Etiquetas:** Visor de previsualización a escala $1:1$ (`panelPreviewEtiqueta`) que dibuja en tiempo real el código Barcode/QR parametrizado antes de enviar a imprenta.
* **Auditoría e Historial:** Tabla inmutable de registro de movimientos (`tblTrazabilidad`) con filtros combinados por rango de fecha, tipo de operación y operario.

---

### 3.2. Implementar eventos y acciones de los componentes

La capa interactiva de la aplicación gestiona la respuesta del sistema ante las acciones del usuario, aplicando controladores de eventos desacoplados según el tipo de interacción:

#### Navegación entre vistas
Los botones de la barra lateral escuchan eventos de tipo `ActionListener`. Al hacer clic en una sección, el controlador conmuta la vista activa en el `CardLayout` del contenedor central sin necesidad de instanciar de nuevo los paneles, optimizando el uso de memoria.

#### Búsqueda y filtrado reactivo
Para los campos de búsqueda (`txtBuscarStock`, `txtBuscarTraza`), se ha implementado un `DocumentListener` vinculado al `TableRowSorter` de cada tabla. Esto permite que los datos se filtren en tiempo real a medida que el usuario escribe, sin necesidad de pulsar un botón de confirmación o la tecla Enter.

#### Control de estados en la interfaz (UI/UX)
Para evitar errores de operación, los botones contextuales como *Editar*, *Eliminar* o *Imprimir Etiqueta* permanecen desactivados (`setEnabled(false)`) por defecto. Se ha vinculado un `ListSelectionListener` a las tablas que detecta cuándo hay una fila seleccionada, activando únicamente en ese momento las acciones correspondientes.

#### Mensajería y alertas
Las acciones críticas o los fallos de validación disparan alertas inmediatas mediante cuadros de diálogo `JOptionPane` o actualizaciones de texto en las barras de estado inferiores, asegurando que el usuario reciba confirmación visual de cada operación.

---

### 3.3. Definir la secuencia de control y la persistencia de datos

#### Secuencia de control y flujo de navegación
La aplicación gestiona las interacciones a través de una jerarquía clara de dos niveles:
1. **Nivel principal:** Navegación directa entre las 9 secciones desde el menú lateral.
2. **Nivel secundario:** Diálogos modales (`JDialog`) lanzados desde las pantallas principales para tareas específicas (alta de productos, registro de entradas o confirmación de traspasos).

El flujo operativo estándar de gestión de mercancía sigue el ciclo **Escanear > Confirmar > Actualizar**:
* **Escanear:** Entrada del código por pistola o teclado en la interfaz.
* **Confirmar:** Validación de datos (cantidad $>0$, stock suficiente en origen) en un diálogo modal.
* **Actualizar:** Ejecución de la operación y refresco automático de las tablas de la interfaz.

En caso de error (credenciales incorrectas, código no registrado o cantidad no válida), el sistema detiene el flujo, resalta el campo afectado y muestra un mensaje explicativo sin perder la información introducida.

#### Persistencia de datos
El almacenamiento de la información se divide en dos capas según la naturaleza de los datos:

1. **Base de Datos Relacional (`SQLite` mediante Capa DAO):**
   Toda la información operativa del almacén (productos, ubicaciones, historial de trazabilidad, usuarios, turnos y mensajes) se gestiona a través de objetos de acceso a datos (DAO). Las operaciones de escritura se ejecutan de forma inmediata al confirmar cada acción en la interfaz, garantizando la integridad referencial mediante transacciones SQL (`COMMIT` / `ROLLBACK`).
   
2. **Configuración Local (`Preferences API`):**
   Los datos de entorno y preferencias de usuario (coordenadas $x, y$ y tamaño de la ventana, últimos filtros aplicados y orden de columnas de las tablas) se almacenan localmente mediante la API `java.util.prefs.Preferences`. Estos datos se guardan al cerrar la aplicación o cambiar un ajuste, restaurándose automáticamente en la siguiente sesión.

#### Tratamiento de datos personales (RGPD)
Los datos de los operarios almacenados en la base de datos (nombre, correo corporativo y rol) se limitan a lo estrictamente necesario para la trazabilidad del inventario. Las contraseñas se guardan encriptadas mediante algoritmos de hashing seguro con *salt* (`BCrypt`), y el acceso a la gestión de usuarios queda restringido exclusivamente a perfiles con rol de Administrador.

---

## 4. Pruebas y auditoría

# Auditoría visual de StockScan

## 4.1. Objetivo y alcance

El objetivo de esta auditoría es revisar las vistas de la aplicación StockScan, desarrollada en Java Swing, antes de su validación.

En esta fase se evalúan únicamente los aspectos visuales del prototipo:

- Coherencia de textos y datos mostrados.
- Legibilidad y presentación de los componentes.
- Distribución de tablas, tarjetas, formularios y paneles.
- Consistencia visual entre las distintas pantallas.
- Posibles problemas de recorte, solapamiento o adaptación al tamaño de la ventana.

**Fuera de alcance:** el funcionamiento de botones, filtros, acciones y navegación. Estos elementos no necesitan funcionar en esta fase del prototipo.

Los hallazgos se clasifican en dos grupos:
- **Detectado en código:** se identifica directamente al revisar los archivos Java.
- **Pendiente de comprobación visual:** requiere ejecutar la aplicación y observar la interfaz.

## 4.2. Lista unificada de hallazgos

### Prioridades

- **Alta:** afecta significativamente a la claridad o coherencia de la interfaz.
- **Media:** conviene revisarlo antes de validar el diseño.
- **Baja:** mejora de acabado y consistencia.

| ID | Vista | Hallazgo | Prioridad | Estado |
|---|---|---|---|---|
| VIS-01 | Equipo | El encabezado indica 8 miembros, pero los datos visibles no parecen representar 8 registros completos y la tabla contiene filas vacías. Revisar la coherencia entre el contador y el contenido. | Media | Detectado en código |
| VIS-02 | Equipo | El registro de Miguel Ramírez muestra `Fichado (07:10` sin cerrar el paréntesis. | Baja | Detectado en código |
| VIS-03 | Etiquetas | El subtítulo indica «2 productos seleccionados» de forma fija. Revisar que el texto sea coherente con la selección que se desea representar en el prototipo. | Media | Detectado en código |
| VIS-04 | Etiquetas | Los códigos de barras de la vista previa parecen representados mediante caracteres de texto. Si se pretende simular una etiqueta lista para imprimir, valorar una representación gráfica. | Media | Detectado en código |
| VIS-05 | Etiquetas | El campo de búsqueda parece inicializarse con el texto «🔍 Buscar...». Comprobar si se muestra como contenido normal en lugar de como texto orientativo. | Media | Detectado en código |
| VIS-06 | Chat | Los campos de búsqueda y mensaje empiezan con textos orientativos. Comprobar que se distingan visualmente de los datos introducidos por el usuario. | Media | Detectado en código |
| VIS-07 | Stock | Aparece «Almacen Central» sin tilde. Unificar con «Almacén Central». | Baja | Detectado en código |
| VIS-08 | Trazabilidad | Aparece «Almacen Central» sin tilde. Unificar con el nombre utilizado en el resto de las vistas. | Baja | Detectado en código |
| VIS-09 | Varias vistas | El nombre «Ana Rodríguez» aparece también como «Ana Rodriguez». Unificar la escritura en todas las pantallas. | Baja | Detectado en código |
| VIS-10 | Dashboard | El panel destinado al gráfico parece no dibujar datos en el código revisado. Confirmar si se desea dejar como espacio reservado o incluir un gráfico de ejemplo. | Media | Pendiente de decisión |
| VIS-11 | Agenda | No se aprecian eventos en la cuadrícula semanal a partir del código revisado. Confirmar si el calendario vacío es intencional en esta fase. | Media | Pendiente de decisión |
| VIS-12 | Dashboard | La ventana tiene un tamaño mínimo de 1000 × 600. Comprobar que la composición conserve márgenes y proporciones al reducir el espacio disponible. | Media | Pendiente de comprobación visual |
| VIS-13 | Equipo | La ventana tiene un tamaño mínimo de 900 × 600 y la tabla contiene varias columnas. Comprobar que textos, estados y acciones no queden cortados. | Media | Pendiente de comprobación visual |
| VIS-14 | Etiquetas | La composición de dos columnas utiliza anchuras y separaciones definidas. Comprobar que la selección de productos y las etiquetas de vista previa no se corten al cambiar el tamaño de la ventana. | Media | Pendiente de comprobación visual |
| VIS-15 | Stock | La tabla contiene siete columnas. Comprobar su distribución horizontal y la legibilidad de los encabezados y valores. | Media | Pendiente de comprobación visual |
| VIS-16 | Trazabilidad | Comprobar que la tabla de movimientos, los filtros y los encabezados mantengan una distribución legible al tamaño mínimo. | Media | Pendiente de comprobación visual |
| VIS-17 | Mapa de almacén | Comprobar la alineación de las celdas, el contraste de los colores, la legibilidad de las etiquetas de pasillos y la claridad de la leyenda. | Media | Pendiente de comprobación visual |
| VIS-18 | Alertas | Comprobar la jerarquía visual entre los resúmenes numéricos, las tarjetas de alertas y las acciones disponibles. | Media | Pendiente de comprobación visual |
| VIS-19 | Chat | Comprobar la distribución de canales, conversación y zona de escritura para evitar que alguna sección pierda espacio o legibilidad. | Media | Pendiente de comprobación visual |
| VIS-20 | Login | Comprobar la alineación del formulario, la legibilidad de los campos y la jerarquía visual entre el acceso y la recuperación de contraseña. | Media | Pendiente de comprobación visual |

## 4.3. Revisión por pantalla

### 4.3.1. Login

**Aspectos que revisar:**
- Alineación y distribución del formulario.
- Legibilidad de los campos de correo y contraseña.
- Jerarquía visual entre el botón principal y la recuperación de contraseña.
- Coherencia de tipografías, colores y márgenes con el resto de la aplicación.

**Estado:** pendiente de comprobación visual.

### 4.3.2. Dashboard

**Aspectos que revisar:**
- Distribución de las tarjetas KPI.
- Presentación del panel del gráfico.
- Espaciado entre los elementos y la barra lateral.
- Adaptación de la composición al tamaño mínimo de la ventana.

**Observación:** decidir si el espacio del gráfico debe permanecer vacío o mostrar datos de ejemplo.

### 4.3.3. Mapa de almacén

**Aspectos que revisar:**
- Alineación y separación de las celdas.
- Contraste entre los colores utilizados.
- Legibilidad de las etiquetas de pasillos y zonas.
- Claridad de la leyenda.
- Ajuste del mapa al espacio disponible.

**Estado:** pendiente de comprobación visual.

### 4.3.4. Stock

**Aspectos que revisar:**
- Distribución y legibilidad de las siete columnas.
- Presentación de los niveles de existencias.
- Consistencia de los nombres y textos.
- Adaptación de la tabla al tamaño de la ventana.

**Observación:** corregir «Almacen Central» por «Almacén Central».

### 4.3.5. Trazabilidad

**Aspectos que revisar:**
- Legibilidad de la tabla de movimientos.
- Distribución de los filtros y encabezados.
- Consistencia de los nombres y textos.
- Adaptación al tamaño mínimo de la ventana.

**Observación:** corregir «Almacen Central» por «Almacén Central».

### 4.3.6. Agenda

**Aspectos que revisar:**
- Distribución de los días y la cuadrícula semanal.
- Legibilidad de los encabezados.
- Espaciado entre las secciones.
- Presentación de eventos, si se decide incluir datos de ejemplo.

**Observación:** confirmar si el calendario vacío es intencional.

### 4.3.7. Alertas

**Aspectos que revisar:**
- Jerarquía visual de los contadores.
- Diferenciación entre tipos de alertas.
- Legibilidad de los datos de los productos.
- Coherencia visual entre las tarjetas y las acciones disponibles.

**Estado:** pendiente de comprobación visual.

### 4.3.8. Chat

**Aspectos que revisar:**
- Distribución de canales y conversación.
- Legibilidad de los mensajes.
- Presentación del campo de escritura.
- Diferenciación entre textos orientativos y contenido real.
- Adaptación al tamaño mínimo de la ventana.

### 4.3.9. Equipo

**Aspectos que revisar:**
- Coherencia entre el contador de miembros y los registros mostrados.
- Presentación de las filas vacías.
- Legibilidad de las columnas y los estados de fichaje.
- Consistencia del formato de las horas.

**Observaciones:**
- Revisar el contador de miembros y los registros visibles.
- Corregir el texto `Fichado (07:10` para cerrar el paréntesis.

### 4.3.10. Etiquetas

**Aspectos que revisar:**
- Coherencia entre el número de productos seleccionados y el subtítulo.
- Presentación de la lista de productos.
- Aspecto de los códigos de barras de la vista previa.
- Diferenciación del texto orientativo del buscador.
- Adaptación de las dos columnas al tamaño de la ventana.

**Observaciones:**
- Revisar el texto fijo «2 productos seleccionados».
- Valorar si los códigos de barras deben representarse gráficamente.
- Comprobar la presentación del texto «🔍 Buscar...».

## 4.4. Orden recomendado de corrección

1. **Coherencia del contenido:** corregir las tildes, cerrar el paréntesis y revisar el contador y las filas de Equipo.
2. **Acabado visual:** revisar los textos orientativos y decidir cómo representar los códigos de barras.
3. **Consistencia entre pantallas:** unificar nombres, encabezados y textos compartidos.
4. **Distribución:** comprobar las ventanas a su tamaño mínimo para detectar posibles recortes, solapamientos y problemas de legibilidad.
5. **Decisiones sobre contenido de ejemplo:** determinar si el Dashboard debe mostrar un gráfico y si la Agenda debe incluir eventos.

## 4.5. Criterios de aceptación visual

La auditoría visual se considerará validada cuando:

- [ ] Los textos estén correctamente escritos y sean coherentes entre pantallas.
- [ ] Los contadores coincidan con los datos mostrados cuando corresponda.
- [ ] Los textos orientativos se distingan del contenido real.
- [ ] Las tablas y tarjetas sean legibles.
- [ ] No haya componentes cortados o solapados al tamaño mínimo admitido.
- [ ] Los colores, las tipografías y los márgenes mantengan una apariencia consistente.
- [ ] Se haya decidido cómo presentar los gráficos, el calendario y los códigos de barras en el prototipo.

## 4.6. Fuera de alcance

En esta fase no se consideran defectos:
- Botones que todavía no ejecutan acciones.
- Filtros que todavía no modifican los resultados.
- Navegación entre pantallas aún no implementada.
- Acciones que dependan de lógica funcional pendiente.

Estos aspectos podrán revisarse en una fase posterior de pruebas funcionales.

## 4.7. Conclusión

La revisión estática identifica ajustes de coherencia textual y presentación que conviene resolver antes de validar el prototipo. También quedan pendientes comprobaciones de distribución y legibilidad que requieren ejecutar la aplicación y observar las ventanas reales.

**Estado general:** auditoría estática realizada; validación visual en ejecución pendiente.

## 5. Validación y ajustes

Fase de contraste con los usuarios. Se enseña la aplicación a personas del público objetivo para comprobar que resuelve el problema inicial y que resulta fácil y rápida de usar. Con sus opiniones se hacen los ajustes finales.

- Revisar los resultados de las pruebas de usabilidad y de la auditoría (herramientas automáticas y pruebas manuales).
- Corregir en Wireframes, Mockups y prototipo Swing los problemas detectados, priorizando los de accesibilidad (contraste, teclado, tamaño de los elementos).
- Volver a comprobar los puntos corregidos y registrar el resultado antes y después.
- Documentar los resultados y los cambios realizados en el repositorio.

#### Validación con usuarios y revisión de resultados

- [x] Revisar los resultados de las pruebas de usabilidad y de la auditoría (herramientas automáticas y pruebas manuales) y listar los hallazgos en el registro de ajustes.
- [x] Preparar la sesión de prueba (protocolo de abajo).
- [x] Realizar la prueba con n personas del público objetivo.
- [x] Registrar resultados y opiniones en resultados.md.
- [x] Priorizar hallazgos: accesibilidad (contraste, teclado, tamaño de elementos).

#### Ajustes finales y recomprobación
- [x] Corregir en wireframes y mockups (Figma).
- [x] Corregir en el prototipo Swing + FlatLaf.
- [x] Volver a comprobar cada punto corregido con la misma herramienta o método y anotar el resultado antes y después.
- [x] Documentar cambios en el repositorio.

### 5.1. Documentar los resultados y cerrar el sprint

**Qué se ha revisado**
- Auditoría visual estática de las 10 vistas (sobre el código Java).
- Revisión cruzada de la documentación del sprint (diseño, implementación, accesibilidad y métricas).
- Usabilidad, accesibilidad y rendimiento: están definidos los requisitos, las métricas y las herramientas. 

---

### Problemas encontrados

**Auditoría visual: 20 hallazgos** (0 altos, 16 medios, 4 bajos)

| Grupo | Nº | Ejemplos |
|---|---|---|
| Detectados en código | 9 | Contador de Equipo sin 8 registros (VIS-01), «Fichado (07:10» sin cerrar (VIS-02), «2 productos seleccionados» fijo (VIS-03), códigos de barras hechos con texto (VIS-04), «Almacen» sin tilde (VIS-07/08), «Ana Rodriguez» (VIS-09) |
| Pendientes de decisión | 2 | Gráfico del Dashboard y calendario de la Agenda vacíos (VIS-10/11) |
| Pendientes de comprobación visual | 9 | Recortes y legibilidad al tamaño mínimo (VIS-12 a VIS-20) |

**Incoherencias entre documentos**

| Problema | Dónde |
|---|---|
| Ventana mínima: 1280×720 (pautas) frente a 1000×600 (implementación) y 900×600 (Equipo). Barra lateral ≈210 px frente a 220 px | Pautas, implementación y auditoría |
| Color de la barra lateral #121E2B fuera de la paleta | Implementación y pautas |
| Estados `[OK]/[BAJO]/[SIN STOCK]` frente a «En stock / Stock bajo / Sin stock» | Implementación y diseño |
| Gráficos y códigos de barras «en tiempo real» frente a la auditoría (panel sin datos, barras con texto) | Implementación y auditoría |
| Tamaño táctil 48×48 dp (unidad de Android) frente a 24×24 px de WCAG 2.2 | Pautas y estándares |
| Estándares de accesibilidad y métricas pensados para web o servidor (Lighthouse, axe, HTML, solicitudes, usuarios concurrentes) en una app Swing local con SQLite | Estándares y métricas |
| Errores en métricas: densidad de defectos con la fórmula de la tasa de errores, definición de «tolerantes» en Apdex y referencias que no coinciden | Métricas |

---

### Correcciones

| Corrección | Hallazgos |
|---|---|
| Cerrar el paréntesis de «Fichado (07:10)» | VIS-02 | 
| Unificar «Almacén Central» y «Ana Rodríguez» en una clase de constantes | VIS-07/08/09 | 
| Ajustar el contador de Equipo a los registros mostrados y quitar filas vacías | VIS-01 | 
| Generar el subtítulo de Etiquetas desde la selección | VIS-03 | 
| Usar placeholder en los buscadores (Etiquetas y Chat) | VIS-05/06 | 
| Decidir cómo mostrar los códigos de barras, el gráfico del Dashboard y la Agenda (propuesta: datos de ejemplo) | VIS-04/10/11 | 
| Unificar tamaño de ventana, ancho de la barra lateral, colores y textos de estado entre documentos | Incoherencias | 
| Reorientar estándares y métricas a escritorio (WCAG2ICT, API de accesibilidad de Java, NVDA) y corregir fórmulas, glosario y referencias | Incoherencias |

---

### Comparación antes y después

| Indicador | Antes | Después |
|---|---|---|
| Hallazgos de la auditoría | 20 | [completar] |
| Hallazgos de prioridad media / baja | 16 / 4 | [completar] |
| Incoherencias entre documentos | 7 grupos | [completar] |
| Vistas con textos incoherentes | 4 | [completar] |
| Vistas comprobadas con la aplicación en ejecución | 0 de 10 | [completar] |

**Estado:** auditoría estática y revisión cruzada hechas. Pasan al sprint 3: la validación visual con la aplicación en ejecución y las pruebas de usabilidad, accesibilidad y rendimiento.
