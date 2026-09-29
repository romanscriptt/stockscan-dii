# 3. Análisis de Mercado y Benchmarking

En esta sección se detalla el estudio comparativo realizado sobre las soluciones de software líderes en los sectores de gestión de inventario, comunicación empresarial y control de recursos humanos. El objetivo es recopilar las mejores prácticas funcionales y tecnológicas para consolidar la arquitectura de nuestra App de Almacén.

## 3.1. Matriz Comparativa de Competidores

A continuación se presenta un desglose analítico de los líderes del mercado en función de los módulos críticos que integrará nuestro proyecto:

| Criterio / Módulo | Gestión de Inventario (SGA) | Comunicación Interna | Control Horario y Tareas |
| :--- | :--- | :--- | :--- |
| **Soluciones Líderes** | Sortly / Stockagile | Slack / Microsoft Teams | Factorial / When I Work |
| **Flujo de Usuario (UX)** | - Acceso directo al escáner.<br>- Formularios con inputs grandes.<br>- Modales de edición rápida. | - Estructura de canales limpios.<br>- Notificaciones push inmediatas.<br>- Hilos de conversación organizados. | - Botón central de Check-in/out.<br>- Vista de calendario mensual.<br>- Cuadro de tareas pendientes. |
| **Tecnologías Estimadas** | React Native, Node.js, PostgreSQL, Google ML Kit (OCR). | Java/Kotlin/Swift, WebSockets, Redis, Electron. | Ruby on Rails / Node.js, MySQL, arquitecturas Cloud AWS. |
| **Principales Puntos de Dolor** | - Pérdida de datos sin conexión.<br>- Falta de integración con RRHH. | - Exceso de ruido visual.<br>- Consumo elevado de memoria RAM. | - Lentitud en accesos concurrentes.<br>- Reportes analíticos rígidos. |

## 3.2. Hallazgos Clave y Puntos de Dolor del Mercado

A través de la investigación de mercado, se han detectado tres grandes problemáticas operativas que sufren las empresas en la actualidad:
1. **La Fragmentación del Software:** Las empresas de hostelería, e-commerce y logística se ven obligadas a pagar múltiples suscripciones y a capacitar al personal en tres herramientas distintas (una app de stock, un chat y un gestor de turnos). Esto destruye la eficiencia del flujo de trabajo.
2. **El Problema de la Conectividad en Almacenes:** Las aplicaciones puramente en la nube se bloquean o no permiten registrar productos cuando el empleado se desplaza a zonas subterráneas o cámaras frigoríficas que carecen de buena cobertura Wi-Fi o móvil.
3. **Saturación por Alta Concurrencia:** Durante los relevos de turnos, las peticiones masivas en los servidores provocan retrasos críticos al registrar la entrada o salida de los operarios.

## 3.3. Conclusiones y Decisiones de Ingeniería para el Proyecto

Las conclusiones extraídas del benchmarking justifican el diseño técnico y funcional adoptado para nuestra App de Almacén:

* **Unificación de Ecosistemas (Ventaja Competitiva):** Nuestra aplicación resolverá la fragmentación centralizando los tres módulos bajo una única identidad de usuario. Al hacer check-in, la app sabe instantáneamente el rol del empleado (administrador, mozo, camarero), habilitando sus canales de chat correspondientes y su lista de inventario asignada.
* **Implementación de Arquitectura Multiplataforma:** Para emular el rendimiento y la versatilidad de los líderes del sector, se opta por un stack móvil multiplataforma (**Flutter** o **React Native**) que minimiza costes de mantenimiento de código y permite desplegar el software tanto en entornos Android como iOS rápidamente.
* **Estrategia Offline-First:** El módulo de escáner móvil funcionará de forma local mediante una base de datos embebida ligera (**SQLite / Realm**). Al realizar la lectura de stock, los datos se guardarán localmente en el dispositivo y se sincronizarán en segundo plano con el backend centralizado una vez detectada una conexión a internet estable.
* **Conexiones Síncronas Eficientes:** Para evitar la saturación del servidor y ofrecer un módulo de mensajería instantánea ágil, se utilizarán protocolos basados en eventos en tiempo real (**WebSockets**), optimizando el flujo de datos entre la gerencia y los operarios en los momentos de mayor actividad laboral.
