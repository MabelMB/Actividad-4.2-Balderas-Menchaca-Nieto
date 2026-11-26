<template>
  <div class="contenedor-TopBar">
    <button class="button"> <img class="img" src="../../assets/Perfil.png" alt="Imagen de perfil"></button>
    <button class="button"><img class="img" src="../../assets/Engranaje.png" alt="Imagen de engranaje"></button>
    <button class="button"><img class="img" src="../../assets/Campana.png" alt="Imagen de campana"></button>
  </div>  
</template>

<style scoped>

.contenedor-TopBar{
    width: 100%; 
    display: flex; 
    background-color: #D6D6D6; 
    align-items: center; 
    justify-content: space-between;
    box-sizing: border-box;
    gap: 12px;
    padding: 10px 16px;
    border-radius: 12px;
    box-shadow: 0 5px 20px -8px rgba(0, 0, 0, 0.50);
}

.button {
  background-color: transparent;
  border: none;
  padding: 4px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
}

.button:active {
  transform: scale(0.96);
}

.button:hover .img {
  filter: grayscale(70%) brightness(0.75);
}

.img {
  width: 28px;
  height: auto;
  display: block;
}

</style>
