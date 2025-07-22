# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
La aleatoriedad es lo que le da la huella a cada pieza de arte. 

###  Actividad 02
El papel de la aleatoriedad en al obra de sofia siento que es como se mueve los puntos haciendo que se creen figuras que hasta cierto siguen como la musica pero de igual manera tienen algo de aleatoriedad en su creacion
de igual manera siento que los colores que van surgiendo son aleatorios. 

En mi campo de trabajo que es el 3d desde el modelado hasta simulaciones , la aleatoriedad juega un papel importante a que como dije esta misma hace cada obra no sea igual a otra empezando desde las diferente ubicacion de puntos en una texturas hasta como cae una gota de agua en una simulacion , la aleatoriedad me parece algo muy lindo que esta en todo y en especial a nuestras areas de trbajo y como cada cosas puede llegar a ser unica gracias a esta.

### Actividad 03 
**Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.**
Lo que voy a hacer es modificiar el numero total aleatorio para pasarlo de 0 a 4(en el codigo quedaria  asi const choice = floor(random(5));), de esta forma por el else del codigo lo que hara es que el walker vaya hacia arriba 

**Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?**
Si ocurrio lo esperaba el walker fue para arriba generando como una especie de un palito de arbol 

### Actividad 04 
**En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.**
Con la distribucion uniforme lo que pasa es que cada uno tiene la misma probabilidad en a infinidad de numeros que haya mientras que con la distribucion no uniforme pasa lo contrario haciendo que haya numeros que tengan mas probabilidades de salir que otros 
**En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.**

<img width="1606" height="599" alt="image" src="https://github.com/user-attachments/assets/3f460922-0b88-4588-a26f-1a5eeeffd4a5" />

Aqui lo que hice fue aumentar el valor de ranom a 5 haciendo que se generen numeros de 0 4 esto hasta le momento seguira una distribucion uniforme pero con la modificacion que le hice que pueda generar mas numeros lo cambie a una distribucion no uniforme  y el x ++ es el que hace que el walker vaya mas hacia la derecha es el que le asigno para que sea el else por que los otros valores que son 0 , 1, 2 solamente dibujaria para ese lado en caso de que salga con ese numero pero con el else dibuja cuando le salen 3 o 4 siendo mas numeros haciendo que dibuje mas para la derecha


### Actividad 05 
**Copia el código en tu bitácora.**

function setup() {
  createCanvas(640, 240);
  background(255);
  noStroke();
}

function draw() {
  let x = 320; // Fijo en el centro horizontal
  let y = randomGaussian(120, 60); 

  fill(0, 10);

 
  let size = 16;
  triangle(
    x, y,                 
    x - size / 2, y + size, 
    x + size / 2, y + size  
  );
}


**Coloca en enlace a tu sketch en p5.js en tu bitácora.**

https://editor.p5js.org/DAITO17/sketches/y-gQW0F-g

**Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.**
<img width="1537" height="442" alt="image" src="https://github.com/user-attachments/assets/d1b1756d-08d2-45c4-a659-6b370dd3c1a0" />
