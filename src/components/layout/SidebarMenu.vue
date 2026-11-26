<script setup lang="ts">
import { ref } from 'vue'

const botonActivo = ref<number | null>(null)

function seleccionarBoton(indice: number) {
  botonActivo.value = botonActivo.value === indice ? null : indice
}
</script>

<template>
  <div class="contenedor-SideBar">
    <button
      type="button"
      class="button"
      :class="{ activo: botonActivo === 0 }"
      @click="seleccionarBoton(0)">
      <img class="img" src="../../assets/Casa.png" alt="Imagen de casa"></button>
    <button type="button"
      class="button"
      :class="{ activo: botonActivo === 1 }"
      @click="seleccionarBoton(1)"
      ><img class="img" src="../../assets/Elemento lateral.png" alt="Imagen de elemento"></button>
    <button type="button"
      class="button"
      :class="{ activo: botonActivo === 2 }"
      @click="seleccionarBoton(2)"
      ><img class="img" src="../../assets/Elemento lateral (1).png" alt="Imagen de elemento"></button>
    <button type="button"
      class="button"
      :class="{ activo: botonActivo === 3 }"
      @click="seleccionarBoton(3)"
      ><img class="img" src="../../assets/Elemento lateral (2).png" alt="Imagen de elemento"></button>
    <button type="button"
      class="button"
      :class="{ activo: botonActivo === 4 }"
      @click="seleccionarBoton(4)"
      ><img class="img" src="../../assets/Elemento lateral (3).png" alt="Imagen de elemento"></button>
  </div>   
</template>

<style scoped>

.contenedor-SideBar {
  width: fit-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 80px;
  padding: 12px 10px;
  margin-top: 16px;
  background-color: #D6D6D6;
  border-radius: 12px;
  box-shadow: 0 5px 20px -8px rgba(0, 0, 0, 0.50);
  box-sizing: border-box;
}

.button {
  position: relative;
  background-color: transparent;
  border: none;
  padding: 6px 10px 6px 16px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
}

.button:active {
  transform: scale(0.96);
}

.button:hover .img,
.button.activo .img {
  filter: grayscale(100%) brightness(0.65);
}

.button.activo::before {
  content: "";
  position: absolute;
  left: 4px;
  top: 50%;
  transform: translateY(-50%);
  width: 4px;
  height: 70%;
  background-color: #1c5d8c;
  border-radius: 4px;
}

.img {
  width: 28px;
  height: auto;
  display: block;
  transition: filter 0.2s ease;
}
</style>
