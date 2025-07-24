# Unidad 1

## 🤔 Fase: Reflect

### Actividad 9
#### parte 1 
**Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?**
La diferencia entre estos dos conceptos es que mientras que con random genera numeros randoms en una pool por ejemplo 1-10 todo los numeros tienen la misma probabilidad de salir por ejemplo de 2 puedo pasar a 10 como puedo pasar a 3 generando a veces saltos mas bruscos , mientras que con noise los saltos son muchisimos mas suaves y no tangrandes , generando transciciones mucho mas suaves en vez de bruscas que es lo que pasaria con random 

**Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?**
una distribucion de probabilidad es la probabilidad de que ocurra o salga un resultado en una pool de diferentes acontecimientos por ejemplo un dado tiene 6 posibilidades pero todas tiene las misma probabilidad de salir , con la distribucion uniforme todos los valores tienen la misma probabilidad de salir de salir como el caso del dado donde todos tienen la mismas probabilidad esto en una caminata aleatoria va a causar que el movimiento sea mas erratico por que van a estar saliendo valores iguales o diferentes todo el tiempo , mientras que con la distribucion normal es como uan campana de gauss esto queriendo decir que los resulatados que mas a van a salir son los mas cercanos a la media pro ejemplo de numeros entre 1-100 los numeros que mas van a salir son los que estenmas cercanos al 50 , esto en la caminata aleatoria hacen que los pasos sean mas cercanos al centro  y suaves y no salen tantos grandes saltos 

**¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple**
La aleatoriedad cumple un grna papel en el arte generativo por que esta es la que hace que cada obra sea diferente una de la otra aunque se genere con los mismos parametros haciendo que cada obra se vuelva unica, como diej anteriromente lo que permite la aleatoriedad  es cada cada obra llegue a ser diferente entre si y ambien gracias a esta se pueden ilustra patrones que ocurren en la vida real el movimeineto del agua como se mueve un insecto por ejemplo el perlin es algo que serviria para estos casos 

**Piensa en tu obra final (Actividad 08). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.**
En mi obra utilice el ruido perlin para hacer que un triangulo tuviera una caminata aleatoria  que fuera suave y no muy brusca tambien para que se sintiera como algo tranquilo  , lo quice hacer asi para que los triangulos generaran una especie de ruido en el centro de la obra y que al mismo tiempo que el lago tang peuqeños pedazos de tierra dentro de si 

**Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?**
una caminata es el camino que deja una forma por asi decirlo la forma va moviendose por el lienzo dejando una estela que va mostrando por donde a pasado nunca sigue un camino prederteminado siempre va haciendo paso al azar lo que si puede pasar es que pase mas por una posicion ue por otras , una caminata con levy flight lo que va a hacer es que la forma vaya dando pequeños pasos pasos cercanos entre si pero de vez encuando va a dar un gran paso haciendo que se produzcan caminos compactos pero de vez en cuando el camino se aleje 
#### parte 2
**¿Cuál fue el concepto más abstracto o difícil de “visualizar” para ti en esta unidad? ¿Qué hiciste para finalmente comprenderlo?**
Siento qur al principio fue ver como desde la programacion como implementar los diferentes tipos de caminatasy aprender a diferenciarlars , al final despues de ver algo de documentacion y modificando cosas dentro del codigo vi como iba cambiando las cosas y al final pude verlo de una manera mas clara 
**Describe un momento durante el desarrollo de tu obra final (Actividad 08) en el que un “error” o un resultado inesperado te llevó a una idea creativa interesante.**
Estaba experimentando con el ruido perlin y el movimiento de los triangulos para que siguieran un cierto patron para que formaran una obra mas clara , pero despues de trbajar con el me gusto la forma en la que los triangulos se movian  formando patrones que me terminaron gustando mucho mas de la idea ORIGNAL QUE HABIA PENSADO 
**Al combinar diferentes técnicas de aleatoriedad, ¿Cuál fue el mayor desafío? ¿La interacción entre los sistemas, el control de los parámetros, el rendimiento?**
En cuanto a mi el mayor problema fue implementarlos todos y que no hubiera problemas entre ellos que de pronto implementaba algo pero cuando iba a probar terminaba modifiando otra cosa y asi 
**Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?**
Empezar con mas orden por que al principio empece metiendo cosas a la loca y todo se iba volviendo un pupurry de codigo creando mucho desorden loq eu hacia que trnajar se volviera mas complicado , gracias a eso me toco empezar desde 0 
