# Comuicaciones

Para definir las comunicaciones usadas en el proyecto se siguieron los siguientes pasos:

1. Se definieron parámetros a los cuales se les va a hacer seguimiento.
2. Se escogieron sensores, controladores y otros componentes que se usarán para seguir estos parámetros.
3. Se consultaron catálogos, manuales y otras fuentes de referecian que proveen los fabricantes.
4. Se planeó una arquitectura de comunicaciones acorde a lo encontrado.

Algo importnte a tener en cuenta es que Sacmi, el fabricante de las máquinas especializadas de fabricación de cerámicas escogidas para la línea de producción, no provee información acerca de conectividad, recolección de datos, manejo remoto, etc. Por lo tanto se trataron estos equipos como cajas negras. Los componentes adicionales listados acá son externos a estas máquinas, y se utilizan para realizar seguimiento a varios parámetros de calidad que se deben tener en cuenta para asegurar la calidad de los productos entre estación y estación.

## Parámetros a Monitorear

- **Prensado:** N/A
- **Secado:** Humedad después del secado.
- **Esmaltado:** N/A
- **Decoración:** N/A
- **Separación de Productos:** Verificación de la correcta banda transportadora.
- **Relieve:** N/A
- **Horneado:** Dimensiones de las losas (longitud, ancho y grosor).
- **Pulido:** Calidad superficial.

## Sensores Utilizados

1. **Secado:**
   - **Sensor de Humedad por Microondas:** Process Sensors MCT466-SF, utilizado para medir el contenido de humedad.
   
2. **Separación de Productos:**
   - **Sensor de Barrera:** Keyence PZ-G series, para detectar la presencia del producto en la banda correcta.
   
3. **Horneado:**
   - **Sensores Láser de Medición de Distancia:** Keyence CL-3000 series, para medir dimensiones precisas. Los sensor heads se conectan a una unidad óptica (por ejemplo, Keyence CL-L(P)007N(G)), la cual se conecta al controlador.

4. **Pulido:**
   - **Sistema de Escaneo Láser:** Keyence LJ-V7000, para detectar defectos superficiales.

## Niveles de la Pirámide de Automatización

### Nivel de Campo

- **Process Sensors MCT466-SF:**
  - **Propósito:** Medir la humedad después del secado.
  - **Comunicación:** El sistema que incluye el sensor tiene el controlador incorporado.

- **Sensores Fotoeléctricos Keyence PZ-G:**
  - **Propósito:** Detectar productos en la banda adecuada.
  - **Comunicación:** Conexión directa al controlador Keyence CL-3000.

- **Sensores Confocales Keyence CL-3000:**
  - **Propósito:** Medir dimensiones de baldosas.
  - **Comunicación:** Los sensor heads se conectan a una unidad óptica Keyence CL-L(P)007N(G), que a su vez se conecta al controlador Keyence CL-3000.

- **Sensores Láser Keyence LJ-V7000:**
  - **Propósito:** Análisis superficial después del pulido.
  - **Comunicación:** Conexión directa al controlador Keyence LJ-V7001.

### Nivel de Control

- **Controladores:**
  - **Keyence CL-3000:** Recoge y procesa datos de los sensores PZ-G y CL-3000.
  - **Keyence LJ-V7001:** Recoge y procesa datos del sensor LJ-V7000.
  - **Comunicación con Sensores:** Protocolos propietarios de Keyence a través de cables dedicados.
  - **Comunicación con el Sistema SCADA:** Ethernet (TCP/IP).

### Nivel de Supervisión

- **Sistema SCADA (Ignition):**
  - Recibe y visualiza datos en tiempo real.
  - **Comunicación con Controladores:** Ethernet (TCP/IP).

## Canales y Protocolos de Comunicación

### De Campo a Control

- **Canales:**
  - Cables dedicados para cada sensor conectados a los controladores.

- **Protocolos:**
  - **Sensores Fotoeléctricos (PZ-G):** Salidas NPN/PNP estándar.
  - **Sensores Confocales (CL-3000):** Comunicación propietaria.
  - **Sensores Láser (LJ-V7000):** Salidas NPN/PNP estándar y comunicación propietaria.

### De Control a Supervisión

