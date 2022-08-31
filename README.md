# Flappy Bird Parte 10: Agregando Sonidos

## Introducción

En el lab anterior agregaste funcionalidad para que el `contador` se actualice cuando `bird` logre evadir un par de `obstaculos`. En este lab agregaremos sonidos al juego utilizando JavaScript!

## Instrucciones

Agrega los siguientes métodos y propiedades dentro de `script.js`. Las descripciones para los métodos y propiedades de los objetos `audio`, `contador`,`juego`, `bird`, y `obstaculos` se encuentran más abajo en este README.

1. Agrega la propiedad `audio.effects`
2. Agrega el método `audio.crear`
3. Llama al método `audio.crear()` dentro de `juego.iniciar()`
4. Llama a `audio.effects.wing.play()` dentro de `bird.mover()`
5. Llama a `audio.effects.hit.play()` dentro de `bird.colision()`
6. Llama a `audio.effects.die.play()` dentro de `juego.terminar()`
7. Llama a `audio.effects.point.play()` dentro de `contador.actualizar()`

## El objeto audio

### Propiedades:
1. `effects`
- **¿Qué valor tiene?**:  `audio.effects` tiene el valor de un objeto vacío (para iniciar)
- **¿Dónde se utiliza?**: `audio.crear()` utiliza a audio.effects para guardar los efectos de sonido.

### Métodos:

1. `crear()`
- **¿Qué hace?**: Crea un audio utilizando `new Audio()`. Guarda los audios dentro de audio.effects.
- **¿Dónde se utiliza?**: `juego.iniciar()` llama a `audio.crear()` 



## El objeto contador

### Propiedades:

1. `unidades`
- **¿Qué valor tiene?**: `contador.unidades` tiene como valor el elemento html con id `#unidades`
- **¿Dónde se utiliza?**: `contador.dibujar()` utiliza la propiedad `unidades` para actualizar la imagen que muestra el numero de unidades del contador.

2. `decenas`
- **¿Qué valor tiene?**: `contador.decenas` tiene como valor el elemento html con id `#decenas`
- **¿Dónde se utiliza?**: `contador.dibujar()` utiliza la propiedad `decenas` para actualizar la imagen que muestra el numero de decenas del contador.

3. `puntaje`
- **¿Qué valor tiene?**: `contador.puntaje` tiene como valor el numero `0`
- **¿Dónde se utiliza?**: `contador.actualizar()` utiliza a la propiedad `contador.puntaje` para mantener un puntaje de la cantidad de `obstaculos` que `bird` ha logrado evadir.


### Métodos:

1. `dibujar()`
- **¿Qué hace?**: `contador.dibujar()` utiliza el valor de `contador.puntaje` para dibujar en el DOM el puntaje del juego.
- **¿Dónde se utiliza?**: `juego.loop()` llama a `contador.dibujar()`

2. `actualizar()`
- **¿Qué hace?**:  `contador.actualizar()` actualiza el `contador.puntaje` cada que `bird` logra evadir un obstaculo. 
- **¿Dónde se utiliza?**: `obstaculos.mover()` llama a `contador.actualizar()`



## El objeto juego

### Propiedades:
1. `timerId`
- **¿Qué valor tiene?**: `juego.timerId` tiene como valor el numero `0` (para iniciar)
- **¿Dónde se utiliza?**: `juego.timerId` se utilizará dentro de `juego.inicar()` para guardar un timer que llame cada 20 milisegundos a `juego.loop`

2. `gravedad`
- **¿Qué valor tiene?**: `juego.gravedad` tiene como valor el numero `2`
- **¿Dónde se utiliza?**: La variable `gravedad` representa el numero de pixeles que se restarán a `bird.bottom` cuando se aplique el método `bird.efectoGravedad()`

3. `skyHeight`
- **¿Qué valor tiene?**: `juego.skyHeight` tiene como valor el numero `580`
- **¿Dónde se utiliza?**: La variable `skyHeight` representa la altura del div que contiene la imagen de fondo de pantalla del juego (el cielo y la ciudad). `juego.skyHeight` se utiliza dentro del método `obstaculos.crear()`, para calcular la altura de los obstaculos.

4. `timerObstaculos`
- **¿Qué valor tiene?**: `juego.timerObstaculos` tiene como valor el numero `0` (para iniciar)
- **¿Dónde se utiliza?**: `juego.timerObstaculos` se utilizará dentro de `juego.inicar()` para guardar un timer que llame cada 20 milisegundos a `juego.loop`



### Métodos:
1. `aleatorio()` 
- **¿Qué hace?**: Devuelve un numero aleatorio entre un minimo y máximo dado
- **¿Dónde se utiliza?**: `bird.bottom` llamará a `juego.aleatorio()` para calcular un numero aleatorio entre `10` y `570`


2. `verificaColision()`
- **¿Qué hace?**: Llama a `bird.colision()` para revisar si `bird` tuvo una colision. Si `bird.colision()` devuelve el valor `true`, llama a `juego.terminar()` para terminar el juego.
- **¿Dónde se utiliza?**:  `juego.loop()` llamará a `juego.verificaColision()` para revisar constantemente si hubo una colisión.  


