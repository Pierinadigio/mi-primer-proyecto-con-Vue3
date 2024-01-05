<script setup>
//cuando uso variables reactivas debo importar ref de VUE

import {ref, computed} from 'vue'

// y le digo que la variable "contador" es una variable reactiva--- Usamos ref porque es mas dinamico que el 'reactive'
//ref acepta cualquier tipo de valor... un entero, string, booleano, un arreglo, etc... Es importante inicializarlo
//en la funcion ( en el script) cuando queramos acceder a la varialbel "contador" hay q agregar el .value... porque VUE devuelve un objeto y para acceder a su valor real uso el value
const contador= ref(0);
const titulo= "Quiero contar"
//metodo contador
//let contador = 0;
const contar= () =>{
  contador.value ++;
  console.log(contador)
}
const disminuir= () =>  contador.value --;

const resetear= () => (contador.value = 0);

//con computed---PROPIEDAD COMPUTADA --primero creo los estilos de las clases y luego las uso con if
const classContador = computed (()=> {
   if (contador.value >= 5){
    return 'positivo'
   }
   else return 'negativo'
})

const name= "hola Marge";
const colorLetraRoja= "color: red";
const colorLetraVerde= "color: green";
const arrayColores= ["red", "blue", "yellow", "peru"];
const activo= false;
const inactivo = true;
const ocupado= true;
const arrayFrutas = ["manzana", "pera", "durazno"];
const arrayObjetosFrutas = [
  { nombre: "manzana",
    precio: "$2",
    descrip: "es una manzana roja",

  },
  {
    nombre: "pera",
    precio: "$3",
    descrip: "esuna pera amarilla",
  },
  {
    nombre: "durazno",
    precio: "$4",
    descrip: "es un durazno color naranhja y rojo",
  }
];
const objetoSolo = 
  { nombre: "manzana",
    precio: "$2",
    descrip: "es una manzana roja",

  };

  const users = [
  {
    id: 1,
    name: 'Juan',
    posts: [
      { id: 1, title: 'Mi primer post' },
      { id: 2, title: 'Mi segundo post' },
    ]
  },
  {
    id: 2,
    name: 'Maria',
    posts: [
      { id: 3, title: 'Mi tercer post' },
      { id: 4, title: 'Mi cuarto post' },
    ]
  }
];

const misPerros = [
  { name : 'Silvio',
    edad : '11 anios',
    tamanio : 'grande',
    id : 1,
  },
  {name : 'Chiquita',
    edad : '10 anios',
    tamanio : 'chico',
    id: 2,
  }

];

//metodo
const onClick = (mensaje) => {
 
  console.log (mensaje)
}
const arrayFavoritos = ref ([])
const add = ()=> {
  arrayFavoritos.value.push(contador.value)
}
const bloquearAdd = computed(()=>{
  const serchNum = arrayFavoritos.value.find((num) => num === contador.value);

  //return serchNum === 0 || serchNum ? true : false;
  return serchNum === 0 || serchNum 
}

)
</script>


<template>
  <h1>... {{ name.toUpperCase() }} js</h1>

  <h2 v-bind:style="colorLetraRoja"> Soy Pier</h2>
  
  <h3 :style=" colorLetraVerde"> Color letra dos</h3>
  <p :style="`color: ${arrayColores[2]}`">El color del parrafo es amarillo</p>
  <h2>
    {{ activo ? "Hello world" : "No estoy actuvoOOOOO" }}
  </h2>
  <p v-if="!activo">No estoy activo</p>
  <p v-else> No estoy activo</p>

  <p v-if="inactivo">INACTIVO ESTOYY</p>

  <p v-if="ocupado === true">Estoy ocupado</p>
<p v-else-if= "ocupado === false"> No estoy ocupado</p>
<p v-else> Estoy indeciso</p>

<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
<div>
  <ol>
    <li v-for="fruta in arrayFrutas" :key="index"
    > {{ fruta }}</li>

  </ol>
</div>
<div>
  <ul>
    <li v-for="fruit in arrayObjetosFrutas" :key="fruit.nombre">
      {{ fruit.nombre }} - {{ fruit.precio }}- {{ fruit.descrip }}
    </li>
  </ul>
</div>
<div>
  <ul>
    <li v-for = "(value, propiedad) in objetoSolo" :key="value">
      {{propiedad}} : {{value}}
    </li>
  </ul>
</div>
<div>
    <h2>Lista de usuarios:</h2>
    <ul>
      <template
        v-for="(user, index) in users"
        :key="user.id"
      >
        <li>
          <h3>{{ user.name }}</h3>
          <ul>
            <template
              v-for="(post, index) in user.posts"
              :key="post.id"
            >
              <li>{{ post.title }}</li>
            </template>
          </ul>
        </li>
      </template>
    </ul>
</div>
<div>
  <h3>Mis Perros</h3>
  <ul>
    <template v-for= "(perro, index) in misPerros" :key= misPerros.id>
      <li>
          <h3>{{perro.name }}</h3>
          <ul>
            
              <li>{{perro.edad }}</li>
              <li>{{ perro.tamanio }}</li>
          </ul>
        </li>    
  </template>
  </ul>
</div>
<div>
  <button v-on:click="onClick('lalala')">boton 1</button>
  <button @click ="onClick ('sarasa')"> boton 2</button>
</div>
<div>
  <button v-on:click.right.prevent="onClick('lalala Derecho')">boton der</button>
  <button @click ="onClick ('sarasa')"> boton izq</button>
  <button @click.middle ="onClick ('sarasaMEDIO')"> boton medio</button>
</div>
<div class = text-center>
  <h1>{{ titulo }}</h1>
  <h2 v-if="contador < 0" v-bind:style="colorLetraRoja">{{ contador }}</h2>
  <h2 v-else="contador > 0" v-bind:style="colorLetraVerde">{{ contador }}</h2>
  
  <h3 :class="contador >= 0 ? 'positivo' : 'negativo' ">{{ contador }}</h3>

  <h4 :class="classContador">{{ contador }}</h4>
  <div class="mx-auto p-2">
    <button type="button"  @click ="contar" class = "btn btn-success text-nowrap ml-20">aumentar</button>
    <button @click ="disminuir" class = "btn btn-danger text-nowrap">disminuir</button>
    <button @click ="resetear" class = "btn btn-secondary">resetear</button>
    <button @click ="add" :disabled = "bloquearAdd" class = "btn btn-primary">Add</button>
  </div>
  <ul class = "list-group mt-4">
    <li class = "list-group-item" v-for="(num, index) in arrayFavoritos" :key="index"
    > {{ num }}</li>
  </ul>
</div>


</template>

<style>
h1{
  color: rgb(102, 233, 102);
}
h2{
  font-family:fantasy;
  color:blue;
}
.positivo{
  color: yellow;
}
.negativo{
color: red;
}
</style>
