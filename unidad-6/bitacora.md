# Evidencias de la unidad 6

## Actividad 01 

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


## Actividad 04


**Explica con tus palabras el objetivo y la lógica general de cálculo de cada una de las tres reglas de Flocking (Separación, Alineación, Cohesión).**

-Separacion: el objetivo es evitar que los voids se amontonen en un solo punto  si por ejemplo los boids vecinos estan a una menor distancia de un radio ay definido se va a generar un vector que apuntara mas lejos del vecino luego se hace un promedio de estos vectores y se limita con maxforce 

-Alineacion: El objetivo de este es que todos lo boids sigan una misma direccion por ejemplo se hace haciendo que un boid se dirija en la misma dirrecion promedio de los boids que hay al su alrededor esto se hace sumando los vectores de velocidad de los boids cercanos luego se calcula el promedio el vector que resulte de esto se ajusta a la maxspeed  por ultima la fuerza de dirrecion se calcula con la diferencia entre el vector deseado y la velocidad actual del boid 

-Cohesion la cohesion es la encargada de mover el boid hacia la dirrecion promedio de los boids que hay alrededor esto se hace sumando la posicion de los boids cercanos luego de esto se calcula el centro de masa luego se genera un vector que va desde la posicion actual al centro de masa y luego de esto se limita la maxforce 

**Lista los parámetros clave identificados (radio de percepción, pesos de las reglas, maxspeed, maxforce).**

Radio de percepcion: Este se encarga de que tan lejos puede ver un boid a sus vecinos para cambiar su separacion alineacion y cohesion entre menor sea este menos boids van a afectar en la decision de nuestro boid 

Pesos de las reglas: este se encargar de dar la importancia de cada una  de la fuerzas antes de sumarlas si el peso es alto esa regla va dominar el comportamiento y viceversa 

Velocidad maxima:  este es el limite superior de la rapidez con la que un boid puede moverse  esto evita que aceleren indefinidamente 

Fuerza maxima: esto es la  fuerza que determina la brusquedad con la que un boid puede girar o corregir su trayectoria esto haciendo que los boids no tengan giros irrealistas 

**Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el comportamiento colectivo del enjambre (¿Se dispersan? ¿Forman grupos compactos? ¿se mueven caóticamente?). Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.**









