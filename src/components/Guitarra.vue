<script setup>
import { onMounted, ref, reactive } from "vue";

const numero = ref(0);

onMounted(() => {
  console.log("Hola desde el onMounted");
});

const props = defineProps({
  guitarra: {
    type: Object,
    required: true,
  },
  data: {
    type: String,
    required: true,
  },
});
defineEmits(['incrementarCantidad', 'agregarProductoCarrito'])
</script>

<template>
  <div class="col-md-6 col-lg-4 my-4 row align-items-center">
    <div class="col-4">
      <img
        class="img-fluid object-cover"
        :src="'/img/' + guitarra.imagen + '.jpg'"
        :alt="'imagen guitarra' + guitarra.nombre"
      />
    </div>
    <div class="col-8">
      <h3 class="text-red-600 fs-4 fw-bold text-uppercase">
        {{ guitarra.nombre }}
      </h3>
      <p class="text-sm text-gray-500 w-full">{{ guitarra.descripcion }}</p>

      <p class="text-yellow-500 font-semibold text-4xl">
        ${{ guitarra.precio }}
      </p>
      <div
        class="d-flex w-fit text-xl text-white p-1 rounded my-5 items-center space-x-5"
      >
        <button
          class="bg-gray-100 border border-gray-100 text-gray-800 rounded-md px-3 py-1"
          @click="numero++"
        >
          +
        </button>
        <p class="text-gray-500 m-0">{{ numero }}</p>
        <button
          class="bg-gray-100 border border-gray-100 text-gray-700 rounded-md px-3 py-1"
          @click="numero--"
        >
          -
        </button>
      </div>
    </div>
    <button
      type="button"
      class="px-2 w-full py-2 bg-slate-500 text-white rounded"
      @click="$emit('agregarProductoCarrito', {guitarra, cantidad: numero})"
    >
      Agregar al Carrito
    </button>
  </div>
</template>

<style lang="scss" scoped></style>
