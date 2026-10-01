# Gestión de eventos y listeners · Java Swing (NetBeans)

> Documentación de cómo se conecta la capa de presentación (**Vista**) con los **controladores** mediante listeners en SCAN ALMACÉN, y cómo mantener limpio el código que genera el GUI Builder de NetBeans.

| | |
|---|---|
| **Prototipo de referencia** | StockScan SGA Interface Design |
| **Tecnología** | Java + Swing + NetBeans (Form Editor) |
| **Patrón** | Vista - Controlador - Modelo |

---

## Objetivo

1. Que la **Vista** solo se encargue de mostrar y exponer sus componentes.
2. Que los **controladores** registren los listeners y decidan qué hacer ante cada acción del usuario.
3. Que el código autogenerado por NetBeans no se mezcle con la lógica de la aplicación.

---

## Arquitectura y flujo de eventos

| Paquete | Contenido |
|---|---|
| `vista` | JFrame / JPanel creados con el Form Editor de NetBeans |
| `controlador` | Un controlador por pantalla (registra los listeners) |
| `modelo` | Clases de datos y servicios (Producto, Operario, Movimiento...) |

### Flujo de un evento

**Usuario pulsa botón → Listener → Controlador → Modelo → Controlador actualiza la Vista**

### Reparto de responsabilidades

| Capa | Hace | No hace |
|---|---|---|
| **Vista** | Mostrar datos y exponer métodos (obtener el correo, mostrar un error, registrar un listener) | Lógica de negocio |
| **Controlador** | Registrar listeners, validar y decidir qué ocurre | Crear componentes gráficos |
| **Modelo** | Datos y reglas del almacén | Conocer la interfaz |

---

## Código generado por NetBeans (GUI Builder)

El Form Editor genera en cada vista un bloque protegido, el método `initComponents()`, delimitado por las marcas `//GEN-BEGIN:initComponents` y `//GEN-END:initComponents`.

### Reglas del equipo

- ❌ **No editar** nada entre `//GEN-BEGIN` y `//GEN-END`: NetBeans lo regenera y se pierden los cambios.
- ✅ Componentes `private` con prefijo: `btnIniciarSesion`, `txtCorreo`, `pwdContrasena`, `tblStock`, `chkProducto`.
- ✅ La personalización propia va en el constructor, **después de `initComponents()`**.
- ✅ Sin lógica de negocio en los métodos `...ActionPerformed` que crea el Form Editor.

### Dos formas de enlazar eventos

| Opción | Cómo | Cuándo |
|---|---|---|
| **A. Registro desde el controlador** (recomendada) | La vista ofrece métodos `addXxxListener(...)` y el controlador los usa | Pantallas con lógica: login, stock, alertas, chat |
| **B. Handler del Form Editor** | Clic derecho en el componente > Events > Action > actionPerformed | Solo acciones triviales de la propia vista |

Si se usa la opción B, el handler se limita a **delegar** en el controlador, sin contener lógica propia.

---

## Ejemplo: pantalla de Login

### Reparto por capas

| Capa | Clase | Responsabilidad |
|---|---|---|
| **Vista** | `LoginView` | Muestra el formulario. Expone el correo, la contraseña y los métodos para registrar listeners y mostrar errores |
| **Controlador** | `LoginController` | Registra los listeners, valida los datos y decide qué pantalla se abre |
| **Modelo** | `AuthService` | Comprueba las credenciales |

### Flujo paso a paso

1. Al arrancar, se crea la vista, se crea el controlador pasándole la vista y se muestra la ventana.
2. El controlador **registra los listeners** a través de los métodos que ofrece la vista.
3. El usuario escribe su correo y contraseña y pulsa **Iniciar sesión** (o pulsa Enter en la contraseña).
4. El controlador lee los datos de la vista y comprueba que no estén vacíos.
5. Si faltan datos, pide a la vista que muestre un mensaje de error.
6. Si están completos, consulta al modelo si las credenciales son correctas.
7. Si son correctas, se cierra el login y se abre el panel principal. Si no, se muestra "Credenciales incorrectas".
8. Al terminar, se borra la contraseña de memoria.

### Eventos de la pantalla

| Componente | Listener | Resultado |
|---|---|---|
| Botón *Iniciar sesión* | `ActionListener` | Inicia el proceso de validación |
| Campo contraseña (Enter) | `ActionListener` | Mismo efecto que el botón |
| Texto *¿Olvidaste tu contraseña?* | `MouseListener` | Abre la recuperación de contraseña |

### Puntos clave

