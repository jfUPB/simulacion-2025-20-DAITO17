# Evidencias de la unidad 4

## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> El concepto que aplique fue el del pendulo con este funciona que es un pendulo que se puede mover con el mouse pero que al mismo tiempo tiene una fuerza de atraccion que atrae los movers que hay moviendose por todo el canvas tambien dependende de la fuerza de atraccion que el pendulo tenga 
>

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> En cuanto lo de la unidad 3 me gusto mucho como el problema de los n cuerpos y la atraccion entonces le implemente que el pendulo tuviera atraccion similar a lo de los n cuerpos dependiendo de la fuerza de atraccion los movers estaran mas cerca del pendulo o lo empezaran a orbitar cuando la atraccion baja los movers algunos se pueden llegar a escapar de igual manera cuando el pendulo se mueve igual los movers se desprenden del pendulo 
>

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Utilice el motion 101 y la forma en la que esta palicado es en lo movers la aceleracion modifica la velocidad y esta modifica la posicion y en cada frame se resetea la aceleracion 
>

* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Utilice levy flight junto con perlin noise para el movimiento de los movers esto haciendo que tengan un comportamiento impredesible y al mismo tiempo natural 
>

## ¿Cómo resolviste la interacción?
> La interaccion la resolvvi con dos cosas fundamentales la primera qes que el pendulo se puede mover con el mouse , segundo se le puede aumentar o disminuir  la atraccion que tiene el pendulo pr ultimo se pueden agregar mas movers a la obra para que hayas mas cuerpos moviendose
>

## Enlace a la obra en el editor de p5.js

[Obra actividad 4 ](https://editor.p5js.org/DAITO17/sketches/-I9m142yU)

## Código de la obra 

``` js
let pendulum;
let movers = [];
let G = 0.8; 
let addButton, increaseButton, decreaseButton;

function setup() {
  createCanvas(800, 600);
  pendulum = new Pendulum(createVector(width / 2, 100), 200);
  for (let i = 0; i < 5; i++) {
    movers.push(new Mover(random(width), random(height)));
  }

  
  addButton = createButton("Agregar Mover");
  addButton.position(10, 10);
  addButton.mousePressed(() => movers.push(new Mover(random(width), random(height))));

  increaseButton = createButton("Aumentar Atracción");
  increaseButton.position(120, 10);
  increaseButton.mousePressed(() => G += 0.2);

  decreaseButton = createButton("Disminuir Atracción");
  decreaseButton.position(260, 10);
  decreaseButton.mousePressed(() => G = max(0.1, G - 0.2));
}

function draw() {
  background(20);

  pendulum.update();
  pendulum.display();

  fill(255);
  textSize(18);
  text(`Fuerza de atracción: ${G.toFixed(2)}`, 20, 50);

  for (let mover of movers) {
    let orbitForce = pendulum.orbit(mover);
    mover.applyForce(orbitForce);

    mover.update();
    mover.display();
  }
}


class Pendulum {
  constructor(origin, r) {
    this.origin = origin.copy();
    this.position = createVector();
    this.r = r;
    this.angle = PI / 4;
    this.aVelocity = 0;
    this.aAcceleration = 0;
    this.ballRadius = 32;
    this.dragging = false;
  }

  update() {
    if (!this.dragging) {
      let gravity = 0.4;
      this.aAcceleration = (-1 * gravity / this.r) * sin(this.angle);
      this.aVelocity += this.aAcceleration;
      this.aVelocity *= 0.99;
      this.angle += this.aVelocity;
    }
    this.position.set(
      this.r * sin(this.angle),
      this.r * cos(this.angle),
      0
    );
    this.position.add(this.origin);
  }

  display() {
    stroke(255);
    strokeWeight(2);
    line(this.origin.x, this.origin.y, this.position.x, this.position.y);

    fill(255);
    ellipse(this.position.x, this.position.y, this.ballRadius, this.ballRadius);

    noStroke();
    fill(0);
    textSize(14);
    textAlign(CENTER, CENTER);
    text(G.toFixed(1), this.position.x, this.position.y);
  }

  orbit(mover) {
    let dir = p5.Vector.sub(this.position, mover.position);
    let distance = dir.mag();
    distance = constrain(distance, 40, 250);
    dir.normalize();

    let radialForce = dir.copy();
    let strength = (G * 2000) / (distance * distance);
    radialForce.mult(strength);

    let tangent = createVector(-dir.y, dir.x);
    let tangentialStrength = map(distance, 40, 250, 3, 0.5);
    tangent.mult(tangentialStrength);

    let totalForce = p5.Vector.add(radialForce, tangent);
    return totalForce;
  }

  clicked(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < this.ballRadius) {
      this.dragging = true;
    }
  }

  stopDragging() {
    this.dragging = false;
  }

  drag(mx, my) {
    if (this.dragging) {
      let diff = p5.Vector.sub(this.origin, createVector(mx, my));
      this.angle = atan2(-diff.x, diff.y);
    }
  }
}


class Mover {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.noiseOffset = random(1000);
    this.trail = [];
    this.maxTrail = 30; 
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
   
    let angle = noise(this.noiseOffset) * TWO_PI * 2;
    let levyStep = pow(random(1), -1.5); // Lévy flight
    let perlinForce = createVector(cos(angle), sin(angle)).mult(levyStep * 0.02);
    this.applyForce(perlinForce);

    this.velocity.add(this.acceleration);
    this.velocity.limit(8);
    this.position.add(this.velocity);
    this.velocity.mult(0.95);
    this.acceleration.mult(0);

    this.checkEdges();

    this.noiseOffset += 0.01;

    
    this.trail.push(this.position.copy());
    if (this.trail.length > this.maxTrail) {
      this.trail.shift();
    }
  }

  display() {
    
    noFill();
    stroke(255, 140, 0, 100);
    beginShape();
    for (let p of this.trail) {
      vertex(p.x, p.y);
    }
    endShape();

    
    noStroke();
    fill(255, 140, 0);
    ellipse(this.position.x, this.position.y, 16, 16);
  }

  checkEdges() {
    if (this.position.x > width) this.position.x = width;
    if (this.position.x < 0) this.position.x = 0;
    if (this.position.y > height) this.position.y = height;
    if (this.position.y < 0) this.position.y = 0;
  }
}


function mousePressed() {
  pendulum.clicked(mouseX, mouseY);
}

function mouseReleased() {
  pendulum.stopDragging();
}

function mouseDragged() {
  pendulum.drag(mouseX, mouseY);
}

```

## Captura de pantalla representativa

<img width="726" height="588" alt="imagen" src="https://github.com/user-attachments/assets/90353d08-f3a7-49ae-9aaa-bf7502d59eb6" />






