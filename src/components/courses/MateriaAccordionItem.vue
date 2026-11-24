
<script setup lang="ts">
import { ref } from 'vue'

interface Parcial {
  nombre: string
  calificacion: number
}

defineProps<{
  materia: string
  grupo: string
  semestre: string
  calificacion: number | null
  parciales: Parcial[]
}>()

const expandido = ref(false)
</script>

<template>
  <div class="materia-card">

    <button class="materia-header" @click="expandido = !expandido">

      <div class="materia-info">
        <h3>{{ materia }}</h3>
        <p>Grupo {{ grupo }} - {{ semestre }}</p>
      </div>

      <span class="flecha">
        {{ expandido ? '⌃' : '⌄' }}
      </span>

      <div class="calificacion" :class="{ gris: calificacion === null }">
        <template v-if="calificacion !== null">
          <strong>{{ calificacion.toFixed(1) }}</strong>
          <small>Acumulado</small>
        </template>
      </div>

    </button>

    <div v-if="expandido" class="parciales">

      <div v-for="(parcial, index) in parciales" :key="index" class="parcial">
        <span>{{ parcial.nombre }}</span>
        <strong>{{ parcial.calificacion.toFixed(1) }}</strong>
      </div>

      <p v-if="parciales.length === 0">
        No hay parciales registrados.
      </p>

    </div>

  </div>
</template>

<style scoped>
.materia-card {
  background: white;
  border: 1px solid #e8e8e8;
  border-radius: 5px;
  overflow: hidden;
}

.materia-header {
  width: 100%;
  min-height: 44px;
  display: flex;
  align-items: center;
  gap: 5px;
  padding: 0;
  border: none;
  background: white;
  cursor: pointer;
  text-align: left;
}

.materia-header:hover {
  background: #fafafa;
}

.materia-info {
  flex: 1;
  padding-left: 9px;
}

.materia-info h3 {
  margin: 0;
  font-size: 14px;
  color: #171717;
}

.materia-info p {
  margin: 2px 0 0;
  font-size: 10px;
  color: #333;
}

.flecha {
  font-size: 19px;
  color: #666;
}

.calificacion {
  width: 44px;
  min-width: 44px;
  height: 44px;
  background: #e7fbd9;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.calificacion strong {
  font-size: 16px;
}

.calificacion small {
  font-size: 8px;
}

.calificacion.gris {
  background: #bdbdbd;
}

.parciales {
  padding: 8px 10px;
  background: #fafafa;
  border-top: 1px solid #eee;
}

.parcial {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  font-size: 12px;
  border-bottom: 1px solid #eee;
}

.parcial strong {
  color: #426a43;
}

.parciales p {
  font-size: 12px;
  color: #888;
}
</style>
