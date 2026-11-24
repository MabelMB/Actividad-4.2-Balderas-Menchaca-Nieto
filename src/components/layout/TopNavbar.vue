<template>
  <div class="contenedor-TopBar">
    <img class="img" src="../../assets/Perfil.png" alt="Imagen de perfil">
    <img class="img" src="../../assets/Engranaje.png" alt="Imagen de engranaje">
    <img class="img" src="../../assets/Campana.png" alt="Imagen de campana">
  </div>>   
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

.img{
    width: 28px;
}

</style>