- **Canales:**
  - Red Ethernet entre controladores y el sistema SCADA.

- **Protocolos:**
  - **TCP/IP:** Para transmisión de datos fiable.

## Nivel de Planificación (MES)

**MES (Manufacturing Execution System)** es responsable de la gestión y optimización de las operaciones de producción en tiempo real. Un MES coordina, monitorea y controla los flujos de producción en la planta de manufactura.

**Software Recomendado:**
- **Ignition MES:** Ignition, además de ser una plataforma SCADA, ofrece módulos específicos para MES, lo que permite una integración directa y sin problemas con el sistema SCADA ya implementado.

**Funcionalidades Clave:**
- **Monitoreo de Producción en Tiempo Real:** Seguimiento de la producción y rendimiento en tiempo real.
- **Gestión de Órdenes de Trabajo:** Asignación, monitoreo y optimización de órdenes de trabajo.
- **Rastreo y Trazabilidad:** Seguimiento detallado de materiales y productos a través del proceso de producción.
- **Gestión de Calidad:** Inspección y control de calidad en cada etapa del proceso.
- **Decisiones de Producción:** Capacidad para decidir entre la fabricación de tres productos diferentes, optimizando el uso de recursos y tiempo de producción.

**Conexión con SCADA/Ignition:**
- **Interfaz Directa:** Dado que Ignition ofrece módulos tanto para SCADA como para MES, la conexión es nativa y sin necesidad de interfaces adicionales.
- **Protocolo de Comunicación:** OPC UA (Open Platform Communications Unified Architecture) o TCP/IP para la transferencia de datos.
- **Acceso a Datos en Tiempo Real:** El SCADA proporciona datos en tiempo real al MES, permitiendo decisiones informadas y ajustes rápidos en la producción.

## Nivel de Gestión (ERP)

**ERP (Enterprise Resource Planning)** se encarga de la gestión de los recursos empresariales, integrando todas las facetas del negocio, incluidas la planificación de producción, gestión de inventarios, contabilidad, recursos humanos, y más.

**Software Recomendado:**
- **SAP ERP:** SAP es uno de los ERP más robustos y utilizados a nivel mundial, ofreciendo módulos específicos para la integración con sistemas MES y SCADA.
- **Oracle ERP Cloud:** Ofrece soluciones flexibles y escalables para la gestión empresarial, con capacidades de integración con MES y SCADA.

**Funcionalidades Clave:**
- **Gestión Financiera:** Control y monitoreo de los recursos financieros.
- **Gestión de Inventarios:** Optimización del inventario de materias primas y productos terminados.
- **Planificación y Programación:** Planificación de la producción a largo plazo basada en la demanda y capacidad.
- **Gestión de Recursos Humanos:** Administración de personal y recursos humanos.

**Conexión con MES:**
- **Middleware o Plataforma de Integración:** Utilización de una capa intermedia como Apache Kafka, RabbitMQ o plataformas específicas de integración como MuleSoft para conectar MES con ERP.
- **API (Interfaz de Programación de Aplicaciones):** Utilización de API RESTful para la comunicación entre MES y ERP.
- **Protocolo de Comunicación:** OPC UA, MQTT (Message Queuing Telemetry Transport) o SOAP (Simple Object Access Protocol).

## Ejemplo de Flujo de Datos:

1. **Desde el Nivel de Campo al Nivel de Control (SCADA/Ignition):**
   - Sensores y controladores envían datos en tiempo real al SCADA.
   - Protocolo: TCP/IP.

2. **Desde el Nivel de Control (SCADA/Ignition) al Nivel de Planificación (MES):**
   - SCADA/Ignition proporciona datos en tiempo real y eventos de producción al MES.
   - Protocolo: OPC UA, TCP/IP.

3. **Desde el Nivel de Planificación (MES) al Nivel de Gestión (ERP):**
   - MES transmite datos de producción, inventarios y órdenes de trabajo al ERP.
   - Protocolo: API RESTful, Middleware.

4. **Desde el Nivel de Gestión (ERP) al Nivel de Planificación (MES):**
   - ERP proporciona datos financieros, inventarios y planificación a largo plazo al MES para una producción optimizada.
   - Protocolo: API RESTful, Middleware.

