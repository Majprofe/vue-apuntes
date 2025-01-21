# vue-apuntes

## ¿Qué es Vue?

Vue es un framework JavaScript creado por Evan You en 2014, combinando lo mejor de Angular y React mientras elimina complejidades innecesarias. Destaca por ser fácil de aprender, con una curva de aprendizaje reducida y una documentación excepcional. Incluso tras la introducción de los hooks en React, Vue respondió con Vue3 en septiembre de 2020, mejorando la gestión de la reactividad de los componentes.

**Características principales**
**Reactividad:** Vue.js utiliza una estructura de datos reactiva que permite una actualización automática de la interfaz cuando los datos cambian.

**Componentes:** La arquitectura de Vue se basa en componentes, lo que facilita la modularidad y reutilización del código.

**Directivas:** Vue ofrece directivas como v-bind y v-if para manipular el DOM de manera declarativa.

Existen dos tipos de APIs en Vue:
- **Option API**
- **Composition API** (introducida a partir de Vue 3)

## Crear un nuevo proyecto
Para utilizar Vue sólo necesitamos enlazarlo en nuestra página desde cualquier CDN como:

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

Pero lo ideal es iniciar un proyecto, lo podemos hacer de dos maneras:

### 1. Vue CLI (Webpack)

```bash
npm install -g @vue/cli
vue create nombre-proyecto
cd nombre-proyecto
npm run serve
```

### 2. Vue@latest (Vite)

```bash
npm init vue@latest nombre-proyecto
cd nombre-proyecto
npm install
npm run dev
```

Es importante tener Node.js instalado en tu ordenador antes de comenzar. Puedes verificar su instalación con `node -v` en la consola.

Al crear el proyecto, se te pedirá configurar diferentes aspectos, como:
- Nombre del proyecto
- TypeScript
- Soporte JSX
- Vue Router
- Pinia
- Testing
- ESLint

En el archivo `main.js`, se importa el componente `App`, que es el punto de entrada para el renderizado. Puedes eliminar el archivo `main.css` si no necesitas esa hoja de estilos.

## Componentes

Borraremos el contenido de App.vue para empezar a crear nuestro componente y todos los componentes que vienen preinstalados.

Un componente tiene que tener como mínimo la siguiente sección:
```html
<template>
  <h1>Hola Mundo</h1>
</template>
```
Donde escribiré el código HTML de mi componente

También tenemos la parte CSS y Javascript:
```html
<style scoped>
  h1 {
    color: red;
  }
</style>

<script setup>
</script>
```
Puedes organizar esas secciones en el orden que prefieras.

## Utilizar variables y directivas

Dentro de las dobles llaves {{}}, podemos incluir expresiones evaluadas por el navegador. Por ejemplo:
```vue
<script setup>
  const miNombre = 'Manuel'
  const miEdad = 18
</script>

<template>
  <h1>Hola, soy {{miNombre}} y tengo {{ miEdad + 1 }}</h1>
</template>
```

Además, podemos utilizar variables en atributos HTML:
```vue
<script setup>
  const miNombre = 'Manuel'
  const miEdad = 18
  const miColor = 'color: green; font-size: 3em'
</script>

<template>
  <h1 v-bind:style="miColor">
    Hola, soy {{miNombre}} y tengo {{ miEdad + 1 }}
  </h1>
</template>
```
Podemos sustituir v-bind: por : directamente, en el siguiente ejemplo vamos a aplicar clases dinámicamente:
```vue
<script setup>
  const miNombre = 'Manuel'
  const miEdad = 18
  const selector = 'azul'
</script>

<template>
  <h1 :class="selector">
    Hola, soy {{miNombre}} y tengo {{ miEdad + 1 }}
  </h1>
</template>

<style scoped>
.azul {
  color: blue;
}
</style>
```
## Eventos

Para declarar eventos lo haremos directamente sobre la etiqueta html que va a recibir el evento:
```vue
  <button v-on:click="saludar(mensaje)">Aceptar</button>
```
Lo realizaremos mediante la directiva v-on:click, que podemos sustituir por @click
Ejemplo:
```vue
<script setup>
  const miNombre = 'Manuel'
  const miEdad = 18
  const selector='azul'
  const saludar = (nombre) => {
    console.log(`Hola ${nombre}`)
  }
</script>

<template>
  <h1 :class="selector">
    Hola, soy {{miNombre}} y tengo {{ miEdad+1 }}
  </h1>
  <button @click="saludar(miNombre)">Aceptar</button>
</template>
```
## Reactividad
Las variables reactivas son aquellas que se modifican en tiempo real, para poder crearlas tenemos que hacer uso de ref en Vue3.

