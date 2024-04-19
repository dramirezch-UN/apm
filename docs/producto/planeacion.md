---
layout: page
title: Planeación del proyecto
permalink: /producto/planeacion
---

Para la planificación del proyecto se siguieron los 7 pasos planteados por [el banco interamericano de desarrollo](http://www.pm4rglobal.org/). El desarrollo detallado de cada uno de los pasos se puede ver en [esta hoja de cálculo](https://github.com/dramirezch-UN/apm/blob/main/producto/planeacion/7_pasos.xlsx).

## Alance

El primer paso indicado es definir el alcance, para esto se realizó la Estructura Desglosada de Trabajo (EDT). Para esto, se analizó la [especificación del proyecto](https://drive.google.com/file/d/1n-xfzP6dzglZlWPY1H2SkVO09-8GEFPX/view?usp=drive_link) y se anotaron todas las posibles tareas o entregables, luego, se dividieron los items encontrados en entregables más pequeños. Para facilitar el desarrollo de los demás pasos, se hizo otra columna con la ruta crítica del proyecto. La EDT y la ruta crítica se pueden encontrar en la primera página de la hoja de calculo mencionada.

## Tiempos

Para planificar el tiempo del proyecto, se tomaron todas las tareas de la ruta crítica encontradas en el paso anterior y:
- Se les asignó una duración, en días.
- Se parametrizó su fecha de inicio dependiendo de la fecha de finalización de otras tareas que son pre-requisitos.

Debido a las anormalidades académicas presentadas durante el semestre, se decidió dejar la fecha de inicio del proyecto como el primero de enero de 2024. La hoja de cálculo está parametrizada, por lo que si se desea se puede asignar una fecha de inicio más pertinente. 

Teniendo la fecha de inicio del proyecto, el orden de realización de las tareas, y su duración, se utilizó la herramienta "Cronograma" de google sheets para visualizar el cronograma del proyecto.

El desarrollo de todo esto se encuentra en las páginas 2 y 3 de la hoja de cálculo.

## Costos

Antes de asignar costos a cada tarea, se decidió investigar los precios de las diferentes licencias de software que se necesitarían para realizar el proyecto. Eso incluye programas como Microsoft office, RobotStudio, Siemens NX, etc. También se tomaron en cuenta los costos de computadores y salarios para el equipo. Finalmente, se decidió dividir el precio de cada insumo entre el número de entregables de la ruta crítica que los usarían. Por ejempo, los computadores y los salarios son necesarios en todas las tareas, por lo que se dividieron en 58; robotstudio solo se necesita en 6 tareas, por lo que el precio de la licencia se dividió en 6. Esto se hizo para facilitar el desarrollo de los pasos 3 y 4.

Con los precios de los insumos definidos, se procedió a realizar el análisis de costos y a graficar la curva S. Para esto, simplemente se asignaron los precios y las fechas ya definidas a las tareas correspondientes. Y se realizó un gráfico de columnas.

Esto se puede encontrar en las páginas "precios" y "3_costos" de la hoja de cálculo.

## Adquisiciones

Para el planteamiento de las adquisiciones, se decidió asignar cada adquisición a la primera tarea que usara el insumo indicado. Y se dejó un N/A en las otras tareas que usaran un insumo ya adquirido.

Esto se encuentra en la página "4_adquisiciones" de la hoja de cálculo.

## Riesgos

Los riesgos se definieron tal como indica el BID. La matriz correspondiente se encuentra en "5_riesgos".

## Comunicaciones

Como en este paso se deben asignar algunas responsabilidades, fue necesario definir algunos roles dentro del equipo:

1. **Administrador de Repositorio y Web** - Encargado de mantener el repositorio de GitHub, aprobar cambios y gestionar el sitio web.
2. **Jefe de Producción y Automatización** - Encargado de la gestión de producción y automatización de procesos.
3. **Especialista en Industria 4.0** - Enfocado en la implementación de tecnologías para la Industria 4.0 utilizando Tecnomatix.
4. **Coordinador de Planificación del Proyecto** - Responsable de la planeación y seguimiento de los proyectos.
5. **Analista de Evaluación Económica** - Encargado de realizar análisis económicos y evaluaciones financieras de proyectos.
6. **Ingeniero de Sistemas Robóticos** - Especializado en el diseño y operación de celdas de manufactura robotizadas usando RobotStudio.
7. **Diseñador de Fábrica Digital** - Encargado de modelar y simular procesos industriales utilizando Siemens NX.
8. **Técnico en Controladores Industriales** - Especializado en la programación y mantenimiento de controladores lógicos programables (PLC) con Studio 5000.
9. **Encargado de Comunicaciones** - Responsable de la gestión y supervisión de las comunicaciones internas y externas del equipo.
10. **Operador de SCADA** - Encargado de supervisar y controlar procesos industriales mediante sistemas SCADA.

Con estos roles definidos, se procedió a llenar la matriz de comunicaciones. Esta se encuentra en "6_comunicaciones".

## RACI

El último paso fue definir los roles: responsable, aprueba, consultado, informado para cada entregable de la ruta crítica. Para esto, se usaron los mismos roles definidos en el paso anterior. Esto se encuentra en "7_raci".
