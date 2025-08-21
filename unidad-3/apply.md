# Unidad 3


## 🛠 Fase: Apply

### Actividad10

**Explica cómo modelaste el problema de los n-cuerpos en tu obra.**

Bueno aqui cada mover calcula la fuerza resultante ejercidada por todos los otros movers el movimiento es dianmico gracias a que la s fuerzas actualizan la acelaeracion , tambien ocurria un error que hacia que todos los movers colapsaran en el centro para arreglar esto se incluyo una pequeña fuerza de separacion para este proeyecto se utilizo tanto levy flight como el perlin , el levy se utilizo para que los movers de vez en cuando den grandes saltos  ademas este ayuda a que todos los movers se queden en el centro y le da a los movers un comportamiento mas antural , ahora hablando acerca del perlin este se utilizo para suavizar la direccion del movimiento en los saltos  esto igual ayuda a que los moviminentos del levy sean un poco mas esteticos y por ultimo hablando de la parte estetica los movers son bolas de 3 diferentes color rojo , amarillo  y negro esto imitando a las esuclturas de calver , tambien cuando los movers se acercan se hace un linea para que se vean como estan unidos ademas de esto cada mover deja una estela por donde se mueve 

[sketch obra generativa unidad 3 ](https://editor.p5js.org/DAITO17/sketches/g7nqow5n0)


```js
const sketch = (p) => {
  const N = 10;
  const MIN_DIST = 30;
  const MAX_DIST = 600;
  const REPEL_RADIUS = 40;
  const REPEL_COEF = 1200;
  const COLORS = ['#000000', '#FF0000', '#FFD700']; 
  const LINE_DIST = 170;
  const USE_LEVY = true;
  const USE_NOISE = true;
  const NOISE_SCALE = 0.003;

  let movers = [];
  let center;
  let t = 0; 
  let Gslider; 
  let G = 0.6; 

  p.setup = () => {
    p.createCanvas(900, 640);
    center = p.createVector(p.width / 2, p.height / 2);

    
    Gslider = p.createSlider(0, 2, 0.6, 0.01);
    Gslider.position(20, 20);
    Gslider.style('width', '150px');

    for (let i = 0; i < N; i++) {
      const angle = p.random(p.TWO_PI);
      const dist = p.random(110, 260);
      const px = center.x + p.cos(angle) * dist;
      const py = center.y + p.sin(angle) * dist;

      const vel = p.createVector(-p.sin(angle), p.cos(angle));
      vel.mult(p.random(1.6, 3.0));

      const mass = p.random(10, 20);
      const col = p.random(COLORS);
      movers.push(new CalderMover(px, py, vel, mass, col));
    }
  };

  p.draw = () => {
    p.background(245);

    G = Gslider.value();

    
    p.noStroke();
    p.fill(0);
    p.textSize(14);
    p.text(`Atracción: ${G.toFixed(2)}`, 180, 34);

    
    p.stroke(0, 100);
    p.strokeWeight(2);
    for (let i = 0; i < movers.length; i++) {
      for (let j = i + 1; j < movers.length; j++) {
        const d = p.dist(movers[i].pos.x, movers[i].pos.y, movers[j].pos.x, movers[j].pos.y);
        if (d < LINE_DIST) {
          p.line(movers[i].pos.x, movers[i].pos.y, movers[j].pos.x, movers[j].pos.y);
        }
      }
    }
    p.noStroke();

    for (let i = 0; i < movers.length; i++) {
      const A = movers[i];

     
      const fCenter = gravToPoint(A, center, A.mass);
      A.applyForce(fCenter);

      
      for (let j = 0; j < movers.length; j++) {
        if (i === j) continue;
        const B = movers[j];
        const f = gravBetween(B, A);
        A.applyForce(f);

        
        const dir = p5.Vector.sub(A.pos, B.pos);
        const dist = dir.mag();
        if (dist > 0 && dist < REPEL_RADIUS) {
          dir.normalize();
          const repelMag = REPEL_COEF / (dist * dist + 1);
          dir.mult(repelMag);
          A.applyForce(dir);
        }
      }

      if (USE_NOISE) {
        const angleNoise = p.noise(A.pos.x * NOISE_SCALE, A.pos.y * NOISE_SCALE, t) * p.TWO_PI * 2;
        const noiseForce = p.createVector(p.cos(angleNoise), p.sin(angleNoise));
        noiseForce.mult(0.5);
        A.applyForce(noiseForce);
      }

     
      if (USE_LEVY && p.random() < 0.003) {
        const theta = p.random(p.TWO_PI);
        const step = Math.pow(p.random(1), -0.8) * 20;
        const jump = p.createVector(p.cos(theta), p.sin(theta)).mult(step);
        A.pos.add(jump);
      }
    }

    
    for (let m of movers) {
      m.update();
      m.edges();
      m.show(p);
    }

    t += 0.01;
  };

  
  function gravBetween(a, b) {
    const dir = p5.Vector.sub(a.pos, b.pos);
    if (!isFiniteVector(dir)) return p.createVector(0, 0);
    let d = p.constrain(dir.mag(), MIN_DIST, MAX_DIST);
    dir.normalize();
    const strength = (G * a.mass * b.mass) / (d * d);
    return dir.mult(strength);
  }

  
  function gravToPoint(m, point, massOfM = 1) {
    const dir = p5.Vector.sub(point, m.pos);
    if (!isFiniteVector(dir)) return p.createVector(0, 0);
    let d = p.constrain(dir.mag(), MIN_DIST, MAX_DIST);
    dir.normalize();
    const M = 2000;
    const strength = (G * M * massOfM) / (d * d);
    return dir.mult(strength);
  }

  function isFiniteVector(v) {
    return v && isFinite(v.x) && isFinite(v.y);
  }

  
  class CalderMover {
    constructor(x, y, vel, mass = 12, col = '#000000') {
      this.pos = p.createVector(x, y);
      this.vel = vel && isFiniteVector(vel) ? vel.copy() : p.createVector(0, 0);
      this.acc = p.createVector(0, 0);
      this.mass = mass;
      this.r = Math.max(6, Math.sqrt(this.mass) * 3.2);
      this.col = col;
      this.trail = [];
    }

    applyForce(force) {
      if (!isFiniteVector(force)) return;
      const f = force.copy();
      if (this.mass === 0 || !isFinite(this.mass)) return;
      f.div(this.mass);
      if (!isFiniteVector(f)) return;
      this.acc.add(f);
    }

    update() {
      if (!isFiniteVector(this.acc)) this.acc.set(0, 0);
      this.vel.add(this.acc);
      this.vel.mult(0.996);
      if (!isFiniteVector(this.vel)) this.vel.set(0, 0);
      this.pos.add(this.vel);
      this.acc.mult(0);

      
      this.trail.push(this.pos.copy());
      if (this.trail.length > 30) this.trail.shift();
    }

    edges() {
      const pad = this.r;
      if (this.pos.x > p.width - pad) {
        this.pos.x = p.width - pad;
        this.vel.x *= -0.7;
      } else if (this.pos.x < pad) {
        this.pos.x = pad;
        this.vel.x *= -0.7;
      }
      if (this.pos.y > p.height - pad) {
        this.pos.y = p.height - pad;
        this.vel.y *= -0.7;
      } else if (this.pos.y < pad) {
        this.pos.y = pad;
        this.vel.y *= -0.7;
      }
    }

    show(ctx) {
      
      ctx.noFill();
      ctx.stroke(this.col + '80'); 
      ctx.strokeWeight(1);
      for (let i = 1; i < this.trail.length; i++) {
        ctx.line(this.trail[i - 1].x, this.trail[i - 1].y, this.trail[i].x, this.trail[i].y);
      }

      
      ctx.push();
      ctx.fill(this.col);
      ctx.noStroke();
      ctx.circle(this.pos.x, this.pos.y, this.r * 2);
      ctx.pop();
    }
  }

};

new p5(sketch);

```

<img width="900" height="632" alt="image" src="https://github.com/user-attachments/assets/8946a168-c999-48b7-b946-2b3cdc6633c7" />
