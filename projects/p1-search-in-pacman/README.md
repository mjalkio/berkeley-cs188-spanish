# Proyecto 1: Buscar en Pacman

Versión original se puede encontrar [aquí](http://http://ai.berkeley.edu/search.html).

## Tabla de contenido

1. Introducción
2. Bienvenido
3. P1: primera búsqueda en profundidad
4. P2: búsqueda en anchura
5. P3: Uniforme Costo Buscar
6. P4: A * Buscar
7. P5: Esquinas Problema: Representación
8. P6: Esquinas Problema: Heurística
9. P7: Comer todos los puntos: Heurística
10. P8: subóptima Buscar

## Introducción

![Pac-man in maze]
> Todas esas paredes de colores, laberintos dan Pacman el blues, así que le enseñan a buscar.

En este proyecto, su agente de Pacman encontrará caminos a través de su mundo laberinto, tanto para llegar a un lugar determinado y de recogida de alimentos de manera eficiente. Usted va a construir algoritmos de búsqueda generales y aplicarlos a situaciones de Pacman.

Al igual que en Proyecto 0, este proyecto incluye un autograder para que usted pueda grado sus respuestas en su máquina. Esto se puede ejecutar con el comando:

```
python autograder.py
```

Ver el tutorial autograder en Project 0 para obtener más información sobre cómo utilizar el autograder.

El código para este proyecto consta de varios archivos de Python, algunos de los cuales deberá leer y entender con el fin de completar la tarea, y algunos de los cuales se puede pasar por alto.

*Los archivos que va a editar:*
* search.py - Donde todas sus algoritmos de búsqueda residirán.
* searchAgents.py - Donde todos sus agentes basados ​​en la búsqueda residirán.

*Archivos es posible que desee mirar:*
* pacman.py - El archivo principal que corre juegos de Pacman. Este archivo describe un tipo Pacman gamestate, que se utiliza en este proyecto.
* game.py - La lógica detrás de cómo funciona el mundo Pacman. Este archivo describe varios tipos de soporte como AgentState, agente, Dirección, y Cuadrícula.
* util.py - estructuras de datos útiles para la implementación de algoritmos de búsqueda.

*Apoyando archivos que puede pasar por alto:*
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
* searchTestClasses.py - Proyecto 1 clases de prueba específicos autograding

*Evaluación:* El código será autograded para la corrección técnica. Por favor, no cambiar los nombres de las funciones o clases establecidas en el código, o va a causar estragos en el autograder.

**Obtención de ayuda:** Usted no está solo! Si usted se encuentra atascado en algo, póngase en contacto con Michael en busca de ayuda. Queremos que estos proyectos sean gratificantes y de instrucción, no frustrante y desmoralizante. Sin embargo, no sabemos cuándo o cómo ayudar a menos que se le pregunte.

## Bienvenido a Pacman

Después de descargar el código y cambiar al directorio, usted debe ser capaz de jugar un juego de Pacman escribiendo lo siguiente en la línea de comandos:

```
python pacman.py
```

Pacman vive en un mundo azul brillante de torcer los pasillos y las golosinas sabrosas redondas. Navegando por este mundo de manera eficiente será el primer paso de Pacman en el dominio de su dominio.

El agente más simple en searchAgents.py se llama el GoWestAgent , que siempre va al Oeste (un agente reflejo trivial). Este agente puede ganar de vez en cuando:

```
python pacman.py --layout testMaze --pacman GoWestAgent
```

Sin embargo, las cosas se ponen feas para este agente cuando se requiere de giro:

```
python pacman.py --layout tinyMaze --pacman GoWestAgent
```

Si Pacman se atasca, puede salir del juego tecleando `CTRL-c` en su terminal.

Pronto, su agente va a resolver no sólo tinyMaze, pero cualquier laberinto desea.

Tenga en cuenta que pacman.py es compatible con una serie de opciones que cada uno puede expresarse en un largo camino (por ejemplo, --layout ) o una forma corta (por ejemplo, -l ). Se puede ver la lista de todas las opciones y sus valores por defecto a través de:

```
python pacman.py -h
```

Además, todos los comandos que aparecen en este proyecto también aparecen en commands.txt, para una fácil copiar y pegar. En UNIX / Mac OS X, puede incluso ejecutar todos estos comandos en orden con `bash commands.txt`.

Nota: si recibe mensajes de error con respecto Tkinter, ver [esta página](http://tkinter.unpythonic.net/wiki/How_to_install_Tkinter).

## Pregunta 1 (3 puntos): Encontrar un punto fijo de Alimentos usando primera búsqueda en profundidad (Depth First Search)

En searchAgents.py, encontrará una totalmente implementado operación de búsqueda , que planea un camino a través del mundo Pacman y después ejecuta ese camino paso a paso. Los algoritmos de búsqueda para la formulación de un plan no se apliquen - que es su trabajo.

En primer lugar, la prueba de que la operación de búsqueda está funcionando correctamente ejecutando:

```
python pacman.py -l tinyMaze -p SearchAgent -a fn=tinyMazeSearch
```

El comando anterior le indica la SearchAgent de usar tinyMazeSearch como su algoritmo de búsqueda, que se implementa en search.py. Pacman debe navegar por el laberinto con éxito.

Ahora es el momento de escribir funciones de pleno derecho genéricos de búsqueda para ayudar a planificar rutas Pacman! Pseudocódigo para los algoritmos de búsqueda que voy a escribir se puede encontrar en las diapositivas de las clases. Recuerde que un nodo de búsqueda debe contener no sólo un estado, sino también la información necesaria para reconstruir la ruta (plan), que llega a ese estado.

*Nota importante:* Todos sus funciones de búsqueda tienen que devolver una lista de **acciones** que conduzcan al agente desde el principio hasta el fin. Todas estas acciones tienen que ser jugadas legales (direcciones válidas, sin que se mueven a través de las paredes).

*Nota importante:* Asegúrese de utilizar la Stack, Queue y PriorityQueue estructuras de datos proporcionado a usted en util.py! Estas implementaciones estructura de datos tienen propiedades particulares que se requieren para la compatibilidad con el autograder.

**Pista:** Cada algoritmo es muy similar. Algoritmos para la DFS, BFS, UCS, y A* sólo difieren en los detalles de cómo se gestiona la franja. Por lo tanto, se concentran en conseguir DFS derecha y el resto debería ser relativamente sencilla. De hecho, una posible implementación requiere solamente un único método de búsqueda genérico que está configurado con una estrategia de puesta en cola específica del algoritmo. (Su aplicación es necesario que no sea de esta forma para recibir crédito completo).

Implementar el algoritmo de búsqueda primero en profundidad (DFS) en el depthFirstSearch función en search.py. Para hacer su algoritmo completo , escribir la versión de búsqueda gráfica de la DFS, lo que evita la expansión de los estados ya visitados.

El código debe encontrar rápidamente una solución para:

```
python pacman.py -l tinyMaze -p SearchAgent
python pacman.py -l mediumMaze -p SearchAgent
python pacman.py -l bigMaze -z .5 -p SearchAgent
```

La junta Pacman mostrará una superposición de los estados exploradas, y el orden en el que fueron explorados (más brillante de color rojo significa la exploración anterior). Es el orden de exploración de lo que habría esperado? Pacman no van realmente a todos los cuadrados explorados en su camino a la meta?

**Sugerencia:** Si se utiliza una pila como la estructura de datos, la solución encontrada por el algoritmo DFS para mediumMaze debe tener una longitud de 130 (siempre que empuja sucesores sobre la franja en el orden establecido por getSuccessors; podría obtener 246 si les mueves en el orden inverso). ¿Es esta una solución menos costo? Si no es así, pensar en lo primero en profundidad de búsqueda está haciendo mal.

## Pregunta 2 (3 puntos): búsqueda en anchura (BFS)

Implementar el algoritmo de búsqueda en anchura (BFS) en el breadthFirstSearch función en search.py. Una vez más, escribir un algoritmo de búsqueda gráfica que evita la expansión de los estados ya visitados. Probar el código de la misma manera que lo hizo para la búsqueda en profundidad.

```
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python pacman.py -l bigMaze -p SearchAgent -a fn=bfs -z .5
```

BFS no encontrar una solución menos costosa? Si no es así, comprobar su aplicación.

**Sugerencia:** Si Pacman mueve con demasiada lentitud para usted, pruebe la opción `--frameTime 0`.

**Nota:** Si usted ha escrito el código de búsqueda de forma genérica, el código debería funcionar igual de bien para el problema de búsqueda de ocho rompecabezas sin ningún cambio.

```
python eightpuzzle.py
```

## Pregunta 3 (3 puntos): La variación de la función de coste

Mientras BFS encontrará un camino de menor número de acciones-a la meta, puede ser que desee encontrar caminos que son los "mejores" en otros sentidos. Considere mediumDottedMaze y mediumScaryMaze.

Al cambiar la función de coste, podemos animar a Pacman para encontrar caminos diferentes. Por ejemplo, podemos cobrar más por etapas peligrosas en las zonas de fantasmas-montado o menos para los pasos en las áreas de alimentos ricos, y un agente racional Pacman debería ajustar su comportamiento en respuesta.

Implementar el algoritmo de búsqueda gráfica uniforme costo en el uniformCostSearch función en search.py. Le animamos a mirar a través de util.py para algunas estructuras de datos que pueden ser útiles en su aplicación. Ahora debe observar el comportamiento de éxito en los tres de los siguientes diseños, en los que los agentes están por debajo de todos los agentes UCS que difieren sólo en la función de coste que utilizan (los agentes y funciones de coste se escriben para usted):

```
python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs
python pacman.py -l mediumDottedMaze -p StayEastSearchAgent
python pacman.py -l mediumScaryMaze -p StayWestSearchAgent
```

**Nota:** Usted debe conseguir unos costes muy bajos y muy altos de ruta para el StayEastSearchAgent y StayWestSearchAgent respectivamente, debido a sus funciones de coste exponenciales (véase searchAgents.py para más detalles).

## Pregunta 4 (3 puntos): búsqueda A*

Poner en práctica búsqueda gráfico A* de la función de vacío aStarSearch en search.py. A* toma una función heurística como argumento. Heurística toman dos argumentos: un estado en el problema de búsqueda (el argumento principal), y el problema mismo (para obtener información de referencia). El nullHeuristic función heurística en search.py ​​es un ejemplo trivial.

Puede probar la aplicación A * en el problema original de encontrar un camino a través de un laberinto a una posición fija usando la heurística de la distancia Manhattan (ya aplicado como manhattanHeuristic en searchAgents.py).

```
python pacman.py -l bigMaze -z .5 -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic
```

Debería ver que A* encuentra la solución óptima ligeramente más rápido que la búsqueda costo uniforme (alrededor de 549 vs. 620 nodos de búsqueda ampliadas en nuestra aplicación, pero los lazos de prioridad puede hacer que sus números difieren ligeramente). ¿Qué ocurre en openMaze para las diferentes estrategias de búsqueda?

## Pregunta 5 (3 puntos): Encontrar todos los rincones

El poder real de A* sólo será evidente con un problema de búsqueda más difícil. Ahora, es el momento de formular un nuevo problema y diseñar una heurística para ello.

En los laberintos de la esquina , hay cuatro puntos, uno en cada esquina. Nuestro nuevo problema de búsqueda es encontrar el camino más corto a través del laberinto que toca las cuatro esquinas (si el laberinto en realidad tiene comida allí o no). Tenga en cuenta que para algunos laberintos como tinyCorners, el camino más corto no siempre van a la comida más cercano primero! **Sugerencia:** el camino más corto a través tinyCorners toma 28 pasos.

**Nota: Asegúrese de completar la pregunta 2 antes de trabajar en la pregunta 5, porque la pregunta 5 se basa en su respuesta a la pregunta 2.**

Implementar el CornersProblem problema de búsqueda en searchAgents.py. Usted tendrá que elegir una representación estatal que codifica toda la información necesaria para detectar si se han alcanzado las cuatro esquinas. Ahora, su agente de búsqueda debe resolver:

```
python pacman.py -l tinyCorners -p SearchAgent -a fn=bfs,prob=CornersProblem
python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs,prob=CornersProblem
```

Es necesario definir una representación abstracta del estado que no codifican información irrelevante (como la posición de los fantasmas, donde la comida extra es, etc.). En particular, no utilice un Pacman gamestate como un estado de búsqueda. Su código será muy, muy lento si lo hace (y también mal).

**Sugerencia:** Las únicas partes del estado juego que necesita para hacer referencia en su aplicación son la puesta en posición de Pacman y la ubicación de las cuatro esquinas.

Nuestra aplicación de breadthFirstSearch se expande un poco menos de 2000 nodos de búsqueda en mediumCorners . Sin embargo, la heurística (utilizados con búsqueda A *) pueden reducir la cantidad de búsqueda requeridos.

## Pregunta 6 (3 puntos): Esquinas Problema: Heurística

**Nota: Asegúrese de completar la pregunta 4 antes de trabajar en la pregunta 6, porque la pregunta 6 se basa en su respuesta a la pregunta 4.**

Implementar un no trivial, heurística consistente para el CornersProblem en cornersHeuristic.

```
python pacman.py -l mediumCorners -p AStarCornersAgent -z 0.5
```

**Nota:** AStarCornersAgent es un atajo para

```
-p SearchAgent -a fn=aStarSearch,prob=CornersProblem,heuristic=cornersHeuristic.
```

*Admisibilidad vs. Consistencia:* Recuerde, la heurística son sólo las funciones que se llevan a estados de búsqueda y los números que estiman el costo para un objetivo más próximo regreso. Heurística más eficaces serán los valores vuelvan a acercarse a los costes reales de gol. Para ser admisibles, los valores heurísticos deben tener límites inferiores sobre el costo real del camino más corto a la meta más cercana (y no negativo). Para ser coherente , debe sostener, además, que si una acción tiene costo c, luego de tomar esa acción sólo puede provocar una caída de heurística de un máximo de c.

Recuerde que la admisibilidad no es suficiente para garantizar la corrección en busca gráfico - que necesita la condición más fuerte de consistencia. Sin embargo, heurística admisible suelen ser también coherente, sobre todo si se derivan de relajaciones de problemas. Por lo tanto, suele ser más fácil de comenzar a cabo por la lluvia de ideas heurística admisible. Una vez que tenga una heurística admisible que funciona bien, se puede comprobar si de hecho es consistente, también. La única manera de garantizar la consistencia es con una prueba. Sin embargo, la inconsistencia menudo se puede detectar mediante la verificación de que para cada nodo se expande, sus nodos sucesores son iguales o mayores en valor de f. Por otra parte, si UCS y A* jamás regresan senderos de diferentes longitudes, su heurística es inconsistente. Esta materia es difícil!

*No trivial Heurística:* La heurística triviales son los que devuelven cero en todas partes (UCS) y la heurística que calcula el coste real finalización. El primero no le ahorrará cualquier momento, mientras que el segundo tiempo de espera del autograder. ¿Quieres una heurística que reduce el tiempo total de cómputo, aunque para esta tarea la autograder sólo comprueba el recuento de nodos (aparte de la aplicación de un límite de tiempo razonable).

*Calificaciones:* Su heurística debe ser un no trivial heurística constante no negativa a recibir los puntos. Asegúrese de que su heurística devuelve 0 en cada estado de la meta y nunca devuelve un valor negativo. Dependiendo de qué tan pocos nodos expande sus heurísticas, se le calificará:

Número de nodos expandidos |  Grado
-------------------------- | ------
más de 2000 | 0/3
como máximo 2000 |  1/3
como máximo 1600 |  2/3
como máximo 1200 |  3/3

**Recuerde:** Si su heurística es inconsistente, recibirá ningún crédito, así que ten cuidado!

## Pregunta 7 (4 puntos): Comer todos los puntos

Ahora vamos a resolver un problema de búsqueda dura: comer todos los alimentos Pacman en el menor número posible de pasos. Para ello, necesitaremos una nueva definición del problema de búsqueda que formaliza el problema de la limpieza de los alimentos: FoodSearchProblem en searchAgents.py (implementado para usted). Una solución se define para ser un camino que recoge toda la comida en el mundo Pacman. Para el presente proyecto, las soluciones no tienen en cuenta ningún fantasmas o pelotillas de la energía; soluciones sólo dependen de la colocación de las paredes, la comida regular y Pacman. (De fantasmas curso pueden arruinar la ejecución de una solución! Vamos a llegar a que en el próximo proyecto.) Si usted ha escrito sus métodos de búsqueda generales correctamente, A* con una heurística nula (equivalente a la búsqueda uniforme costo) deberíamos rápidamente encontrar una solución óptima para testSearch sin cambio de código de su parte (coste total de 7).

```
python pacman.py -l testSearch -p AStarFoodSearchAgent
```

**Nota:** AStarFoodSearchAgent es un atajo para `-p SearchAgent -a fn=astar,prob=FoodSearchProblem,heuristic=foodHeuristic`.

Usted debe encontrar que UCS se hace más lento, incluso para el aparentemente simple tinySearch . Como referencia, nuestra aplicación toma 2.5 segundos para encontrar un camino de longitud 27, después de expandirse 5057 nodos de búsqueda.

**Nota: Asegúrese de completar la pregunta 4 antes de trabajar en la pregunta 7, porque la pregunta 7 se basa en su respuesta a la pregunta 4.**

Rellene foodHeuristic en searchAgents.py con una consistente heurística para la FoodSearchProblem. Probar su agente en el trickySearch tabla:

```
python pacman.py -l trickySearch -p AStarFoodSearchAgent
```

Nuestro agente UCS encuentra la solución óptima en unos 13 segundos y explorar más de 16.000 nodos.

Cualquier heurística consistente no negativo no trivial recibirá 1 punto. Asegúrese de que su heurística devuelve 0 en cada estado de la meta y nunca devuelve un valor negativo. Dependiendo de qué tan pocos nodos expande sus heurísticas, obtendrá puntos adicionales:

Número de nodos expandidos | Grado
-------------------------- | ------
más de 15.000 | 1/4
como máximo 15.000 | 2/4
como máximo 12.000 | 3/4
como máximo 9000 | 4/4 (crédito completo; medio)
como máximo 7000 | 5/4 (crédito adicional opcional; duro)

**Recuerde:** Si su heurística es inconsistente, recibirá ningún crédito, así que ten cuidado! ¿Se puede resolver mediumSearch en un corto período de tiempo? Si es así, estamos muy bien, muy impresionado, o su heurística es inconsistente.

## Pregunta 8 (3 puntos): subóptima Buscar

A veces, incluso con A* y una buena heurística, la búsqueda de la ruta óptima a través de todos los puntos es difícil. En estos casos, todavía gustaría encontrar un razonable buen camino, de forma rápida. En esta sección, que voy a escribir un agente que siempre come con avidez el punto más cercano. ClosestDotSearchAgent se implementa para usted en searchAgents.py, pero le falta una función clave que encuentra una ruta de acceso al punto más cercano.

Implementar la función findPathToClosestDot en searchAgents.py . Nuestro agente resuelve este laberinto (subóptima!) En menos de un segundo con un coste de la ruta de 350:

```
python pacman.py -l bigSearch -p ClosestDotSearchAgent -z .5
```

**Pista:** La forma más rápida de completar findPathToClosestDot es llenar en el AnyFoodSearchProblem, que está ausente de su prueba de gol. Entonces, resolver ese problema con una función de búsqueda apropiada. La solución debe ser muy corto!

Su ClosestDotSearchAgent no siempre va a encontrar el camino más corto posible a través del laberinto. Asegúrese de que usted entiende por qué y tratar de llegar a un pequeño ejemplo en el que ir varias veces para que el punto más cercano no da lugar a encontrar el camino más corto para comer todos los puntos.

## Sumisión

No se requiere la presentación. Felicidades para pasar el autograder y ayudar a Pacman!!
