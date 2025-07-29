# Unidad 2

## 🔎 Fase: Set + Seek

###  Actividad 01

**¿Cómo funciona la suma de dos vectores en p5.js?**
En p5 funciona con el .add y esto lo que hace es modificar el vector original sumandole el otro  y no crea una copia ni anda parecido

**¿Por qué esta línea position = position + velocity; no funciona?**
No funciona la linea dado a que como estamos trbajando en java scprit este lenguaje no tiene la capacidad de sumar objetos +  que son vectores  por eso es que esa linea no funcionaria 

###  Actividad 02
**¿Qué tuviste que hacer para hacer la conversión propuesta?**
En vez de trabajar con la posicion x , y se crea un vector para reemplazar estos 2 y en vez de sumar x o y se crea un vector de movimiento que cambia segun como le indiquemos 

**Muestra el código que utilizaste para resolver el ejercicio.**

``` js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y);
  }

  step() {
    let step = createVector(0, 0);
    const choice = floor(random(4));
    if (choice == 0) {
      step.x = 1;
    } else if (choice == 1) {
      step.x = -1;
    } else if (choice == 2) {
      step.y = 1;
    } else {
      step.y = -1;
    }

    
    this.position.add(step);
  }
}
```

### Actividad 03 
**¿Qué resultado esperas obtener en el programa anterior?**
Que me suelte dos valores , por que primero le estoy pasando 2 valores para que luego me devuelva valores diferentes despues de pasarlo por funcion 
**¿Qué resultado obtuviste?**<
me estar dando esos valores que esperaba pero seguidos por 0 
**Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.**
Esta el paso por el valor y paso por referencia el primero es darle como una fotocopia del valor a la funcion y el 2do le da el objeto original a la funcion 
**¿Qué tipo de paso se está realizando en el código?**
se esta haciendo paso por referencia 
**¿Qué aprendiste?**
LOs vectores son obejtos y como hacer para que el codgio modifique o cree una copia del vector para que este no se sobrescriba 
