# Evidencias de la unidad 8

## Actividad 01 

### Describe tus observaciones sobre la conexión sonido-imagen en al menos dos de las performances vistas.

Bueno mas que todo hubieron dos momentos que me llamaron la atencion en los links el primero fue LE PARODY & ALBA G. CORRAL — En directo en el Teatro Principal de Zaragoza en el minuto 11 donde se ven los acuadrados por que sinto que aqui la musica le estaba dando vida a estos mismos respiraban como la musica se hacian mas grandes o mas pequeños segun la misma musica . El segundo momento que me llamo mucho la atencion fue el de become ocean de jonh adams esto por que con lo del fractal sentia que por ejemplo con el sonido del piano se iba expandiendo y volviendose mas grande pero de iugal manera hbainedo puntos donde este tenia que cambiar de fortma desde los fractal , se que los cuadros que dije y de los fractales no tienen que ver mucho estos mismos con otros pero de igual manera me gustaria buscar una manera de incorporarlos en un mismo proyecto 

### Explica qué elementos te parecieron generativos y por qué crees que cada visualización sería única.
Siento que donde mas hubo elementos generativos fue en o ocean con el fractal esto dado por que siento que habia alguien manejandolo para que fuera generandose asi mismo ademas de crecer y una vez que ya hubiera crecido lo suficiente se convierte en algo diferente , en cuantto a lo de los caudrso no siento que haya sido tan generativo puesto que los cuadros reaccionaban perfectamente a la musica algo que yo creo que seria muy compliocado de conseguir y siento que ahi de igual manera esta la belleza de los gneerativo puesto que como cada persona es diferente al mismo tiempo los visuales terndran cosas unicas dependiendo de quien los toque 


### Comparte tu reflexión sobre la sensación de “liveness”.
siento que esto le da una belleza unica cada visuale no importa si la misma persona ya a tocado el mismo visuale por cuenta propia siempre va a ver algo nuevo algo que haga que la obra sea unica a su manera siendo que cada show no sea repicable de alguna manera 



## Actividad 02

