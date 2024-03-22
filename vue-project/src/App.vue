<script setup>
  import {ref, computed} from 'vue';

  const name = 'Vue dinamico';

  const counter = ref(0);
  
  const increment = () => {
    counter.value ++;
  };
  const restar = () => {
    counter.value --;
  };

  const start = () => {
    counter.value = 0;
  }

  const classCounter = computed(() => { 
    if (counter.value === 0){
      return 'zero'
    };
    if (counter.value > 0){
      return 'positive'
    };
    if (counter.value < 0){
      return 'negative'
    };
   });
  const arrayFavoritos = ref([]);

  const add = () => { arrayFavoritos.value.push(counter.value) };

  const bloquearBtnAdd = computed(() => { 
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  // if (numSearch === 0 ) return true;
  // return numSearch? true : false;
    return numSearch || numSearch === 0;
   });

</script>

<template class="align-item-center justify-content-center">
  <div class="container text-center ">
    
    <h1 class="card text-bg-danger">Hola {{ name.toUpperCase() }}!!
    <hr></h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar Contador</button>
      <button @click="restar" class="btn btn-danger">Restar Contador</button>
      <button @click="start" class="btn btn-secondary" >Iniciar Contador</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
      
    </div>
    
    <ul class="list-group mt-4">
      <li v-for="(num, index) in arrayFavoritos" :key="index" :class="classCounter" class="list-group-item">
      {{ num }}</li>
    </ul>
    

  </div>


</template>

<style>
.positive{
  color:green;
}
.negative{
  color:red;
}
.zero{
  color:peru;
}
</style>