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


###   Actividad 6
**Explica por qué usaste esta técnica y qué resultados esperabas obtener.**
 bueno hablando del levy flight en el codgio primero cogi el ejemplo de la actividad anterior pero en evz de que se pinte verticalmente se pinta horizontalmente , ahora si hablando del levy , el let beta es lo que define cuan grandes pueden ser los saltos  , el let u random  genera un numero aleotorio u queesta entre 0 y 1 y por ultimo el pow lo que hace es que  transform el numero en una potencia para que este siga una distribuciond e levy esto hace que genere pequeño saltos la mayoria del tiempo pero a veces genera alguno grande entre mas pequeño sea el numero mas grande es el salto  gracias a la division de -1/beta 

 **Copia el codgio en tu bitacora**

 let x = 320; // posición inicial horizontal
let y = 120; // fijo en el centro vertical

function setup() {
  createCanvas(640, 240);
  background(255);
  noStroke();
}

function draw() {
 
  let step = levy();
  x += step;

 
  x = constrain(x, 0, width);

  fill(0, 10);

  let size = 16;
  // Triángulo apuntando hacia arriba
  triangle(
    x, y,
    x - size / 2, y + size,
    x + size / 2, y + size
  );
}

// Función de paso tipo Lévy (colas largas)
function levy() {
  let beta = 1.5;
  let u = random(1);
  let step = pow(u, -1 / beta);

  // Aleatoriedad de dirección: izquierda o derecha
  if (random() < 0.5) step *= -1;

  return step;
}
**Coloca en enlace a tu sketch en p5.js en tu bitácora.**

https://editor.p5js.org/DAITO17/sketches/eVPw9hHJ9

**Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.**
<img width="1603" height="722" alt="image" src="https://github.com/user-attachments/assets/89d65acb-2295-4a5f-8628-5aa8713198eb" />

###  Actividad07 
**Explica el concepto qué resultados esberabas obtener.**
Los resultados que espero es que un circulo este pintando otro circulo y dejando un path por donde pasa pero este circulo el cual se esta pintando nunca va a terminar de cerrar por como funciona el noise que utilizare para el perlin , entonces al final va  a quedar una c 

**copia el codigo en tu bitacora**
let t = 0;

function setup() {
  createCanvas(640, 240);
  background(255);
  stroke(0, 20);
  fill(0, 10);
}

function draw() {
  let radius = 80;
  let angle = noise(t) * TWO_PI;
  let x = width / 2 + cos(angle) * radius;
  let y = height / 2 + sin(angle) * radius;

  ellipse(x, y, 10, 10);

  t += 0.01;
}

**Coloca en enlace a tu sketch en p5.js en tu bitácora.**
https://editor.p5js.org/DAITO17/sketches/fETtOsERG

**Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.**
<img width="1604" height="691" alt="image" src="https://github.com/user-attachments/assets/26783713-f42a-45a3-a550-d3df86fe5fa8" />
