# Evidencias de la unidad 7


## Actividad 01


### Tu análisis de 3-4 ejemplos de Ji Lee, explicando cómo logran la conexión palabra-imagen.

<img width="395" height="381" alt="image" src="https://github.com/user-attachments/assets/f4a84134-2add-41a1-bfa8-823eca42b156" />
<img width="406" height="403" alt="image" src="https://github.com/user-attachments/assets/d6f710c2-f0af-47c7-be42-7751d11ecb35" />
<img width="383" height="389" alt="image" src="https://github.com/user-attachments/assets/c0afd987-e828-42e0-8e71-ec00858fd6ec" />
<img width="401" height="398" alt="image" src="https://github.com/user-attachments/assets/5a1c9640-2f4d-49bf-9e9b-77e1e748faf0" />


**imagen 1**
Bueno la primera imagen que legi fue la de garfield y esta hace la conceion iamgen palabra poniendo los dos ojos del garfield al principio meientras que el primer ojo esta cerrado el segundo ojo tiene una pequeña abertura esto provocando que que se interprete como un G la primera letra de la palabra garfield

**imagen 2**
En este caso es la imagen de dali y esta se coneceta con este por que en donde termina la A tiene como dos curvas salientes pareciendose al bigote caracteristico del pintor dali 
**imagen 3**
esta es la imagen que dice titanic la conexion de este se crea gracias a que es la palabra titanic escrite diagonalmente como si se estuviera hundiendo la parte que esta fuera es negra mientras que la otra mitad esta en un gris asemejandose como se hundio el titanic 
**imagen 4**
La ultima es high que el punto de la i esta mas arriba de lo normal como si estuviera volando 

### Tus propias ideas (descripción o boceto simple) para representar visualmente 2-3 palabras distintas de forma estática.
**Primera descripcion**
Bueno ene ste caso seria la palabra bull y que en la punta de arriba de las dos L salga un cacho de arriba de ellas  haria la conexion por que el toro tienen cuernos entonces ahi estaria 
**Segunda descripcion**
La segunda seria videogames y para hacer la asosicacion primero la o en vez de ser ella seria el dibujo de un monitor y segundo la M de games seria un control ya sea de play o de xbox



## Actividad 02


**Muestra el código de los dos (o más) experimentos básicos que replicaste integrando Matter.js y p5.js.**

**Codigo1**
``` js
// --- Experimento 1: Cajas y círculos con gravedad ---
// Asegúrate de importar matter.js desde el menú de p5.js

// Variables principales de Matter.js
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies;

let engine;
let world;
let boxes = [];
let ground;

function setup() {
  createCanvas(800, 600);

  // Crear el motor y el mundo de física
  engine = Engine.create();
  world = engine.world;

  // Crear el suelo (estático, no se mueve)
  let options = {
    isStatic: true
  };
  ground = Bodies.rectangle(width / 2, height - 20, width, 40, options);
  World.add(world, ground);
}

function mousePressed() {
  // Al hacer clic, generar una caja o círculo aleatorio
  if (random() < 0.5) {
    boxes.push(Bodies.rectangle(mouseX, mouseY, 40, 40));
  } else {
    boxes.push(Bodies.circle(mouseX, mouseY, 20));
  }
  World.add(world, boxes[boxes.length - 1]);
}

function draw() {
  background(30);
  Engine.update(engine);

  fill(255);
  noStroke();

  // Dibujar las cajas y círculos
  for (let b of boxes) {
    let pos = b.position;
    let angle = b.angle;
    push();
    translate(pos.x, pos.y);
    rotate(angle);
    if (b.circleRadius) {
      ellipse(0, 0, b.circleRadius * 2);
    } else {
      rectMode(CENTER);
      rect(0, 0, 40, 40);
    }
    pop();
  }

  // Dibujar el suelo
  fill(200, 100, 100);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, width, 40);
}
```

