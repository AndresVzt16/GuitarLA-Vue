<script setup>
import { ref, reactive, onMounted } from "vue";

import { db } from "./data/guitarras";
import Guitarra from "./components/Guitarra.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

/* const state = reactive({
  guitarras: db,
}); */

const guitarras = ref([]);
const carrito = ref([])
const state = reactive({
  guitarras: [],
});


onMounted(() => {
  (guitarras.value = db), (state.guitarras = db);
});


const AgregarProductoCarrito = (data) => {
  const {guitarra, cantidad} =  data
  guitarra.cantidad = cantidad
  carrito.value.push(guitarra)
  
}

</script>

<template>
  <Header/>

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5 gap-5">
      <Guitarra 
        v-for="guitarra in guitarras" 
        :guitarra="guitarra"
        :data="true"  
        @agregarProductoCarrito="AgregarProductoCarrito"
        @incrementarCantidad= "incrementarCantidad"
      />
    </div>
  </main>

  <Footer/>

</template>
