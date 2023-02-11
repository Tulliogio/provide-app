<template>
     <h1 class="my-5">Lista de tareas</h1>
     <hr>
 
     <tarea-formulario />
 
     <div 
         class="alert alert-dark mt-3"
         v-if="tareas.length === 0"
     >
         No hay tareas 😍
     </div>
 
     <tarea-item
         v-for="tarea in tareas" :key="tarea.id"
         :tarea="tarea"
     />
 </template>
 
 <script>
 import { provide, ref, watchEffect } from 'vue'
 import TareaFormulario from './TareaFormulario.vue'
 import TareaItem from './TareaItem.vue'
 
 export default {
     components: {
         TareaFormulario,
         TareaItem
     },
     setup(){
         const tareas = ref([])
 
         provide('tareas', tareas)
 
         if(localStorage.getItem('tareas')){
             const tareasLocalStorage = JSON.parse(localStorage.getItem('tareas'))
             tareas.value = tareasLocalStorage
         }
 
         watchEffect(() => {
             localStorage.setItem('tareas', JSON.stringify(tareas.value))
         })
 
         return {tareas}
     }
 }
 </script>