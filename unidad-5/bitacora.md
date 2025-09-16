# Evidencias de la unidad 5

## Actividad 02

### Modificacion del 4.2 

Bueno para este quise agregarle un ruido perlin al codigo este hace parte de la unidad 1 ahora habalando de este como modifica el funcionamiento del codigo , antes la particulas al caer terminaban formando como la forma de un arbol de navidad arribangosto pero al final ancho y siempre seguia una forma muy semejante , ahora agregandole un ruido perlin hace que las particulas al caer se vayan mas a los lados de pornto se podria acemjar como cae el plovo o o las hojas , con el perlin se utiliza un noise que va desde 0 a 1 la diferencia con otros noise es que este va gradualemnte de 0 a l teniendo un movimiento mas natural , luego este noise se convierte en una fuerza y todo esto termina provocando que la particual sufra un empujon lateral en cada frame 

Habalndo acerca de las particulas y de sus ciclo

Estas se crean en la funcion draw que se ejecuta 60 veces por segundo , o sea cada vez que draw es ejecutado se crea una nueva particula luego de esto se recorre un array de atras hacia adelante , esto es una técnica común porque si eliminas un elemento en medio del splice, no se rompen los índices de los elementos que aún no se han procesado luego de esto hay un if que revisa si la particula sigue existiendo o no, si esta muerta se elimina del array ahora hablando de memoria con el splice (splice i,1) lo que hace es que borra el elemento i del array cuando se borra la referencia del objeto en el array el recolector de basura detcta que ya ese pbnjeto no tiene ninguna referencia activa haciendo que se libere la memoria que estab ocupando ese objeto en especifico

**Codigo modificado**
[Link a la modificacion del codigo](https://editor.p5js.org/DAITO17/sketches/ixWzWoVpM)
``` js
let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  particles.push(new PerlinParticle(width / 2, 20));

  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.run();
    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }
}


class PerlinParticle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-1, 1), random(-2, 0));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.noiseOffset = random(1000);
  }

  run() {
    this.applyPerlin();
    this.update();
    this.display();
  }

  applyPerlin() {
    
  let n = noise(this.noiseOffset);
  let lateral = map(n, 0, 1, -0.05, 0.05);

  // Aplicar fuerza combinada: ruido (X) + gravedad (Y)
  this.applyForce(createVector(lateral, 0.05));

  this.noiseOffset += 0.01;
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 2;
  }

  display() {
    noStroke();
    fill(0, this.lifespan);
    ellipse(this.pos.x, this.pos.y, 12, 12);
  }

  isDead() {
    return this.lifespan < 0;
  }
}
```

**Codigo fuente**
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  particles.push(new Particle(width / 2, 20));

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
}
``` 
**Imagen del codigo modoficado
<img width="638" height="238" alt="image" src="https://github.com/user-attachments/assets/fbc9b023-b651-4fa9-85c0-098c0c648d97" />


### Modificacion del 4.4

Bueno a este codigo lo que hice agregarle levy flihgt al movimiento de las particulas antes de esto estas cain como en una casacada en un pátron de caida muuy definido ahora con la adiccion del levy lo que hace es que haya un poco mas de caos por asi decirlo por que cuando las particulas nacen sean muy erraticas por ejemplo las particulas siguen cayendo pero a veces dan saltos para los lado o para arriba a abajo  siendo todo mucho mas caotico , en si lo que el levy flightr lo que hace es que devuelve un vector corto o largo de manera probabilistica o sea muchos vectores o pasos pequeños y pocos grandes al sumar este vector a vel hacemos que la velocidad cambie ligeramente en cada frame en ua dirrecion aleatoria , en si no se esta modificando el codigo de la particula si no que se le agrego un componente para que este fyuera mucho mas diferente 


En cuanto a las particulas y si su ciclo  , sigue siendo igual al ejemplo anterior el array se hace de atras hacia a adelante para evitar que se pase por alto alguna posicion del array 


**Codigo modificado**
[Link a la modificacion del codigo](https://editor.p5js.org/DAITO17/sketches/A6GeOvCVb)
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

// Particles are generated each cycle through draw(),
// fall with gravity and fade out over time
// A ParticleSystem object manages a variable size
// list of particles.

// an array of ParticleSystems
let emitters = [];

function setup() {
  createCanvas(640, 240);
  let text = createP("click to add particle systems");
}

function draw() {
  background(255);
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

// -----------------
// Particle class
class Particle {
  constructor(position) {
    this.pos = position.copy();
    this.vel = createVector(random(-1, 1), random(-2, 0));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update() {
    // aplicar levy flight
    let step = this.levyFlight();
    this.vel.add(step);

    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 2;
  }

  levyFlight() {
    // Genera un paso tipo Levy Flight
    // Paso pequeño la mayoría de las veces, grande pocas veces
    let theta = random(TWO_PI);
    let stepLength = pow(random(1), -1.5); // heavy-tail distribution
    stepLength = constrain(stepLength, 0, 3); // evita pasos demasiado grandes
    return p5.Vector.fromAngle(theta).mult(stepLength * 0.2); // escala para que no se descontrole
  }

  display() {
    stroke(0, this.lifespan);
    fill(0, this.lifespan);
    ellipse(this.pos.x, this.pos.y, 8);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

// -----------------
// Emitter class
class Emitter {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.pos));
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.applyForce(createVector(0, 0.05)); // gravedad
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```
Imagen de la obra modificada 
<img width="644" height="278" alt="image" src="https://github.com/user-attachments/assets/9691b8d9-fc1e-419e-99b2-c44eee6fb516" />