3. `loop()`
- **¿Qué hace?** :Llama a `bird.efectoGravedad()`, `bird.dibujar()` y `juego.verificaColision()`
- **¿Dónde se utiliza?**: `juego.iniciar()` inicia un `setInterval()` que llama a `juego.loop()` cada 20 milisegundos. De ésta manera cada 20 milisegundos se aplicará el efecto de gravedad a bird, se dibujará bird en su nueva posicion, y se verificará si hubo una colisión


4. `iniciar()`
- **¿Qué hace?** : Agrega un eventListener de tal forma que cada que se pulse una tecla, se llame a `bird.move`. También asigna a `juego.timerId` un `setInterval()` que llame a `juego.loop()` cada 20 milisegundos. 
- **¿Dónde se utiliza?**: `juego.iniciar()` se tiene que llamar para iniciar el juego. A través del `setInterval()` cada 20 milisegundos se aplicará el efecto de gravedad a `bird`, se dibujará `bird` en su nueva posicion, y se verificará si hubo una colisión. A través del eventListener, se puede mover `bird`

5. `terminar()`
- **¿Qué hace?**: Limpia el timer guardado dentro de `game.timerId` (el que llama cada 20 milisegundos a `game.loop`). También, llama a `juego.mostrarGameOver()` y `juego.pararEfectos()`. 
- **¿Dónde se utiliza?**: El metodo `juego.terminar()` se llama cuando hay una colision


6.  `mostrarGameover()`
- **¿Qué hace?**:  Agrega el id "game-over" al elemento html con clase `.message`
- **¿Dónde se utiliza?**: `juego.terminar()` llama a `juego.mostrarGameOver` para mostrar el mensaje "Game Over" cuando el juego termina

7. `pararEfectos()`
- **¿Qué hace?**: quita el id al elemento con clase `.ground`. También agrega el id "fall" al div con clase `.bird`
- **¿Dónde se utiliza?**: `juego.terminar()` llama a `juego.pararEfectos()` para que bird deje de aleatear y el suelo deje de moverse 


## El objeto bird:

### Propiedades
1. `div`
- **¿Qué valor tiene?**: `bird.div` tiene como valor el elemento html con clase `.bird`
- **¿Dónde se utiliza?**: `bird.div` se utiliza dentro del método `bird.dibujar` de tal forma que se pueda dibujar el elemento en posiciones determinadas

2. `bottom`
- **¿Qué valor tiene?**: `bird.bottom` tiene un valor aleatorio entre `10` y `570`. Para calcular este valor aleatorio `bird.bottom` utiliza el método `juego.aleatorio()`
- **¿Dónde se utiliza?**:  El valor de `bird.bottom` basicamente determina en donde se va a posicionar el elemento `bird`. Por lo tanto `bird.bottom` se utiliza en los metodos `bird.efectoGravedad()`, `bird.dibujar()`, `bird.mover()` y `bird.colision()`

3. `left`
- **¿Qué valor tiene?**: `bird.left` tiene como valor el numero `250`
- **¿Dónde se utiliza?**: `bird.left` se utiliza dentro de `bird.dibujar()`. El valor de bird.left basicamente determinará el numero de pixeles a la izquierda del elemento con clas `.bird`

4. `width`
- **¿Qué valor tiene?**: `bird.width` tiene como valor el numero `60`
- **¿Dónde se utiliza?**: El valor de de `bird.width` se utilizará más adelante para determinar si hubo una colision entre `bird` y los `obstaculos`

5. `height`
- **¿Qué valor tiene?**: `bird.height` tiene como valor numero `45`
- **¿Dónde se utiliza?**: El valor de de `bird.height` se utilizará más adelante para determinar si hubo una colision entre `bird` y los `obstaculos`


### Métodos:

1. `efectoGravedad()`
- **¿Qué hace?**: `bird.efectoGravedad()` disminuye la propiedad `bird.bottom` por el valor de `juego.gravedad`
- **¿Dónde se utiliza?**: `juego.loop()` llama a `bird.efectoGravedad()`. Recuerda que `juego.loop()` se llama cada 20 milisegundos a través de `juego.iniciar()`. 

2. `dibujar()`
- **¿Qué hace?**: `bird.dibujar()` asigna a la propiedad bottom de `bird.div` (el elemento html con clas bird) el valor en pixeles de la propiedad `bird.bottom`
- **¿Dónde se utiliza?**: `juego.loop()` llama a `bird.dibujar()`. Recuerda que `juego.loop()` se llama cada 20 milisegundos a través de `juego.iniciar()`. 

3. `mover()`
- **¿Qué hace?**: `bird.mover()` agrega `40` a `bird.bottom`
- **¿Dónde se utiliza?**: `juego.iniciar()` agrega un eventListener de tal forma que cuando se pulse una tecla, se llame a `bird.mover()`

