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

bueno la modificacion que hice esta dentro del metodo flock subiendole mas la separacion la alineacion se la baje y la cohesion sigue igual gracias a esto los boids se dispersan mas rapido ya no se alinea tanto esto provocando como si fuera un enjambre pero cada agente tiene muy buen espacio los unos de los otros tambien genera un poco de desorden en los patrones de movimiento 

<img width="638" height="241" alt="image" src="https://github.com/user-attachments/assets/db4389e4-813a-496a-9f09-32830d48469c" />


## Actividad 05


<img width="957" height="537" alt="image" src="https://github.com/user-attachments/assets/5ef4183a-8a29-4a38-9670-252c4251c09e" />

<img width="957" height="540" alt="image" src="https://github.com/user-attachments/assets/645f4fbf-195c-43cc-944d-20a39e0edb36" />

Bueno para este trbajo lo que quiero hacer es usando un flow field que las particulas se vayan moviendo como en grupitos , ademas de esto quiero ver si puedo hacer que el color de las particulas cambien con base en la musica en caso de que no lo logre hare que cambien de color con un lerp  ademas de eso agragar que con  flechas del teclado cambien de dirrecion las particulas , generar como una especie de quick para que cuando en la cancion lo haga yo igual lo pueda hacer y por ultimo poder cambiar la cohesion en tiempo real . Siento que con esto puedo llegar a tener el suficiente control de la obra para modificarla en tiempo real y poderla tocar en tiempo real 

**La cancion que legi es polynomical-c de aphex twin**
``` js
let flock = [];
let song;
let fft;
let steerGlobal;

let colorA, colorB;

// Tamaño de la celda para la grilla espacial
let cellSize = 50;
let grid = {};

// ---- NUEVO: peso ajustable para la cohesión ----
let cohesionWeight = 0.8;

function preload() {
  song = loadSound("Polynomial-C2.mp3"); // tu canción
}

function setup() {
  createCanvas(800, 600);
  fft = new p5.FFT();
  song.loop();

  steerGlobal = createVector(0, 0);

  colorA = color(200, 50, 255); // morado
  colorB = color(0, 255, 200);  // verde agua marina

  // Crear boids
  for (let i = 0; i < 350; i++) {
    flock.push(new Boid(random(width), random(height)));
  }
}

function draw() {
  background(20);

  // FFT
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let bassLevel = map(bass, 0, 255, 0, 1);

  // Limpiar grilla
  grid = {};

  // Repartir boids en celdas
  for (let boid of flock) {
    let gx = floor(boid.position.x / cellSize);
    let gy = floor(boid.position.y / cellSize);
    let key = gx + "," + gy;
    if (!grid[key]) grid[key] = [];
    grid[key].push(boid);
  }

  // Actualizar boids
  for (let boid of flock) {
    boid.flock(getNeighbors(boid));
    boid.applyForce(steerGlobal);
    boid.update();
    boid.edges();
    boid.show(bassLevel);
  }

  steerGlobal.mult(0.9);

  // Mostrar valor de cohesión actual
  fill(255);
  noStroke();
  textSize(14);
  text("Cohesion weight: " + cohesionWeight.toFixed(2), 10, height - 10);
}

// Obtener vecinos desde la grilla
function getNeighbors(boid) {
  let neighbors = [];
  let gx = floor(boid.position.x / cellSize);
  let gy = floor(boid.position.y / cellSize);

  // Revisar celda actual + vecinas
  for (let i = -1; i <= 1; i++) {
    for (let j = -1; j <= 1; j++) {
      let key = (gx + i) + "," + (gy + j);
      if (grid[key]) {
        neighbors = neighbors.concat(grid[key]);
      }
    }
  }
  return neighbors;
}

function keyPressed() {
  if (keyCode === UP_ARROW) steerGlobal.add(createVector(0, -0.5));
  if (keyCode === DOWN_ARROW) steerGlobal.add(createVector(0, 0.5));
  if (keyCode === LEFT_ARROW) steerGlobal.add(createVector(-0.5, 0));
  if (keyCode === RIGHT_ARROW) steerGlobal.add(createVector(0.5, 0));

  // Barra espaciadora: "kick" que sacude todo
  if (key === ' ') {
    for (let boid of flock) {
      let kick = p5.Vector.random2D().mult(random(3, 6));
      boid.applyForce(kick);
    }
  }

  // ---- NUEVO: control de cohesión ----
  if (key === 'a' || key === 'A') {
    cohesionWeight += 0.1;
  }
  if (key === 'd' || key === 'D') {
    cohesionWeight -= 0.1;
    cohesionWeight = max(0, cohesionWeight); // evitar negativos
  }
}

// ----------------- Clase Boid -----------------
class Boid {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = p5.Vector.random2D();
    this.velocity.setMag(random(2, 4));
    this.acceleration = createVector();
    this.maxForce = 0.2;
    this.maxSpeed = 3;
  }

  edges() {
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }

  align(boids) {
    let perceptionRadius = 40;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        steering.add(other.velocity);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  cohesion(boids) {
    let perceptionRadius = 40;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        steering.add(other.position);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.sub(this.position);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  separation(boids) {
    let perceptionRadius = 20;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        let diff = p5.Vector.sub(this.position, other.position);
        diff.div(d * d);
        steering.add(diff);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  flock(boids) {
    let alignment = this.align(boids);
    let cohesion = this.cohesion(boids);
    let separation = this.separation(boids);

    alignment.mult(1.0);
    cohesion.mult(cohesionWeight); // <-- ahora depende de la variable global
    separation.mult(1.2);

    this.applyForce(alignment);
    this.applyForce(cohesion);
    this.applyForce(separation);
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.position.add(this.velocity);
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.acceleration.mult(0);
  }

  show(bassLevel) {
    let t = (sin(frameCount * 0.01) + 1) / 2;
    let col = lerpColor(colorA, colorB, t);

    let arrowSize = map(bassLevel, 0, 1, 6, 20);

    push();
    translate(this.position.x, this.position.y);
    rotate(this.velocity.heading());
    fill(col);
    stroke(col);
    strokeWeight(1);
    beginShape();
    vertex(0, -arrowSize * 0.3);
    vertex(arrowSize, 0);
    vertex(0, arrowSize * 0.3);
    endShape(CLOSE);
    pop();
  }
}
``` 
[enlace al codigo en p5](https://editor.p5js.org/DAITO17/sketches/_4IAyqzmK)

<img width="800" height="596" alt="image" src="https://github.com/user-attachments/assets/52b97f8d-1f9f-42ad-b253-552a2939df04" />


## Autoevaluacion 

YO siento que para esta unidad me merezco un 5 , esto gracias a que desarolle todas las actividades tal y como estaban propuestas en la bitacora siguiendo toodos los paso y yo siendo que el que diseña y no chatgpt


