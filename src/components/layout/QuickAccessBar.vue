<template>
  <div class="contenedor-QuickAccess">
    <button
      v-for="n in 8"
      :key="n"
      type="button"
      class="btn-cuadro"
    >
      <span class="cuadro"></span>
    </button>
  </div>
</template>

<style scoped>

.contenedor-QuickAccess {
  width: 100%;
  max-width: 640px;
  margin: 0 auto;
  padding: 12px 16px;
  background-color: #D3E9FF;
  display: grid;
  grid-template-columns: repeat(8, minmax(0, 1fr));
  gap: 14px;
  box-sizing: border-box;
}

.btn-cuadro {
  width: 100%;
  aspect-ratio: 1 / 1;
  padding: 0;
  border: none;
  background-color: #ffffff;
  border-radius: 14px;
  box-shadow: 0 1px 10px 5px rgba(24, 68, 112, 0.08);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.btn-cuadro:hover {
  box-shadow: 0 1px 15px 10px rgba(0, 128, 255, 0.12);
}

.btn-cuadro:active {
  transform: scale(0.97);
}

@media (max-width: 900px) {
  .contenedor-QuickAccess {
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 12px;
  }
}

@media (max-width: 520px) {
  .contenedor-QuickAccess {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 10px;
  }
}

</style>