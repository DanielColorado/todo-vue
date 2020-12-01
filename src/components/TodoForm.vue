<template>
  <form id="form-todo" @submit.prevent="formulario">
    <input 
        type="text"
        class="form-control"
        placeholder="Create a new todo..."
        v-model.trim="texto"
    >
  </form>
</template>

<script>
import { inject, ref } from 'vue'
export default {
    setup(){
        const todos = inject('todos')
        const texto = ref('')
        
        const formulario = () => {
            // console.log(texto.value)
            if(texto.value === ''){
                console.log('está vacio')
                return
            }
            const todo = {
                texto: texto.value,
                estado: false,
                id: Date.now()
            }

            todos.value.push(todo)
            // console.log(todos.value)

            texto.value = ''
            // console.log(todo)
        }

        return {formulario, texto}
    }
}
</script>

<style>

</style>