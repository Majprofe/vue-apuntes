# vue-apuntes

## ¿Qué es Vue?

Vue es un framework JavaScript creado por Evan You en 2014, combinando lo mejor de Angular y React mientras elimina complejidades innecesarias. Destaca por ser fácil de aprender, con una curva de aprendizaje reducida y una documentación excepcional. Incluso tras la introducción de los hooks en React, Vue respondió con Vue3 en septiembre de 2020, mejorando la gestión de la reactividad de los componentes.

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

#Componentes

Borraremos el contenidos de App.vue para empezar a crear nuestro componente

