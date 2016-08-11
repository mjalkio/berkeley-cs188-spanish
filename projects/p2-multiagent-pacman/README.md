# Proyecto 2: Multi-Agente de Pacman

Versión original se puede encontrar [aquí](http://ai.berkeley.edu/multiagent.html).

## Tabla de contenido

1. Introducción
2. Bienvenido
3. P1: Reflex Agente
4. P2: Minimax
5. P3: La poda alfa-beta
6. P4: Expectimax
7. P5: la función de evaluación

## Introducción

![Pac-man being chased](https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/pacman_multi_agent.png)
> Pacman, ahora con fantasmas.
> Minimax, Expectimax,
> Evaluación.

En este proyecto, se le diseñar agentes para la versión clásica de Pacman, incluyendo fantasmas. En el camino, va a poner en práctica tanto Minimax y expectimax buscar y probar su mano en el diseño de la función de evaluación.

La base de código no ha cambiado mucho desde el proyecto anterior, pero por favor, comenzar con una instalación nueva, en lugar de entremezclar archivos del proyecto 1.

Al igual que en el proyecto 1, este proyecto incluye un autograder para que usted pueda grado sus respuestas en su máquina. Esto se puede ejecutar en todas las preguntas con el comando:

```
python autograder.py
```

Puede ser ejecutado por una pregunta en particular, por ejemplo Q2, por:

```
python autograder.py -q q2
```

Se puede ejecutar durante una prueba en particular por medio de comandos de la forma:

```
python autograder.py -t test_cases/q2/0-small-tree
```

Por defecto, el autograder muestra gráfica con la `-t` opción, pero no lo hace con la `-q` opción. Puede forzar gráficos mediante el uso de la `--graphics` bandera, o forzar ningún tipo de gráficos mediante el uso de la `--no-graphics` bandera.


El código para este proyecto contiene los siguientes archivos.

**Los archivos que va a editar:**
* multiAgents.py - Donde todas sus multiagente agentes de búsqueda residirán.
* pacman.py - El archivo principal que corre juegos de Pacman. Este archivo también describe un Pacman GameStatetipo, que va a utilizar ampliamente en este proyecto
* game.py - La lógica detrás de cómo funciona el mundo Pacman. Este archivo describe varios tipos de soporte como AgentState, agente, Dirección, y Cuadrícula.
* util.py - estructuras de datos útiles para la implementación de algoritmos de búsqueda.

**Apoyando archivos que puede pasar por alto:**
* graphicsDisplay.py - Gráficos de Pacman
* graphicsUtils.py - Soporte para gráficos de Pacman
* textDisplay.py - gráficos ASCII para Pacman
* ghostAgents.py - Agentes para el control de los fantasmas
* keyboardAgents.py - interfaces de teclado para controlar Pacman
* layout.py - Código para la lectura de archivos de diseño y almacenar sus contenidos
* autograder.py - autograder proyecto
* testParser.py - Analiza los archivos de prueba y solución autograder
* testClasses.py - clases de prueba autograding general
* test_cases/ - Directorio que contiene los casos de prueba para cada pregunta
* multiagentTestClasses.py - Proyecto 2 clases de prueba específicos autograding

**Evaluación:** El código será autograded para la corrección técnica. Por favor, no cambiar los nombres de las funciones o clases establecidas en el código, o va a causar estragos en el autograder.

**Obtención de ayuda:** Usted no está solo! Si usted se encuentra atascado en algo, póngase en contacto con Michael en busca de ayuda. Queremos que estos proyectos sean gratificantes y de instrucción, no frustrante y desmoralizante. Sin embargo, no sabemos cuándo o cómo ayudar a menos que se le pregunte.

## Multi-Agente de Pacman

En primer lugar, jugar un juego de Pacman clásico:

```
python pacman.py
```

Ahora, ejecute el proporcionado ReflexAgent en multiAgents.py:

```
python pacman.py -p ReflexAgent
```

Tenga en cuenta que juega bastante mal incluso en diseños sencillos:

```
python pacman.py -p ReflexAgent -l testClassic
```

Inspeccionar su código (en multiAgents.py) y asegúrese de entender lo que está haciendo.

## Pregunta 1 (4 puntos): Reflex Agente

Mejorar la ReflexAgent de multiAgents.py jugar respetable. El código de agente reflejo proporcionado proporciona algunos ejemplos útiles de los métodos que consultan la GameStateinformación. Un agente reflejo capaces tendrá que considerar tanto los lugares de comida y lugares de fantasmas para un buen desempeño. Su agente debe limpiar con facilidad y de forma fiable el testClassicdiseño:

```
python pacman.py -p ReflexAgent -l testClassic
```

Pruebe su agente reflejo en el defecto mediumClassicde diseño con un fantasma o dos (y animación de apagado a acelerar la visualización):

```
python pacman.py --frameTime 0 -p ReflexAgent -k 1
python pacman.py --frameTime 0 -p ReflexAgent -k 2
```

¿Cómo le fue a su agente? Es probable que a menudo mueren con 2 fantasmas en el tablero por defecto, a menos que su función de evaluación es bastante bueno.

*Nota:* Como características, prueba el recíproco de valores importantes (tales como la distancia a la alimentación) en lugar de sólo los propios valores.

*Nota:* La función de evaluación se está escribiendo está evaluando pares estado-acción; en las partes posteriores del proyecto, se le evaluando estados.

*Opciones:* fantasmas predeterminados son aleatorios; también se puede jugar por diversión con los fantasmas de dirección ligeramente más inteligentes usando `-g DirectionalGhost`. Si la aleatoriedad está evitando que indica si el agente está mejorando, se puede utilizar `-f` para funcionar con una semilla aleatoria fijo (las mismas opciones al azar cada juego). También se puede jugar varios juegos en una fila con `-n`. Desactivar los gráficos con `-q` ejecutar un montón de juegos rápidamente.

*Calificaciones:* vamos a ejecutar el agente en el openClassic diseño de 10 veces. Usted recibirá 0 puntos si sus tiempos de agente, o nunca gana. Usted recibirá 1 punto si gana su agente de al menos 5 veces, o 2 puntos si su agente gana los 10 juegos. Recibirá un punto de adición 1 si puntuación media de su agente es mayor que 500, o 2 puntos si es mayor que 1000. Puede probar su agente a cabo bajo estas condiciones con

```
python autograder.py -q q1
```

Para ejecutarlo sin gráficos, utilice:

```
python autograder.py -q q1 --no-graphics
```

No gaste demasiado tiempo en esta cuestión, sin embargo, ya que la carne del proyecto está por venir.

## Pregunta 2 (5 puntos): Minimax

Ahora usted va a escribir una cuenta de búsqueda de confrontación en el proporcionado MinimaxAgent trozo de clases en multiAgents.py. Su agente Minimax debería funcionar con cualquier número de fantasmas, por lo que tendrá que escribir un algoritmo que es ligeramente más general que lo que ha visto previamente en la conferencia. En particular, su árbol Minimax tendrá múltiples capas min (uno para cada fantasma) para todas las capas máx.

El código también debe ampliar el árbol de juego a una profundidad arbitraria. Anotar las hojas de su árbol Minimax con el suministrado self.evaluationFunction, que por defecto scoreEvaluationFunction. MinimaxAgent extiende MultiAgentSearchAgent, lo que da acceso a la self.depth y self.evaluationFunction. Asegúrese de que su código de Minimax hace referencia a estas dos variables en su caso ya que estas variables se rellenan en respuesta a la orden opciones de línea.

*Importante:* Una sola capa de búsqueda se considera que es un movimiento Pacman y todas las respuestas de los fantasmas ', por lo que la profundidad de búsqueda 2 implicará Pacman y cada fantasma se mueve dos veces.

*La clasificación:* Nos será revisar su código para determinar si se explora el número correcto de los estados de juego. Esta es la única manera confiable de manera de detectar algunos errores muy sutiles en las implementaciones de Minimax. Como resultado, la autograder será muy exigente con la cantidad de veces que llame GameState.generateSuccessor. Si usted lo llama ni más ni menos de lo necesario, el autograder se quejará. Para probar y depurar el código, ejecute

```
python autograder.py -q q2
```

Esto le mostrará lo que hace su algoritmo en un número de árboles pequeños, así como un juego de Pacman. Para ejecutarlo sin gráficos, utilice:

```
python autograder.py -q q2 --no-graphics
```

**Sugerencias y Observaciones**

* La aplicación correcta de Minimax dará lugar a perder el juego Pacman en algunas pruebas. Este no es un problema: como es el comportamiento correcto, se pasan las pruebas.
* La función de evaluación de la prueba de pacman en esta parte ya está escrito ( self.evaluationFunction). Usted no debe cambiar esta función, pero reconocen que ahora estamos evaluando \*estados\* en lugar de acciones, ya que estábamos para el agente reflejo. Agentes de preanálisis evalúan los estados futuros mientras que los agentes evalúan las acciones reflejas de la situación actual.
* Los valores minimax del estado inicial en el minimaxClassic diseño son 9, 8, 7, -492 para profundidades de 1, 2, 3 y 4 respectivamente. Tenga en cuenta que su agente de Minimax menudo va a ganar (665/1000 juegos para nosotros) a pesar de la alarmante predicción de la profundidad de 4 Minimax.

```
python pacman.py -p MinimaxAgent -l minimaxClassic -a depth=4
```

* Pacman es siempre el agente 0, y los agentes se mueven con el fin de aumentar el índice agente.
* Todos los estados de Minimax deben ser GameStates, ya sea en el pasado para getActiono generados a través GameState.generateSuccessor. En este proyecto, no se extraerán a los estados simplificados.
* En las placas de mayor tamaño, como openClassicy mediumClassic(el valor predeterminado), se encuentra Pacman para ser bueno en no morir, pero bastante malo en ganar. A menudo va agite sin avanzar. Incluso podría retorcerse justo al lado de un punto sin comer porque él no sabe dónde iría después de comer ese punto. No se preocupe si usted ve este comportamiento, la pregunta 5 va a limpiar todas estas cuestiones.
* Cuando Pacman cree que su muerte es inevitable, que tratará de terminar el juego tan pronto como sea posible debido a la sanción constante para la vida. A veces, esto es lo peor que ver con fantasmas al azar, pero los agentes minimax siempre ha de asumir lo peor:
```
python pacman.py -p MinimaxAgent -l trappedClassic -a depth=3
```

Asegúrese de que usted entiende por qué Pacman se precipita el fantasma más cercano en este caso.

## Pregunta 3 (5 puntos): poda alfa-beta

Hacer un nuevo agente que utiliza la poda alfa-beta para explorar de manera más eficiente el árbol Minimax, en AlphaBetaAgent. Una vez más, el algoritmo será un poco más general que el pseudocódigo de la conferencia, por lo que parte del reto es extender la lógica de la poda alfa-beta apropiada a múltiples agentes minimizador.

Debería ver una aceleración (tal vez la profundidad de 3 alfa-beta se ejecutará tan rápido como la profundidad Minimax 2). Idealmente, la profundidad de 3 smallClassic debe funcionar en tan sólo unos segundos por movimiento o más rápido.

```
python pacman.py -p AlphaBetaAgent -a depth=3 -l smallClassic
```

Los AlphaBetaAgent valores minimax deben ser idénticos a los MinimaxAgentvalores minimax, a pesar de las acciones que selecciona puede variar debido a diferentes comportamientos de desempate. Una vez más, los valores minimax del estado inicial en el minimaxClassicdiseño son 9, 8, 7 y -492 para profundidades de 1, 2, 3 y 4 respectivamente.

*La clasificación:* Puesto que comprobamos su código para determinar si se explora el número correcto de los estados, es importante que realice la poda alfa-beta y sin reordenar los niños. En otras palabras, los Estados sucesores siempre deben ser procesados en el orden que devuelve GameState.getLegalActions. Una vez más, no llame GameState.generateSuccessor más de lo necesario.

**Debe no podar en la igualdad con el fin de que coincida con el conjunto de estados explorados por nuestra autograder.** (De hecho, en su defecto, pero incompatible con nuestra autograder, sería permitir también para la poda en la igualdad e invocar alfa-beta una vez en cada niño de la nodo raíz, pero esto no coincidir con el autograder.)

El pseudo-código de abajo representa el algoritmo que debe aplicar para esta pregunta.

![Alpha-Beta Implementación](https://s3-us-west-2.amazonaws.com/cs188websitecontent/projects/release/multiagent/v1/002/alpha-beta-on-inequality.png)

Para probar y depurar el código, ejecute

```
python autograder.py -q q3
```

Esto le mostrará lo que hace su algoritmo en un número de árboles pequeños, así como un juego de Pacman. Para ejecutarlo sin gráficos, utilice:

```
python autograder.py -q q3 --no-graphics
```

La aplicación correcta de la poda alfa-beta dará lugar a la pérdida de Pacman algunas de las pruebas. Este no es un problema: como es el comportamiento correcto, se pasan las pruebas.

## Pregunta 4 (5 puntos): Expectimax

Minimax y alfa-beta son grandes, pero los dos se supone que está jugando contra un adversario que toma decisiones óptimas. Como cualquiera que haya ganado el tic-tac-dedo del pie puede decir, esto no siempre es el caso. En esta pregunta se le implementar el ExpectimaxAgent, que es útil para modelar el comportamiento probabilístico de agentes que pueden tomar decisiones óptimas.

Al igual que con la búsqueda y problemas de satisfacción de restricciones cubierto hasta ahora en esta clase, la belleza de estos algoritmos es su aplicabilidad general. Para acelerar su propio desarrollo, hemos suministrado algunos casos de prueba basados en árboles genéricos. Se puede depurar su aplicación en los pequeños los árboles de juego utilizando el comando:

```
python autograder.py -q q4
```

Se recomienda la depuración en estos casos de prueba pequeñas y manejables y le ayudará a encontrar los fallos rápidamente. **Asegúrese de que al calcular sus promedios que se utilizan flotadores.** La división entera trunca en Python, por lo que 1/2 = 0, a diferencia del caso con los flotadores cuando 1.0/2.0 = 0.5.

Una vez que el algoritmo está trabajando en árboles pequeños, se puede observar su éxito en el Pacman. Fantasmas al azar son, por supuesto, los agentes minimax no óptimas, y así modelar con la búsqueda minimax pueden no ser apropiados. ExpectimaxAgent, Ya no tendrá el mínimo sobre todas las acciones de fantasmas, pero la expectativa de acuerdo con el modelo de su agente de cómo actúan los fantasmas. Para simplificar el código, suponga que sólo va a correr contra un adversario que elige entre sus getLegalActions uniformemente al azar.

Para ver cómo se comporta el ExpectimaxAgent en Pacman, ejecute:

```
python pacman.py -p ExpectimaxAgent -l minimaxClassic -a depth=3
```

Ahora debería observar un enfoque más cavalier en cuartos cercanos con fantasmas. En particular, si Pacman percibe que podía ser atrapada, pero podría escapar a tomar unas cuantas más piezas de alimentos, que va a al menos intentarlo. Investigar los resultados de estas dos situaciones:

```
python pacman.py -p AlphaBetaAgent -l trappedClassic -a depth=3 -q -n 10
python pacman.py -p ExpectimaxAgent -l trappedClassic -a depth=3 -q -n 10
```

Usted debe encontrar que sus ExpectimaxAgent victorias sobre la mitad del tiempo, mientras que su AlphaBetaAgent siempre pierde. Asegúrese de entender por qué el comportamiento aquí difiere del caso Minimax.

La aplicación correcta de expectimax dará lugar a la pérdida de Pacman algunas de las pruebas. Este no es un problema: como es el comportamiento correcto, se pasan las pruebas.

## Pregunta 5 (6 puntos): la función de evaluación

Escribe una mejor función de evaluación de pacman en la función prevista betterEvaluationFunction. La función de evaluación debe evaluar estados, en lugar de acciones como su función de evaluación agente reflejo hicieron. Es posible utilizar cualquier herramienta a su disposición para la evaluación, incluyendo el código de búsqueda del último proyecto. Con una profundidad de 2 búsqueda, su función de evaluación debe borrar el smallClassic diseño con un fantasma al azar más de la mitad del tiempo y todavía funcionar a una velocidad razonable (para obtener crédito completo, Pacman debe ser un promedio de alrededor de 1000 puntos cuando está ganando).

```
python autograder.py -q q5
```

La clasificación: la autograder ejecutará el agente en el smallClassic diseño de 10 veces. Vamos a asignar puntos a su función de evaluación de la siguiente manera:

* Si gana al menos una vez y sin tiempo de espera del autograder, recibirá 1 punto. Cualquier agente que no satisfagan estos criterios recibirán 0 puntos
* +1 para ganar al menos 5 veces, +2 por ganar todos los 10 veces
* +1 para una puntuación media de al menos 500, +2 para una puntuación media de al menos 1000 (incluyendo las puntuaciones de los juegos perdidos)
* +1 Si sus juegos tienen en promedio menos de 30 segundos en la máquina autograder. El autograder se ejecute en EC2, por lo que esta máquina tendrá una buena cantidad de recursos, pero el ordenador personal podría ser mucho menos eficiente (netbooks) o (plataformas de juegos) mucho más performant.
* Los puntos adicionales para la puntuación media y el tiempo de cálculo sólo se conceden si gana al menos 5 veces.

### Sugerencias y Observaciones

* En cuanto a su función de evaluación agente reflejo, es posible que desee utilizar el recíproco de valores importantes (tales como la distancia a la alimentación) en lugar de los propios valores.
* Una forma es posible que desee escribir su función de evaluación es el uso de una combinación lineal de funciones. Es decir, calcular los valores de características sobre el estado que cree son importantes, y luego combinar estas características multiplicándolos por diferentes valores y sumando los resultados. Usted puede decidir lo que se multiplique por cada característica basada en la importancia de que piensa que es.



## Sumisión

No se requiere la presentación. Felicidades para pasar el autograder y ayudar a Pacman!!
