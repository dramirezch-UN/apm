# Controladores industriales (PLC)

Los controladores industriales son esenciales para el desarrollo del proyecto, ya que son los que permiten la conexión entre la base de la pirámide de la automatización y las partes superiores, para esto los PLCs de simens con sus módulos de entradas y salidas. Nos permite controlar  los actuadores implementados en el proceso y supervisar los sensores empleados en la planta. Para esto planteamos el uso de 4 controladores, los cuales supervisan, operan, registran datos, y nos dan alarmas del proceso. La organización la podemos ver en la siguiente imagen 

<img src="https://github.com/dramirezch-UN/apm/controladores_industriales/control_de_planta.png">

## Excel

La programación de los controladores industriales se planificó en [esta hoja de cálculo](https://github.com/dramirezch-UN/apm/blob/main/producto/controladores_industriales/arquitectura_plc_scada.xlsx).

### Logica Ladder
La hoja `Logica Ladder` detalla las etapas del proceso de control en un formato estructurado. Para cada etapa se especifican los actuadores que deben estar encendidos, las condiciones de activación y desactivación, y una descripción funcional. Por ejemplo, se puede encontrar una etapa que indica la entrada de cajas, detallando los actuadores involucrados y las condiciones necesarias para la transición a la siguiente etapa. También se consideran estados de mantenimiento y fallos, indicando acciones como "Apagar todo y reset" para manejar estos eventos. Esto proporciona una guía clara sobre cómo se deben configurar y gestionar las distintas etapas del proceso en el PLC.

### Factory
En la hoja `Factory` se enumeran los elementos del sistema, como actuadores y sensores, junto con sus etiquetas (`Tags`). Esta hoja sirve para identificar claramente cada componente físico y su función. Por ejemplo, incluye detalles sobre las bandas transportadoras, rodillos y sensores, especificando su ubicación y tipo de operación. Esta información es esencial para la programación de los controladores, ya que permite asignar y referenciar correctamente cada dispositivo en los programas ladder.

### OPC
La hoja `OPC` proporciona un mapeo entre los `Tags` utilizados en el sistema de control y los `Tags` utilizados en el servidor OPC. Este mapeo es crucial para la integración con sistemas SCADA, permitiendo que los datos de los PLCs sean accesibles y manipulables desde una interfaz SCADA. Cada elemento del sistema tiene un `Tag` específico en el servidor OPC, facilitando la comunicación y el control remoto de los dispositivos. Por ejemplo, un actuador de una banda transportadora tendrá un `Tag` que se mapea directamente al servidor OPC, asegurando la coherencia de los datos.

### SCADA
La hoja `SCADA` expande el mapeo de `Tags` para la interfaz SCADA, proporcionando detalles adicionales sobre la visualización y control de los elementos del sistema. Además de los `Tags` OPC, incluye información sobre los perilleros asociados a cada elemento y los códigos de colores que indican diferentes estados operativos (encendido, apagado, mantenimiento, falla). Esto facilita la representación visual y el monitoreo en tiempo real desde el sistema SCADA, permitiendo una gestión eficiente y clara del proceso industrial.

## Implementación
El archivo con la implementación de la programación en Ladder se encuentra en este [enlace](https://github.com/dramirezch-UN/apm/blob/main/producto/controladores_industriales/programacion_plcs.ACD).
