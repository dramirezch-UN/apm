---
layout: page
title: Comunicaciones.
permalink: /producto/comunicaciones
nav:false
---

## Comunicaciones

### Definiciones

Para definir las comunicaciones usadas en el proyecto se siguieron los siguientes pasos:

1. Se definieron parámetros a los cuales se les va a hacer seguimiento.
2. Se escogieron sensores, controladores y otros componentes que se usarán para seguir estos parámetros.
3. Se consultaron catálogos, manuales y otras fuentes de referencia que proveen los fabricantes.
4. Se planeó una arquitectura de comunicaciones acorde a lo encontrado.

#### Parámetros a Monitorear

- Después de la estación de secado, se mide la **humedad** del producto. Este control es crucial para garantizar que las baldosas tengan el contenido de humedad adecuado antes de pasar a las siguientes etapas del proceso.
- Hay un punto de bifurcación en donde el material se va por una u otra banda trasportadora, dependiendo del producto que se esté fabricando. Tras este punto de bifurcación, se verifica que las piezas se encuentran en la **banda transportadora correcta.**
- Como las piezas no sufrirán cambios significativos tras salir del horno, después de esta estación se miden sus **dimensiones**. Así se garantiza que cada baldosa cumpla con las especificaciones requeridas y se identifican deformaciones.
- Finalmente, tras la estación de pulido, se verifica la **calidad superficial** de las baldosas que se fabrican con este proceso. Se utilizan sistemas avanzados de escaneo láser para detectar cualquier defecto en la superficie, asegurando así que cada producto cumpla con los estándares de calidad visual y táctil necesarios antes de ser enviado al cliente.

Estos controles de calidad se realizan utilizando sensores y sistemas de medición avanzados, que son externos a las máquinas de fabricación proporcionadas por Sacmi. Dado que Sacmi no proporciona información sobre conectividad, recolección de datos o manejo remoto, estos equipos se tratan como cajas negras. Los sensores y componentes adicionales instalados permiten recopilar y monitorear los datos necesarios para mantener la alta calidad de los productos en cada etapa del proceso de fabricación.

#### Sensores Utilizados

1. **Humedad:** Process Sensors MCT466-SF.
2. **Posición:** Keyence PZ-G.
3. **Dimensiones:** Keyence CL-3000. Los sensor heads se conectan a una unidad óptica (por ejemplo, Keyence CL-L(P)007N(G)), la cual se conecta al controlador.
4. **Calidad superficial:** Keyence LJ-V7000.

### Niveles de la Pirámide de Automatización

#### Nivel de Campo

- **Process Sensors MCT466-SF:**
  - **Propósito:** Medir la humedad después del secado.
  - **Comunicación:** El sistema que incluye el sensor tiene el controlador incorporado.

- **Sensores Keyence PZ-G:**
  - **Propósito:** Detectar que los productos estén en la banda adecuada.
  - **Comunicación:** Conexión directa al controlador Keyence CL-3000. El fabricante no especifica el protocolo utilizado, se asume que es un protocolo propietario de Keyence.

- **Sensores Confocales Keyence CL-3000:**
  - **Propósito:** Medir dimensiones de baldosas.
  - **Comunicación:** Los sensor heads se conectan a una unidad óptica Keyence CL-L(P)007N(G), que a su vez se conecta al controlador Keyence CL-3000. El fabricante no especifica el protocolo utilizado, se asume que es un protocolo propietario de Keyence.

- **Sensores Láser Keyence LJ-V7000:**
  - **Propósito:** Análisis superficial después del pulido.
  - **Comunicación:** Conexión directa al controlador Keyence LJ-V7001. El fabricante no especifica el protocolo utilizado, se asume que es un protocolo propietario de Keyence.

#### Nivel de Control

- **Controladores:**
  - **Keyence CL-3000:** Recoge y procesa datos de los sensores PZ-G y CL-3000.
  - **Keyence LJ-V7001:** Recoge y procesa datos del sensor LJ-V7000.
  - **Comunicación con Sensores:** Protocolos propietarios de Keyence a través de cables dedicados.
  - **Comunicación con el Sistema SCADA:** Ethernet (TCP/IP).

#### Nivel de Supervisión

- **Sistema SCADA (Ignition):**
  - Recibe y visualiza datos en tiempo real.
  - **Comunicación con Controladores:** Ethernet (TCP/IP).
 
#### Nivel de Planificación (MES)

**Ignition MES:** Ignition, además de ser una plataforma SCADA, ofrece módulos específicos para MES, lo que permite una integración directa y sin problemas con el sistema SCADA ya implementado.

**Conexión con SCADA/Ignition:**
- **Interfaz Directa:** Dado que Ignition ofrece módulos tanto para SCADA como para MES, la conexión es nativa y sin necesidad de interfaces adicionales.
- **Protocolo de Comunicación:** OPC UA (Open Platform Communications Unified Architecture) o TCP/IP para la transferencia de datos.
- **Acceso a Datos en Tiempo Real:** El SCADA proporciona datos en tiempo real al MES, permitiendo decisiones informadas y ajustes rápidos en la producción.

#### Nivel de Gestión (ERP)

**SAP ERP:** SAP es uno de los ERP más robustos y utilizados a nivel mundial, ofreciendo módulos específicos para la integración con sistemas MES y SCADA.

**Conexión con MES:**
- **Middleware o Plataforma de Integración:** Utilización de una capa intermedia como Apache Kafka, RabbitMQ o plataformas específicas de integración como MuleSoft para conectar MES con ERP.
- **API (Interfaz de Programación de Aplicaciones):** Utilización de API RESTful para la comunicación entre MES y ERP.
- **Protocolo de Comunicación:** OPC UA, MQTT (Message Queuing Telemetry Transport) o SOAP (Simple Object Access Protocol).
