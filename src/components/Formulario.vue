<template>
  <div>
      <Message :msg="msg" v-show="msg" />
      <div>
        <form id="formulario" method="POST" @submit="pedir">
          <div class="input-container">
            <label for="nome">Nome do cliente:</label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
          </div>
          <div class="input-container">
            <label for="massa">Escolha a massa:</label>
            <select name="massa" id="massa" v-model="massa">
              <option value="">Selecione a sua massa</option>
              <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">{{ massa.tipo }}</option>
            </select>
          </div>
          <div class="input-container">
            <label for="carne">Escolha a carne para a sua massa:</label>
            <select name="carne" id="carne" v-model="carne">
              <option value="">Selecione o tipo de carne</option>
              <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
            </select>
          </div>
          <div id="molhos-container" class="input-container">
            <label id="molhos-title" for="molhos">Selecione o molho:</label>
            <select name="molho" id="molho" v-model="molho">
              <option value="">Selecione o molho para a sua massa</option>
              <option v-for="molho in molhos" :key="molho.id" :value="molho.tipo">{{ molho.tipo }}</option>
            </select>
          </div>
          <div class="input-container btn-container">
            <input class="submit-btn" type="submit" value="Pedir!">
          </div>
        </form>
      </div>
  </div>

</template>

<script>
import Message from './Message'

export default {
  name: "Formulario",
  data() {
    return {
      nome: null,
      massa: null,
      carne: null,
      molho: null,
      status: "Solicitado",
      msg: null,
      pedidos: [],
      
      massas: [
      { id: 1, tipo: "Espaguete" },
      { id: 2, tipo: "Fettuccine" },
      { id: 3, tipo: "Penne" },
      { id: 4, tipo: "Ravioli" },
      { id: 5, tipo: "Nhoque de batata" },
      { id: 6, tipo: "Talharim" },
      { id: 7, tipo: "Canelone" },
      { id: 8, tipo: "Lasanha" },
      { id: 9, tipo: "Fusilli" },
      { id: 10, tipo: "Capeletti" }
    ],
    carnes: [
      { id: 1, tipo: "Maminha" },
      { id: 2, tipo: "Alcatra" },
      { id: 3, tipo: "Picanha" },
      { id: 4, tipo: "Veggie burger" },
      { id: 5, tipo: "Frango grelhado" },
      { id: 6, tipo: "Carne moída" },
      { id: 7, tipo: "Bacon crocante" },
      { id: 8, tipo: "Costela desfiada" },
      { id: 9, tipo: "Frango empanado" },
      { id: 10, tipo: "Lombo suíno" }
    ],
    molhos: [
      { id: 1, tipo: "Molho ao Sugo" },
      { id: 2, tipo: "Molho Pesto" },
      { id: 3, tipo: "Molho Branco" },
      { id: 4, tipo: "Molho Bolonhesa" },
      { id: 5, tipo: "Molho Alfredo" },
      { id: 6, tipo: "Molho Quatro Queijos" },
      { id: 7, tipo: "Molho Funghi" },
      { id: 8, tipo: "Molho Carbonara" },
      { id: 9, tipo: "Molho Rosé" },
      { id: 10, tipo: "Molho de Gorgonzola" }
    ]
    }
  },

  
  methods: {
    pedir(e) {
    e.preventDefault();
    const novoId = new Date().getTime(); // Gera um ID único com base no tempo

  const novoPedido = {
    id: novoId,
    nome: this.nome,
    carne: this.carne,
    massa: this.massa,
    molho: this.molho,
    status: "Solicitado"
  };

  console.log(this.novoPedido)

  // Pega os pedidos já salvos (ou array vazio)
  const pedidos = JSON.parse(localStorage.getItem('pedidos')) || [];

  // Adiciona o novo
  pedidos.push(novoPedido);

  // Salva de volta
  localStorage.setItem('pedidos', JSON.stringify(pedidos));

  this.msg = "Pedido realizado com sucesso!";

  // limpar campos
  this.nome = "";
  this.carne = "";
  this.massa = "";
  this.molho = "";

  setTimeout(() => this.msg = "", 3000);
}
},


  components: {
    Message
  }
}
</script>

<style scoped>
  #formulario {
    max-width: 400px;
    margin: 0 auto;
    display: flex;
    flex-flow: column;
    align-items: center;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #molhos-title {
    width: 100%;
  }


  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>