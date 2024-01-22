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

Puedes iniciar un proyecto de dos maneras:

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

##Componentes

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




