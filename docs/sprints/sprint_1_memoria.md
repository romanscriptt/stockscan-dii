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
