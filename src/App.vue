
<script setup lang="ts">
import { ref } from 'vue'

import TopNavbar from './components/layout/TopNavbar.vue'
import SearcherBar from './components/layout/SearcherBar.vue'
import QuickAccessBar from './components/layout/QuickAccessBar.vue'
import SidebarMenu from './components/layout/SidebarMenu.vue'

import InfoBanner from './components/common/InfoBanner.vue'
import InfoModal from './components/common/InfoModal.vue'

import CalificacionesCard from './components/cards/CalificacionesCard.vue'

const busqueda = ref('')
const modalAbierto = ref(false)
const seccionActiva = ref<number | null>(null)

function buscar(texto: string) {
  console.log('Búsqueda:', texto)
}
</script>

<template>
  <div class="dashboard">

    <!-- Barra superior -->
    <header class="barra-superior">
      <TopNavbar />

      <SearcherBar
        v-model="busqueda"
        placeholder="Buscar..."
        @buscar="buscar"
      />
    </header>

    <div class="separador"></div>

    <!-- Accesos rápidos -->
    <section class="accesos">
      <QuickAccessBar />
    </section>

    <div class="separador"></div>

    <!-- Aviso informativo -->
    <section class="aviso">
      <InfoBanner
        titulo="Aviso Informativo"
        textoBoton="Abrir"
        @abrir="modalAbierto = true"
      />
    </section>

    <!-- Contenido principal -->
    <div class="contenido">

      <aside class="menu-lateral">
        <SidebarMenu @seleccionar="seccionActiva = $event" />
      </aside>

      <main class="area-principal">

        <!-- Calificaciones -->
        <CalificacionesCard v-if="seccionActiva === 1" />

      </main>

    </div>

    <!-- Ventana modal -->
    <InfoModal
      :abierto="modalAbierto"
      titulo="Información importante"
      mensaje="Aquí va un anuncio importante."
      textoBoton="Aceptar"
      :requiereConfirmacion="true"
      @cerrar="modalAbierto = false"
    />

  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

html, body, #app {
  width: 100%;
  min-height: 100%;
  margin: 0;
}

body {
  font-family: Arial, sans-serif;
  background-color: #cccccc;
}

.dashboard {
  width: 94%;
  max-width: 1600px;
  min-height: calc(100vh - 40px);
  margin: 20px auto;
  padding: 16px 20px;
  background-color: #d3e9ff;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

/* Barra superior */
.barra-superior {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 30px;
  padding: 0 6px;
}

.barra-superior > :first-child {
  width: 52%;
}

.barra-superior > :last-child {
  width: 28%;
  margin-right: 10%;
}

/* Separadores */
.separador {
  width: 100%;
  height: 1px;
  flex-shrink: 0;
  background-color: #555555;
}

/* Accesos rápidos */
.accesos {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4px 0;
}

/* Aviso */
.aviso {
  width: 100%;
}

/* Contenido principal */
.contenido {
  display: grid;
  grid-template-columns: 76px minmax(0, 1fr);
  gap: 16px;
  flex: 1;
  min-height: 500px;
  align-items: stretch;
}

/* Menú lateral */
.menu-lateral {
  width: 76px;
  min-width: 76px;
  min-height: 100%;
  position: relative;
  z-index: 1;
}

.menu-lateral .contenedor-SideBar {
  width: 100%;
  height: 100%;
  min-height: 100%;
  margin: 0;
  padding: 18px 8px;
  gap: 28px;
  justify-content: flex-start;
  align-items: center;
}

/* Área principal */
.area-principal {
  width: 100%;
  min-width: 0;
  min-height: 100%;
  background-color: #d6d6d6;
  border-radius: 12px;
  padding: 20px;
  overflow: auto;
  position: relative;
  z-index: 0;
}

/* Tarjeta de calificaciones */
.area-principal .card {
  width: 100%;
  max-width: none;
  height: 100%;
  min-height: 100%;
  margin: 0;
  display: flex;
  flex-direction: column;
}

.area-principal .card-header {
  flex-shrink: 0;
}

.area-principal .card-body {
  flex: 1;
}

.area-principal .card-footer {
  flex-shrink: 0;
}

/* Pantallas medianas */
@media (max-width: 900px) {
  .dashboard {
    width: 97%;
    padding: 12px;
  }

  .barra-superior > :first-child {
    width: 55%;
  }

  .barra-superior > :last-child {
    width: 35%;
    margin-right: 0;
  }
}

/* Pantallas pequeñas */
@media (max-width: 600px) {
  .dashboard {
    width: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 10px;
  }

  .barra-superior {
    flex-wrap: wrap;
    gap: 12px;
  }

  .barra-superior > :first-child,
  .barra-superior > :last-child {
    width: 100%;
  }

  .contenido {
    grid-template-columns: 60px minmax(0, 1fr);
    gap: 10px;
    min-height: 400px;
  }

  .menu-lateral {
    width: 60px;
    min-width: 60px;
  }

  .menu-lateral .contenedor-SideBar {
    padding: 12px 4px;
    gap: 20px;
  }

  .area-principal {
    padding: 10px;
  }
}
</style>
