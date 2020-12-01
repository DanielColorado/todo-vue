<template>
  <div class="card mt-3">
      <div class="card-body d-flex justify-content-center align-items-center">
          <span :class="{'active':filterActive === 0}"
            role="button"
            @click="filtrar('all')"
          >
            All
          </span>
          <span :class="{'active':filterActive === 1}"
            role="button"
            @click="filtrar('active')"
          >
            Active
          </span>
          <span :class="{'active':filterActive === 2}"
            role="button"
            @click="filtrar('complete')"
          >
            Completed
          </span>
      </div>
  </div>
</template>

<script>
import { computed, inject } from 'vue'
export default {
    setup(){
        const estado = inject('estado')
        // console.log(estado.value)

        const filtrar = valor => {
            estado.value = valor
        }

        const filterActive = computed(()=>{
          if(estado.value === 'active')
            return 1;
          else if(estado.value === 'complete')
            return 2;
          else
            return 0;
        })

        return {filtrar,filterActive}
    }
}
</script>

<style>

</style>