### La pieza musical elegida (con enlace/archivo si es posible).
Elegi end sky de c678924  [link de la cancion ](https://www.youtube.com/watch?v=KUjGkwuct8Y&list=RDKUjGkwuct8Y&start_radio=1)

### La descripción de tu concepto visual.
Bueno voy a trbajar con particulas que van a hacer circulos los cuales van a ser reactivos a la musica cambiando su tamaño y comportamineto  que igual manera se van a ir moviendo por todo el lienzo cuando una particula llega al borde de algo reaparece del otro lado 

### Los inputs seleccionados y la justificación de por qué los elegiste.
Bueno ademas del audio voya utilizar teclado mouse y unso slider el audio va a cambiar el tamaño de las particulas con el wasd voy a mover la dirrecion de las particulas con el click del mouse se puede cambiar los colores de las particulas y por ultimo con los sliders podre modificar que tan cerca estan o que tan lejos la velocidad de las particulas y por ultimo la cantidad de particulas dentro del lienzo 

### ¿Qué algoritmos o técnicas planeas usar (ej: flow fields, flocking, física, partículas, etc.) y por qué?
voy a utilizar particulas que se van a mover con base a la musica aunque de iugal manera le quiero poner un movimiento que se base en la musica 


### Tus bocetos y una explicación de cómo los inputs influirán en los visuales.
<img width="959" height="544" alt="image" src="https://github.com/user-attachments/assets/b0e209eb-3309-4244-8f0f-8edd414480f8" />

la explicaciones de los inputs ya esta escrita en la pregunta de los inputs seleccionados 

## Actividad 03

### El código fuente completo de tu sketch en p5.js.

``` js
let song;
let fft;
let circles = [];
let baseSpeed = 1.0;

let separationSlider;
let amountSlider;
let speedSlider;

let globalDirection;
let colorPalette = [];
let currentColorIndex = 0;
let currentColor;

let kickForce = 0;
let breathingPhase = 0;
let kickPulse = 0;

function preload() {
  song = loadSound("End Sky.mp3");
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  noStroke();
  fft = new p5.FFT();
  song.loop();

  globalDirection = createVector(0, 0);

 
  colorPalette = [
  [255, 70, 50],
  [255, 140, 0],
  [180, 70, 255]
];
currentColor = color(...colorPalette[currentColorIndex]);

  
  separationSlider = createSlider(0, 200, 80, 1);
  separationSlider.position(20, 20);
  separationSlider.style('width', '200px');

  amountSlider = createSlider(0, 400, 0, 1);
  amountSlider.position(20, 50);
  amountSlider.style('width', '200px');

  speedSlider = createSlider(0.2, 3, 1, 0.1);
  speedSlider.position(20, 80);
  speedSlider.style('width', '200px');
}

function draw() {
  background(10, 10, 30, 100);

  
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let mid = fft.getEnergy("mid");
  let treble = fft.getEnergy("treble");


  let numCircles = int(amountSlider.value());
  baseSpeed = speedSlider.value();
  let repulsionValue = separationSlider.value();

  while (circles.length < numCircles) {
    circles.push(new Circle(random(width), random(height), currentColor));
  }
  while (circles.length > numCircles) {
    circles.pop();
  }

 
  let totalEnergy = (bass * 0.5 + mid * 0.3 + treble * 0.2);
  totalEnergy = map(totalEnergy, 0, 255, 0.5, 2.0);

  breathingPhase += 0.05;
  let breathingOffset = sin(breathingPhase) * 0.15 + 1;

  kickForce *= 0.9;
  kickPulse *= 0.85;

  for (let c of circles) {
    c.update(bass, mid, treble, kickForce, kickPulse, globalDirection, totalEnergy, breathingOffset, repulsionValue);
    c.display();
    c.edges();
  }

  fill(255);
  textSize(14);
  text("Repulsión: " + nf(separationSlider.value(), 1, 0), 240, 35);
  text("Cantidad: " + nf(amountSlider.value(), 1, 0), 240, 55);
  text("Velocidad: " + nf(speedSlider.value(), 1, 1), 240, 75);
  text("ESPACIO = Kick | WASD = Dirección | ENTER = Pantalla completa | CLIC IZQ = Cambiar color", 20, height - 20);
}

function keyPressed() {
  if (key === 'w' || key === 'W') globalDirection = createVector(0, -1);
  if (key === 's' || key === 'S') globalDirection = createVector(0, 1);
  if (key === 'a' || key === 'A') globalDirection = createVector(-1, 0);
  if (key === 'd' || key === 'D') globalDirection = createVector(1, 0);

  if (keyCode === ENTER) fullscreen(!fullscreen());

 
  if (key === ' ') {
    kickForce = 15;
    kickPulse = 1.5;
    for (let c of circles) {
      let impulse = p5.Vector.random2D().mult(random(2, 3));
      c.vel.add(impulse);
    }
  }
}

function mousePressed() {
  if (mouseButton === LEFT) {
    currentColorIndex = (currentColorIndex + 1) % colorPalette.length;
    currentColor = colorPalette[currentColorIndex];
    for (let c of circles) {
      c.setColor(currentColor);
    }
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

class Circle {
  constructor(x, y, col) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.2, 0.5));
    this.baseSize = random(30, 40);
    this.currentSize = this.baseSize;
    this.color = col;
  }

  setColor(newColor) {
    this.color = newColor;
  }

  update(bass, mid, treble, kickForce, kickPulse, direction, totalEnergy, breathingOffset, repulsionValue) {
    let repulsionStrength = repulsionValue / 1000;

    let movementStrength = map(totalEnergy, 0.5, 2.0, 0.1, 1.2) * baseSpeed;
    let flow = p5.Vector.random2D().mult(movementStrength * 0.3);
    this.vel.add(flow);

   
    this.vel.add(direction.copy().mult(0.3));

   
    if (kickForce > 0.1) {
      this.vel.add(p5.Vector.random2D().mult(kickForce * 0.05));
    }

   
    for (let other of circles) {
      if (other != this) {
        let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
        if (d < 100 && d > 0) {
          let force = p5.Vector.sub(this.pos, other.pos);
          force.normalize();
          force.div(d);
          force.mult(repulsionStrength * (100 - d));
          this.vel.add(force);
        }
      }
    }

 
    this.vel.limit(1.5 * baseSpeed);
    this.pos.add(this.vel);
    this.vel.mult(0.93);

   
    let bassInfluence = map(bass, 0, 255, 0.8, 1.8);
    let breathing = breathingOffset * bassInfluence * (1 + kickPulse * 0.3);
    this.currentSize = lerp(this.currentSize, this.baseSize * breathing, 0.1);
  }

  display() {
    fill(red(this.color), green(this.color), blue(this.color), 180);
    ellipse(this.pos.x, this.pos.y, this.currentSize);
    noFill();
    stroke(red(this.color), green(this.color), blue(this.color), 120);
    ellipse(this.pos.x, this.pos.y, this.currentSize * 1.4);
    noStroke();
  }

  edges() {
    if (this.pos.x > width) this.pos.x = 0;
    if (this.pos.x < 0) this.pos.x = width;
    if (this.pos.y > height) this.pos.y = 0;
    if (this.pos.y < 0) this.pos.y = height;
  }
}

```

### Un enlace a tu sketch en el editor de p5.js.
[Link del codigo en p5.js](https://editor.p5js.org/DAITO17/sketches/H5TvAt5fS)


###Capturas de pantalla mostrando tu pieza en acción.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ca3756c6-bfaf-4a66-89af-620e3979f3a9" />
<img width="1914" height="1070" alt="image" src="https://github.com/user-attachments/assets/1429f81e-ce77-4799-80ed-0bb03085902c" />




