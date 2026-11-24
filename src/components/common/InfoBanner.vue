<script setup lang="ts">
interface Props {
  titulo?: string
  textoBoton?: string
}

withDefaults(defineProps<Props>(), {
  titulo: 'Aviso Informativo',
  textoBoton: 'Abrir'
})

const emit = defineEmits<{
  (e: 'abrir'): void
}>()

function manejarClic() {
  emit('abrir')
}
</script>

<template>
  <div class="info-banner" role="region" :aria-label="titulo">
    <span class="info-badge">{{ titulo }}</span>
    <button type="button" class="info-btn" @click="manejarClic">
      {{ textoBoton }}
    </button>
  </div>
</template>

<style scoped>
.info-banner {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 10px 16px;
  border-radius: 16px;
  background-color: #dcdcdc;
  box-sizing: border-box;
}

.info-badge {
  background-color: #00b7ff;
  color: #000000;
  font-family: 'Inter', sans-serif;
  font-weight: 700;
  font-size: 14px;
  padding: 6px 18px;
  border-radius: 999px;
}

.info-btn {
  background-color: #155284;
  color: #ffffff;
  font-family: 'Inter', sans-serif;
  font-size: 13px;
  font-weight: 600;
  border: none;
  border-radius: 12px;
  padding: 6px 16px;
  cursor: pointer;
}

.info-btn:hover {
  opacity: 0.92;
}
</style>