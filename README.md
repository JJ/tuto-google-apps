Tutorial de Google App Script
=============================


## Empecemos por el principio

[Software as a Service o SaaS](http://es.wikipedia.org/wiki/Software_como_servicio)
es un modelo de uso de software en el cual parte, o toda, la lógica de
la aplicación está en la web. Podemos denominar SaaS tanto a las
apliaciones ricas de Internet (con un interfaz como el de cualquiera
aplicación de escritorio) como a aplicaciones *clásicas* basadas en
formularios, pero en propiedad se corresponde más a las primeras.

Las aplicaciones en modo SaaS están sustituyendo hoy en día a la
mayoría de las aplicaciones de escritorio e, igual que en estas el
modelo habitual (en aplicaciones privativas) es de pago por licencia,
en el modelo SaaS se suele pagar por su implantación y,
posteriormente, por uso en diferentes modalidades, tarifa plana o por
intensidad de uso.

Muchas aplicaciones, además, son un *marco* sobre el cual se pueden
desarrollar funcionalidades adicionalees. A modo de sistema operativo,
ofrecen una serie de servicios a los que se puede acceder a modo de
*plugins* o *addons*. Los lenguajes usados para esto son generalmente
Javascript u otros lenguajes *empotrados* como Lua, aunque algunos
servicios pueden tener lenguajes propios o simplemente no permitir
nuevas funcionalidades.

Las que lo permiten, como Google Drive, se convierten en plataformas
donde se pueden desarrollar verdaderas aplicaciones.

> Discutir diferentes SaaS de uso habitual y sus ventajas e
> inconvenientes frente a aplicaciones de escritorio.

## Intro a Google Drive

[Google Drive](http://drive.google.com) es una suite ofimática y de
aplicaciones de Google que incluye las aplicaciones ofimáticas
básicas, más una serie de aplicaciones conectables como GeoGebra,
MindMeister e incluso un corregidor de ortografía, estilo y
gramática. Muchas de ellas son gratuitas, pero en realidad se trata de
una nueva plataforma de distribución y de creación de software en la
nube.

Como se ha visto anteriormente, a un nivel muy básico una aplicación
en la nube es simplemente un formulario. Los formularios de Google
Drive están conectados a una hoja de cálculo y automáticamente crean
gráficos con las respuestas.

Dentro de la hoja de cálculo donde se depositan las respuestas, se
pueden crear tablas dinámicas. Estas tablas dinámicas son fáciles de
crear y, en muchos casos, permiten realizar informes de forma
dinámica.

> Crear un formulario que permita, por ejemplo, introducir respuestas
> a una encuesta. Examinar la hoja de respuestas y crear un informe de
> tabla dinámica (Datos->Informe de Tabla dinámica)

Una de las aplicaciones más desconocidas y más útiles son las Tablas
Dinámicas de Google (o *Fusion Tables*). Se puede usar como punto de
partida una hoja de cálculo qeu tengamos almacenada, pero tiene
también una serie de demos que muestran lo que es capaz de
hacer. Aparte de presentar la información de la hoja de diferentes
formas, es capaz de situarla sobre un mapa y de crear todo tipo de
visualizaciones sobre la misma.

Lo interesante de todas estas aplicaciones es que van a ser accesibles
desde los *scripts* y por tanto podremos trabajar con ellas
dinámicamente o acceder a unas desde otras, usando todas sus funciones
como si de una librería se tratara. Lo veremos a continuación, después de ver un par de cosas, la primera de las cuales es

## El modelo de objetos

Un sistema operativo incluye una serie de llamada que permite a los
programas que se ejecutan sobre él acceder a las funciones del
sistema: abrir y cerrar ficheros, reservar memoria y todas las
operaciones de mayor o menor nivel.

Los entornos de operación modernos incluyen una gama de posibiliades
mucho mayor que el simple sistema operativo; también cambian de
paradigma del procedural al orientado a objetos; en general, los
sistemas operativos u entornos gráficos modernos incluyen un modelo de
objetos (OM) al que se puede acceder desde el lenguaje preferido y,
por supuesto, desde cualquier otra aplicación a la que se exponga el
interfaz de programación (API). El navegador tiene un
[DOM](http://es.wikipedia.org/wiki/Document_Object_Model), un modelo
de objetos para documentos, que incluye una serie de objetos ya
instanciados como `document` o `window`.

Generalmente, un SaaS extensible como las Google Apps tienen una serie
de objetos que permiten usar los llamados
[servicios](https://developers.google.com/apps-script/guides/services/)
de Google Apps. Todas las aplicaciones básicas y avanzadas tienen uno,
y a veces varios objetos, y estos servicios se suelen llamar
`AlgoApp`. Por ejemplo, Google Drive tiene
[`DriveApp`](https://developers.google.com/apps-script/reference/drive/)
y las hojas de cálculo la
[`SpreadsheetApp`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app). Todos
estos objetos están instanciados y accesibles a todos los scripts que
vayamos a usar. Pero antes, tendremos que aprender sobre los

## Métodos de autenticación

Cuando se trabaja en la nube se está trabajando con un interfaz de
aplicación, un API, igual que en el sistema operativo; en éste hay una
jerarquía de privilegios que te permiten activar, o no, diferentes
funciones y esos privilegios afectan por un lado a los usuarios y por
otro lado a los programas. Un usuario *autoriza* a un programa a
ejecutarse y acceder a sus recursos (sistema de ficheros, la red)
simplemente ejecutándolo. El permiso es implícito.

Sin embargo, en la nube el entorno es un poco más complicado. Primero,
porque muchos programas se ejecutan también desde la misma nube y el
considerar que hay una autorización implícita puede ser un poco
peligroso. Segundo, porque los recursos están compartimentalizados y
se puede decidir de forma granular a qué recursos se tiene acceso.

Por eso generalmente se usa, igual que en el móvil cuando se instala
una aplicación, un proceso de autorización explícita; en casi todos
los casos se usa un sistema llamado
[OAuth2](https://developer.github.com/v3/oauth_authorizations/#create-a-new-authorization). En
la práctica, eso significa que hay dos conjuntos de claves

* Una clave y un *secreto* por aplicación.
* Una clave y un *secreto* por usuario que autorice.

Por eso se suele hacer un sistema de autorización en dos pasos: en un
primer paso se descargan (generalmente del portal del desarrollador)
la clave y el secreto y, cada vez que se accede a un nuevo usuario,
este tiene que autorizarlo explícitamente, con lo que le *concede* a
la aplicación la segunda clave y secreto.

Dependiendo del sistema que usemos, esto habrá que hacerlo y
almacenarlo por parte de nuestro programa. En el caso de Google App,
simplemente veremos que, cuando un usuario ejecuta por primera vez un
*script*, tiene que autorizarlo. Lo que haremos justamente a
continuación, cuando ejecutemos

## Nuestro primer programa en la nube

[Google Script](https://script.google.com/) es a la vez un entorno de
programación que nos permite crear y ejecutar nuestro programa. Vamos
a por el primero, el clásico hola mundo. Si creamos un script en
blanco, nos saldrá algo así; el entorno completa los nombres de las
funciones para aquellas que estén declaras:

![Captura de pantalla del IDE](logger.png)

El primer programa se reduce a lo siguiente:

```javascript
function myFunction() {
  Logger.log("¡Ola k ase!");
}
```

Como podéis ver, es una función que se tiene que llamar precisamente
así, `myFunction` y que no recibe ningún parámetro. Es Javascript, que
es el lenguaje de *macros* de este entorno. Esta función será el
equivalente al `main` de otros lenguajes: es la función que se llama
al arrancar el script; puedes cambiarle el nombre, pero hasta que no
guardes no podrás ejecutarla.

Y contiene una sola orden,
`Logger.log("¡Ola k
ase!");`. [`Logger` es uno de los objetos estándar de GAS](https://developers.google.com/apps-script/reference/base/logger),
disponible para todos y cada uno de los scripts que usemos y es un
registro de las acciones de cada programa. No nos queda más remedio
que usar esto para salida, al menos para empezar. Los *scripts* en GAS
no tienen salida estándar y por tanto no pueden simplemente usar el
`writeln` de JS o el `console.log` (sinceramente, esto no lo he
probado). `log` añade una línea a ese registro, simplemente.

Se puede ejecutar directamente con la flechita que aparece al lado del
bicho (que es, lo pillasteis, para depurar o desenbichar). Te pedirá
que le asignes un nombre y luego se olvidará de que querías
ejecutarlo, así que luego lo ejecutas.

Y no pasa nada. Le das de nuevo a ejecutar. Sigue sin pasar nada. ¿Qué
ocurre? Nada. No, es broma. Ocurre que, efectivamente, donde pasa algo
es en el registro, al que se accede dando a Control-Enter o al menú
Ver -> Registros. Saldrá algo así:

![Registro de resultados](registro.png)

> Escribir un script que escriba en el registro una tabla de
> multiplicar de un número determinado.

Desde los scripts tenemos también acceso a la librería estándar de
Javascript. Por ejemplo, a `JSON`, la librería para procesar las
estructuras de datos de JS y transformarlas a cadenas y viceversa.

```javascript
  var foo = [1,2,3, {clave: "Valor"}];
  Logger.log(JSON.stringify(foo));
``` 

La segunda línea convierte a una cadena la estructura de datos
compleja `foo`, lo que puede ser útil a la hora de depurar una
aplicación *a la antigua*, imprimiendo variables aparte de "Estoy por
aquí", "No debería estar aquí", y todo eso.

Valga lo anterior como prueba de que la clase JSON está incluida en la
librería estándar, aunque en realidad `Logger.log(foo)` haría
exactamente lo mismo (con un resultado ligeramente diferente). No
[todas las clases (objetos globales) de JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
están presentes en el GAS, pero sí los principales. 

##Vamos a hacer algo

El script anterior no hace nada, pero es un ejemplo de un tipo de
script denominado
[*standalone*](https://developers.google.com/apps-script/guides/standalone),
útil principalmente para usar el sistema como plataforma de
cómputo. Pero, como se ha visto antes, estos scripts son los
equivalentes a los de `bash` o de cualquier intérprete de
comandos. Nos permiten acceder a lo que tenemos en el sistema. Por
ejemplo, a los ficheros que tengamos en Google Drive, como vamos a
hacer a continuación.









