<template>
     <form @submit.prevent="agregarTarea">
       <input 
           type="text"
           placeholder="Agregar tarea..."
           class="form-control my-2"
           v-model="texto"
       >
       <button
           type="submit"
           class="btn btn-dark btn-block"
       >Agregar</button>
     </form>
   </template>
   
   <script>
   import { inject, ref } from 'vue'
   export default {
       setup(){
           const texto = ref('')
           const tareas = inject('tareas')
           const agregarTarea = () => {
               const tarea = {
                   texto: texto.value,
                   id: Date.now(),
                   estado: false
               }
   
               texto.value = ''
               tareas.value.push(tarea)
           }
           return {texto, agregarTarea}
       }
   }
   </script>