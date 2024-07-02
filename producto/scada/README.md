# SCADA

#### Arquitectura del Sistema

El sistema SCADA en la nube supervisará las variables obtenidas de la comunicación OPC y MQTT. Para lograr esto, se utilizarían tres PCs (PC1, PC2 y opcionalmente PC3) junto con Ignition Cloud Edition en Azure, aprovechando el plugin disponible en Azure Marketplace, lo que facilita la integración y gestión del sistema SCADA en la nube.

#### PC1: Comunicación OPC entre Controlador Industrial e Ignition Local 1

En PC1, se establecería una comunicación OPC entre el controlador industrial e Ignition Local 1. El controlador ejecutaría la lógica del proceso programada en Studio 5000, leería la información de sensores virtuales diseñados en Siemens NX, resolvería la lógica de control y enviaría señales de control a los actuadores virtuales en Siemens NX. Ignition Local 1 supervisaría y recopilaría datos de las variables del controlador, transmitiéndolos a Ignition Cloud Edition mediante el protocolo MQTT.

#### PC2: Comunicación OPC entre Siemens NX e Ignition Local 2

En PC2, se establecería una comunicación OPC entre Siemens NX e Ignition Local 2. Siemens NX se utilizaría para diseñar y simular sensores y actuadores virtuales. Ignition Local 2 supervisaría y recopilaría datos de las variables simuladas en Siemens NX y los transmitiría a Ignition Cloud Edition usando MQTT.

#### PC3 (Opcional): Comunicación OPC entre otra Plataforma Industrial e Ignition Local 3

En PC3, se podría establecer una comunicación OPC entre otra plataforma industrial e Ignition Local 3. Esta configuración opcional supervisaría y recopilaría datos adicionales, que serían transmitidos a Ignition Cloud Edition utilizando MQTT.

#### Ignition Cloud Edition en Azure

Ignition Cloud Edition se alojaría en Microsoft Azure, aprovechando su plugin disponible en Azure Marketplace. Esto permitiría extender las operaciones empresariales, utilizar arquitecturas elásticas que se escalan instantáneamente y alojar y desplegar soluciones en la plataforma segura de Azure. La conexión entre Ignition Local y Ignition Cloud Edition se realizaría mediante MQTT, lo que garantizaría una transmisión de datos eficiente y en tiempo real.

1. **Funciones de Ignition Cloud Edition:**
   - Recibir datos de todas las instancias de Ignition Local (1, 2 y opcionalmente 3) a través de MQTT.
   - Proporcionar una interfaz de supervisión y control accesible desde cualquier lugar con conexión a Internet.
   - Almacenar y analizar datos históricos para mejorar la toma de decisiones.

2. **Acceso Remoto:**
   - Se configuraría una IP pública para que los usuarios pudieran visualizar y operar el sistema SCADA en la nube.
   - Se implementarían medidas de seguridad adecuadas, como autenticación de usuarios y cifrado de datos.

#### Plan de Desarrollo

1. **Configuración del Controlador Industrial:**
   - Se programaría la lógica del proceso en Studio 5000.
   - Se configurarían los sensores y actuadores virtuales en Siemens NX.

2. **Configuración de Ignition Local 1:**
   - Se establecería comunicación OPC con el Controlador Industrial.
   - Se configuraría la transmisión de datos a Ignition Cloud Edition usando MQTT.

3. **Configuración de Siemens NX:**
   - Se diseñarían y simularían sensores y actuadores virtuales.
   - Se establecería comunicación OPC con Ignition Local 2.

4. **Configuración de Ignition Local 2:**
   - Se establecería comunicación OPC con Siemens NX.
   - Se configuraría la transmisión de datos a Ignition Cloud Edition usando MQTT.

5. **Configuración de la Plataforma Industrial Adicional (Opcional):**
   - Se establecería comunicación OPC con Ignition Local 3.
   - Se configuraría la transmisión de datos a Ignition Cloud Edition usando MQTT.