4. `colision()`
- **¿Qué hace?**: `bird.colision()` revisa si `bird.bottom` es menor a `0`. Si eseto es verdad, devuelve el valor `true`. También revisa si `bird.colisionY()` y `bird.colisionX()` devuelven un valor `true`. Si esto es verdad, llama a `juego.terminar() `y agrega el id colision a los elementos con los que `bird` tuvo una colision. 
- **¿Dónde se utiliza?**: `juego.verificaColision()` llama a `bird.colision()` para verificar si hubo una colision.

5. `colisionY()`
- **¿Qué hace?**: Revisa si `bird` tiene una colision con los obstaculos de manera vertical (con el eje Y). Recibe como parametro un elemento de `obstaculos.lista`.
- **¿Dónde se utiliza?**: `bird.colision()` llama a `bird.colisionY()` para revisar si hubo una colision.

6. `colisionX()`
- **¿Qué hace?**: Revisa si `bird` tiene una colision con los obstaculos de manera horizontal (con el eje X). Recibe como parametro un elemento de `obstaculos.lista`.
- **¿Dónde se utiliza?**: `bird.colision()` llama a `bird.colisionX()` para revisar si hubo una colision.


## El objeto obstaculos

### Propiedades:

1. `velocidad`
- **¿Qué valor tiene?**:  `obstaculos.velocidad` tiene como valor el numero `1`
- **¿Dónde se utiliza?**: `obstaculos.mover()` disminuye la propiedad `left` de los obstaculos por el valor de `obstaculos.velocidad`. 

2. `obstacleContainer`
- **¿Qué valor tiene?**: `obstaculos.obstacleContainer` tiene como valor el elemento html con clase `.obstacles`
- **¿Dónde se utiliza?**: `obstaculos.crearObstaculos()` utiliza `obstaculos.obstacleContainer` para agregar al DOM un nuevo obstaculo.

3. `gap`
- **¿Qué valor tiene?**: `obstaculos.gap` tiene como valor el numero `200`
- **¿Dónde se utiliza?**: `obstaculos.crear()` utiliza a `obstaculos.gap` para calcular el espacio que debe de haber entre el obstaculo superior y el obstaculo inferior

4. `maxHeight`
- **¿Qué valor tiene?**: `obstaculos.maxHeight` tiene como valor el numero `320`
- **¿Dónde se utiliza?**: la propiedad `maxHeight` representa el valor maximo de altura que puede tener un obstaculo. El método `obstaculos.crear()` utiliza a `obstaculos.maxHeight` para determinar la altura de los obstaculos.

5. `minHeight`
- **¿Qué valor tiene?**: `obstaculos.minHeight` tiene como valor el numero `50`
- **¿Dónde se utiliza?**:la propiedad `minHeight` representa la altura minima que puede tener un obstaculo. El método `obstaculos.crear()` utiliza a `obstaculos.minHeight` para determinar la altura de los obstaculos.

6. `width`
- **¿Qué valor tiene?**: `obstaculos.width` tiene como valor el numero `52`
- **¿Dónde se utiliza?**: la propiedad `width` representa el ancho de los obstaculos. El método `obstaculos.crear()` utiliza a `obstaculos.width` para determinar el ancho de los obstaculos. 

7. `lista`
- **¿Qué valor tiene?**: `obstaculos.lista` tiene como valor inicial un array vacio
- **¿Dónde se utiliza?**: `obstaculos.lista` representa una lista de los obstaculos que se muestran en el DOM. El método `obstaculos.crear()` agrega los obstaculos que se van creando dentro del array `obstaculos.lista`

### Métodos:

1. `crear()`
- **¿Qué hace?**: `obstaculos.crear()` crea un par de obstaculos (obstaculo superior y obstaculo inferior) y los agrega a `obstaculos.lista`. 
- **¿Dónde se utiliza?**: `juego.iniciar()` llama a `obstaculos.crear()`

2. `dibujar()`
- **¿Qué hace?**: `obstaculos.dibujar()` dibuja a los obstaculos dentro de `obstaculos.lista`
- **¿Dónde se utiliza?**: `juego.loop()` llama a `obstaculos.dibujar()` para dibujar a los obstaculos en el DOM

3. `mover()`
- **¿Qué hace?**: `obstaculos.mover` itera sobre el array `obstaculos.list` y le substrae el valor de `obstaculos.velocidad` a la propiedad `left` de cada elemento del array. 
- **¿Dónde se utiliza?**: `juego.loop()` llama a `obstaculos.mover()`

4. `eliminar()`
- **¿Qué hace?**:  `obstaculos.eliminar()` recibe un objeto con un par de obstaculos como argumento (basicamente un elemento del array `obstaculos.lista`). Si la propiedad `left` del par de obstaculos mas el valor de `obstaculos.width` es menor a cero, entonces se quita del DOM el par de obstaculos y se quita de `obstaculos.lista` el objeto con el par de obstaculos. La lógica de esto es que si la propiedad `left` del par de obstaculos mas el valor de `obstaculos.width` es menor a cero, entonces el par de obstaculos no es visible en el DOM, por lo tanto se tiene que eliminar.
- **¿Dónde se utiliza?**: `obstaculos.mover()` llama a `obstaculos.eliminar()` de tal forma que cada que se mueva un obstaculo, se verifica si se tiene que eliminar del DOM.

