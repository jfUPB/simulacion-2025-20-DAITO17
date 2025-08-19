# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 09

##Friccion##



**Explica cómo modelaste cada fuerza.**
 La fuerza esta modelada como un cambio en la velocidad no directamente en la acceleracion , si no mas bien esta dentro del viento que se utiliza la obra disminuyendo la velocidad de las bolitas

 
**Conceptualmente cómo se relaciona la fuerza con la obra generativa.**

lo que pasa en el codigo es que cuando se arrastra el mouse para la izquierda o derecha crea una fuerza que arrastra todas las particulas hacia la dirrecion en la que se arrastro el mouse como simulando el viento y luego la friccion actua aqui disminuyendo la velocidad multiplicandola por 0.99 y esto sucede en cada frame 


[Sketch friccion](https://editor.p5js.org/DAITO17/sketches/5FfrWLUbi)

``` js 
let particles = [];
let friction = 0.99;
let windForce = 0;  
let lastMouseX;

function setup() {
  createCanvas(800, 600);
  background(0);
  for (let i = 0; i < 100; i++) {
    particles.push(new Particle(random(width), random(height), random(-2, 2), random(-2, 2)));
  }
}

function draw() {
  background(0);

  
  windForce *= 0.95;

  for (let p of particles) {
    p.applyForce(windForce);
    p.update();
    p.show();
  }
}


function mouseDragged() {
  if (lastMouseX !== undefined) {
    let dragSpeed = mouseX - lastMouseX;
    windForce = constrain(dragSpeed * 0.05, -1, 1); 
  }
  lastMouseX = mouseX;
}


function mouseReleased() {
  lastMouseX = undefined;
}

class Particle {
  constructor(x, y, vx, vy) {
    this.x = x;
    this.y = y;
    this.vx = vx;
    this.vy = vy;
    this.color = color(random(255), random(255), random(255));
  }

  applyForce(force) {
    this.vx += force; 
  }

  update() {
    this.vx *= friction;
    this.vy *= friction;
    this.x += this.vx;
    this.y += this.vy;

    // Rebote en los bordes
    if (this.x < 0 || this.x > width) {
      this.vx *= -1;
      this.x = constrain(this.x, 0, width);
    }
    if (this.y < 0 || this.y > height) {
      this.vy *= -1;
      this.y = constrain(this.y, 0, height);
    }
  }

  show() {
    noStroke();
    fill(this.color);
    ellipse(this.x, this.y, 8);
  }
}
```
<img width="847" height="650" alt="image" src="https://github.com/user-attachments/assets/33a02479-af06-4123-9ce2-3e3f565f03bb" />



##Resistencia al aire y fluido#

**Explica cómo modelaste cada fuerza.**


En el código las fuerza se modelaronusando vectores más la segunda ley de Newton  Simulando la resistencia del aire, se aplica una fuerza que es opuesta a la velocidad del objeto,   a mayor velocidad, mayor resistencia. Por otro lado, la resistencia del fluido  , donde la fuerza depende de el cuadrado de la velocidad. En medios densos, por ejemplo el agua, por lo tanto, la resistencia aumenta mucho más. Ambas fuerzas se aplican mediante la suma de vectores que imitan cómo el aire o el fluido frenan el movimiento de un objeto reduciendo la velocidad.


**Conceptualmente cómo se relaciona la fuerza con la obra generativa.**

se relaciona de manera que por ejmplo si el fluido esta prendido las particulas se moveran mas lentamente por que se esta aplicando al resistencia al fluido mientras que si el fluido esta apagado estas se movera mas erraticamente y rapido por que no se esta aplicando la resistencia del fluido y aire 


[sketch aire y fluido](https://editor.p5js.org/DAITO17/sketches/0TaCd-s63)


``` js 
let particles = [];
let fluidResistance = true;
let fluidDensity = 0.02;  
let shakeForce = 0;

function setup() {
  createCanvas(800, 600);
  background(0);
  for (let i = 0; i < 100; i++) {
    particles.push(new Particle(random(width), random(height), random(-2, 2), random(-2, 2)));
  }
}

function draw() {
  background(0);

  
  shakeForce *= 0.9;

  for (let p of particles) {
    if (fluidResistance) {
     
      let velocity = createVector(p.vx, p.vy);
      let drag = calcularFuerzaArrastre(velocity, fluidDensity, 0.47, 1); 
      p.applyForce(drag);
    }

    
    if (shakeForce > 0.1) {
      let randomForce = p5.Vector.random2D();
      randomForce.mult(shakeForce);
      p.applyForce(randomForce);
    }

    p.update();
    p.show();
  }

  
  fill(255);
  textSize(16);
  text(`Fluido: ${fluidResistance ? "ON" : "OFF"}`, 10, 20);
  text(`Densidad: ${nf(fluidDensity, 1, 3)}`, 10, 40);
  text(`Controles: f (fluido), a/d (densidad), n (nuevas partículas), SPACE (agitar)`, 10, height - 20);
}

function keyPressed() {
  if (key === 'f') {
    fluidResistance = !fluidResistance;
  }
  if (key === 'a') {
    fluidDensity = min(fluidDensity + 0.01, 0.5);
  }
  if (key === 'd') {
    fluidDensity = max(fluidDensity - 0.01, 0);
  }
  if (key === 'n') {
    for (let i = 0; i < 20; i++) {
      particles.push(new Particle(random(width), random(height), random(-2, 2), random(-2, 2)));
    }
  }
  if (key === ' ') { 
    shakeForce = 3; 
  }
}

// === Función para calcular fuerza de arrastre ===
function calcularFuerzaArrastre(velocidad, densidad, coefArrastre, area) {
  if (!(velocidad instanceof p5.Vector)) {
    return createVector(0, 0);
  }
  let v = velocidad.mag();
  if (v === 0) return createVector(0, 0);

  let drag = velocidad.copy().normalize().mult(-1); // dirección opuesta
  let magnitud = 0.5 * densidad * v * v * coefArrastre * area;
  drag.mult(magnitud);

  return drag;
}

class Particle {
  constructor(x, y, vx, vy) {
    this.x = x;
    this.y = y;
    this.vx = vx;
    this.vy = vy;
    this.color = color(random(255), random(255), random(255));
  }

  applyForce(force) {
    this.vx += force.x;
    this.vy += force.y;
  }

  update() {
    this.x += this.vx;
    this.y += this.vy;

    // Rebote en bordes
    if (this.x < 0 || this.x > width) {
      this.vx *= -1;
      this.x = constrain(this.x, 0, width);
    }
    if (this.y < 0 || this.y > height) {
      this.vy *= -1;
      this.y = constrain(this.y, 0, height);
    }
  }

  show() {
    noStroke();
    fill(this.color);
    ellipse(this.x, this.y, 8);
  }
}

```
<img width="798" height="594" alt="image" src="https://github.com/user-attachments/assets/825d1c2e-33d6-48c8-bfc9-80e12c2b3d22" />

##Atraccion gravitacional##

**Explica cómo modelaste cada fuerza.**


el planeta atrae a cada satélite en dirección hacia su centro, además esa atracción depende de qué tan lejos están uno del otro, así como de la masa del planeta y del satélite. La fuerza resulta ser más fuerte mientras más cerca están ellos. Es mucho más débil mientras más lejos están. El movimiento orbital se genera al traducirse esa fuerza hacia una aceleración para el satélite, cambiando su velocidad y posición con el tiempo.

**Conceptualmente cómo se relaciona la fuerza con la obra generativa.**

Primero hay una bola en el centro y a medida que se van generando los satelites estos se ven atraidos por la fuerza de la bola haciendo qu estos siempre tengan diferentes posiciones y no se queden quietos 

[sketch Atraccion gravitacional](https://editor.p5js.org/DAITO17/sketches/KqiApdbne)


``` js 
let planet;
let satellites = [];
let G = 1; 
let dragging = false;

function setup() {
  createCanvas(800, 600);
  planet = new Planet(width / 2, height / 2, 50, 2000); 
}

function draw() {
  background(10);

 
  if (dragging) {
    planet.pos.set(mouseX, mouseY);
  }

  planet.show();

  for (let s of satellites) {
    let force = planet.attract(s); // Fuerza gravitacional
    s.applyForce(force);
    s.update();
    s.show();
  }

  // Instrucciones
  fill(255);
  textSize(16);
  text("Presiona 1(baja), 2(media) o 3(alta) para agregar satélites con diferentes velocidades", 20, 20);
  text("Arrastra el planeta con el mouse para moverlo", 20, 40);
}

function keyPressed() {
  if (key === '1') {
    satellites.push(new Satellite(random(width), random(height), random(5, 15), 5, createVector(random(-1, 1), random(-1, 1))));
  } else if (key === '2') {
    satellites.push(new Satellite(random(width), random(height), random(5, 15), 5, createVector(random(-3, 3), random(-3, 3))));
  } else if (key === '3') {
    satellites.push(new Satellite(random(width), random(height), random(5, 15), 5, createVector(random(-5, 5), random(-5, 5))));
  }
}

function mousePressed() {
  let d = dist(mouseX, mouseY, planet.pos.x, planet.pos.y);
  if (d < planet.r) {
    dragging = true;
  }
}

function mouseReleased() {
  dragging = false;
}

class Planet {
  constructor(x, y, r, m) {
    this.pos = createVector(x, y);
    this.r = r;
    this.mass = m;
  }

  show() {
    fill(0, 100, 255);
    noStroke();
    ellipse(this.pos.x, this.pos.y, this.r * 2);
  }

  attract(satellite) {
    let force = p5.Vector.sub(this.pos, satellite.pos);
    let distanceSq = constrain(force.magSq(), 100, 5000); 
    let strength = (G * this.mass * satellite.mass) / distanceSq;
    force.setMag(strength);
    return force;
  }
}

class Satellite {
  constructor(x, y, r, m, vel) {
    this.pos = createVector(x, y);
    this.vel = vel;
    this.acc = createVector(0, 0);
    this.r = r;
    this.mass = m;
  }

  applyForce(f) {
    let a = p5.Vector.div(f, this.mass);
    this.acc.add(a);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show() {
    fill(255, 200, 0);
    noStroke();
    ellipse(this.pos.x, this.pos.y, this.r * 2);
  }
}
```
<img width="796" height="609" alt="image" src="https://github.com/user-attachments/assets/e1f13aca-7c58-4287-b8e1-eabfe59ff78d" />
