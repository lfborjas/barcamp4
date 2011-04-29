!SLIDE 

#Javascript: el lenguaje más incomprendido del mundo

!SLIDE bullets

* No tiene *nada* que ver con java
* Es un lenguaje de programación dinámico orientado a objetos
  (lo hace mejor que java)

!SLIDE

#Variables y valores

!SLIDE code

    @@@javascript
    var a = 1, //Number
        b = 2.0e10, //Number
        c = false, //Boolean
        d = 'hola', //String
        e = "mundo" //String
        f = new Date(),//Date
        g = /[a-z]+/ //RegExp
        h, //undefined (nulidad implícita)
        i = null //nulidad explícita

!SLIDE bullets

* No hay tipos explícitos
* Si necesitás una variable: `var`
* Omitir `var` la hace ¡*global*!
* Punto y coma es *opcional*

!SLIDE 

#PUNTO Y COMA ES OPCIONAL

!SLIDE center

![crap](fuuu.jpg)

!SLIDE bullets

* Sólo se necesita para:
* Cuando tenés varias sentencias en una línea
* Cuando una línea se podría interpretar como 
  la continuación de la anterior
* Cuando querés un bloque vacío 

!SLIDE code

    @@@javascript
    a = b + c
    (d + e).toString()
    x = [1,2,3]
    [4,5,6].concat([7,8,9])

!SLIDE code

    @@@javascript
    a = b + c(d+e).toString()
    x = [1,2,3][4,5,6].concat([7,8,9])

!SLIDE code

    @@@javascript
    a = b + c;
    (d + e).toString()
    x = [1,2,3];
    [4,5,6].concat([7,8,9])

!SLIDE 

##Lógica

!SLIDE code
    
    @@@javascript
    x = 0 || ""  || 666
    //x es 666
    y = 0 && 1/0 || "uff"
    Boolean(y) // true


!SLIDE bullets

* Todo lo que no sea 0 o "" es *verdadero*
* Las expresiones booleanas devuelven un *valor* (**no** true o false)
* Para ver el valor de verdad de algo: `Boolean(algo)`

!SLIDE 

#Estructuras de control

!SLIDE code small
    
    @@@javascript
    var arr = "hola mundo adiós hola".split(" "),
        saludos = 0

    for(var i=0; i<arr.length; i++)
        switch(arr[i]){
            case "hola":
                saludos++
        }
    
    if(saludos > 1)
        console.log("¡Me saludaron!")

     while(saludos){
        console.log("Y también hay do...while")
        saludos--
     }

!SLIDE

#Arreglos

!SLIDE code
    
    @@@javascript
    var a = [1,2,3,4],
        b = [1, true, 2, 3, ""]
    a.concat(b)
    b.slice(1,3).join() #"true,2"
    "esto es un string".split(" ").sort()[2]
    #[ 'es', 'esto', 'string', 'un' ]
    #esto

!SLIDE bullets
    
* Pueden ser heterogéneos
* Son más *listas* que arreglos

!SLIDE code
    
    @@@javascript
    var a = [1,2,3]
    a.pop() //3, [1,2]
    a.push(4) //[1,2,4]
    a.shift() //[2,4]

!SLIDE 

#Objetos

!SLIDE code

    @@@javascript
    var a = {foo: 1, bar: 2, 'baz': 6}
    a.foo
    a['bar']
    typeof a
    a.otro = 3
    a['otro']
    for(var p in a)
        a[p] = p
    a

!SLIDE bullets

* *Todo* es un objeto
* Las llaves pueden ser identificadores o strings
* Los objetos son *flexibles*
* La notación de objetos es *sucinta*


!SLIDE 

#Funciones

!SLIDE code
    
    @@@javascript
    function suma(a,b){
        return a+b
    }
    suma(1,2)
    var resta = function(x,y){
        return x-y
    }
    resta(2,1)

!SLIDE code

    @@@javascript
    function meVale(a,b){
        x = a || b || "no me mandaste nada :("
        return x;
    }

    meVale(1,2)
    meVale(1)
    meVale(null, 2)
    meVale()

!SLIDE code

    @@@javascript
    function sum(){
        console.log(arguments.callee.name)
        console.log(typeof arguments)
        var res = 0;
        for(var i = 0; i < arguments.length; i++)
            res += arguments[i]
        return res
    }
    sum(1,2,3,4)


!SLIDE code small
    
    @@@javascript
    typeof(function(){})
    var x = {
        metodo: function(y){return y*y}
    }
    x.metodo(2)
    x.otro = function(n){
        return n*n*n;
    }
    x.otro(3)
    x.otro.apply(null, [3])
    x.otro.name #es anónima!
    x.conNombre = function hola(){}
    x['conNombre'].name

!SLIDE bullets

* Como las funciones *son objetos también*, podés:
* ¡Mandarlas de parámetros o devolverlas desde otras funciones!
* `Array` tiene algunas [operaciones de iteración interesantes]()

!SLIDE code
    
    @@@javascript
    var squares = [1,2,3,4].map(function(n){
        return n*n;
    })
    var odds = [4,3,2,1].filter(function(n){
        return n%2
    })

!SLIDE code

    @@@javascript
    function negate(f){
        return function(){
            return !f.apply(null, arguments)
        }
    }
    function verdad(){
        return true;
    }
    mentira = negate(verdad)
    mentira()

!SLIDE

#Programación orienta a objetos

!SLIDE code smaller

    @@@javascript
    var Response = function(body, status, headers){
        this.body = typeof body == 'object' ? 
                    JSON.stringify(body):
                    body
        this.status = status || 200
        this.headers = headers || {'Content-Type': "text/plain"}
        this.to_a = function(){
            return [this.body, this.status, this.headers]
        }
    }
    var r = new Response({hola: "mundo"})
    r.to_a()

!SLIDE bullets

* Cuando llamás una función con `new`, todo lo que esté en `this`
  se pondrá dentro de un nuevo objeto
* Todos los objetos tienen un *prototipo*
* El prototipo también es flexible

!SLIDE code

    @@@javascript
    Response.prototype.getBody = function(){
        return this.body
    }
    r.getBody()


!SLIDE code

    @@@javascript
    Object.prototype.merge = function(other){
        for(var prop in other){
            //por el prototipo
            if(other.hasOwnProperty(prop))
                this[prop] = other[prop]
        }
    }   

!SLIDE bullets

##Referencias

* <http://www.delicious.com/lfborjas/barcamp4+javascript>
* [Node.js](http://nodejs.org/)


!SLIDE bullets 

##Ejemplos en js:

* [Un reversi](http://lfborjas.com/experiments/reversi/board.html)
* [Un intérprete del lenguaje scheme](https://github.com/lfborjas/minimalisp/tree/javascript)
* [Una aplicación en node.js](https://github.com/lfborjas/eddie/tree/javascript)
* [Un juego basado en texto](http://lfborjas.com/progra2/dwemthy.html)
