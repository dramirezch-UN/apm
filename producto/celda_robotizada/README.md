# Celda robotizada

Para el diseño de una celda robotizada en el proceso de producción de baldosas cerámicas es importante conocer cada uno del proceso, este fue identificado por completo en el VSM. 
Además, se sigue la guía para la implementación de celdas robotizadas extraída de la literatura.

![Fugó creación celda robo]

## Viabilidad 
En este proceso se identificó una etapa crucial en la que los movimientos son repetitivos complejos, plantando la automatización de las rutinas y teniendo en cuenta el desgaste físico que tomara a un humano haciendo la labor planteada repetida veces, creando riesgos asociados con enfermedades laborales como lo expone en el siguiente post de la  [Agencia Europea para la Seguridad y la Salud en el Trabajo](https://saludlaboralydiscapacidad.org/wp-content/uploads/2019/05/Facts-73-Riesgos-asociados-a-la-manipulaci%C3%B3n-manual-de-cargas-en-el-lugar-de-trabajo-1.pdf). 

Teniendo ya las rutinas viables para robotizar las cuales son  **selección** **empacado** identificamos las variables encontradas en el proceso como son: el color de la baldosa, lineamientos se deben seguir en el empacado de la baldosa, teniendo en cuenta que  el proceso para cada una de estas se debe dar en un tiempo de 5.7 segundos, peso de cada uno de los elementos,  siendo estos los principales.

![Variables](https://github.com/dramirezch-UN/apm/celda_robotizada/Variables.PNG)
## Rutina robotizada 
Posteriormente, se plantea el diagrama de flujo que se presenta en la realización de la tarea y como esta puede ser ejecutada por un robot. 
![Variables](https://github.com/dramirezch-UN/apm/celda_robotizada/Flujo.PNG)
## Layaout
Para ejecutar la rutina satisfactoriamente planteamos un layaout acorde con la tarea deseada, poniendo dos robots para la tarea. 
![Layout-Modelo](https://github.com/dramirezch-UN/apm/celda_robotizada/Layaut.png)

## Selección de elementos de celda 
Para la selección de los elementos de celda  como el manipulador, el controlador, los sensores,  y se tiene en cuenta la fragilidad de material manipulado, así como las velocidades. 
### Selección del robot
Por un lado se plantea que la velocidad del empacado debe ser cada 5.7 segundos una baldosa, por lo que se usara dos manipuladores, para no llegar a la velicdades altas por la frajiidad del material 

Al buscar las características de un robot que tenga maniobrabilidad en un rango de 1 m con un peso de hasta 15 kg contando el gipper y además pudiendo llegar a la velocidad requerida sin problema. Para esto se seleccionó el manipulador i4-6/850H la ficha técnica se encuentra en los archivos. 

![Robot](https://github.com/dramirezch-UN/apm/celda_robotizada/Robot.jpg)


### Selección Gripper
Para la seleccion del griper se uso un actudor nematico con varias ventosas el cual nos permite la sujecion del material de una manera que este no se vea afectado en el, tambien este es compatible con el robot y puede tener una carga maxima de hasta 20 kg. Este es el VGC10 del cual podemos encontrar la ficha tecnica en la documentacion. 

### Selección de elementos de seguridad 
Se opta por un encerramiento en malla de alambre para la prevención de la entrada de personal al área de los robots . 
![Robot](https://github.com/dramirezch-UN/apm/celda_robotizada/Celda1.PNG)
## Programacion de rutinas y trayectorias
La programacion de las diferentes rutinas y traectorias se hicieron en RoboDK teniendo en cuenta las rutinas anteriormente planeadas , y dividiendolas en 3 programas  **Inicio** **empacado**  **Separacion**  teniendo en cuanta las alcanzabilidades del robot y su velocidad de manipulacion. teniendo en cuenta que el controlador debe ejecutar estas rutinas desde la orden de un PLC maestro. Estas trayectorias y montaje lo podemos ver en la imagen. 
![Robot](https://github.com/dramirezch-UN/apm/celda_robotizada/Celda2.PNG)