```vue
<template>
  <button @click="decremento">-</button>
  <span>{{ contador }}</span>
  <button @click="incremento">+</button>
</template>
  
<script setup>
  import { ref } from 'vue'
  const contador = ref(0)
  const decremento = () => {
    contador.value--
  }
  const incremento = () => {
    contador.value++
  }
</script>
```
Si lo que queremos declarar son objetos o arrays reactivos lo haremos con reactive en vez de ref.

Para aplicar un color condicional según el valor de contador, siendo rojo<0, verde > 5 y azul entre 0 y 5:
```vue
<template>
  <button @click="decremento">-</button>
  <span :class="miColor">{{ contador }}</span>
  <button @click="incremento">+</button>
</template>
  
<script setup>
import { ref } from 'vue'
const miColor = ref('azul')
  const contador = ref(0)
  const decremento = () => {
    contador.value--
    if (contador.value<0){
      miColor.value = 'rojo'
    }
  }
  const incremento = () => {
    contador.value++
    if (contador.value>5){
      miColor.value = 'verde'
    }
  }
</script>


<style scoped>
span {
  padding: 0 5px;
}
.rojo{
  color: red;
}
.verde{
  color: green;
}
.azul{
  color: blue;
}
</style>
```

## v-if
Con v-if podemos mostrar o no un elemento HTML en caso de que sea true o false la condición que evaluamos. Cuando estamos referenciando un variable en template, no necesitamos usar .value para acceder a su valor.
```vue
<div v-if="contador<0">Escribe una cantidad mayor de 0</div>
<div v-else-if="contador>=5">Escribe una cantidad menor de 5</div>
<div v-else>La cantidad es correcta</div>
```

### v-show
Esta directiva oculta o muestra un elemento HTML, pero siempre va a existir ese elemento, no como v-if que sólo lo crea si es verdad la propiedad y sino no lo crea.

```vue
<template>
  <button @click="decremento">-</button>
  <span :class="miColor">{{ contador }}</span>
  <button @click="incremento">+</button>
  <div v-if="contador<0">Escribe una cantidad mayor de 0</div>
  <div v-else>La cantidad es correcta</div>
  <div v-show="visible">No está permitido el número 0</div>
</template>
  
<script setup>
import { ref } from 'vue'
const visible = ref(true)
const miColor = ref('azul')
  const contador = ref(0)
  const decremento = () => {
    contador.value--
    if (contador.value<0){
      miColor.value = 'rojo'
    }
    visible.value = contador.value === 0
  }
  const incremento = () => {
    contador.value++
    if (contador.value>5){
      miColor.value = 'verde'
    }
    visible.value = contador.value === 0
  }
</script>
```
## v-for
Esta directiva repite el elemento HTML en que se encuentra una vez por cada elemento del array al que se enlaza.

```vue
  <ul>
    <li v-for="elem in todos">
      {{ elem.title}}
    </li>
  </ul>
```
Vue es más eficiente a la hora de renderizar si cada elemento que crea v-for tiene su propia clave, lo que se consigue con el atributo key. Podemos indicar como clave algún campo único del elemento o el índice:
```vue
<... v-for="(elem,index) in todos" :key="index" ...>
```
Pasar una key en cada v-for es recomendable ahora pero será obligatorio al usarlo en componentes así que conviene usarlo siempre.

También podemos usar v-for para que se ejecute sobre un rango (como el típico for (i=0;i<10;i++)):
```vue
<span v-for="n in 10" :key="n"></span>
```
NOTA: No se recomienda usar v-for y v-if sobre el mismo elemento. Si se hace siempre se ejecuta primero el v-if.
## Propiedades computadas
Función que se ejecuta cada vez que cambia alguno de los valores que analiza, es una función reactiva. Sólo se ejecuta cuando los valores que analiza han cambiado, en una función se ejecuta siempre que se llama a esa función. Una función computada siempre tiene que devolver algo.
```vue
<template>
  <button @click="decremento">-</button>
  <span :class="miColor">{{ contador }}</span>
  <button @click="incremento">+</button>
  <div v-if="contador<0">Escribe una cantidad mayor de 0</div>
  <div v-else>La cantidad es correcta</div>
  <div v-show="comprobacion">No está permitido el número 0</div>
</template>
  
<script setup>
import { ref, computed } from 'vue'
const miColor = ref('azul')
  const contador = ref(0)
  const decremento = () => {
    contador.value--
    if (contador.value<0){
      miColor.value = 'rojo'
    }
  }
  const incremento = () => {
    contador.value++
    if (contador.value>5){
      miColor.value = 'verde'
    }
  }
  const comprobacion = computed (() => {
    return contador.value === 0
  })
</script>
```

