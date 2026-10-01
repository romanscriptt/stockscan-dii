# MEMORIA DE PROYECTO INTERMODULAR (MÓDULO 0492)
## Proyecto: SCAN ALMACÉN / StockScan SGA

**Componentes del Grupo:**
* **Álvaro López** 
* **Carmen Monge**
* **Elena Sáez**
* **Ángel Luis**

* **Tutor:** Willman Acosta Lugo 
* **Ciclo Formativo:** Desarrollo de Aplicaciones Multiplataforma (DAM) 
* **Fecha:** Octubre 2026
## ÍNDICE GENERAL

1. **INTRODUCCIÓN**
   - 1.1. Contexto del proyecto 
   - 1.2. Problema o necesidad detectada 
   - 1.3. Propuesta de solución 
   - 1.4. Objetivos del proyecto 
   - 1.5. Alcance y limitaciones 
2. **ANÁLISIS DEL CONTEXTO Y VIABILIDAD**
   - 2.1. Sector profesional y perfil de usuarios / User Personas 
   - 2.2. Benchmarking y soluciones existentes 
   - 2.3. Estudio de viabilidad técnica y normativa 
   - 2.4. Estudio de viabilidad económica y presupuesto inicial 
3. **PLANIFICACIÓN Y GESTIÓN DEL PROYECTO**
   - 3.1. Metodología de desarrollo y GitHub Projects 
   - 3.2. Reparto de roles y responsabilidades en el equipo 
   - 3.3. Cronograma e hitos del proyecto 
4. **ANÁLISIS DE REQUISITOS**
   - 4.1. Requisitos funcionales de la interfaz 
   - 4.2. Requisitos no funcionales y usabilidad 
   - 4.3. Matriz de trazabilidad por perfil de usuario 
5. **DISEÑO DE LA SOLUCIÓN**
   - 5.1. Objetivos principales de la interfaz UX/UI 
   - 5.2. Prototipado interactivo en Figma 
   - 5.3. Sistema de Tokens de Diseño y Paleta Cromática 
   - 5.4. Diseño de la Base de Datos y Modelo E/R 
6. **DESARROLLO E IMPLEMENTACIÓN**
   - 6.1. Evaluación técnica de librerías candidatas para Java Swing 
   - 6.2. Mapeo conceptual POO: Figma vs. Estructura Java 
   - 6.3. Implementación del Backend, Controladores y Persistencia 
7. **PRUEBAS Y ASEGURAMIENTO DE LA CALIDAD**
   - 7.1. Criterios de Aceptación y Pruebas UX/UI 
   - 7.2. Pruebas Unitarias, Integración y Sistema
8. **DESPLIEGUE Y PUESTA EN PRODUCCIÓN** 
9. **RESULTADOS Y EVALUACIÓN FINAL**
   - 9.1. Cumplimiento de objetivos del Sprint
   - 9.2. Trabajo pendiente para próximos Sprints 
10. **REFERENCIAS BIBLIOGRÁFICAS**

---

## RESUMEN EJECUTIVO

El proyecto **SCAN ALMACÉN / StockScan** es una solución informática de gestión de almacén (SGA) orientada a la optimización de procesos logísticos, reducción de errores operativos y aceleración del tiempo de aprendizaje del personal. 

Esta memoria recoge el trabajo de análisis de mercado, diseño del público objetivo, definición de los criterios de usabilidad UX/UI, maquetación interactiva en Figma, especificación de tokens de diseño, selección técnica de librerías en Java Swing (`FlatLaf`, `ZXing`, `JFreeChart`, `MigLayout`)y el mapeo conceptual hacia la Programación Orientada a Objetos (POO).

---

# 1. INTRODUCCIÓN

### 1.1. Contexto del proyecto
En el sector logístico actual y en los operadores e-commerce, la precisión del stock y la rapidez en la preparación de pedidos resultan fundamentales para mantener la competitividad operativa.

### 1.2. Problema o necesidad detectada
Según estudios del sector logístico (CSCMP), más del 65% de los errores de inventario en Startups e-commerce y almacenes de distribución se deben a interfaces de software complejas o mal adaptadas al entorno de trabajo diario.

### 1.3. Propuesta de solución
Diseñar una interfaz gráfica intuitiva, limpia y de alto contraste para **StockScan SGA**, orientada a minimizar la carga cognitiva del operario y agilizar la toma de decisiones en tareas de picking, packing y control de inventario.

