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

> Introducir aquí la parte de Implementación (introducción general, si procede).

### 3.1. Desarrollar componentes visuales e interactivos

> Introducir aquí la parte de desarrollo de componentes visuales e interactivos.

### 3.2. Implementar eventos y acciones de los componentes

> Introducir aquí la parte de implementación de eventos y acciones de los componentes.

### 3.3. Definir la secuencia de control y la persistencia de datos

> Introducir aquí la parte de secuencia de control y persistencia de datos.

---

## 4. Pruebas y auditoría

> Introducir aquí la parte de Pruebas y auditoría (introducción general, si procede).

### 4.1. Realizar pruebas de usabilidad y accesibilidad

> Introducir aquí la parte de pruebas de usabilidad y accesibilidad.

### 4.2. Auditar la interfaz con herramientas automáticas y pruebas manuales

> Introducir aquí la parte de auditoría de la interfaz con herramientas automáticas y pruebas manuales.

---

## 5. Validación y ajustes

> Introducir aquí la parte de Validación y ajustes (introducción general, si procede).

### 5.1. Corregir problemas detectados y validar los cambios

> Introducir aquí la parte de corrección de problemas detectados y validación de los cambios.

### 5.2. Documentar los resultados y cerrar el sprint

> Introducir aquí la parte de documentación de resultados y cierre del sprint.
