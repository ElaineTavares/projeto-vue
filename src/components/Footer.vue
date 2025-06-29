<template>
  <div id="footer">
    <p>Hora do Almoço! &copy; 2025</p>
    <h3>Desenvolvido por Elaine Tavares</h3>
  </div>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style scoped>
  #footer {
    height: 200px;
    background-color: rgba(85, 157, 109, 1);
    border-top: 4px solid rgba(85, 157, 109, 1);
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
    gap: 20px;
  }
</style>