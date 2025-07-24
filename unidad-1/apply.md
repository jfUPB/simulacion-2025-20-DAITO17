# Unidad 1

## 🛠 Fase: Apply

### Actividad 8
**Un texto donde expliques el concepto de obra generativa.**
La obra generativa es aquella que esta hecha del azar  , las matematicas y progrmacion , haciendo que cada obra llegue a ser unica en su tipo no importa si tiene la misma progrmacin y matematica el azar va a ser que no esa igual y justamente es el azar lo que hace que la obra generativa sea tan supremamente unica 

Hablando mas acerca de mi obra lo que quise plasmar fue un paisaje , arriba del todo se generan cubos blancos con una distribucion normal esto quiere imitar el cielo  , mientras que los cuadrados color cafe quieren imitar arboles en un valle estos estan generados con levy flight , los triangulos color azul que dejan una estela que quiere imitar un rio en la mitad de la obra estos se mueve con ruido perlin y por ultimo el fondo verde oscuro todo junto se asemeja a una obra de un paisje del campo        

**Copia el código en tu bitácora.**

``` js 

let t = 0;
let showTriangles = true;
let showSky = true;
let showWood = true;

function setup() {
  createCanvas(640, 240);
  background(137, 224, 145); // fondo verde claro
  noStroke();
}

function draw() {
  // 1. "Cielo" de cuadrados grises con distribución normal
  if (showSky) {
    push();
    noStroke();
    fill(224, 224, 224); // gris claro

    let mean = width / 2;
    let sd = 80;
    let x = constrain(randomGaussian(mean, sd), 0, width);
    let y = random(0, 5); // parte superior
    square(x, y, 20);
    pop();
  }

  // 2. Triángulos animados con ruido Perlin
  if (showTriangles) {
    push();
    fill(93, 184, 224, 50); // azul semitransparente
    let xNoise = noise(t) * width;
    let yNoise = noise(t + 100) * height;
    let size = 16;

    triangle(
      xNoise, yNoise,
      xNoise - size / 2, yNoise + size,
      xNoise + size / 2, yNoise + size
    );
    pop();

    t += 0.01;
  }

  // 3. Cuadrados "de madera" con Lévy flight
  if (showWood) {
    push();
    fill(160, 82, 45, 50); // marrón madera
    noStroke();

    let side = random() < 0.5 ? 'left' : 'right';
    let xWood = side === 'left'
      ? constrain(levy() * 2, 0, 60)
      : constrain(width - (levy() * 2), width - 60, width);

    let yWood = constrain(random(height) + levy(), 0, height);
    square(xWood, yWood, 20);
    pop();
  }
}

// Función de Lévy flight
function levy() {
  let beta = 1.5;
  let u = random(1);
  let step = pow(u, -1 / beta);
  if (random() < 0.5) step *= -1;
  return step * 10;
}

// Manejo de teclado
function keyPressed() {
  if (key === 't' || key === 'T') {
    showTriangles = !showTriangles;
  }
  if (key === 'y' || key === 'Y') {
    showSky = !showSky;
  }
  if (key === 'u' || key === 'U') {
    showWood = !showWood;
  }

  // Limpiar todo con la tecla I
  if (key === 'i' || key === 'I') {
    background(137, 224, 145); // repintar fondo verde
  }
}
```
**Coloca en enlace a tu sketch en p5.js en tu bitácora.**
[Sketch Act 8](https://editor.p5js.org/DAITO17/sketches/cvm1yw3Qd)

**Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.**
<img width="1593" height="777" alt="image" src="https://github.com/user-attachments/assets/c6c2ce05-7bdc-48f3-815b-0aafe6ffcd27" />
