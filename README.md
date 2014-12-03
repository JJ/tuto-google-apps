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
vayamos a usar.