- La vista **no decide** nada: solo informa de lo que ocurre y muestra lo que el controlador le pide.
- El controlador nunca crea componentes gráficos.
- El arranque de la interfaz se hace siempre con `EventQueue.invokeLater`.

---

## Mapa de eventos por pantalla (según el prototipo)

| Pantalla | Componente | Listener | Acción del controlador |
|---|---|---|---|
| **Login** | *Iniciar sesión* / Enter en contraseña | `ActionListener` | Validar credenciales y abrir el panel |
| | *¿Olvidaste tu contraseña?* | `MouseListener` | Abrir recuperación |
| **Menú lateral** | Dashboard, Mapa, Stock, Etiquetas, Trazabilidad, Alertas, Equipo, Agenda, Chat | `ActionListener` | Cambiar el panel (`CardLayout`) |
| **Dashboard** | Pestañas *Día / Semana / Mes* | `ActionListener` | Recargar gráfica de actividad |
| **Mapa de almacén** | Clic en una estantería | `MouseListener` | Mostrar contenido en el panel *Resumen* |
| **Stock** | Búsqueda por nombre o código | `DocumentListener` | Filtrar la tabla al escribir |
| | Filtros de categoría y estado | `ActionListener` | Aplicar filtro a la tabla |
| | *Añadir producto* / *Editar* | `ActionListener` | Abrir diálogo de alta/edición |
| **Etiquetas** | Casillas de producto | `ItemListener` | Añadir/quitar etiqueta de la vista previa |
| | *Quitar* | `ActionListener` | Eliminar la etiqueta |
| | *Exportar PDF* | `ActionListener` | Generar el PDF |
| **Trazabilidad** | Operario, tipo de movimiento, fecha | `ActionListener` / `PropertyChangeListener` | Filtrar movimientos |
| **Alertas** | *Generar pedido* / *Notificar* | `ActionListener` | Crear pedido / avisar al responsable |
| | *Generar pedido múltiple* | `ActionListener` | Pedido con todas las alertas |
| **Equipo** | *Añadir operario*, *Ver*, *Editar* | `ActionListener` | Diálogos de operario |
| **Agenda** | *← Anterior*, *Hoy*, *Siguiente →* | `ActionListener` | Cambiar la semana mostrada |
| **Chat** | Botón enviar / Enter | `ActionListener` | Enviar mensaje y limpiar el campo |
| | Canales y mensajes directos | `ListSelectionListener` | Cargar la conversación |

---

## Listeners habituales y cuándo usarlos

| Listener | Se dispara cuando... | Dónde lo usamos |
|---|---|---|
| `ActionListener` | Se pulsa un botón o Enter en un campo de texto | Botones de todas las pantallas, envío de mensajes en el chat |
| `DocumentListener` | Cambia el texto de un campo (al escribir o borrar) | Búsqueda en tiempo real en Stock |
| `ItemListener` | Se marca o desmarca una casilla | Selección de productos en Etiquetas |
| `MouseListener` | Se hace clic sobre un componente | Estanterías del mapa, enlace de recuperar contraseña |
| `ListSelectionListener` | Cambia la selección de una lista o tabla | Canales y mensajes directos del chat |
| `PropertyChangeListener` | Cambia una propiedad del componente | Selector de fecha en Trazabilidad |

### Cómo funcionan los casos más importantes

- **Búsqueda en Stock:** cada vez que cambia el texto, el controlador lee lo escrito y aplica un filtro sobre la tabla. Si el campo queda vacío, se quita el filtro y se muestran todos los productos.
- **Navegación de la Agenda:** *Anterior* y *Siguiente* desplazan la semana mostrada, y *Hoy* vuelve a la semana actual.
- **Etiquetas:** al marcar una casilla, el producto se añade a la vista previa; al desmarcarla, se quita.
- **Chat:** al enviar, se ignoran los mensajes vacíos; si hay texto, se envía al canal activo y se limpia el campo.

---

## Buenas prácticas y comprobaciones

- Un **controlador por pantalla**; el menú lateral solo cambia de panel.
- Los componentes de la vista son `private` y la vista ofrece métodos con significado, no los componentes completos.
- Nada de lógica de negocio en los métodos `...ActionPerformed` que genera el Form Editor: solo delegan en el controlador.
- La personalización propia de la vista va en el constructor, después de `initComponents()`.
- Las tareas lentas (base de datos, exportar PDF) se ejecutan fuera del *Event Dispatch Thread* con `SwingWorker` para que la interfaz no se congele.
- Nombres coherentes: `btnXxx`, `txtXxx`, `pwdXxx`, `tblXxx`, `chkXxx`.
