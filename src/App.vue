<script setup>
import {ref, computed} from "vue"

const name = "Contador Dinamico";

const counter = ref(0);

const arrayCounter = ref([]);

const increment = () => {
    counter.value++;
   
}

const reiniciar = () => {
    counter.value=0;
}

const disminuir = () => {
    counter.value--;
}
 
const add = () => {
    arrayCounter.value.push(counter.value)
}

const quitar = () => {
    arrayCounter.value.shift(counter.value)
}

const blockNumber = computed(()=> {
    const number = arrayCounter.value.find((num) => num ===  counter.value);
    return number || number === 0;
})
const classCounter = computed (()=>{
    if (counter.value == 0){
        return "zero"
    }
    if (counter.value > 0 ){
        return "positive"
    }
    if (counter.value < 0){
        return "negative"
    }
})
 
</script>

<template> 
<div  class="container text-center mt-5  ">
    <div>
        <h1>{{ name }}</h1>
    </div>

    <div>
        <h2 :class="classCounter">{{ counter }}</h2>
    </div>

    <div class="btn-group">
        <button @click="increment" class="btn btn-success">Incrementar</button>
        <button @click="reiniciar" class="btn btn-secondary">reiniciar</button>
        <button @click="disminuir" class="btn btn-danger">disminuir</button>
        <button @click="add"  :disabled="blockNumber" class="btn btn-primary">Agregar</button>
        <button @click="quitar" :disabled="false"  class="btn btn-secondary">Quitar</button>
    </div>
     <ul class="list-group"><li v-for="(num, index) in arrayCounter" key="index" class="list-group-item mt-4"> {{ num }}</li></ul>
        
</div>
</template>

<style>
    .zero {
        color: yellow;
    }
    .negative {
        color: red;
    }

    .positive {
        color: green;
    }
</style>

 