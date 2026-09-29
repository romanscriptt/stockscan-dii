# Análisis de Información y Planificación del Proyecto

Este documento recoge el análisis funcional, la definición de usuarios y la gestión del backlog para el sistema **StockScan (SCAN ALMACÉN)**.

---

## 1. Identificación del Público Objetivo (Issue #9)

Para garantizar una usabilidad adaptada al entorno logístico, se establecen tres arquetipos de usuario:

### 1.1. Operario de Almacén (Mozo)
* **Requisitos:** Interfaz con alto contraste visual, fuentes monospaciadas para lectura rápida de ubicaciones (`PAS-XX-EST-XX`) y confirmación al escaneo de códigos de barras en tiempo inferior a 1000 ms.
* **Puntos de dolor:** Tareas repetitivas y errores de digitación manual.

### 1.2. Supervisor de Stock
* **Requisitos:** Vista panorámica mediante Badges visuales de estado (*En stock* `#27AE60`, *Stock bajo* `#F39C12`, *Sin stock* `#E74C3C`), filtros rápidos por categoría (*Ferretería*, *Electrónica*, *EPI*, *Consumibles*) y alertas de reabastecimiento.

### 1.3. Administrador del Sistema
* **Requisitos:** Mantenimiento de catálogo y trazabilidad de operaciones.

