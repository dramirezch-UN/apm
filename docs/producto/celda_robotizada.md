---
layout: page
title: Celda de Manufactura Robotizada.
permalink: /producto/celda-robotizada
nav:false
---

Para el diseño de una celda robotizada en el proceso de producción de baldosas cerámicas es importante conocer cada uno del proceso, este fue identificado por completo en el VSM. 
Además, se sigue la guía para la implementación de celdas robotizadas extraída de la literatura.

![Fugó creación celda robo](https://hackmd.io/_uploads/S1fLggEW0.jpg)

## Viabilidad 
En este proceso se identificó una etapa crucial en la que los movimientos son repetitivos complejos, plantando la automatización de las rutinas y teniendo en cuenta el desgaste físico que tomara a un humano haciendo la labor planteada repetida veces, creando riesgos asociados con enfermedades laborales como lo expone en el siguiente post de la  [Agencia Europea para la Seguridad y la Salud en el Trabajo](https://saludlaboralydiscapacidad.org/wp-content/uploads/2019/05/Facts-73-Riesgos-asociados-a-la-manipulaci%C3%B3n-manual-de-cargas-en-el-lugar-de-trabajo-1.pdf). 

Teniendo ya las rutinas viables para robotizar las cuales son  **selección** **empacado** identificamos las variables encontradas en el proceso como son: el color de la baldosa, lineamientos se deben seguir en el empacado de la baldosa, teniendo en cuenta que  el proceso para cada una de estas se debe dar en un tiempo de 0.94 segundos, peso de cada uno de los elementos,  siendo estos los principales.

![GIF-BUENO](https://hackmd.io/_uploads/SJ4HmgVW0.gif)
## Rutina robotizada 
Posteriormente, se plantea el diagrama de flujo que se presenta en la realización de la tarea y como esta puede ser ejecutada por un robot. 
![image](https://hackmd.io/_uploads/BJ5JUWEbA.png)
## Layaout
Para ejecutar la rutina satisfactoriamente planteamos un layaout acorde con la tarea deseada, poniendo dos robots para la tarea. 
![Layout-Modelo](https://hackmd.io/_uploads/rJFO5WV-C.png)

## Selección de elementos de celda 
Para la selección de los elementos de celda  como el manipulador, el controlador, los sensores,  y se tiene en cuenta la fragilidad de material manipulado, así como las velocidades. 
### Selección del robot
Por un lado se plantea que la velocidad del empacado debe ser cada 0.94 segundos una baldosa, por lo que se usara dos manipuladores como se puede ver en la  siguiente tabla encontrada en los archivos.
![image](https://hackmd.io/_uploads/HJCmGFNZR.png)

Al buscar las características de un robot que tenga maniobrabilidad en un rango de 2 m con un peso de hasta 5 kg contando el gipper y además pudiendo llegar a la velocidad requerida sin problema. Para esto se seleccionó el manipulador IRB 4600-20/2.05  la ficha técnica se encuentra en los archivos. 

![image](https://hackmd.io/_uploads/SyWHtF4bR.png)


### Selección Gripper
### Selección del Controlador
### Selección de elementos de seguridad 
Se opta por un encerramiento en malla de alambre para la prevención de la entrada de personal al área de los robots . 
![image](https://hackmd.io/_uploads/BJxMqFVWR.png)