### Modificacion del 4.5


Bueno para esta modificacion quise modelar alguna fuerza o alog por estilo a si que me fui a la unidad 3 a ver que encontraba y hubo que me llamo mucho la atencion que fue la de fluid resistance , entonces lo primero fue dibujar el rectangulo que va a asemejar donde va a estar el liquido , luego de esto se hace un metodo que revise si la particula esta dentro del liquido chequeando su altura en caso de lo este se le aplica la fuerza esta esta dada de la siguiente resistencia del fluido = -c⋅v^2⋅v^ , donde c es valor que indica que tan biscoso esta el liquido , v es la velocidad de la particula y v^ es el vector dirrecion de la velocidad pero normalizado por ultimo el signo menos al principio de la ecuacion indica que va en contra de la dirrecion del movimiento y ya por ultimo si la particula esta en el liquido se calcula la fuerza luego se llama apllyforce para sumarle la aceleracion esto haciendo que en cad aupdate la velocidad se reduzca.


En cuanto al aprovechamineto de la memoria la cosa sigue igual en este codigo de iugal manera cuando la particula va llegando al fondo del liquido se mepieza a desaparecer como pasbaa en loa anterirores codigos 

**Codigo modificado**
[Link a la modificacion del codigo](https://editor.p5js.org/DAITO17/sketches/UCwqabmOy)
``` js

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);

   
    if (this.isInsideLiquid()) {
      let drag = this.calculateDrag(0.1); 
      this.applyForce(drag);
    }

    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }

  
  isInsideLiquid() {
    return this.position.y > height * 0.75;
  }

  
  calculateDrag(c) {
    let speed = this.velocity.mag();
    let dragMagnitude = c * speed * speed;
    let drag = this.velocity.copy();
    drag.mult(-1);
    drag.normalize();
    drag.mult(dragMagnitude);
    return drag;
  }
}


class Confetti extends Particle {
  show() {
    let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
    rectMode(CENTER);
    fill(127, this.lifespan);
    stroke(0, this.lifespan);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    square(0, 0, 12);
    pop();
  }
}


class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    let r = random(1);
    if (r < 0.5) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}


let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 20);
}

function draw() {
  background(255);
 rectMode(CORNER);
  
  noStroke();
  fill(100, 150, 255, 150);
  rect(0, height * 0.75, width, height * 0.25);

  emitter.addParticle();
  emitter.run();
}
```
**Imagen del codigo funcionando**

<img width="644" height="253" alt="image" src="https://github.com/user-attachments/assets/82ffb317-e16e-41b7-9fa3-c7d801830ced" />



### Modificacion del 4.6


Bueno en este caso se que de igual manera la particulas en este codigo tienen gravedad aplicada ahora la modificacion que le puse al codigo fue el viento , cuando el click del mouse esta presionado hace que las particulas vayan en esa dirrecion igual se podria hablar de que utilice en la unidad 3 de fuerzas pero ahora modelando otra fuerza , bueno ahora si hablando concretamente dle codigo , primero en draw se llama a un condicional que solo funciona si el mouse esta presioando se empeiza a aplicar las fuerzas en la particulas , esta se calcula de la sigueinte manera esta el map(mousex , esto para lo que sirve es transformar la posicion horizontal del mouse en una fuerza , luego con la fuerza se crea un vector este solo tiene componente en x y en Y es 0 esto haciendo que solamente se pueda mover el viento horizontalmente , luego en apply force cada particula recibe la misma fuerza dle viento  ya dentro de Particle.applyForce esta fuerza se convierte en acceleracion traduciendo esto significa que el viento no cambia de velocidad directamente si no que que agrega aceleracion , todo esto genera que la aceleraccion de la particula sea modificada pero solamente horizontalmente 


Igual el ahorramiento de la memoria y la desaparacion de las particulas funciona igual en este codigo 

**Codigo modificado**
[enlace al codigo en p5](https://editor.p5js.org/DAITO17/sketches/ryI8ZV_vt)
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0.0);
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.lifespan = 255.0;
    this.mass = 1;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2.0;
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

let emitter;

function setup() {
  createCanvas(1280, 480);
  emitter = new Emitter(width / 2, 50);
}

function draw() {
  background(255, 30);

  // Gravedad
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // Viento controlado por el mouse (solo cuando está presionado)
  if (mouseIsPressed) {
    // Mapeamos mouseX a un rango de fuerza
    let windStrength = map(mouseX, 0, width, -0.2, 0.2);
    let wind = createVector(windStrength, 0);
    emitter.applyForce(wind);
  }

  emitter.addParticle();
  emitter.run();
}
``` 

**Imagen del codigo**
<img width="820" height="481" alt="image" src="https://github.com/user-attachments/assets/1c978c21-45d7-46e2-b5b7-b7452b913ea0" />


### Modificacion del 4.7

Bueno para este caso hice uso del concepto de la unidad 4 que son los resortes entonces en vez de que haga la repulsion actua un resorte como atryendo y empujando , hablando tecnicamente repeller ya no existe ahora es spring entonces con la ley de hooke que es f= -k⋅x⋅d , k es la constante de elasticidad x es la elongacion (distancia actual -elongacion del peso) y la d es la direccion normalizada del resorte , entonces para cada particula se calcula la distancia entre ella y luego la elongacion  esta se calcula stretch = distance - restLength si el strech es positivo el resorte atrae en cambio si es negativa el resorte empuja luego de este calcula se normaliza el vector direccion luego se multiplica por -k * strech para generar la fuerza y por ultima esta fuerza se aplica a la generacion de la particula 

el ahorramiento de memoria y la gestion de las particulas funciona igual 
**Codigo modificado**
[enlace al codigo en p5](https://editor.p5js.org/DAITO17/sketches/NMkaGualC)
``` js

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  applySpring(spring) {
    for (let particle of this.particles) {
      let force = spring.attract(particle);
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}


class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(f) {
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}


class Spring {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.k = 0.05;          
    this.restLength = 100;  
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 32);
  }

  attract(particle) {
    let force = p5.Vector.sub(particle.position, this.position);
    let distance = force.mag();

    
    let stretch = distance - this.restLength;

   
    force.normalize();
    force.mult(-1 * this.k * stretch);

    return force;
  }
}


let emitter;
let spring;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 60);
  spring = new Spring(width / 2, 200);
}

function draw() {
  background(255);

  emitter.addParticle();

  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  emitter.applySpring(spring);
  emitter.run();

  spring.show();
}
```

**Imagen del codigo**
<img width="636" height="241" alt="image" src="https://github.com/user-attachments/assets/54ea904a-e151-4b19-ad02-a7a5037f5a7b" />

