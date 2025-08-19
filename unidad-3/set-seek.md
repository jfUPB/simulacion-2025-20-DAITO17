# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 09

**Friccion**



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
