# Gestión de producción y automatización

## Planta sin automatizar

Para definir si la planta tenía posibilidad de aplicar en un proceso de automatización se reviso el estado actual de sus procesos de manufactura, para ello se inicio elaborando el VSM del proceso que lleva la planta y se realizo su simulación en el software de Siemens Tecnomatix Plant Simulation de la forma mas aproximada a la realidad. En el VSM se considera que el producto con acabado tipo piedra debe ser enviado a una maquina encargada de dar relieve a la superficie de la baldosa posterior a su esmaltado y previo ingreso al horno, mientras que la baldosa con acabado tipo marmol se dirige a una etapa de pulido superficial, o polichado, luego de su salida del horno. A continuacion una imagen del VSM planteado.

![VSM](/producto/gestion_de_produccion/VSM.png)

Se consultan las maquinas existentes en la planta y se establecen sus dimensiones físicas asi como las capacidades de producción de las mismas. De esta forma, se obtiene la siguiente tabla:

|Proceso|Máquina|Dimensiones|Tiempo de proceso|Disponibilidad|MTTR|
|:----:|:----:|:----:|:----:|:----:|:----:|
|Prensado|SACMI PH1500|4.2 x 4.3 m|1.6 s|90%|5 h|
|Secado|SACMI EVA 983|2.5 x 2.5 m|35 min|90%|5 h|
|Esmaltado|Cabina aerografo F40|6.5 x 2 m|2.4 s|95%|3 h|
|Decoración|Impresora SACMI DHD 708|4.65 x 1.95 m|1 s|70%|2.5 h|
|Relieve|-|3.6 x 2.45 m|3 s|70%|6 h|
|Horno|SACMI Maestro Kiln|120 x 2.5 m|60 min|90%|3 h|
|Pulido|-|10 x 2 m|3 s|80%|4 h|

Para su simulación se considera que:
- la materia prima de las baldosas entra por lotes con la cantidad necesaria para fábricar 960 baldosas equivalentes a 160 cajas.
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

Se evidencia que los tiempos de bloqueo son altos previo a la interacción humana en la división y transporte de las baldosas, maquinas como la prensa, la secadora y las estaciones de decoración y va reduciendo su porcentaje de bloqueo a medida que avanzan las etapas de intervención humana como en el horno. Adicionalmente, se evidencia como, suponiendo una tasa de calidad del 100%, el _OEE_ de las maquinas es bajo, siendo el horno y la secadora las más altas por encima del 20%, mientras las demas estaciones se encuentran por debajo del 4%. Adicionalmente, resalta como las maquinas estan disponibles por debajo del 50% del tiempo simulado gracias a las jornadas laborales que maneja la empresa. Al final del periodo simulado se terminan elaborando un total de 81629 cajas de baldosas con 6 unidades cada una, para un total de 489774 baldosas equivalentes a 127390.2174 m<sup>2</sup>. Con estos datos es posible establecer un _takt time_ de 64.565 s.

Debido a esto, se observa una necesidad de automatizar aun mas la planta y permitir una mayor eficiencia de la misma.

## Planta automatizada

Para realizar la simulación de la planta automatizada se reemplazan las tareas realizadas por trabajadores por bandas de transporte y por las celdas roboticas diseñadas en su componente. Sin embargo, debido a limitaciones a la hora de manejar el software, se hace una aproximación del proceso de ensamblaje calculando los tiempos empleados por el robot y colocandolos sobre la estación de ensamble al igual que los tiempos de falla. Adicionalmente, el material de origen mantiene su tiempo de generación, mientras la velocidad de las bandas se aumenta de 0.2 a 0.25 m/s. Tambien, dado que no se requieren trabajadores dentro de la linea de manufactura se elimina el uso de las jornadas configuradas. Se ejecuta la simulación con los mismos tiempos de la simulación previa y se obtienen los resultados del archivo [Resultados](/producto/gestion_de_produccion/Resultados_Auto.pdf) y cuyo resumen se encuentra en la siguiente gráfica:

![Resultados Auto](/producto/gestion_de_produccion/Uso_maquinas_auto.png)

Se puede apreciar que se terminan generando un total de 175583 cajas con 6 baldosas equivalentes a 2.15 veces más producción que en el modelo anterior y un _takt time_ de 30.0165 s. Sin embargo, es apreciable como la disponibilidad de las maquinas tambien limita la cantidad de baldosas procesadas en especial de la impresora que es una maquina por la cual pasan todos los tipos de baldosas.


### Referencias
- https://sacmi.com/SacmiCorporate/media/ceramics/Catalogues/Serie-2000-Sacmi-(EN-IT-ES).pdf
- https://sharedcontent.sacmi.com/sharedcontent/media/Documents/Ceramics/catalogue/Terzo-fuoco-Smaltatura-(EN-IT).pdf
- https://sacmi.com/SacmiCorporate/media/ceramics/Catalogues/DHD708_DHD908_DHD1208-Intesa-(ITA_ENG).pdf
- https://sacmi.com/sharedcontent/media/Documents/Ceramics/2022/Catalogo_EVA_20210916-doppia-lingua.pdf
- https://hybrid-machine-moss.sacmi.com/sharedcontent/media/Documents/Ceramics/catalogue/MAESTRO-EN-ES.pdf
- 
