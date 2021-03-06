TDD workshop test doubles
=========================

Repositorio con "esqueletos" de proyectos para comenzar el taller de test doubles. 
También se incluyen algunos ejemplos mostrados en la presentación previa al taller.

De momento se incluyen los siguientes esqueletos:

 - java: con mockito y jmock
 - groovy: con spock
 - ruby: con rspec
 
Enunciado de la kata:

Mars Rover (versión modificada para practicar con dobles de prueba)

Esta kata consiste en programar la unidad de control del robot mars rover. A diferencia de la kata original (http://craftsmanship.sv.cmu.edu/katas/mars-rover-kata) vamos a implementar algo más “parecido” a un robot real. La diferencia fundamental es que no es suficiente con cambiar una posición (x,y) en memoria para considerar que el robot se ha movido, nuestra unidad de control procesará los comandos y se comunicará con los motores del robot para pedirles que hagan cosas.

Vamos a suponer que disponemos ya de un interfaz definido para comunicarnos con los motores del robot:

- left(time) -> activa el motor izquierdo del robot durante el tiempo indicado
- right(time) -> activa el motor derecho del robot durante el tiempo indicado
- fordward(time) -> activa los dos motores, izquierdo y derecho, haciendo avanzar al robot durante el tiempo indicado
- backward(time) -> activa los dos motores, izquierdo y drecho, en dirección inversa haciando que el robot retroceda durante el tiempo indicado

Los cuatro comandos básicos de movimiento con este esquema implican:

- f -> mover 1s hacia delante
- b -> mover 1s hacia atras
- l -> mover 1s el motor de la derecha
- r -> mover 1s el motor de la izquierda

nota: Para que nuestro robot gire a la derecha necesitamos activar el motor izquierdo, y para que gire a la izquierda activamos el derecho, si al reves jeje, como el timon de un barco.

Con estas modificaciones vamos a implementar lo siguiente:

- El rover recibe un array de comandos
- Es capaz de moverse hacia delante y hacia atrás (comandos f/b)
- Es capaz de moverse a izquierda y derecha (comandos l/r)
- Tener en cuenta que parar y arrancar los motores cuesta energía. De modo que si por ejemplo recibimos dos comandos f seguidos en lugar de decirle al motor dos veces que avanza 1s le decimos una vez que avance 2s. Lo mismo es aplicable para ir hacia atrás y para los giros, un par de ejemplos: 
	
	- la lista de comandos “FFFLL” se traduce en las siguientes llamadas al motor:
		- fordward(3)
		- right(2) 
	- lista de comandos “BBBFFFRRR”
		- backward(3)
		- fordward(3)
		- left(3)

- El mars rover ha ido a marte en busca de vida no solo de paseo!, vamos a contar con un nuevo comando para chequear la existencia de vida “c”, cuando llegue este comando el robot usará su dispositivo de detección de vida, en caso de encontrarla usará su dispositivo de localización y cuando termine de procesar todos los comandos de movimientos nos entregará una lista con las posiciones donde encontro vida. Todavía no conocemos el interfaz con estos dispositivos porque los ingenieros del robot hacen waterfall y además son de hablar poco, pero esto no es ningún problema, nosotros hacemos TDD!.

Nota: tener en cuenta el orden en el que hacemos las llamadas al motor!.

