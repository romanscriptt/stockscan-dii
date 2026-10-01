# Documentación de arquitectura y análisis del prototipo

## 1. Selección del patrón MVC y arquitectura general

Para el desarrollo de **SCAN ALMACÉN** se ha seleccionado el patrón de arquitectura **MVC (Modelo - Vista - Controlador)**, ya que permite separar claramente la interfaz gráfica, la lógica de negocio y la gestión de eventos.

La arquitectura propuesta se divide en:

- **Modelo:** representa los datos y entidades del sistema.
- **Vista:** contiene las interfaces desarrolladas mediante Java Swing.
- **Controlador:** recibe las acciones del usuario y coordina las operaciones.
- **Servicios:** contienen la lógica de negocio.
- **Repositorio:** gestiona el acceso y persistencia de los datos.

El flujo general será:

```text
Usuario
   ↓
Vista Swing
   ↓
Controlador
   ↓
Servicio
   ↓
Modelo / Repositorio
   ↓
Base de datos
```

Esta separación permitirá reducir el acoplamiento entre componentes y facilitar el mantenimiento y ampliación del sistema.

---

## 2. Análisis general de las interfaces del prototipo

A partir del prototipo **StockScan SGA Interface Design**, se han identificado las principales funcionalidades que deberá incorporar la aplicación.

Entre las pantallas analizadas se encuentran:

- Inicio de sesión.
- Dashboard principal.
- Mapa del almacén.
- Gestión de stock.
- Gestión de etiquetas.
- Trazabilidad.
- Alertas de stock.
- Gestión del equipo.
- Agenda de turnos.
- Comunicación mediante chat.

La mayoría de las pantallas comparten una estructura visual formada por una cabecera, un menú lateral y un área central de contenido.

En Java Swing se propone utilizar un `MainFrame` como ventana principal y diferentes paneles para representar cada funcionalidad:

```text
MainFrame
├── Sidebar
├── Header
└── ContentPanel
    ├── DashboardPanel
    ├── MapaAlmacenPanel
    ├── StockPanel
    ├── EtiquetasPanel
    ├── TrazabilidadPanel
    ├── AlertasPanel
    ├── EquipoPanel
    ├── AgendaPanel
    └── ChatPanel
```

La navegación entre los diferentes paneles podrá gestionarse mediante `CardLayout`, evitando crear una ventana independiente para cada funcionalidad.

---

## 3. Gestión del inventario, almacén y trazabilidad

Una de las funcionalidades principales del sistema será la gestión del inventario y de las ubicaciones del almacén.

La pantalla de stock deberá permitir consultar información como:

- Código del producto.
- Nombre.
- Categoría.
- Ubicación.
- Stock actual.
- Stock mínimo.
- Nivel de stock.
- Disponibilidad.

Para representar esta información se proponen diferentes entidades dentro del modelo:

```text
Producto
Categoría
Stock
Ubicación
Almacén
Pasillo
Estantería
```

La estructura física del almacén podrá representarse mediante la siguiente jerarquía:

```text
Almacén
└── Pasillo
    └── Estantería
        └── Ubicación
            └── Stock
```

También será necesario implementar la trazabilidad de los movimientos realizados sobre los productos. Para ello se propone una entidad `MovimientoStock`, que almacene información como:

- Fecha y hora.
- Operario responsable.
- Tipo de movimiento.
- Producto afectado.
- Ubicación de origen.
- Ubicación de destino.
- Cantidad.

Los principales tipos de movimiento podrán ser:

```text
Entrada
Salida
Picking
Traspaso
Ajuste
```

De esta forma será posible conocer el historial de movimientos de cada producto y mantener un control sobre las operaciones realizadas en el almacén.

---

## 4. Alertas, pedidos y gestión del equipo

El sistema deberá disponer de un módulo de alertas que permita detectar situaciones relacionadas con el nivel de stock.

Inicialmente se plantean las siguientes reglas:

```text
Stock actual = 0
        ↓
   SIN STOCK

Stock actual < Stock mínimo
        ↓
   STOCK BAJO
```

Desde la pantalla de alertas se podrán realizar acciones como:

- Generar un pedido.
- Gestionar varios pedidos.
- Consultar productos afectados.
- Notificar la incidencia correspondiente.

La comunicación entre los diferentes componentes podrá seguir el siguiente flujo:

```text
AlertasController
        ↓
PedidoService
        ↓
PedidoRepository
```

Además, el prototipo incluye una sección destinada a la gestión del equipo de trabajo.

Se contemplan diferentes roles:

```text
Administrador
Supervisor
Operario
```

Y diferentes estados de los trabajadores:

```text
Activo
Fichado
Inactivo
```

Los permisos de cada usuario deberán controlarse desde la lógica de la aplicación y no únicamente mediante la visibilidad de determinados elementos de la interfaz.

---

## 5. Agenda, etiquetas y comunicación interna

El sistema también deberá gestionar los turnos de trabajo de los operarios mediante una agenda.

Como propuesta inicial, los turnos pueden organizarse de la siguiente manera:

```text
Mañana → 08:00 - 16:00
Tarde  → 14:00 - 22:00
Noche  → 22:00 - 06:00
```

Para representar esta funcionalidad se propone una entidad `AsignacionTurno`, relacionada con:

- Operario.
- Fecha.
- Turno.
- Pedido asociado.

Otra funcionalidad identificada en el prototipo es la generación de etiquetas.

El flujo de esta funcionalidad podría ser:

```text
EtiquetasPanel
      ↓
EtiquetaController
      ↓
EtiquetaService
      ↓
PdfGenerator / BarcodeGenerator
```

La interfaz permitirá seleccionar un producto, generar una previsualización de la etiqueta y posteriormente exportarla a PDF.

Finalmente, el prototipo incluye una funcionalidad de comunicación interna mediante chat.

Para esta parte se plantean entidades como:

```text
Usuario
Canal
Mensaje
Conversacion
Notificacion
```

Estas funcionalidades estarán separadas de la interfaz mediante sus correspondientes controladores y servicios, siguiendo la arquitectura MVC.

---

## 6. Estructura final propuesta y conclusiones

A partir del análisis realizado, se propone organizar el proyecto **SCAN ALMACÉN** mediante una estructura de paquetes que mantenga separadas las responsabilidades de cada componente:

```text
scanalmacen/
├── model/
├── view/
├── controller/
├── service/
├── repository/
└── util/
```

Dentro de `model` se podrán incluir entidades como:

```text
Producto
Ubicacion
MovimientoStock
Operador
Pedido
AlertaStock
Turno
```

En `view` se encontrarán las interfaces Java Swing:

```text
LoginFrame
MainFrame
DashboardPanel
StockPanel
MapaAlmacenPanel
EtiquetasPanel
TrazabilidadPanel
AlertasPanel
EquipoPanel
AgendaPanel
ChatPanel
```

Los controladores gestionarán las acciones realizadas desde las vistas, mientras que los servicios contendrán la lógica de negocio y los repositorios gestionarán la persistencia de los datos.

El flujo final de la arquitectura será:

```text
Vista
  ↓
Controlador
  ↓
Servicios
  ↓
Modelo / Persistencia
```

Con esta organización se consigue una separación clara entre la interfaz gráfica, la lógica de negocio y la gestión de datos, facilitando el desarrollo, mantenimiento y futuras ampliaciones del sistema **SCAN ALMACÉN**.
