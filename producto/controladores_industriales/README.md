# Controladores industriales (PLC)

Los controladores industriales son esenciales para el desarrollo del proyecto, ya que son los que permiten la conexión entre la base de la pirámide de la automatización y las partes superiores, para esto los PLCs de simens con sus módulos de entradas y salidas. Nos permite controlar  los actuadores implementados en el proceso y supervisar los sensores empleados en la planta. Para esto planteamos el uso de 4 controladores, los cuales supervisan, operan, registran datos, y nos dan alarmas del proceso. La organización la podemos ver en la siguiente imagen:

<img src="https://raw.githubusercontent.com/dramirezch-UN/apm/dev/producto/controladores_industriales/plc_estructura.jpg" />

La programación de los controladores industriales se planificó en [esta hoja de cálculo](https://github.com/dramirezch-UN/apm/blob/main/producto/controladores_industriales/arquitectura_plc_scada.xlsx).

### Logica Ladder
La hoja `Logica Ladder` proporciona una estructura detallada de las etapas del proceso, los actuadores involucrados, y las condiciones de activación y desactivación. Por ejemplo, en la etapa `E00`, se encienden los actuadores `B0` y `R00` cuando se alcanza la condición de "Fin". Esto implica que, al iniciar el proceso, la banda de entrada (`B0`) y los rodillos (`R00`) se activarán para mover las cajas hacia la siguiente etapa. La condición para apagar estos actuadores y pasar a la siguiente etapa (`E01`) es simplemente la transición a la etapa `E01`.

En la etapa `E01`, el sistema espera un cambio de tipo, lo que podría referirse a una variación en el tipo de producto que se está procesando. Esto podría ser activado por un cambio detectado en los sensores o por una intervención manual. Una vez que el tipo cambia, la etapa se completa y el sistema espera a que termine el proceso actual (`Fin`) para avanzar.

Las subetapas como `E001` y `E002` representan modos específicos de operación. Por ejemplo, `E001` se activa si el tipo es 0, indicando que no hay relieve en el producto, y se desactiva cuando se sale de la etapa `E00`. `E002` se activa si el tipo es 1 y la condición `S0D` es verdadera (un sensor específico está activo), y se desactiva si se cumple alguna de las condiciones `!E00` o `S1D`.

Cada etapa tiene una descripción que detalla su función específica, como "Entrando cajas" para `E00` y "Esperando cambio de tipo" para `E01`. Además, se consideran escenarios de mantenimiento y fallos, indicando acciones como "Apagar todo y reset" para reiniciar el sistema en caso de problemas.

### Factory
La hoja `Factory` detalla los componentes físicos del sistema, como actuadores y sensores, asignándoles etiquetas (`Tags`) que facilitan su identificación y uso en los programas de control. Por ejemplo:
- **Actuador B0**: Representa la banda de entrada, encargada de mover las cajas hacia el proceso inicial.
- **Sensor S0**: Situado a la salida de la banda de entrada, detecta la presencia de cajas y permite al sistema avanzar al siguiente paso.
- **Actuador R00**: Controla los rodillos del R0, que pueden estar encendidos o apagados.
- **Actuador R01**: Maneja los rodillos del R0, pudiendo estar en posición recta o girados en diagonal.

Esta información es esencial para la programación ladder, ya que permite definir claramente qué actuadores y sensores están involucrados en cada etapa del proceso.

### OPC
La hoja `OPC` proporciona un mapeo entre los `Tags` utilizados en el sistema de control y los `Tags` que se utilizan en el servidor OPC. Este mapeo es crucial para la integración con sistemas SCADA, permitiendo que los datos del PLC sean accesibles y manipulables desde la interfaz SCADA. Por ejemplo:
- **Actuador B0**: En el sistema de control se etiqueta como `B0`, mientras que en el servidor OPC se etiqueta como `GD_B0`.
- **Sensor S0**: Etiquetado como `S0` en el sistema de control y como `GD_S0` en el servidor OPC.

Este mapeo asegura que los datos sean coherentes y accesibles a través del servidor OPC, permitiendo la comunicación eficiente entre el PLC y el SCADA.

### SCADA
La hoja `SCADA` expande el mapeo a la interfaz SCADA, proporcionando `Tags` adicionales y detalles de visualización. Por ejemplo:
- **Banda de entrada (IoT_B0)**: Se mapea a `GD_B0` en el OPC y se representa como `IoT_B0` en el SCADA.
- **Perillero P0**: Asociado a la banda de entrada, con un código de colores que indica el estado del perillero (Encendido, Apagado, Mantenimiento, Falla).

Además, se especifican los valores del perillero para diferentes estados, lo que permite una representación visual clara y efectiva en el sistema SCADA. Por ejemplo, un valor de `0` podría indicar que todo está bien, mientras que valores entre `0` y `10` podrían indicar que se requiere mantenimiento.

### Integración con SCADA
Los datos serán transmitidos al sistema SCADA a través del servidor OPC, utilizando el mapeo de `Tags` definido en la hoja `OPC`. Esto permitirá que la interfaz SCADA tenga acceso en tiempo real a los datos de los PLCs, facilitando el monitoreo y control del proceso industrial.

En resumen, la programación de los PLCs seguirá una lógica estructurada y detallada, con una integración eficiente con sistemas OPC y SCADA para asegurar un control y monitoreo precisos del proceso industrial.

### Implementación en PLC
Para la implementación en los PLCs, se utilizará la lógica ladder detallada en la hoja `Logica Ladder`. Cada etapa del proceso será programada como un bloque de lógica ladder, donde se definirán las condiciones de activación y apagado, así como las acciones correspondientes a cada etapa.

1. **Definición de condiciones de entrada**: Utilizando las condiciones de activación especificadas en la hoja `Logica Ladder`.
2. **Activación de actuadores**: Encendiendo los actuadores indicados para cada etapa.
3. **Definición de condiciones de salida**: Basándose en las condiciones de apagado para transicionar a la siguiente etapa.
4. **Documentación y manejo de fallos**: Usando las descripciones y las acciones de apagado/reset para mantener la integridad del sistema.

Para finalizar, el archivo con la implementación de la programación en Ladder se encuentra en este [enlace](https://github.com/dramirezch-UN/apm/blob/main/producto/controladores_industriales/programacion_plcs.ACD).
