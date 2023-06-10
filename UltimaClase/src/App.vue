<script setup>
import { ref , computed } from 'vue';

const valorBoleta = 5000
let aplicarDescuento = ref(false)

let cantidadEntradas = ref(0)

const mostrarMensaje = computed (()=>{
  return cantidadEntradas.value >= 4 ? true : false
 
})


const comprarBoletos = () =>{
  const cant = +cantidadEntradas.value
  if(cant >= 4){
    aplicarDescuento.value = true
    const valorPleno = cant * valorBoleta
    const descuento  = valorPleno * 0.3
    totalPagar.value = valorPleno - descuento
  }else{
    totalPagar.value = cant *valorBoleta
  }
}

const totalPagar = ref(0)
</script>

<template>
  <div class="bg-slate-300 w-96 mx-auto py-4 px-6 rounded-md mt-8 shadow-md ">
    <label for="entradas">
      Cantidad
    </label>
    <input id="entradas" name="entradas" type="text" v-model="cantidadEntradas">

    <button class="ml-2 bg-red-500 px-2 rounded-md text-blue-50 hover:bg-red-600"
    @click="comprarBoletos()">
      Comprar
    </button>
  </div>
  <p >
    Valor a pagar : {{ totalPagar }}
    <span v-if="aplicarDescuento" class="text-green-600 font-bold ">
      ¡Descuento aplicado!😎
    </span>
    <span v-if="mostrarMensaje" class="text-green-600 font-bold">
      decuentos aplicadooooo
    </span>
  </p>
</template>


