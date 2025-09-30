# Evidencias de la unidad 6

##Actividad 01 

<img width="737" height="731" alt="image" src="https://github.com/user-attachments/assets/4f473911-39e3-43f2-9595-0004e25d15bc" />

<img width="821" height="965" alt="image" src="https://github.com/user-attachments/assets/7f141581-bb3f-4ed1-93fa-bdcf512798bf" />

**¿Qué te inspira de su trabajo?**
siento que lo que mas me llama la atencion es como las obras que utiliza son las que cumplen con sus expectativas ps el algoritm saca varias imagenes pero no solo por eso las utiliza todas si no las que me le llamen la atencion a el , tambien otro punto que me llama la atencion es que se influencia mucho por otras corriente artisticas y obras por que en las obras que tiene expuesta se nota que hay como una rewferencia de ciertas corrientes artisiticas 

## Actividad 02

**¿Qué es una fuerza de dirección (steering force)?**

la steering force es la fuerza la cual es calculada para determinar la aceleracion que necesita un agente para lograr un movimiento en especifico como por ejemplo huir de un depredador 

**¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?**

Mientras que con las otras fuerza vienen directamente del entono  o objetos externos con la steering forces vienen de la intenticon del agente y/o particula por ejemplo mientras que por la gravedad la particula cae hacia abajo con la steering force la particula sobrescribira la trayectoria para terminar llegando en vez de caer normalmente , las fuerzas con las que hemos trabajado son para generar movimientos mas naturales mientras que con la otra es mas enfocado a consguir metas como escapar de algo o llegar a un punto 

**¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?**
la steerging force esta totalmente relacionada con el trbajo de craig reynolds esto gracias a que  esta es la principal herramienta para su trabajo de simular comportamientos de animales como por ejemplo el de los cardumenes de peces igual gracias a este trabajo es por lo que hoy tenemos simulaciones de multitudes enjambres y vehiculos autonomos en animacion videojugos etc 


## Actividad 03
**Explica brevemente la estructura de datos usada para el campo de flujo y cómo se generan sus vectores.**
El campo de flujo se guarda en una matriz donde cada elemento de la matriz  es un vector de direccion en la inicializacion cada vector se genera usando un perlin noise  convertido en angulo y luego en un vector unitario , todo esto genera que cada celda contenga un vector que apunta en alguna direccion generando que los agentes puedan consultarlo segun su posicion 

**Describe con tus palabras cómo un agente utiliza el campo para calcular su fuerza de dirección.**
el agente consulta en la matriz donde apunta su campo en su celda el agente compara a donde va y aplicac una pequeña correcion para alinerase con esa direccion 


**Lista los parámetros clave identificados (resolución, maxspeed, maxforce).**
la resolucion define el tamaño de las celdas del campo de flujo 
El maxspeed es el limite superior de que tan rapido se mueve el agente 
maxforce que tan rapido puede girar o corregir su trayectoria para seguir el campo 

**Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el movimiento y comportamiento colectivo de los agentes. Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.**
la modificacion que le hice al codigo fue que reemplaze el perlin por una funcion sinusoidal con esta el campo se vuelve repetitivo y periodico los agentes igual se alinean en patrones ondulante provocando que su movimiento se vea menos natural 

<img width="802" height="599" alt="image" src="https://github.com/user-attachments/assets/c2d7b266-0833-40bf-91b1-89c01dbeedcf" />
