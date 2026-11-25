<script setup lang="ts">
import { ref, watch } from 'vue'

interface Props {
  abierto: boolean
  titulo?: string
  mensaje?: string
  textoBoton?: string
  requiereConfirmacion?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  titulo: 'Información importante',
  mensaje:
    'Aquí va un anuncio importante c:',
  textoBoton: 'Aceptar',
  requiereConfirmacion: true
})

const emit = defineEmits<{
  (e: 'cerrar'): void
}>()

const confirmado = ref(false)

watch(
  () => props.abierto,
  (estaAbierto) => {
    if (estaAbierto) {
      confirmado.value = false
    }
  }
)

function aceptarYcerrar() {
  if (props.requiereConfirmacion && !confirmado.value) return
  emit('cerrar')
}
</script>

<template>
  <Teleport to="body">
    <div
      v-if="abierto"
      class="modal-backdrop"
      role="dialog"
      aria-modal="true"
      @click.self="emit('cerrar')"
    >
      <div class="modal-card">
        <h2 class="modal-title">{{ titulo }}</h2>
        <p class="modal-text">{{ mensaje }}</p>

        <label v-if="requiereConfirmacion" class="check-wrapper">
          <input
            v-model="confirmado"
            type="checkbox"
            class="check-input"
            aria-label="Confirmar lectura de información"
          />
          <span class="check-box" aria-hidden="true">
            <svg
              v-if="confirmado"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="3"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="20 6 9 17 4 12" />
            </svg>
          </span>
        </label>

        <button
          type="button"
          class="modal-btn"
          :disabled="requiereConfirmacion && !confirmado"
          @click="aceptarYcerrar"
        >
          {{ textoBoton }}
        </button>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(120, 120, 120, 0.55);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  z-index: 1000;
}

.modal-card {
  width: 100%;
  max-width: 1280px;
  background-color: #ffffff;
  border: 1.5px solid #1e1e1e;
  border-radius: 16px;
  padding: 28px 36px 24px;
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.25);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 14px;
  font-family: 'Inter', sans-serif;
  box-sizing: border-box;
}

.modal-title {
  margin: 0;
  color: #00b7ff;
  font-family: 'Inter', sans-serif;
  font-size: 32px;
  font-weight: 700;
  line-height: 1;
  letter-spacing: 0;
  text-align: center;
}

.modal-text {
  margin: 0;
  color: #4a4a4a;
  font-size: 13px;
  line-height: 1.45;
  max-width: 820px;
}

.check-wrapper {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.check-input {
  position: absolute;
  opacity: 0;
  width: 100%;
  height: 100%;
  margin: 0;
  cursor: pointer;
}

.check-box {
  width: 36px;
  height: 24px;
  border-radius: 8px;
  border: 1.5px solid #6b7280;
  background-color: #ffffff;
  color: #ffffff;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.15s ease, border-color 0.15s ease;
}

.check-wrapper:hover .check-box {
  border-color: #155284;
}

.check-input:checked + .check-box {
  background-color: #28a745;
  border-color: #28a745;
}

.check-box svg {
  width: 16px;
  height: 16px;
}

.modal-btn {
  background-color: #155284;
  color: #ffffff;
  border: none;
  border-radius: 12px;
  padding: 7px 22px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: opacity 0.15s ease;
}

.modal-btn:hover:not(:disabled) {
  opacity: 0.92;
}

.modal-btn:disabled {
  opacity: 0.45;
  cursor: not-allowed;
}
</style>