**Codigo2**
``` js
// --- Experimento 2: Arrastrar cuerpos con el mouse ---
// Asegúrate de importar matter.js desde el menú de p5.js

// Variables principales
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies,
    Mouse = Matter.Mouse,
    MouseConstraint = Matter.MouseConstraint;

let engine, world;
let boxes = [];
let ground;
let mConstraint;

function setup() {
  createCanvas(800, 600);

  // Crear motor y mundo
  engine = Engine.create();
  world = engine.world;

  // Crear suelo estático
  let options = { isStatic: true };
  ground = Bodies.rectangle(width / 2, height - 20, width, 40, options);
  World.add(world, ground);

  // Crear algunos cuerpos
  for (let i = 0; i < 5; i++) {
    boxes.push(Bodies.rectangle(200 + i * 100, 100, 60, 60));
    World.add(world, boxes[i]);
  }

  // Crear mouse constraint para interactuar con los cuerpos
  let canvasmouse = Mouse.create(canvas.elt);
  let optionsMouse = {
    mouse: canvasmouse
  };
  mConstraint = MouseConstraint.create(engine, optionsMouse);
  World.add(world, mConstraint);
}

function draw() {
  background(30);
  Engine.update(engine);

  // Dibujar las cajas
  for (let b of boxes) {
    let pos = b.position;
    let angle = b.angle;
    push();
    translate(pos.x, pos.y);
    rotate(angle);
    rectMode(CENTER);
    fill(100, 200, 255);
    rect(0, 0, 60, 60);
    pop();
  }

  // Dibujar el suelo
  fill(200, 100, 100);
  rectMode(CENTER);
  rect(ground.position.x, ground.position.y, width, 40);

  // Visualizar cuando el mouse está sujetando un objeto
  if (mConstraint.body) {
    let pos = mConstraint.body.position;
    let m = mConstraint.mouse.position;
    stroke(255);
    line(pos.x, pos.y, m.x, m.y);
  }
}
```

**Incluye una **captura de pantalla o ENLACE a un GIF (no olvides, enlace) de cada experimento funcionando.**

Captura 1 
<img width="799" height="598" alt="image" src="https://github.com/user-attachments/assets/921cb62f-8608-4da8-908d-92cacc0b6726" />

Captura 2 
<img width="797" height="624" alt="image" src="https://github.com/user-attachments/assets/986214c5-5871-4ec7-aae1-3dec294c4369" />


**Proporciona tu explicación clara y concisa de los conceptos clave (Engine, World, Bodies, Constraint, MouseConstraint).**


**Engine**
el engine es el motor de las fisicas es el que hace los calculos para que la fisicas funcionen correctamente tambien es el encargado de actualizar los cuerpos en cada frame 


**World**
este es el espacio donde estan contenidos todos los objetos que hay dentro del canvas 


**Bodies**
Son cuerpos fisicos que son por ejemplo circulos o cuadrados tambien estos se ven afectados por la fisica ademas de que tienen masa , friccion densidad etc.

**Constraint**
es un herramienta que ayuda a crear vinculos entre dos bodies se puede utilizar para hacer uniones cadenas o articulaciones etc.

**MouseConstraint**
Este es un constraint que nos ayuda a empujar arrastrar o hacer otras cosas con los objetos para poderlos manipular con el mouse 

**Menciona brevemente cualquier dificultad encontrada al configurar o usar Matter.js inicialmente.**

Siento que los que mas se me dificulto fue setear el matter para que funcionara en el editor web de p5.js por que habia que modificar el index pero como que si lo modificaba no lo aceptaba o que por ejemplo las urls que utilizaba no funcionaba bien o los objetos no los devolvia de manera apaorpiada



## Actividad 03


**Indica claramente la palabra elegida.**

La palabra que voy a elegir va a ser deus que significa dios en latin 

**Explica tu idea conceptual: ¿Cómo la animación física representa el significado de la palabra?**

Bueno mi idea es que la palabra aparezca volando de arriba hacia el centro(como si estuviera cayendo) y que salga como una luz detras de esta , esto esta asosiado con la palabra gracias a que evoca como a lo que esta asosiado a dios que vuela y que de iugal manera brilla 

**Describe brevemente los aspectos técnicos clave de tu implementación: ¿Cómo formaste las letras con Matter.js? ¿Qué propiedades físicas fueron importantes? ¿Usaste restricciones?**

Cada letra es un cuerpo inidividual el objetivo de las letras es que sean cuerpos visibles mas no fisicos o sea hay un circulo invisble que es un collider para que las letras no sigan cayendo infinitamente y las letras se dibujan por encima de este cuerpo , le baje la gravedad para que cayera mas suvemente para dar el efecto de que estaba decendiendo , tambien hay un suelo invisibel que impide que las letras sigan cayendo y tampoco utilice ningun constraint 

