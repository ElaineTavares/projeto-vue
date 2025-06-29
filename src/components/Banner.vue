<template>
  <div id="main-banner">
    <h1>Hora do Almoço!😋</h1>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>

  #main-banner {
    background-image: url('/img/refeicao_saudavel.jpg');
    background-position: center;
    background-size: cover;
    width: 100%;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }

  #main-banner h1 {
    color: #FFF;
    text-align: center;
    font-size: 60px;
    background-color: rgba(85, 157, 109, 1);
    padding: 20px 40px;
  }

</style>