### 1.4. Objetivos del proyecto
* **Objetivo General:** Definir la experiencia de usuario (UX), el sistema de diseño visual (UI) y la arquitectura de componentes Java Swing para el sistema StockScan.
* **Objetivos Específicos:**
  * Caracterizar a los usuarios finales del sistema mediante *User Personas*.
  * Maquetar el prototipo interactivo en Figma con flujos navegables y componentes estandarizados.
  * Definir la paleta cromática y tokens de diseño para su fácil traslado a código `java.awt.Color`.
  * Investigar la viabilidad de librerías para la futura interfaz gráfica en NetBeans/Java.
  * Establecer la trazabilidad POO entre las vistas visuales de Figma y las clases Java.
 
### 1.5. Alcance y limitaciones 
El alcance redactado por Álvaro López comprende el análisis de requerimientos visuales, prototipado de alta fidelidad, documentación de librerías y estructuración POO. Las capas de persistencia y servicios backend corresponden a los siguientes hitos del equipo.

---

# 2. ANÁLISIS DEL CONTEXTO Y VIABILIDAD

### 2.1. Sector profesional y perfil de usuarios
Para adecuar la herramienta al entorno operativo real, se han definido tres perfiles principales:

1. **Operario de Almacén (Perfil Operativo):**
   * **Entorno:** Terminales táctiles.
   * **Necesidades UX:** Botones de gran tamaño, lecturas rápidas mediante códigos de barras, contraste elevado y flujos simples en pocos clics.
     
2. **Supervisor / Manager de Logística (Perfil de Gestión):**
   * **Entorno:** Puesto de escritorio / PC.
   * **Necesidades UX:** Dashboard central con KPIs en tiempo real, gestión de alertas de stock mínimo y reportes tabulares.
     
3. **Administrador del Sistema (Perfil Técnico):**
   * **Entorno:** Gestión de infraestructura y usuarios.
   * **Necesidades UX:** Vistas desacopladas mediante patrón MVC, asignación de permisos y control de acceso por roles.
  
### 2.2. Benchmarking y soluciones existentes
Se investigaron marcos de trabajo y librerías modernas de interfaz gráfica para justificar la elección de layouts flexibles y temas oscuros/claros sin reescribir la base del framework Swing.

### 2.3. Estudio de viabilidad técnica y normativa

### 2.4. Estudio de viabilidad económica y presupuesto inicial

---

# 3. PLANIFICACIÓN Y GESTIÓN DEL PROYECTO

### 3.1. Metodología de desarrollo y GitHub Projects 
El seguimiento del proyecto se gestiona de forma ágil organizando el flujo de trabajo en **GitHub Projects** a través del **Sprint Backlog #16**. Las tareas se han clasificado y documentado mediante etiquetas especializadas (`design`, `documentation`, `enhancement`).

### 3.2. Reparto de roles y responsabilidades en el equipo

| Componente | Responsabilidades Principales |
| :--- | :--- |
| **Álvaro López** | Análisis de perfiles, Objetivos UI/UX , Sprint Backlog , Tokens de diseño , Librerías  y Mapeo POO. |
| **Carmen Monge** | |
| **Elena Sáez** |  |
| **Ángel** | |

### 3.3. Cronograma e hitos del proyecto

---

# 4. ANÁLISIS DE REQUISITOS

### 4.1. Requisitos funcionales de la interfaz 
* **RF-01:** Visualización limpia de stock, ubicación física y estado en menos de 2 segundos.
* **RF-02:** Flujos de interacción directa (búsqueda, filtrado e inventario) en un máximo de 3 pasos.
* **RF-03:** Notificación visual inmediata mediante códigos de color semánticos frente a acciones destructivas o errores.
  
### 4.2. Requisitos no funcionales y usabilidad 
* **RNF-01 (Usabilidad):** Diseño de bajo esfuerzo cognitivo adaptado a la fatiga visual de entornos industriales.
* **RNF-02 (Adaptabilidad):** Maquetación responsiva basada en Auto-Layout para resoluciones de monitores y tablets industriales.

### 4.3. Matriz de trazabilidad por perfil de usuario 

| Perfil de Usuario | Componentes Swing Clave | Requisito Principal UX | Impacto en el Negocio |
| :--- | :--- | :--- | :--- |
| **Operario** | `JButton` grandes, `JTextField` autofocus | Mínimos clics por acción | Reducción del 40% en tiempos de registro |
| **Supervisor** | `JTable` personalizada, `JFreeChart` | Visualización consolidada de KPIs | Prevención de roturas de stock |
| **Administrador** | `JTree` / `JTabbedPane` | Aislamiento y control de permisos | Cumplimiento de políticas de trazabilidad |

---

 5. DISEÑO DE LA SOLUCIÓN

### 5.1. Objetivos principales de la interfaz UX/UI
* **Reducción de Carga Mental:** Priorización de datos críticos eliminando distracciones visuales.
* **Prevención de Errores:** Confirmaciones claras en cuadros modales y banners de notificación cromática.
