# Unidad 2


## 🛠 Fase: Apply

### Actividad 08

**Describe el concepto de tu obra generativa.**
lo que quiero hacer son como unos trails que sean de diferentes colores qeu vayan pintando la obra por donde pasen en el centro va a ver un circulo el cual siempre va a a estar ahi , de igual manera tiene una paleta de colores verdes naranjas y blancos , para ganerar mas trails se puede hacer con la letra G 

**¿Cómo piensas aplicar el marco MOTION 101 y por qué?**
 El motion 101 lo aplico de manera que afecte los trails su movimiento de igual manera empieza desde el centro de la pnatalla donde esta el circulo 

 **¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?**
voy a utilizar uno del tipo levy flight esto por que quiero que los trails se muevan naturalemente para que los trazos sean mas'limpios' , de igual con este siento que los trazos pueden ser llamativos por este tipo de movimiento 

**El código de la aplicación.**

``` js
let movers = [];
let palette = ['#012622', '#003B36', '#ECE5F0', '#E98A15'];
let center;
let spawnRadius = 200;

function setup() {
  createCanvas(800, 600);
  noStroke();
  background('#000'); 

  center = createVector(width / 2, height / 2);

  
  for (let i = 0; i < 4; i++) {
    movers.push(new Mover());
  }
}

function draw() {
  
  fill('#01584F');
  ellipse(center.x, center.y, spawnRadius * 2);

  // Dibujar todos los movers
  for (let mover of movers) {
    mover.update();
    mover.display();
  }
}

// ⌨️ Cuando presionas la tecla G o g
function keyPressed() {
  if (key === 'g' || key === 'G') {
    movers.push(new Mover());
  }
}

class Mover {
  constructor() {
   
    let angle = random(TWO_PI);
    let r = random(spawnRadius);
    this.position = p5.Vector.fromAngle(angle).mult(r).add(center);

    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.size = random(4, 8);
    this.color = random(palette);
  }

  applyLevyFlight() {
    let angle = random(TWO_PI);
    let magnitude = pow(random(1), -1.5);
    let a = p5.Vector.fromAngle(angle).mult(magnitude * 0.01);
    this.acceleration.add(a);
  }

  update() {
    this.applyLevyFlight();
    this.velocity.add(this.acceleration);
    this.velocity.limit(2);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;

   
    
  }

  display() {
    fill(this.color);
    rect(this.position.x, this.position.y, this.size, this.size);
  }
}
```

**Un enlace al proyecto en el editor de p5.js.**
https://editor.p5js.org/DAITO17/sketches/BQ7ypuQny

**Una captura de pantalla representativa de tu pieza de arte generativo.**
<img width="828" height="624" alt="image" src="https://github.com/user-attachments/assets/1062e4fb-ba2f-4854-bc80-9dee48048387" />
