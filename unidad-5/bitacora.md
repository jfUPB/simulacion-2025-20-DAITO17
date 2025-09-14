# Evidencias de la unidad 5

## Actividad 02

### Modificacion del 4.2 

Bueno para este quise agregarle un ruido perlin al codigo este hace parte de la unidad 1 ahora habalando de este como modifica el funcionamiento del codigo , antes la particulas al caer terminaban formando como la forma de un arbol de navidad arribangosto pero al final ancho y siempre seguia una forma muy semejante , ahora agregandole un ruido perlin hace que las particulas al caer se vayan mas a los lados de pornto se podria acemjar como cae el plovo o o las hojas , con el perlin se utiliza un noise que va desde 0 a 1 la diferencia con otros noise es que este va gradualemnte de 0 a l teniendo un movimiento mas natural , luego este noise se convierte en una fuerza y todo esto termina provocando que la particual sufra un empujon lateral en cada frame 

Habalndo acerca de las particulas y de sus ciclo

Estas se crean en la funcion draw que se ejecuta 60 veces por segundo , o sea cada vez que draw es ejecutado se crea una nueva particula luego de esto se recorre un array de atras hacia adelante , esto es una técnica común porque si eliminas un elemento en medio del splice, no se rompen los índices de los elementos que aún no se han procesado luego de esto hay un if que revisa si la particula sigue existiendo o no, si esta muerta se elimina del array ahora hablando de memoria con el splice (splice i,1) lo que hace es que borra el elemento i del array cuando se borra la referencia del objeto en el array el recolector de basura detcta que ya ese pbnjeto no tiene ninguna referencia activa haciendo que se libere la memoria que estab ocupando ese objeto en especifico

**Codigo modificado**
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


