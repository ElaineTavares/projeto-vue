<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Faça o seu pedido!😋</h1>
      <Formulario />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner'
import Formulario from '../components/Formulario'

export default {
  name: 'Home',
  components: {
    Banner,
    Formulario
  }
}
</script>