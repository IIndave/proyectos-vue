<script setup>
import {ref, computed} from "vue";
const counter = ref(0);//Variable reactiva con el ref
const lista = ref([]);

const increment = () =>{
  console.log("Aumentar contador")
  counter.value++;
  console.log(counter)
}

const decrease =()=>{
  counter.value--;
}
const reset =()=>{
  counter.value = 0;
}

const agregar = () =>{
  lista.value.push(counter.value)
  console.log(lista.value)
}
// eslint-disable-next-line
const classDisabled= computed(() => {
  const numRep= lista.value.find(num=>num===counter.value)
  if (numRep === 0){
    return true;
  }
  return numRep ? true : false
});

// eslint-disable-next-line
const classCounter= computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
});

const handleClick = () => {
  console.log("Me diste click")
}
const titulo="Hola Vue"
  const personas=[
    {
      name:"Carlos",
      edad:25
    },
    {
      name:"Iñigo",
      edad:31
    },
    {
      name:"Andrea",
      edad:33
    },
  ]
  const objetoFruta = {
    name:"Manzana",
    precio:"5€",
    peso:"125gr"
  }

</script>

<template>
  <div class="container text-canter">
    <h2 :class="classCounter" >{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrease" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-warning">Reset</button>
      <button @click="agregar" :disabled="classDisabled" class="btn btn-secondary">Agregar numero</button>
      <button v-on:click="handleClick" class="btn btn-primary">Activame</button>
    </div>
    <ul class="list-group">Lista:
      <li v-for="(numero,index) in lista" :key="index" class="list-group-item">{{index}} : {{ numero }}</li>
    </ul>
    <h1>{{titulo.toUpperCase()}}</h1>
    <ul class="list-group"> 
      <template v-for="(persona, index) in personas" :key="index">
        <li v-if="persona.edad > 26" class="list-group-item">
          {{index}} -
          {{persona.name}} -
          {{ persona.edad }} años
        </li>      
      </template>
      
    </ul>
    Lista con atributos del objeto
    <ul class="list-group">
      <!-- En objetos el segundo argujmento "propiedad" es el nombre de la propiedad
      y el tercero -->
      <li v-for="(value,propiedad,index) in objetoFruta" :key="value" class="list-group-item">
        {{index}} - {{propiedad}}: {{ value }}
      </li>
    </ul>
  </div>
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.positive{
  color: green;
}
.negative{
  color: red;
}
.zero{
  color: blue;
}
</style>
