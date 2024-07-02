---
layout: page
title: SCADA.
permalink: /producto/scada
---


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
