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
**¿Qué resultado obtuviste?**


me estar dando esos valores que esperaba pero seguidos por 0 
**Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.**


Esta el paso por el valor y paso por referencia el primero es darle como una fotocopia del valor a la funcion y el 2do le da el objeto original a la funcion 
**¿Qué tipo de paso se está realizando en el código?**


se esta haciendo paso por referencia 
**¿Qué aprendiste?**


Los vectores son obejtos y como hacer para que el codgio modifique o cree una copia del vector para que este no se sobrescriba 

### Actividad 04 

**¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?**

Mientras que el metodo .mag nos da la magnitud del vector exacta ,el metodo .MagSq nos da la magnitud del vector al cuadrado y el metodo .MagSq es mas eficiente que el mag esto por que este no utiliza la raiz cuadrada que es una operacion costosa solo hace multiplicaciones y sumas aunque lo malo de este es que no es tan preciso como el .Mag


**¿Para qué sirve el método normalize()?**

Convierte un vector con la misma direccion pero con magnitud 1 , esto podria ser util en casos donde solo nso importer la direccion con la que se mueve algo y no que tan rapido se mueve este 


**Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?**

El metodo .Dot sirve para medir cuanto apuntan dos vectores en la misma direccion por ejemplo si el resultado es positivo apuntan en una direccion similar , si es 0 son perpendiculares y si es negativo apuntan en direcciones opuestas y respondiendo la pregunta en una frase diria que : El .Dot te dice cuando dos vectores estan alineados entre si 


**El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?**

EN si las dos hacen el msimo calculo solo cambia su modo de uso , la version de instancia sirve cuadno ya se tiene un vector y se quiere hacer el producto punto con el otro vector , mientras que la version estatica se utiliza cuando se quiere hacer el calculo sin depender de un vector en particular


**Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.**

El producto cruz de dos vectores un nuevo vector perpendicular a ambos ,  la magnitud del resultado termina siendo igual al area del paralelogramo formada por los dos vectores por los que se hizo el producto punto mientras que la orientacion del vector resultante es perpendiculara los dos vectores originales 


**¿Para que te puede servir el método dist()?**


El metodo lo que hace es calcular la disntancia entre dos vectores , esto puede servir cuando quiero calcular la disntancia que hya entre dos puntos en un espacio 
**


¿Para qué sirven los métodos normalize() y limit()?**

Normalize sirve para convertir  un vector con la misma direccion pero con magnitud 1 , mientras que limit limita la magnitud de un vector a una valor maximo 
