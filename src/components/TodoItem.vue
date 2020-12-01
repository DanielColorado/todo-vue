<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <div class="d-flex justify-content-between align-items-center"
            role="button" 
            @click="completado(todo.id)"
            :class="{'tachado': todo.estado}"
        >
        <span :class="{'active': todo.estado}" class="container-check d-flex justify-content-center align-items-center">
            <img v-if="todo.estado" class="check" src="../../public/img/icon-check.svg" alt="">
        </span>
            {{todo.texto}}
        </div>
        <div role="button" @click="eliminar(todo.id)">
            <!-- <i class="fas fa-times"></i> -->
            <img class="cross" src="../../public/img/icon-cross.svg" alt="">
        </div>
    </li>
</template>

<script>
import { inject } from 'vue'
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    setup(){
        const todos = inject('todos')

        const eliminar = id => {
            todos.value = todos.value.filter(item => item.id !== id)
        }

        const completado = id => {
            todos.value = todos.value.map(item => {
                if(item.id === id){
                    item.estado = true
                }
                return item
            })
        }

        return {eliminar, completado}
    }
}
</script>

<style>

</style>