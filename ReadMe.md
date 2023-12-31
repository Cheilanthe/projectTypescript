# Apuntes sobre Curso de Fundamentos de TypeScript

## Crear un archivo TSConfig.json

En la terminar se ejecuta: 
```
  npx tsc --init
  Created a new tsconfig.json with:                                          
                                                                        TS 
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true
```

Esto crea un archivo con propiedades comentadas las cuales podemos activar. El código de Typescript se compila con las preferencias que nosotros realicemos en el archivo _TSConfig.json_

    npx tsc // Ejecula la compilación
    
    npx tsc --watch //detecta los cambios en los archivos ts y realiza la compilación en automatico. 

### Preferencias recomendadas
* outDir: indicando la carpeta dist como el directorio destino de los archivos transpilados.
* rootDir: indicamos que nuestros archivos TypeScript, los cuales serán “compilados” luego, estarán en la carpeta src.

Se pueda habilitar el análisis de código de TypeScript en un archivo JavaScript con 
```
@ts-check
```

## Tipado 
JS < ESNext < Typescript

Js no tiene un sistema de tipado fuerte. P. eje. renombrar una variable.
En Typescript podemos tener tipado fuerte con flexibilidad. 

### verbose: declaración de variables en TS
Declaraión de la variable | tipado (typer anootation)| valor
```
          const product   :            numbre        =  12  
```
Se pueden inferir los tipos o mandar de forma explicita. 
 * Tipos inferidos - los detecta automaticamente.
Para ver ejemplos revisar el archivo _03-typing.js_
si nombramos dos archivos con el mismo cógido habrá errores. Usualmente en producción estos problemas no se presentan ya que el scope esta bien definido. 
NOTA: ¿Qué es una función anónima autoejecutable? 
```
      (()=>{
          // permite establecer el scope de la variables
      })(); 
```
 * Valores Booleanos
 Los valores booleanos se declaran con tipado en minusculas 
    const myBooolean : boolean = true;
 Los valores se pueden reasignar y evaluar siempre y cuando sean de tipo booleano: 
      let isNew : boolean = false;
      isNew = random>= 0.5 ? true : false;

 * String 
 Se comportan de forma muy similar a JS vanilla, también se puede hacer uso de template strings.

 * Arrays 
 Por defecto hay que indicar qué tipos de datos pueden almacenar ya que por defecto se restringen a los datos con los que se inicializan. Por ejemplo, si se inicializa con solo numeros no podrán integrarse al array otro tipo de datos. 

 * Any 
 Permite que una variable pueda almacenar cualquier tipo de dato. No se suele recomedar su uso. Permite migrar gradualmente de JS a TS, o que no este bien tipada. No se recomienda usar en proyectos altamente desarrollados. 
 Se puede usar _Cast_ para pasar de un tipo de dato a otro.Le decimos a TypeScript que confíe en nuestro tipado. Que trate a esa variable como ese tipo de dato que le especificamos:
 ```
    (variableName as dataType)
    (<dataType>variableName)
 ```
* Union Types
 Permite realizar tipados estrictos pero dinámicos. podemos hacer que las funciones puedan recibir datos de tipos especificos dentro del scope de esta función podemos asignarles un comportamiento.

* Alias y tipos de datos
Permiten darle un nombre a no o varios tipos de datos en conjunto, también se pueden aplicar tipos de datos especificos, o con combinaciones determinadas. 
Se pueden combinar para hacer variables seguras y flexibles: 

Alias: le da un nombre a varios tipos de datos
```
    type UserID = string | boolean | number;
```
Se pueden usar los 3 tipos de datos. 

Union Types: se puede poner un tipo de dato y luego llamar ese tipo en una variable para que adquiera los tipos de datos del type: 
```
    type UserID = string | boolean | number;
    let dynamicVar: UserID = "300";
```
* Null y Undefined
Nos permiten que una variable o función trabaje con datos null o undefined. Cuando queremos hacer funciones con argumentos opcionales en una función, estas deben ubicarse al final, si no TypeScript nos indicará un **error, ya que podría haber confusiones al momento de invocar la función y enviar los respectivos parámetros:
```
  function randomFunc(title: string, amount?: number){} //CORRECTO

  function otherFunc(title?: string, amount: number){} // ERROR

```
* Void 
Podemos hacer funciones que reciban parametros de un tipo en especifico: 
```
const printTotal = (prices: number [])=>{
 //
 }
```
También podemos especificar el tipo de dato que debe retornar: 
```

const calcTotal = (prices: number []): number =>  { //
}
```

También se especifica que una función no tiene el retorno de un dato (recuerda que si no hay return, el resultado puede ser undefined): 

```
const calcTotal = (prices: number []): void =>  { //
}
```
  * Enviando Objetos como parametros de las funciones
  Con el tipado podemos darle seguridad a 
  - Los tipos de datos de las variables que se pueden almacenar.En una variable se puede tipar un objeto con una estructura determinada.
  - Utilizar dicho objeto como parametro de una función, o como valor de retorno de dicha función. 
  Revisar _15-objs.ts_.  

Teniendo en cuenta esta instrucción `const rta = 1 + '1';` ¿Cuál sería el tipo de dato que infiere TS de rta?
Cuando hay librerías que no tiene  soporte a tipos se puede agregar el soporte a tipos usando el comando 

```
  npm i @types/lodash --save-dev

```

