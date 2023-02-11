<template>
     <div
       class="mt-3 alert d-flex justify-content-between align-items-center"
       :class="tarea.estado ? 'alert-primary' : 'alert-warning'"
     >
       <p class="m-0" :class="{ tachado: tarea.estado }">
         {{ tarea.texto }}
       </p>
       <h3 class="m-0">
         <i
           class="fas text-success mr-2"
           :class="tarea.estado ? 'fa-undo-alt' : 'fa-check-circle'"
           role="button"
           @click="accionTarea(tarea.id)"
         ></i>
         <i
           class="fas fa-minus-circle text-danger"
           role="button"
           @click="eliminarTarea(tarea.id)"
         ></i>
       </h3>
     </div>
   
   </template>
   
   <script>
   import { inject } from "vue";
   export default {
     props: {
       tarea: { type: Object, required: true },
     },
     setup() {
       const tareas = inject("tareas");
   
       const eliminarTarea = (id) => {
         tareas.value = tareas.value.filter(tarea => tarea.id !== id)
       };
   
       const accionTarea = (id) => {
         tareas.value = tareas.value.map(tarea => {
           if(tarea.id === id){
             tarea.estado = !tarea.estado
           }
           return tarea
         })
       };
   
       return { eliminarTarea, accionTarea };
     },
   };
   </script>
   
   <style>
   .tachado {
     text-decoration: line-through;
   }
   </style>