6. **Configuración de Ignition Cloud Edition en Azure:**
   - Se configuraría la recepción de datos de todas las instancias de Ignition Local usando MQTT.
   - Se desarrollaría la interfaz de usuario para la supervisión y control remoto.
   - Se publicaría la IP pública y se asegurarían las medidas de acceso.


# Diseño del sistema SCADA

El sistema SCADA será la interfaz bidireccional para el monitoreo y control de la planta, desde él se podrá elegir el tipo de baldosa que se producirá y monitorear el estado de las diferentes máquinas en la planta (operativa o disponible, en mantenimiento, en falla). En este caso, enfocamos el sistema a las bandas encargadas de transportar y dividir las baldosas que requieren, o no, paso por la estación de relieve. Este sistema se diseño en primer lugar para su integración con el software _FactoryIO_.

Conociendo las etiquetas empleadas por la comunicación OPC se hacen corresponder con las etiquetas empleadas para el sistema SCADA acorde a la siguiente tabla, donde hay elementos en los cuales se tienen dos etiquetas para identificar, el estado operativo del elemento (encendido/apagado) asi como tambien la dirección en la que se esta moviendo. 

|Elemento|Tag SCADA|Tag OPC|
|:---:|:---:|:---:|
|Banda de entrada|IoT_B0|GD_B0|
|Banda diagonal entrada|IoT_B1|GD_B1|
|Máquina relieve|IoT_B2|GD_B2|
|Banda curva|IoT_B3|GD_B3|
|Banda larga|IoT_B4|GD_B4|
|Banda de salida|IoT_B5|GD_B5|
|Rodillos de entrada|IoT_R00<br>IoT_R01|GD_R00<br>GD_R01|
|Rodillos de salida|IoT_R10<br>IoT_R11|GD_R10<br>GD_R11|
|Acomodador entrada relieve|IoT_A00<br>IoT_A01|GD_A00<br>GD_A01|
|Acomodador salida relieve|IoT_A10<br>IoT_A11|GD_A10<br>GD_A11|

De igual forma, se realiza la asociación entre etiqueteas para los sensores implementados:

|Sensor|Tag SCADA|Tag OPC|
|:---:|:---:|:---:|
|Sensor B0 - R0|IoT_S0|GD_S0|
|Sensor R0 - B1|IoT_S1|GD_S1|
|Sensor R0 - B4|IoT_S2|GD_S2|
|Sensor B1 - A0|IoT_S3|GD_S3|
|Sensor A0 - B2|IoT_S4|GD_S4|
|Sensor A0 - B2|IoT_S4|GD_S5|
|Sensor B2 - A1|IoT_S5|GD_S6|
|Sensor B2 - A1|IoT_S5|GD_S7|
|Sensor A1 - B3|IoT_S6|GD_S8|
|Sensor B3 - R1|IoT_S7|GD_S9|
|Sensor B4 - R1|IoT_S8|GD_S10|
|Sensor R1 - B5|IoT_S9|GD_S11|

Debido al uso del software _FactoryIO_ se tiene la restriucción de no poder usar selectores por lo cual se recurre a perilleros los cuales simulan valores enteros entre 0 y 10, y se asignan a su respectiva etiqueta en el sistema SCADA. Con estos, se realiza una relación entre el valor entregado por el perillero y la etiqueta del elemento (IoT_##) para obtener un resultado del estado de la maquina acorde a la siguiente combinación:

|**Valor del perillero**|**Valor del Tag IoT_##**|**Estado del elemento**|**Código de colores**|
|:---:|:---:|:---:|:---:|
|0|0|Apagado|Gris|
|0|1|Encendido|Verde|
|0<X<10|-|-|Amarillo|
|10|-|-|Rojo|

Por último, se tiene una variable para indicar si el producto elaborado requiere proceso en las estaciones encargadas del relieve o pulido.
