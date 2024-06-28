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
- La materia prima de las baldosas entra por lotes con la cantidad necesaria para fábricar 960 baldosas equivalentes a 160 cajas.
- Los trabajadores son encargados de realizar el transporte de las baldosas cuando se requiere separación en su trayectoria, esto es entre la estación de esmaltado para el acabado, la maquina de relieve y el horno, y el horno, la maquina de pulido y las estaciones de embalaje.
- Previo a la primera bifurcación, las maquinas estan conectadas con bandas transportadoras.

Ademas, debido a limitaciones con el uso del software de Tecnomatix se encuentra que:
- Se emplean bandas y converters para realizar las tareas de separación de material y dirigirlo a las siguientes estaciones de trabajo.
- No fue posible incluir tiempos de preparación y encendido de las maquinas debido a comportamientos anormales en la simulación.
- El comportamiento de los trabajadores en la simulación puede no asemejarse a los comportamientos realizados en la vida real.
- No se incluyen los días festivos en la simulación por lo que se asume que estos días son laborales.

Acorde a lo anterior, se ejecuta una simulación de los 366 días del año 2024 donde se obtienen los resultados del archivo [Resultados](/producto/gestion_de_produccion/Resultados_Manual.pdf) y cuyo resumen se encuentra en la siguiente gráfica:

![Resultados Manual](/producto/gestion_de_produccion/Uso_maquinas_manual.png)

Se evidencia que los tiempos de bloqueo son altos previo a la interacción humana en la división y transporte de las baldosas, maquinas como la prensa, la secadora y las estaciones de decoración y va reduciendo su porcentaje de bloqueo a medida que avanzan las etapas de intervención humana como en el horno. Adicionalmente, se evidencia como, suponiendo una tasa de calidad del 100%, el _OEE_ de las maquinas es bajo en general, con usos máximos aproximadamente del 12% para las estaciones de esmaltado, con tiempos sin uso mayores al 55% y estaciones bloqueadas en un máximo del 23% del tiempo simulado, sin embargo, la secadora y el horno si cuentan con un uso elevado con _OEE_ de 81.33% y 90.11% respectivamente. Al final del periodo simulado se terminan elaborando un total de 263181 cajas de baldosas con 6 unidades cada una, para un total de 1579086 baldosas equivalentes a 410720.268 m<sup>2</sup>. Con estos datos es posible establecer un _takt time_ de 20.025 s.

Debido a la disponibilidad de las máquinas se observa que la planta puede aplicar a un proceso de automatización.

## Planta automatizada

Para realizar la simulación de la planta automatizada se reemplazan las tareas realizadas por trabajadores por bandas de transporte y por las celdas roboticas diseñadas para realizar el apilamiento de las baldosas en las cajas sobre las que se empacan. Sin embargo, debido a limitaciones a la hora de manejar el software, se hace una aproximación del proceso de ensamblaje calculando los tiempos empleados por el robot y colocandolos sobre la estación de ensamble al igual que los tiempos de falla.

En primer lugar, se realiza una aproximación manteniendo los tiempos de generación de la materia prima y la velocidad de las bandas instaladas y nuevas. Así, se obtienen que  ejecuta la simulación con los mismos tiempos de la simulación previa y se obtiene un total de 263392 cajas generadas mientras que los KPI de las máquinas permanecen en gran medida igual. Los resultados de esta simulación se encuentran [aquí](/producto/gestion_de_produccion/Resultados_Auto1.pdf) 

Considerando esto, se realiza un ajuste sobre los tiempos de entreda de materia prima y la velocidad de las bandas, reduciendo el primero un 25% e incrementando el segundo un 25%. De esta forma, se obtienen un total de 351059 cajas equivalentes a un aumento del 33.39% de aumento en la producción de baldosas. Al revisar los KPI de esta planta se observa que el _OEE_ de las estaciones con metrica mas baja aumenta en cantidades entre 1 y 2 puntos porcentuales pero tambien se aprecia como la secadora y, especialmente, el horno bajan su porcentaje de tiempo en uso. De esta forma, se obtiene un _takt time_ de 15.01 s. A continuación se observa el resumen de tiempos de uso de las diferentes estaciones en la nueva simulación, mientras en el [documento](/producto/gestion_de_produccion/Resultados_Auto2.pdf) se encuentran los resultados detallados de la misma.

![Resultados Auto2](/producto/gestion_de_produccion/Uso_maquinas_auto2.png)

Por último, se observa que los tiempos de espera en las estaciones debido a que su salida se encuentra bloqueada tambien disminuyen, por lo que un siguiente paso sería mejorar la disponibilidad de las máquinas. 

### Referencias
- https://sacmi.com/SacmiCorporate/media/ceramics/Catalogues/Serie-2000-Sacmi-(EN-IT-ES).pdf
- https://sharedcontent.sacmi.com/sharedcontent/media/Documents/Ceramics/catalogue/Terzo-fuoco-Smaltatura-(EN-IT).pdf
- https://sacmi.com/SacmiCorporate/media/ceramics/Catalogues/DHD708_DHD908_DHD1208-Intesa-(ITA_ENG).pdf
- https://sacmi.com/sharedcontent/media/Documents/Ceramics/2022/Catalogo_EVA_20210916-doppia-lingua.pdf
- https://hybrid-machine-moss.sacmi.com/sharedcontent/media/Documents/Ceramics/catalogue/MAESTRO-EN-ES.pdf
- 