## Imágenes
Todas las imágenes que están dentro de public no necesitan ser procesadas y se pueden poner directamente como ruta en el src de la etiqueta, pero fuera de esa carpeta tenemos que importarla:
```vue
import imagen from "./assets/log.svg"
```
## Importar datos
Para importar datos lo haremos de la siguiente manera:
```vue
import {valores} from "./datos.js"
```
## Props
Los props se utilizan para pasar parámetros de componentes padres a componentes hijos.
Para ello primero debemos importar el componente hijo en el padre:
import Hijo from './components/Hijo.vue'
Y luego renderizar este componente incluyendo los parámetros que le vamos a pasar al hijo:
<Hijo :nombre="nombre" :edad="edad" />
En el componente hijo para poder recibir los parámetros tenemos que declararlos de la siguiente manera:
const props = defineProps({
    nombre: String,
    edad: Number
})

El componente padre quedaría así:
```vue
<script setup>
import {ref} from 'vue'
import Hijo from './components/Hijo.vue'

const nombre = ref('Manuel')
const edad = ref(18)
</script>

<template>
  <div>
    <h1>Padre:</h1>
    <Hijo :nombre="nombre" :edad="edad" />
  </div>
</template>
```
Y el componente hijo así:
```vue
<script setup>
const props = defineProps({
    nombre: String,
    edad: Number
})
</script>

<template>
<div>
    <h1>Hijo:</h1>
    <h2>Te llamas {{ nombre }} y tienes {{ edad }} años</h2>
</div>
</template>
```
## Emits
Se usan para pasar parámetros de componentes hijos a componentes padres, se realiza a través de un evento.
Para ello creamos un evento en el componente hijo:
<button @click="enviar">Cambiar valores</button>
Y en la función declaramos qué emits vamos a pasarle, en este caso se llamará modificar y le pasará 2 valores:
const emit=defineEmits(['modificar'])
const enviar=()=>{
    emit('modificar', 'Vue', 9)
}
En el padre tendremos que controlar ese paso de parámetros de la siguiente manera:
<Hijo :nombre="nombre" :edad="edad" @modificar="cambiarValor"/>

const cambiarValor = (valor1,valor2)=>{
    nombre.value=valor1
    edad.value=valor2
}

Quedando el código del hijo así:
```vue
<script setup>
const props = defineProps({
    nombre: String,
    edad: Number
})
const emit=defineEmits(['modificar'])
const enviar=()=>{
    emit('modificar', 'Vue', 9)
}
</script>

<template>
<div>
    <h1>Hijo:</h1>
    <h2>Te llamas {{ nombre }} y tienes {{ edad }} años</h2>
    <button @click="enviar">Cambiar valores</button>
</div>
</template>
```
Y el del padre así:
```vue
<script setup>
import {ref} from 'vue'
import Hijo from './components/Hijo.vue'

const nombre = ref('Manuel')
const edad = ref(18)

const cambiarValor = (valor1,valor2)=>{
    nombre.value=valor1
    edad.value=valor2
}
</script>

<template>
  <div>
    <h1>Padre:</h1>
    <Hijo :nombre="nombre" :edad="edad" @modificar="cambiarValor"/>
  </div>
</template>
```
## Provide - Inyección
Con este método podemos pasar datos entre componentes de una manera más sencilla. Usando la funcionalidad provide indicamos que variable va a pasarse al componente hijo, luego en el coponente hijo la capturamos con el método inject y se la asignamos a una variable.
Componente padre:
```vue
<script setup>
import {provide, ref} from 'vue'
import Hijo2 from './components/Hijo2.vue'

const ciclo = ref('DAW')

provide('miCiclo',ciclo)
</script>

<template>
  <div>
    <h1>Padre:</h1>
    <Hijo2/>
  </div>
</template>
```
Componente hijo:
```vue
<script setup>
import { inject } from 'vue';
const ciclohijo = inject('miCiclo') // Aqui ya tengo acceso a la variable ciclo del padre
const modificar = () => {
    ciclohijo.value = 'DAM'
}
</script>

<template>
    <div>
        <h1>Hijo2:</h1>
        <h2>{{ ciclohijo }}</h2>
        <button @click="modificar">Cambiar</button>
    </div>
</template>

```
