# myvueplayground

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### CUADERNO DE CONCEPTOS
Object.freeze(NOMBRE_OBJETO) => interrumpe la reactividad del DOM, por imposibilitar cambios en el _obj argumento
en html tienes la directiva v-once="", que sólo ejecutará una sola vez

ALGUNAS PROPIEDADES DE INSTANCIA POR DEFECTO PUEDEN SER APROVECHADAS => 
vm.$el === document.getElementById('ID-ELEMENTO')
LAS PROPIEDADES DE INSTANCIA POR DEFECTO SE ANTECEDEN CON $
vm.$watch('a', function (newValue, oldValue) {
  // ESTA FUNCIÓN SE INVOCA CUANDO `vm.a` CAMBIA
})

var vm = new Vue ({
    el: `ID-ELEMENTO`,
    data: {
        a: `ejemplo`
})

https://vuejs.org/v2/api/#Instance-Properties => LA API DE VUE

CONCEPTO GANCHOS EN EL CICLO DE VIDA => Las instancias recorren un camino por partes: necesita instaurar el rastreo de datos, compilar la plantilla, llevar la propia instancia al DOM y observar cambios para la actualización del mismo DOM (la interactividad que maneja el usuario). Las diferentes funciones con las que 'gobernaremos' el proceso son las denominadas 'LIFECYCLE HOOKS', como las que entran en el grupo del objeto app, 'created':

created: function () {
    // `this` => CUANDO USAMOS 'THIS' ESTAMOS HACIENDO A LA REFERENCIA vm previa ) var vm = new Vue ({... ( 
    console.log(`a es: ` + this.a) => ("a es: ejemplo")
}

Otros 'GANCHOS' importantes son 'mounted', 'updated' y 'destroyed'. Todos los LIFECYCLE HOOKS utilizan este 'autoreferimiento' con "this" => ESTO NOS PRESENTA EL TERRIBLE PROBLEMÓN DE QUE, POR AHORA, NO SE PUEDEN USAR FUNCIONES FLECHA EN LAS INSTANCIAS

###########################################

CONCEPTO RAWHTML y directiva v-html=""

<p> {{ rawHtml }}</p> reactivo
<p> <span v-html="rawHtml"></span></p> CON ESTO LIMITAS EL RE-RENDER, NO ES ACONSEJABLE

###########################################

EXPRESIONES JAVASCRIPT Y DIRECTIVAS (STANDARD Y CON ARGUMENTOS)
{{id + 1}} {{nombre.toUpperCase()}} {{Math.random()}} {{Date.get..}}
OH DIOS MÍO: TERNARIAS SÍ!!!! => {{ QUÉ TE PARECE ? 'bien' : 'mal' }}

NUNCA VIENE MAL PONERLO AUNQUE SE SEPA: v-bind:class="PROPIEDAD_vm" | :class="..." para bindear características dentro de los elementos <html>
UN USO INTERESANTE DE LA DIRECTIVA V-BIND => v-bind:checked="PROPIEDAD_vm"
ESTA PROPIEDAD HA DE DEVOLVER UN TRUE PARA SER ACTIVADA, FALSE, NULL O UNDEFINED NO APLICARÁN ESTE ESTADO AL ELEMENTO

PERO ESTE TIPO DE TRATAMIENTO NO FUNCIONA
{{ if (CONDICION) { return 'NO FUNCIONARÁ' } }}

TENEMOS EL YA SÚPER FAMOSO v-if="" · TODAS LAS DIRECTIVAS VUE PARA LOS <template> USAN EL PREFIJO v-
LAS QUE HE USADO SON v-if v-for v-bind v-on v-model. HE VISTO EN DOCU v-cloak v-once v-html
EL CASO DE V-BIND ES DISTINTO: v-for="" v-bind: ESTO SE DEBE A QUE LAS DE V-BIND TOMAN UN "ARGUMENTO", QUE SE UTILIZARÁ PARA EL TRATAMIENTO DE LAS FUNCIONES. MEJOR EXPLICADO: V-ON:change ES UN 'EVENT LISTENER' (OYENTE DE EVENTO), LO QUE SUPONE QUE TENDRÁ FUNCIONES EFECTUANDO PROCESOS QUE REQUIEREN ESE ARGUMENTO.

###########################################

ATOMIZANDO AÚN MÁS: DIRECTIVAS DINÁMICAS DE ARGUMENTOS
<a v-bind:[NOMBRE_ATRIBUTO_EN_vm]="url"> ... </a> => SEGÚN EL TRATAMIENTO DE LA LÓGICA QUE HAGAMOS, PODEMOS UTILIZAR ESTO PARA TENER UN method : nombre_atributo_referido, que a su vez tome información de la instancia vm utilizando this. lo que significa mayor procedurización <html> - ATRIBUTO DINAMIZADO - CONTENIDO ATR DINAMIZADO
CUANDO NOMBRE_ATRIBUTO_EN_vm = "href", SERÁ COMO HABER PUESTO v-bind:href="".
<a v-on:[NOMBRE,,]="manifiéstate"> ... </a> => CUANDO NOMBRE,, SEA = "focus", === v-bind:focus
CUANDO LOS VALORES DE ESTOS ARGUMENTOS nombre_atribut... SEA NULL SE ELIMINARÁ EL BINDEO. OTROS TIPOS DE DATOS DEVOLVERÁN UNA ALERTA O ADVERTENCIA DE ERROR
<a v-bind:['algo' + ARGUMENTO ]="val"> ... </a> WRONG
<a v-bind:[unAtributoHtml]="val"> ... </a> OH YEAH!

MODIFICADORES
SON SUFIJOS ESPECIALES QUE SE UTILIZAN EN LAS DIRECTIVAS DE CAMBIO PARA AFECTARLAS DE MANERA SUSTANCIAL. ESTE EJEMPLO TRATA UNA UTILIDAD MUY TÍPICA, LA DEL event.preventDefault() =>
<form v-on:submit.prevent="NOMBRE_FUNCIÓN_vm"> ... </form> PERFECTA PARA BOTONES LIKE O PSEUDO ACTUALIZADORES DE PÁGINA

SINTAXIS
BÁSICA <a v-bind:href="url"> ... </a>           ||      <a v-on:click="doSomething"> ... </a>  
ACORTADA <a :href="url"> ... </a>               ||      <a @click="doSomething"> ... </a>
ACORTADA DINÁMIDA <a :[NOMBRE_KEY]="url"> ... </a>     ||      <a @[EVENTO]="doSomething"> ... </a>

###########################################

