# Proyecto 0: Unix / Python / Autograder Tutorial

Versión original se puede encontrar [aquí](http://ai.berkeley.edu/tutorial.html).

## Tabla de contenido

1. Introducción
2. Conceptos básicos de Unix
3. Conceptos básicos de Python
4. Autograding
5. P1: Adición
6. P2: ComprarMuchasFrutas
7. P3: ComprarInteligente

## Introducción

Los proyectos de esta clase supone que se utilizan Python 2.7.
Proyecto 0 comprenderá los siguientes aspectos:

* Un tutorial mini-UNIX (particularmente importante si se trabaja en máquinas de instrucción),
* Un tutorial mini-Python,
* Proyecto de clasificación: la liberación de cada proyecto incluye su autograder para ejecutar usted mismo.

**Archivos para editar:** Usted llenará en porciones de adicion.py , comprarMuchasFrutas.py , y comprarInteligente.py durante la asignación.

**Evaluación:** El código será autograded para la corrección técnica. Por favor, no cambiar los nombres de las funciones o clases establecidas en el código, o va a causar estragos en el autograder.

**Obtención de ayuda:** Usted no está solo! Si usted se encuentra atascado en algo, póngase en contacto con Michael en busca de ayuda. Queremos que estos proyectos sean gratificantes y de instrucción, no frustrante y desmoralizante. Sin embargo, no sabemos cuándo o cómo ayudar a menos que se le pregunte.

## Conceptos básicos de Unix

Éstos son los comandos básicos de UNIX para navegar y editar archivos.

*Nota: el entorno local puede comportarse de manera diferente a la descrita aquí.*

### Archivo / Manipulación Directorio

Cuando se abre una ventana de terminal, que está colocado en un símbolo del sistema:

```
[cs188-ta@nova ~]$
```

El indicador muestra el nombre de usuario, el host está conectado a, y su ubicación actual en la estructura de directorios (la ruta). El carácter de tilde es la abreviatura de su directorio personal. Tenga en cuenta que su indicador puede ser un poco diferente. Para hacer un directorio, utilice el `mkdir` comando. Use `cd` para cambiar a ese directorio:

```
[cs188-ta@nova ~]$ mkdir foo
[cs188-ta@nova ~]$ cd foo
[cs188-ta@nova ~/foo]$
```

Utilice `ls` para ver una lista de los contenidos de un directorio, y `touch` para crear un archivo vacío:

```
[cs188-ta@nova ~/foo]$ ls
[cs188-ta@nova ~/foo]$ touch hola_mundo
[cs188-ta@nova ~/foo]$ ls
hola_mundo
[cs188-ta@nova ~/foo]$ cd ..
[cs188-ta@nova ~]$
```

Algunos otros comandos Unix útiles:

* `cp` copia un archivo o archivos
* `rm` elimina (borra) un archivo
* `mv` mueve un archivo (es decir, cortar / pegar en lugar de copiar / pegar)
* `man` muestra la documentación de un comando
* `pwd` imprime su ruta actual
* `xterm` abre una nueva ventana de terminal
* `firefox` se abre un navegador web
* Pulse la tecla "Ctrl-C" para matar a un proceso en ejecución
* Anexar `&` a un comando para ejecutarlo en segundo plano
* `fg` trae un programa que se ejecuta en el fondo al primer plano

### El editor de texto Emacs

*Nota: en esta clase Michael utilizará Sublime Text en lugar de Emacs.*

Emacs es un editor de texto personalizable que tiene algunas características interesantes adaptados específicamente para los programadores. Sin embargo, se puede utilizar cualquier otro editor de texto que es posible que prefiera (por ejemplo, vi , pico , o Joe en Unix, o Notepad en Windows, o TextWrangler en OS X, y [muchos más](http://en.wikipedia.org/wiki/Python_IDE#Python)).

Para ejecutar Emacs, tipo `emacs` en un símbolo del sistema:

```
[cs188-ta@nova ~/python_basics]$ emacs holaMundo.py &
[1] 3262
```

Aquí nos dimos el argumento `holaMundo.py` que, o bien abrir ese archivo para la edición de si existe, o crear de otra manera. Emacs se da cuenta que se trata de un archivo fuente de Python (debido a la `.py` final) y entra en modo de Python, que se supone para ayudarle a escribir código. Al editar este archivo puede notar un poco de ese texto se colorea de forma automática: este es el resaltado de sintaxis para ayudarle a distinguir elementos tales como palabras clave, variables, cadenas y comentarios. Al pulsar Enter, Tab, o Retroceso puede hacer que el cursor salte a lugares extraños: esto se debe a Python es muy exigente con la sangría, y Emacs es la predicción de la tabulación adecuada que se debe utilizar.

Algunos comandos de edición de Emacs básicos (`C-` significa "mientras mantiene la tecla Ctrl"):

* `C-x C-s` Guardar el archivo actual
* `C-x C-f` Abrir un archivo, o crear un nuevo archivo si no existe
* `C-k` Cortar una línea, añadir al portapapeles
* `C-y` Pegar el contenido del portapapeles
* `C-_` Deshacer
* `C-g` Abortar un comando media entrado

También puede copiar y pegar usando sólo el ratón. Con el botón izquierdo, seleccione una región de texto a copiar. Haga clic en el botón central para pegar.

Hay dos formas de usar Emacs para desarrollar código Python. La forma más sencilla es utilizar sólo como un editor de texto: crear y editar archivos en Emacs Python; a continuación, ejecutar Python para probar el código en otro lugar, como en una ventana de terminal. Como alternativa, puede ejecutar Python dentro de Emacs: ver las opciones en "Python" en la barra de menú, o escribe `C-c!` iniciar un intérprete de Python en una pantalla dividida. (Uso `C-x o` para cambiar entre las pantallas divididas, o simplemente haga clic en `C-x` si no funciona).

Si desea pasar un tiempo adicional de configuración de convertirse en un usuario avanzado, puede intentar un IDE como [Eclipse](http://www.eclipse.org/downloads/) (Eclipse Descargar el paquete clásico en la parte inferior). Salida [PyDev](http://pydev.org/manual_101_root.html) para el soporte de Python en Eclipse.

## Conceptos básicos de Python

### Archivos necesarios

Puede descargar todos los archivos asociados con el Python mini-tutorial del [curso repositorio de Github](https://github.com/mjalkio/berkeley-cs188-spanish). Es en el directorio de `projects/P0-unix-python-tutorial/ python_basics`. Es probable que esté leyendo esto desde ese directorio en este momento!

### Tabla de contenido

* Llamando al intérprete
* Operadores
* Instrumentos de cuerda
* Dir y Ayuda
* Built-in Estructuras de Datos
  * listas
  * tuplas
  * conjuntos
  * diccionarios
* Secuencias de comandos de escritura
* Sangría
* Fichas vs Espacios
* Funciones de escritura
* Fundamentos de objetos
  * Definición de clases
  * El uso de objetos
  * Estática vs variables de instancia
* Consejos y trucos
* Solución de problemas
* Más Referencias

Las tareas de programación de este curso serán escritos en [Python](http://www.python.org/about/), un lenguaje orientado a objetos interpretado que comparte algunas características con Java y Scheme . Este tutorial le guiará a través de las construcciones sintácticas primarias en Python, usando ejemplos cortos.

Le recomendamos que escribir todos pitón se muestra en el tutorial en su propia máquina. Asegurarse de que responde de la misma manera.

Es posible encontrar la solución de problemas sección útil si llegas a tener problemas. Contiene una lista de los problemas frecuentes estudiantes CS188 anterior se han enfrentado al seguir este tutorial.

### Llamando al intérprete

Python se puede ejecutar en uno de dos modos. O bien se puede utilizar de forma *interactiva*, a través de un interpeter, o puede ser llamado desde la línea de comandos para ejecutar una *secuencia de comandos*. Vamos a utilizar por primera vez el intérprete de Python de forma interactiva.

Se invoca el intérprete mediante la introducción de pitón en el símbolo del sistema Unix.
Nota: es posible que tenga que escribir `python2.4`, `python2.5`, `python2.6` o `python2.7`, en lugar de `python`, dependiendo de su máquina.

```
[cs188-ta@nova ~]$ python
Python 2.6.5 (r265:79063, Jan 14 2011, 14:20:15)
[GCC 4.4.1] on sunos5
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### Operadores

El intérprete de Python se puede utilizar para evaluar expresiones, por ejemplo, simples expresiones aritméticas. Si introduce este tipo de expresiones en el indicador ( >>> ) serán evaluados y el resultado serán devueltos en la línea siguiente.

```
>>> 1 + 1
2
>>> 2 * 3
6
```

Operadores booleanos también existen en Python para manipular los primitivos `True` y `False` valores.

```
>>> 1==0
False
>>> not (1==0)
True
>>> (2==2) and (2==3)
False
>>> (2==2) or (2==3)
True
```

### Instrumentos de cuerda

Como Java, Python ha construido en un tipo de cadena. El `+` operador está sobrecargado de hacer la concatenación de cadenas de valores de cadena.

```
>>> "Inteligencia" + "Artificial"
'Inteligencia Artificial'
```

Hay muchos métodos incorporados que permiten manipular cadenas.

```
>>> 'artificial'.upper()
'ARTIFICIAL'
>>> 'AYUDA'.lower()
'ayuda'
>>> len('ayuda')
5
```

Tenga en cuenta que podemos utilizar comillas simples '' o comillas dobles "" para rodear cadena. Esto permite una fácil anidación de cadenas.

También podemos almacenar expresiones en variables.

```
>>> s = 'hola mundo'
>>> print s
hola mundo
>>> s.upper()
'HOLA MUNDO'
>>> len(s.upper())
10
>>> num = 8.0
>>> num += 2.5
>>> print num
10.5
```

En Python, usted no tiene declarar las variables antes de asignar a los mismos.

### Ejercicio: Dir y Help

Más información sobre los métodos de Python proporciona para las cuerdas. Para ver qué métodos Python prevé un tipo de datos, utilice el `dir` y `help` a los comandos:

```
>>> s = 'abc'

>>> dir(s)
['__add__', '__class__', '__contains__', '__delattr__', '__doc__', '__eq__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getslice__', '__gt__', '__hash__', '__init__','__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__','__repr__', '__rmod__', '__rmul__', '__setattr__', '__str__', 'capitalize', 'center', 'count', 'decode', 'encode', 'endswith', 'expandtabs', 'find', 'index', 'isalnum', 'isalpha', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'replace', 'rfind','rindex', 'rjust', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']

>>> help(s.find)

Help on built-in function find:

find(...)
    S.find(sub [,start [,end]]) -> int

    Return the lowest index in S where substring sub is found,
    such that sub is contained within s[start,end].  Optional
    arguments start and end are interpreted as in slice notation.

    Return -1 on failure.

>> s.find('b')
1
```

Probar algunas de las funciones de cadena que aparecen en `dir` (ignorar aquellos con guiones bajos _ '' alrededor del nombre del método).

### Built-in Estructuras de Datos

Python viene equipado con algunas estructuras de datos incorporados útiles, en términos generales similares a las colecciones del paquete de Java.

### listas

Listas de almacenar una secuencia de elementos mutables:

```
>>> frutas = [ 'manzana', 'naranja', 'pera', "platano"]
>>> frutas[0]
'manzana'
```

Podemos utilizar el + operador de concatenación para hacer la lista:

```
>>> otrasFrutas = [ 'kiwi', 'fresa']
>>> frutas + otrasFrutas
>>> [ 'manzana', 'naranja', 'pera', 'platano', 'kiwi', 'fresa']
```

Python también permite la indexación negativa de la parte posterior de la lista. Por ejemplo, las `frutas[-1]` accederán al último elemento "platano":

```
>>> frutas[-2]
'pera'
>>> frutas.pop()
"platano"
>>> frutas
[ 'manzana', 'naranja', 'pera']
>>> frutas.append('pomelo')
>>> frutas
[ 'manzana', 'naranja', 'pera', 'pomelo']
>>> frutas[-1] = 'pina'
>>> frutos
[ 'manzana', 'naranja', 'pera', 'pina']
```

También podemos índice de múltiples elementos adyacentes usando el operador de división. Por ejemplo, los `frutas[1:3]`, devuelve una lista que contiene los elementos en la posición 1 y 2. En general las `frutas[inicio:parada]` obtendrá los elementos de inicio, inicio+1,..., parada-1. También podemos hacer las `frutas[inicio:]` que devuelve todos los elementos a partir de la puesta índice. También `frutos[:parada]` volverán todos los elementos antes de que el elemento de la posición parada:

```
>>> frutas[0:2]
[ 'manzana', 'naranja']
>>> frutas[:3]
[ 'manzana', 'naranja', 'pera']
>>> frutos [2:]
[ 'pera' , 'pina']
>>> len(frutas)
4
```

Los elementos almacenados en las listas pueden ser cualquier tipo de datos de Python. Así por ejemplo podemos tener listas de listas:

```
>>> lstOfLsts = [['a','b','c'],[1,2,3],['one','two','three']]
>>> lstOfLsts[1][2]
3
>>> lstOfLsts[0].pop()
'c'
>>> lstOfLsts
[['a', 'b'],[1, 2, 3],['one', 'two', 'three']]
```

### Ejercicio: Listas

Juega con algunas de las funciones de la lista. Puede encontrar los métodos que puede llamar en un objeto a través de la `dir` y obtener información sobre ellos a través de la `help` de comandos:

```
>>> dir(list)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__',
'__delslice__', '__doc__', '__eq__', '__ge__', '__getattribute__',
'__getitem__', '__getslice__', '__gt__', '__hash__', '__iadd__', '__imul__',
'__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__',
'__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__',
'__rmul__', '__setattr__', '__setitem__', '__setslice__', '__str__',
'append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse',
'sort']

>>> help(list.reverse)
Help on built-in function reverse:

reverse(...)
    L.reverse() -- reverse *IN PLACE*
>>> lst = ['a','b','c']
>>> lst.reverse()
>>> ['c','b','a']
```

Nota: No haga caso de funciones con guiones bajos "_" en torno a los nombres; estos son métodos de ayuda privadas. Presione 'q' a la parte posterior de una pantalla de ayuda.

### tuplas

Una estructura de datos similar a la lista es la *tupla*, que es como una lista, excepto que es inmutable, una vez que se ha creado (es decir, no se puede cambiar su contenido una vez creado). Tenga en cuenta que las tuplas están rodeados de paréntesis mientras que las listas tienen corchetes.

```
>>> par = (3,5)
>>> par[0]
3
>>> x, y = par
>>> x
3
>>> y
5
>>> par[1] = 6
TypeError: object does not support item assignment
```

El intento de modificar una estructura inmutable produce una excepción. Excepciones indicar errores: Índice fuera de límites errores, errores de tipo, y así sucesivamente lo harán todas las excepciones de informe de esta manera.

### conjuntos

Un *conjunto* es otra estructura de datos que sirve como una lista desordenada, sin elementos duplicados. A continuación, se muestra cómo crear un conjunto, añadir cosas al conjunto, prueba de si un artículo está en el conjunto, y llevar a cabo operaciones de conjuntos comunes (diferencia, intersección, unión):

```
>>> shapes = ['circle','square','triangle','circle']
>>> setOfShapes = set(shapes)
>>> setOfShapes
set(['circle','square','triangle'])
>>> setOfShapes.add('polygon')
>>> setOfShapes
set(['circle','square','triangle','polygon'])
>>> 'circle' in setOfShapes
True
>>> 'rhombus' in setOfShapes
False
>>> favoriteShapes = ['circle','triangle','hexagon']
>>> setOfFavoriteShapes = set(favoriteShapes)
>>> setOfShapes - setOfFavoriteShapes
set(['square','polyon'])
>>> setOfShapes & setOfFavoriteShapes
set(['circle','triangle'])
>>> setOfShapes | setOfFavoriteShapes
set(['circle','square','triangle','polygon','hexagon'])
```

**Tenga en cuenta que los objetos del conjunto no tienen orden; no se puede asumir que su orden transversal o impresión será a través de las mismas máquinas!**

### diccionarios

La última estructura de datos integrada es el *diccionario* que almacena un mapa de un tipo de objeto (la clave) a otro (el valor). La clave debe ser un tipo inmutable (cadena, número o tupla). El valor puede ser cualquier tipo de datos de Python.

Nota: En el siguiente ejemplo, la orden impresa de las teclas devueltos por Python podría ser diferente que se muestra a continuación. La razón es que a diferencia de las listas que tienen un orden fijo, un diccionario es simplemente una tabla hash para la cual no existe una ordenación fija de las claves (como HashMaps en Java). El orden de las claves depende de cómo exactamente el algoritmo de hash mapas de teclas para cubos, y por lo general parece arbitraria. El código no debe depender de ordenamiento clave, y no debe sorprenderse si incluso una pequeña modificación en la forma en que su código utiliza un diccionario que da como resultado un nuevo ordenamiento clave.

```
>>> studentIds = {'knuth': 42.0, 'turing': 56.0, 'nash': 92.0 }
>>> studentIds['turing']
56.0
>>> studentIds['nash'] = 'ninety-two'
>>> studentIds
{'knuth': 42.0, 'turing': 56.0, 'nash': 'ninety-two'}
>>> del studentIds['knuth']
>>> studentIds
{'turing': 56.0, 'nash': 'ninety-two'}
>>> studentIds['knuth'] = [42.0,'forty-two']
>>> studentIds
{'knuth': [42.0, 'forty-two'], 'turing': 56.0, 'nash': 'ninety-two'}
>>> studentIds.keys()
['knuth', 'turing', 'nash']
>>> studentIds.values()
[[42.0, 'forty-two'], 56.0, 'ninety-two']
>>> studentIds.items()
[('knuth',[42.0, 'forty-two']), ('turing',56.0), ('nash','ninety-two')]
>>> len(studentIds)
3
```

Al igual que con las listas anidadas, también puede crear diccionarios de diccionarios.

## Ejercicio: Diccionarios

Usar `dir` y `help` a aprender acerca de las funciones que puede llamar en los diccionarios.

### Secuencias de comandos de escritura

Ahora que usted tiene una manija en el uso de Python de forma interactiva, vamos a escribir una secuencia de comandos de Python sencillo que muestra de Python para el bucle. Abra el archivo llamado `foreach.py` y actualizarlo con el siguiente código:

```
# Esto es lo que se ve como un comentario
frutas = ['manzanas','naranjas','peras','platanos']
for fruta in frutas:
    print fruta + ' para la venta'

preciosDeLasFrutas = {'manzanas': 2.00, 'naranjas': 1.50, 'peras': 1.75}
for fruta, precio in preciosDeLasFrutas.items():
    if precio < 2.00:
        print '%s cuestan %f por libra' % (fruta, precio)
    else:
        print fruta + ' son demasiado caros!'
```

En la línea de comandos, utilice el siguiente comando en el directorio que contiene `foreach.py`:

```
[cs188-ta@nova ~/tutorial]$ python foreach.py
manzanas para la venta
naranjas para la venta
peras para la venta
platanos para la venta
naranjas cuestan 1.500000 por libra
peras cuestan 1.750000 por libra
manzanas son demasiado caros!
```

Recuerde que las declaraciones de impresión se enumeran los costos pueden estar en un orden diferente en la pantalla que en este tutorial; eso es debido al hecho de que estamos en bucle sobre las claves de diccionario, que son desordenados. Para obtener más información sobre las estructuras de control (por ejemplo, `if` y `else`) en Python, echa un vistazo a [la oficial de la sección guía](http://docs.python.org/tut/) de aprendizaje sobre este tema.

Si te gusta la programación funcional que puede que al igual que el `map` y `filter`:

```
>>> map(lambda x: x * x, [1,2,3])
[1, 4, 9]
>>> filter(lambda x: x > 3, [1,2,3,4,5,4,3,2,1])
[4, 5, 4]
```

Se puede obtener [más información sobre lambda](http://www.secnetix.de/olli/Python/lambda_functions.hawk) si está interesado.

El siguiente fragmento de código muestra de Python *lista por comprensión* de la construcción:

```
nums = [1,2,3,4,5,6]
plusOneNums = [x+1 for x in nums]
oddNums = [x for x in nums if x % 2 == 1]
print oddNums
oddNumsPlusOne = [x+1 for x in nums if x % 2 ==1]
print oddNumsPlusOne
```

Este código se encuentra en un archivo llamado `listcomp.py`, que se puede ejecutar:

```
[cs188-ta@nova ~]$ python listcomp.py
[1,3,5]
[2,4,6]
```

### Ejercicio: Listas por comprensión

Escribe una lista por comprensión, que, a partir de una lista, genera una versión en minúsculas de cada cadena que tiene una longitud superior a cinco. Puede encontrar la solución en `listcomp2.py`.

### Cuidado con los Indendation!

A diferencia de muchos otros idiomas, Python usa la sangría en el código fuente para la interpretación. Así, por ejemplo, para la siguiente secuencia de comandos:

```
if 0 == 1:
    print 'Estamos en un mundo de dolor aritmética'
print 'Gracias por jugar'
```

salida voluntad

```
Gracias por jugar
```

Pero si hubiéramos escrito el guión como

```
if 0 == 1:
    print 'Estamos en un mundo de dolor aritmética'
    print 'Gracias por jugar'
```

no habría ninguna salida. La moraleja de la historia: vea cómo sangría! Lo mejor es usar cuatro espacios para el sangrado - eso es lo que utiliza el código del curso.

### Fichas vs Espacios

Debido a que Python utiliza sangría para la evaluación de código, que necesita para realizar un seguimiento del nivel de sangrado a través de bloques de código. Esto significa que si el archivo cambia de Python usando pestañas como el sangrado para espacios como la sangría, el intérprete de Python no será capaz de resolver la ambigüedad del nivel de sangría y lanzar una excepción. A pesar de que el código puede ser alineado visualmente en el editor de texto, Python "ve" un cambio en la indentación y muy probablemente arrojará una excepción (o rara vez, producir un comportamiento inesperado).

Esto ocurre más comúnmente cuando se abre un archivo de Python que utiliza un esquema de sangría que es lo contrario de lo que usa su editor de texto (también conocido como el editor de texto utiliza espacios y utiliza el archivo de fichas). Cuando se escribe una línea nueva de un bloque de código, habrá una mezcla de tabuladores y espacios, a pesar de que el espacio en blanco se alinea. Para una discusión más amplia sobre las pestañas vs espacios, ver [este](http://stackoverflow.com/questions/119562/tabs-versus-spaces-in-python-programming) debate en StackOverflow.

### Funciones de escritura

Al igual que en Java, en Python puede definir sus propias funciones:

```
fruitPrices = {'apples':2.00, 'oranges': 1.50, 'pears': 1.75}

def buyFruit(fruit, numPounds):
    if fruit not in fruitPrices:
        print "Sorry we don't have %s" % (fruit)
    else:
        cost = fruitPrices[fruit] * numPounds
        print "That'll be %f please" % (cost)

# Main Function
if __name__ == '__main__':
    buyFruit('apples',2.4)
    buyFruit('coconuts',2)
```

En lugar de tener un `main` función que en Java, el `__name__ == '__main__'` cheque se utiliza para delimitar las expresiones que se ejecutan cuando el archivo se llama como un script desde la línea de comandos. El código después de la retención principal es, pues, el mismo tipo de código que pondría en un `main` función en Java.

Guarde este script como fruit.py y ejecutarlo:

```
[cs188-ta@nova ~]$ python fruit.py
That'll be 4.800000 please
Sorry we don't have coconuts
```

### Ejercicio avanzado

Escribe una *quickSort* función en Python usando listas por comprensión. Utilice el primer elemento como el pivote. Puede encontrar la solución en `quickSort.py`.

### Fundamentos de objetos

Aunque esta no es una clase en la programación orientada a objetos, que tendrá que utilizar algunos objetos en los proyectos de programación, por lo que vale la pena que cubre los conceptos básicos de los objetos en Python. Un objeto encapsula datos y proporciona funciones para interactuar con dichos datos.

### Definición de clases

He aquí un ejemplo de definición de una clase denominada Fruitshop :

```
class FruitShop:

    def __init__(self, name, fruitPrices):
        """
            name: Name of the fruit shop

            fruitPrices: Dictionary with keys as fruit
            strings and prices for values e.g.
            {'apples':2.00, 'oranges': 1.50, 'pears': 1.75}
        """
        self.fruitPrices = fruitPrices
        self.name = name
        print 'Welcome to the %s fruit shop' % (name)

    def getCostPerPound(self, fruit):
        """
            fruit: Fruit string
        Returns cost of 'fruit', assuming 'fruit'
        is in our inventory or None otherwise
        """
        if fruit not in self.fruitPrices:
            print "Sorry we don't have %s" % (fruit)
            return None
        return self.fruitPrices[fruit]

    def getPriceOfOrder(self, orderList):
        """
            orderList: List of (fruit, numPounds) tuples

        Returns cost of orderList. If any of the fruit are
        """
        totalCost = 0.0
        for fruit, numPounds in orderList:
            costPerPound = self.getCostPerPound(fruit)
            if costPerPound != None:
                totalCost += numPounds * costPerPound
        return totalCost

    def getName(self):
        return self.name
```

El FruitShop clase tiene algunos datos, el nombre de la tienda y los precios por libra de algunas frutas, y proporciona funciones o métodos, en estos datos. ¿Qué ventaja hay que envolver estos datos en una clase?

1. El encapsulado de datos impide que se modifiquen o se utiliza de forma inapropiada,
2. La abstracción que proporcionan los objetos hacen que sea más fácil escribir código de propósito general.

### El uso de objetos

Entonces, ¿cómo hacer que un objeto y lo usamos? Asegúrate de que tienes el FruitShop aplicación en `shop.py`. A continuación, importar el código de este archivo (para hacerla accesible a otros scripts) utilizando `import shop`, ya que `shop.py` es el nombre del archivo. Entonces, podemos crear FruitShop objetos de la siguiente manera:

```
import shop

shopName = 'the Berkeley Bowl'
fruitPrices = {'apples': 1.00, 'oranges': 1.50, 'pears': 1.75}
berkeleyShop = shop.FruitShop(shopName, fruitPrices)
applePrice = berkeleyShop.getCostPerPound('apples')
print applePrice
print('Apples cost $%.2f at %s.' % (applePrice, shopName))

otherName = 'the Stanford Mall'
otherFruitPrices = {'kiwis':6.00, 'apples': 4.50, 'peaches': 8.75}
otherFruitShop = shop.FruitShop(otherName, otherFruitPrices)
otherPrice = otherFruitShop.getCostPerPound('apples')
print otherPrice
print('Apples cost $%.2f at %s.' % (otherPrice, otherName))
print("My, that's expensive!")
```

Este es el código de `shopTest.py`; se puede ejecutar la siguiente manera:

```
[cs188-ta@nova ~]$ python shopTest.py
Welcome to the Berkeley Bowl fruit shop
1.0
Apples cost $1.00 at the Berkeley Bowl.
Welcome to the Stanford Mall fruit shop
4.5
Apples cost $4.50 at the Stanford Mall.
My, that's expensive!
```

Así que lo que acaba de happended? La `import shop` comunicado dijo Python para cargar todas las funciones y clases en `shop.py`. La línea de `berkeleyShop = shop.FruitShop(shopName, fruitPrices)` construye una *instancia* de la FruitShop clase definida en `shop.py`, llamando a la `__init__` función en esa clase. Tenga en cuenta que sólo pasamos dos argumentos, mientras que `__init__` parece tomar tres argumentos: `(self, name, fruitPrices)`. La razón de esto es que todos los métodos de una clase tienen auto como primer argumento. El mismo valor de la `self` variable se establece automáticamente en el objeto en sí; cuando se llama a un método, sólo se suministra el resto de argumentos. El `self` variable contiene todos los datos (`name` y `fruitPrices`) para la instancia específica de corriente (similar a `this` en Java). Las declaraciones de `print` utilizan el operador de sustitución (que se describe en los [documentos de Python](https://docs.python.org/2/library/stdtypes.html#string-formatting) si tienes curiosidad).

### Estática vs variables de instancia

El siguiente ejemplo ilustra cómo utilizar las variables estáticas y de instancia en Python.

Crear el `person_class.py` que contiene el código siguiente:

```
class Person:
    population = 0
    def __init__(self, myAge):
        self.age = myAge
        Person.population += 1
    def get_population(self):
        return Person.population
    def get_age(self):
        return self.age
```

En primer lugar, compilar la secuencia de comandos:

```
[cs188-ta@nova ~]$ python person_class.py
```

Ahora usa la clase de la siguiente manera:

```
>>> import person_class
>>> p1 = person_class.Person(12)
>>> p1.get_population()
1
>>> p2 = person_class.Person(63)
>>> p1.get_population()
2
>>> p2.get_population()
2
>>> p1.get_age()
12
>>> p2.get_age()
63
```

En el código anterior, `age` es una variable de instancia y `population` es una variable estática. `population` es compartida por todas las instancias de la persona de clase mientras que cada instancia tiene su propia `age` variable.

### Más Python Consejos y trucos

Este tutorial ha tratado brevemente algunos aspectos importantes de Python que serán relevantes para el curso. Aquí hay algunas cositas más útiles:

* Utilice `range` para generar una secuencia de números enteros, útil para generar tradicional indexados `for` bucles:
```
for index in range(3):
    print lst[index]
```

* Después de importar un archivo, si edita un archivo de origen, los cambios no se propagan inmediatamente en el intérprete. Para ello, utilice la `reload` comando:
```
>>> reload(shop)
```



### Solución de problemas

Estos son algunos de los problemas (y sus soluciones) que los nuevos aprendices de Python suelen encontrar.

* **Problema:**
ImportError: No module named py

  * **Solución:**
Cuando se utiliza `import`, No incluyen la ".py" del nombre de archivo, por ejemplo, debe decir: `import shop` NO: `import shop.py`

* **Problema:**
NameError: name 'MY VARIABLE' is not defined
Incluso después de la importación es posible que vea esto.

  * **Solución:**
Para acceder a un miembro de un módulo, que tiene que escribir `MODULE NAME.MEMBER NAME`, donde `MODULE NAME` es el nombre de la .py archivo y `MEMBER NAME` es el nombre de la variable (o función) que está intentando acceder .

* **Problema:**
TypeError: 'dict' object is not callable

  * **Solución:**
Diccionario mira hacia arriba se llevan a cabo utilizando corchetes: [ y ]. NO paréntesis: ( y ).

* **Problema:**
ValueError: too many values to unpack

  * **Solución:**
Asegúrese de que el número de variables que asigna en una `for` bucle coincide con el número de elementos en cada elemento de la lista. Del mismo modo para trabajar con tuplas.

Por ejemplo, si `par` es una tupla de dos elementos (por ejemplo, `par = ( 'manzana', 2.0)` ), entonces el siguiente código, causaría el "too many values to unpack":
```
(a, b, c) = par
```

He aquí un caso problemático que implica una `for` bucle:
```
pairList = [('apples', 2.00), ('oranges', 1.50), ('pears', 1.75)]
for fruit, price, color in pairList:
    print '%s fruit costs %f and is the color %s' % (fruit, price, color)
```

* **Problema:**
AttributeError: 'list' object has no attribute 'length' (o algo similar)

  * **Solución:**
Longitud hallazgo de las listas se realiza mediante `len(NOMBRE DE LA LISTA)`.

* **Problema:**
Los cambios en un archivo no están surtiendo efecto.

  * **Solución:**
    1. Asegúrese de que está guardando todos sus archivos después de cualquier cambio.
    2. Si está editando un archivo en una ventana distinta a la que está utilizando para ejecutar pitón, asegúrese de que vuelva a `reload(YOUR_MODULE)` para garantizar los cambios están siendo reflejadas. `reload` funciona de forma parecida a `import`.

### Más Referencias

* El lugar a donde ir para obtener más información Python: www.python.org
* Un buen libro de referencia: [Learning Python](http://oreilly.com/catalog/9780596513986/) (desde el campus de UCB, se puede leer todo el libro en línea)

## Autograding

Para ayudarle a familiarizarse con el autograder, se le pedirá al código, prueba, y presentar soluciones para tres preguntas.

Puede descargar todos los archivos asociados con el tutorial autograder del [curso repositorio de Github](https://github.com/mjalkio/berkeley-cs188-spanish). Es en el directorio de `projects/P0-unix-python-tutorial/tutorial`. Examinar su contenido:

```
[cs188-ta@nova ~]$ cd tutorial
[cs188-ta@nova ~/tutorial]$ ls
addition.py
autograder.py
buyLotsOfFruit.py
grading.py
projectParams.py
shop.py
shopSmart.py
testClasses.py
testParser.py
test_cases
tutorialTestClasses.py
```

Este contiene una serie de archivos que va a editar o ejecutar:

* addition.py : archivo de origen para la pregunta 1
* buyLotsOfFruit.py : archivo de origen para la pregunta 2
* shop.py : archivo de origen para la pregunta 3
* shopSmart.py : archivo de origen para la pregunta 3
* autograder.py : autograding guión (véase más adelante)

y otras personas que pueden pasar por alto:

* test_cases : directorio contiene los casos de prueba para cada pregunta
* grading.py : Código autograder
* testClasses.py : Código autograder
* tutorialTestClasses.py : clases de prueba para este proyecto en particular
* projectParams.py : los parámetros del proyecto

Los comandos `python autograder.py` calificaciones de su solución a los tres problemas. Si corremos antes de modificar cualquier archivo obtenemos una página o dos de salida:

```
[cs188-ta@nova ~/tutorial]$ python autograder.py
Starting on 1-21 at 23:39:51

Question q1
===========
*** FAIL: test_cases/q1/addition1.test
***   anadir(a,b) must return the sum of a and b
***   student result: "0"
***   correct result: "2"
*** FAIL: test_cases/q1/addition2.test
***   anadir(a,b) must return the sum of a and b
***   student result: "0"
***   correct result: "5"
*** FAIL: test_cases/q1/addition3.test
***   anadir(a,b) must return the sum of a and b
***   student result: "0"
***   correct result: "7.9"
*** Tests failed.

### Question q1: 0/1 ###


Question q2
===========
*** FAIL: test_cases/q2/food_price1.test
***   buyLotsOfFruit must compute the correct cost of the order
***   student result: "0.0"
***   correct result: "12.25"
*** FAIL: test_cases/q2/food_price2.test
***   buyLotsOfFruit must compute the correct cost of the order
***   student result: "0.0"
***   correct result: "14.75"
*** FAIL: test_cases/q2/food_price3.test
***   buyLotsOfFruit must compute the correct cost of the order
***   student result: "0.0"
***   correct result: "6.4375"
*** Tests failed.

### Question q2: 0/1 ###


Question q3
===========
Welcome to shop1 fruit shop
Welcome to shop2 fruit shop
*** FAIL: test_cases/q3/select_shop1.test
***   shopSmart(order, shops) must select the cheapest shop
***   student result: "None"
***   correct result: "<FruitShop: shop1>"
Welcome to shop1 fruit shop
Welcome to shop2 fruit shop
*** FAIL: test_cases/q3/select_shop2.test
***   shopSmart(order, shops) must select the cheapest shop
***   student result: "None"
***   correct result: "<FruitShop: shop2>"
Welcome to shop1 fruit shop
Welcome to shop2 fruit shop
Welcome to shop3 fruit shop
*** FAIL: test_cases/q3/select_shop3.test
***   shopSmart(order, shops) must select the cheapest shop
***   student result: "None"
***   correct result: "<FruitShop: shop3>"
*** Tests failed.

### Question q3: 0/1 ###


Finished at 23:39:51

Provisional grades
==================
Question q1: 0/1
Question q2: 0/1
Question q3: 0/1
------------------
Total: 0/3

Your grades are NOT yet registered.  To register your grades, make sure
to follow your instructor's guidelines to receive credit on your project.
```

Para cada una de las tres preguntas, esto muestra los resultados de las pruebas de esta cuestión, el grado de preguntas, y un resumen final al final. Debido a que aún no ha resuelto las preguntas, todas las pruebas fallan. Como a resolver cada pregunta se puede encontrar algunas pruebas pasan, mientras que otros fracasan. Cuando todas las pruebas pasan a una pregunta, se obtiene la máxima puntuación.

En cuanto a los resultados de la pregunta 1, se puede ver que ha fracasado tres pruebas con el mensaje de error "add(a,b) must return the sum of a and b". La respuesta da su código es siempre 0, pero la respuesta correcta es diferente. Vamos a arreglar esto en la siguiente pestaña.

## Pregunta 1: Adición

Abrir `addition.py` y vistazo a la definición de `add`:

```
def add(a, b):
    "Devolver la suma de a y b"
    "*** aqui tu codigo ***"
    return 0
```

Las pruebas llamaron a este con un y b establecer en valores diferentes, pero el código siempre devuelven cero. Modificar esta definición para que diga:

```
def add(a, b):
    "Devolver la suma de a y b"
    print "Aprobada a=%s y b=%s, regresar a+b=%s" % (a, b, a + b)
    return a + b
```

Ahora vuelva a ejecutar el autograder (omitiendo los resultados de las preguntas 2 y 3):

```
[cs188-ta@nova ~/tutorial]$ python autograder.py -q q1
Starting on 1-21 at 23:52:05

Question q1
===========

Paso a=1 y b=1, regresar a+b=2
*** PASS: test_cases/q1/addition1.test
***   add(a,b) returns the sum of a and b
Paso a=2 y b=3, regresar a+b=5
*** PASS: test_cases/q1/addition2.test
***   add(a,b) returns the sum of a and b
Paso a=10 y b=-2.1, regresar a+b=7.9
*** PASS: test_cases/q1/addition3.test
***   add(a,b) returns the sum of a and b

### Question q1: 1/1 ###

Finished at 23:41:01

Provisional grades
==================
Question q1: 1/1
Question q2: 0/1
Question q3: 0/1
------------------
Total: 1/3
```

Ahora pasa todas las pruebas, consiguiendo la máxima puntuación en la pregunta 1. Aviso de las nuevas líneas `Paso a = ...`, que aparecen antes `*** PASS: ...`. Estos son producidos por la sentencia de impresión en `add`. Puede utilizar declaraciones de impresión como que la información de salida útil para la depuración. También puede ejecutar el autograder con la opción `--mute` ocultar temporalmente dichas líneas, de la siguiente manera:

```
[cs188-ta@nova ~/tutorial]$ python autograder.py -q q1 --mute
Starting on 1-22 at 14:15:33

Question q1
===========
*** PASS: test_cases/q1/addition1.test
***   add(a,b) returns the sum of a and b
*** PASS: test_cases/q1/addition2.test
***   add(a,b) returns the sum of a and b
*** PASS: test_cases/q1/addition3.test
***   add(a,b) returns the sum of a and b

### Question q1: 1/1 ###
```

Pregunta 2: Función buyLotsOfFruit

Añadir un buyLotsOfFruit (OrderList) función para buyLotsOfFruit.py que tiene una lista de (frutas, libra) tuplas y devuelve el coste de su lista. Si hay algo de fruta en la lista que no aparece en fruitPrices debe imprimir un mensaje de error y volver Ninguno . Por favor, no cambie el fruitPrices variable.

Ejecutar pitón autograder.py que llegue la pregunta 2 pasa todas las pruebas y se obtiene la máxima puntuación. Cada prueba confirmará que buyLotsOfFruit (OrderList) devuelve la respuesta correcta dada varias entradas posibles. Por ejemplo, test_cases / Q2 / food_price1.test prueba si:

Costo de [( 'manzanas', 2,0), ( 'peras', 3,0), ( 'limas', 4,0)] es 12.25
Pregunta 3: Función ShopSmart

Rellenar la función ShopSmart (pedidos, tiendas) en shopSmart.py , que toma un OrderList (como el tipo aprobado para FruitShop.getPriceOfOrder ) y una lista de Fruitshop y devuelve el Fruitshop en su pedido le cuesta a la menor cantidad en total. No cambie el nombre del archivo o nombres de variables, por favor. Tenga en cuenta que vamos a ofrecer la shop.py aplicación como un archivo de "apoyo", por lo que no necesita dejar su opinión.

Ejecutar pitón autograder.py que llegue la pregunta 3 pasa todas las pruebas y se obtiene la máxima puntuación. Cada prueba confirmará que ShopSmart (pedidos, tiendas) devuelve la respuesta correcta dada varias entradas posibles. Por ejemplo, con las siguientes definiciones de las variables:

Orders1 = [( 'manzanas', 1,0), ( 'naranjas', 3,0)]
Orders2 = [( 'manzanas', 3,0)]
dir1 = { 'manzanas': 2,0 ', naranjas': 1.0}
shop1 = shop.FruitShop ( 'shop1', dir1)
directorio2 = { 'manzanas': 1,0, 'naranjas': 5,0}
shop2 = shop.FruitShop ( 'shop2', directorio2)
tiendas = [shop1, shop2]
test_cases / Q3 / select_shop1.test prueba si:

shopSmart.shopSmart (solicitudes1, tiendas) == shop1

y test_cases / Q3 / select_shop2.test prueba si:

shopSmart.shopSmart (Orders2, tiendas) == shop2

Sumisión

No hemos terminado todavía! Siga las indicaciones de su instructor para recibir crédito en su proyecto!