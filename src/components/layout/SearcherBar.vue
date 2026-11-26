<script setup lang="ts">
import lupaIcon from '../../assets/Lupa.png'

interface Props {
  modelValue?: string
  placeholder?: string
  disabled?: boolean
}

withDefaults(defineProps<Props>(), {
  modelValue: '',
  placeholder: 'Buscar...',
  disabled: false
})

const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void
  (e: 'buscar', value: string): void
}>()

function alEscribir(event: Event) {
  const target = event.target as HTMLInputElement
  emit('update:modelValue', target.value)
}

function alEnviar(value: string) {
  emit('buscar', value)
}
</script>

<template>
  <form
    class="search-bar"
    :class="{ 'is-disabled': disabled }"
    @submit.prevent="alEnviar(modelValue)"
  >
    <input
      type="text"
      class="search-input"
      :value="modelValue"
      :placeholder="placeholder"
      :disabled="disabled"
      aria-label="Buscar"
      @input="alEscribir"
    />

    <button
      type="submit"
      class="search-btn"
      :disabled="disabled"
      aria-label="Ejecutar búsqueda"
      @click="alEnviar(modelValue)"
    >
      <img :src="lupaIcon" alt="Buscar" class="search-icon" />
    </button>
  </form>
</template>

<style scoped>
.search-bar {
  width: 100%;
  max-width: 340px;
  height: 36px;
  padding: 0 14px 0 18px;
  background-color: #ffffff;
  border: 2px solid #7a7a7a;
  border-radius: 999px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
  box-sizing: border-box;
  transition: border-color 0.15s ease, border-width 0.15s ease, box-shadow 0.15s ease;
}

.search-bar:hover:not(.is-disabled),
.search-bar:focus-within:not(.is-disabled) {
  border-color: #155284;
  border-width: 2.5px;
  box-shadow: 0 0 0 3px rgba(21, 82, 132, 0.18);
}

.search-bar.is-disabled {
  background-color: #ebebeb;
  border-color: #d4d4d4;
  cursor: not-allowed;
}

.search-input {
  width: 100%;
  border: none;
  outline: none;
  background: transparent;
  color: #1e1e1e;
  font-family: 'Inter', sans-serif;
  font-size: 13px;
}

.search-input::placeholder {
  color: #1e1e1e;
}

.search-bar.is-disabled .search-input,
.search-bar.is-disabled .search-input::placeholder {
  color: #9e9e9e;
  cursor: not-allowed;
}

.search-btn {
  background: transparent;
  border: none;
  padding: 0;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.search-bar.is-disabled .search-btn {
  cursor: not-allowed;
}

.search-icon {
  width: 18px;
  height: 18px;
  object-fit: contain;
  display: block;
  mix-blend-mode: multiply;
}

.search-bar.is-disabled .search-icon {
  opacity: 0.45;
  filter: grayscale(100%);
}
</style>