**Incluye el código completo de tu sketch final.**

[P5.js code](https://editor.p5js.org/DAITO17/sketches/eLiqSLMV8)

```js
// Importar módulos de Matter.js
const { Engine, World, Bodies } = Matter;

let engine;
let world;
let letters = [];
let ground;
let glowAlpha = 0;
let glowActive = false;
let hasLanded = false;
let landingSound;

function preload() {
  // 🔹 Carga tu archivo de sonido (debe estar en la misma carpeta del sketch)
  landingSound = loadSound("Cantos.mp3"); 
}

function setup() {
  createCanvas(800, 600);

  engine = Engine.create();
  world = engine.world;

  // 🔸 Gravedad reducida para caída suave
  engine.world.gravity.y = 0.3;

  // 🔸 Suelo invisible
  ground = Bodies.rectangle(width / 2, height / 2 + 100, width, 20, {
    isStatic: true,
    render: { visible: false },
  });
  World.add(world, ground);

  // 🔸 Crear letras "DEUS"
  let word = "DEUS";
  let startX = width / 2 - 120;
  for (let i = 0; i < word.length; i++) {
    let letter = new Letter(startX + i * 80, 0, word[i]);
    letters.push(letter);
  }
}

function draw() {
  background(15);
  Engine.update(engine);

  // 🔹 Detectar si todas las letras están quietas
  let allStopped = letters.every(
    (l) =>
      abs(l.body.velocity.y) < 0.05 &&
      abs(l.body.position.y - (height / 2 + 50)) < 60
  );

  if (allStopped && !hasLanded) {
    hasLanded = true;

    // 🔊 Reproducir sonido
    if (landingSound && !landingSound.isPlaying()) {
      landingSound.play();
    }

    // 💫 Activar brillo luego de una pequeña pausa
    setTimeout(() => {
      glowActive = true;
    }, 800);
  }

  // 🔹 Dibujar brillo si está activo
  if (glowActive) {
    glowAlpha = lerp(glowAlpha, 180, 0.05);
    drawGlow();
  }

  // 🔹 Dibujar letras
  for (let l of letters) {
    l.show();
  }
}

// ---------------------- Clase Letter ----------------------
class Letter {
  constructor(x, y, char) {
    this.char = char;
    this.body = Bodies.circle(x, y, 20, {
      restitution: 0.0,
      friction: 1.0,
      density: 0.002,
    });
    World.add(world, this.body);
  }

  show() {
    const pos = this.body.position;
    const angle = this.body.angle;

    push();
    translate(pos.x, pos.y);
    rotate(angle);
    textAlign(CENTER, CENTER);
    textSize(64);

    // 🎨 Dorado brillante animado
    let gold = color(255, 215, 0);
    let shine = color(255, 255, 150);
    let c = lerpColor(gold, shine, sin(frameCount * 0.05) * 0.5 + 0.5);

    fill(c);
    noStroke();
    text(this.char, 0, 0);
    pop();
  }
}

// ---------------------- Efecto de Brillo ----------------------
function drawGlow() {
  push();
  noStroke();
  for (let i = 0; i < 10; i++) {
    let alpha = map(i, 0, 10, glowAlpha, 0);
    fill(255, 220, 50, alpha);
    ellipse(width / 2, height / 2 + 50, 300 + i * 50, 120 + i * 20);
  }
  pop();
}

```

**Inserta una captura de pantalla estática Y un enlace a un GIF animado (¡Esencial!) que muestre tu tipografía semántica animada en acción.**



<img width="787" height="594" alt="image" src="https://github.com/user-attachments/assets/be259b09-b15e-4a20-89ee-f9f74d0c8e1a" />





https://github.com/user-attachments/assets/f72d2ac5-99e6-4f08-996b-d5cebec15bef


# Autoevaluacion

## Tu nota propuesta.
Mi nota propuesta para esta unidad es de 5

## Mi defensa 

Bueno yo siento que me merezco el 5 en esta unidad gracias a que segui al pie de la letra lo que pedia cada actividad y hice todas las actividades propuestas 





