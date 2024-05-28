# Gestión de producción y automatización

## Planta sin automatizar

Para definir si la planta tenía posibilidad de aplicar en un proceso de automatización se reviso el estado actual de sus procesos de manufactura, para ello se inicio elaborando el VSM del proceso que lleva la planta y se realizo su simulación en el software de Siemens Tecnomatix Plant Simulation de la forma mas aproximada a la realidad. En el VSM se considera que el producto con acabado tipo piedra debe ser enviado a una maquina encargada de dar relieve a la superficie de la baldosa posterior a su esmaltado y previo ingreso al horno, mientras que la baldosa con acabado tipo marmol se dirige a una etapa de pulido superficial, o polichado, luego de su salida del horno. A continuacion una imagen del VSM planteado.

![VSM](/producto/gestion_de_produccion/VSM.png)

Para su simulación se considera que: 
- La planta emplea 2 turnos de trabajo de 8h cada uno, de 6:00 a 14:00 y de 14:00 a 22:00 de lunes a viernes.
- Los trabajadores son encargados de realizar el transporte de las baldosas cuando se requiere separación en su trayectoria, esto es entre la estación de esmaltado para el acabado, la maquina de relieve y el horno, y el horno, la maquina de pulido y las estaciones de embalaje.
- Las máquinas solo estan operativas durante estos turnos.
- Previo a la primera bifurcación, las maquinas estan conectadas con bandas transportadoras.

Ademas, debido a limitaciones con el uso del software de Tecnomatix se encuentra que:
- Se emplean bandas y converters para realizar las tareas de separación de material y dirigirlo a las siguientes estaciones de trabajo.
- No fue posible incluir tiempos de preparación y encendido de las maquinas debido a comportamientos anormales en la simulación.
- El comportamiento de los trabajadores en la simulación puede no asemejarse a los comportamientos realizados en la vida real.
- No se incluyen los días festivos en la simulación por lo que se asume que estos días son laborales.

Acorde a lo anterior, se ejecuta una simulación de los 366 días del año 2024 donde se obtienen los resultados del archivo [Resultados](/producto/gestion_de_produccion/Resultados_Manual.pdf) y cuyo resumen se encuentra en la siguiente gráfica:

![Resultados Manual](/producto/gestion_de_produccion/Uso_maquinas_manual.png)

Se evidencia que los tiempos de bloqueo son altos previo a la interacción humana en la división y transporte de las baldosas, maquinas como la prensa, la secadora y las estaciones de decoración y va reduciendo su porcentaje de bloqueo a medida que avanzan las etapas de intervención humana como en el horno. Adicionalmente, se evidencia como las maquinas estan siendo usadas muy poco, siendo el horno y la secadora las más altas por encima del 20% mientras las demas estaciones tienen un uso máximo menor al 4%. Adicionalmente, resalta como las maquinas estan disponibles por debajo del 50% del tiempo simulado gracias a las jornadas laborales que maneja la empresa. Al final del periodo simulado se terminan elaborando un total de 81629 cajas de baldosas con 6 unidades cada una, para un total de 489774 baldosas equivalentes a 127390.2174 m<sup>2</sup>.

Debido a esto, se observa una necesidad de automatizar aun mas la planta y permitir una mayor eficiencia de la misma.

## Planta automatizada

Para realizar la simulación de la planta automatizada se reemplazan las tareas realizadas por trabajadores por bandas de transporte y por las celdas roboticas diseñadas en su componente. Sine mbargo, debido a limitaciones a la hora de manejar el software, no fue posible ejecutar la simulación de igual manera, dado que la programación de los elementos *pick and place* hacia que se bloquearan si no podian soltar el objeto manipulado, en este caso, asumimos que las cajas de empaque siempre se encontraban disponibles y modificar los tiempos de creacion en su fuente implicaba que las baldosas se podian bloquear de igual forma. Se carga el archivo de simulación hasta donde fue posible desarrollarlo.
