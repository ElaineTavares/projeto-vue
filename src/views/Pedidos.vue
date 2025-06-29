<template>
  <div class="corpo">
    <h1>Gerenciar Pedidos:</h1>
    <p v-show="msg" class="msg">{{ msg }}</p>
    <div v-if="pedidos.length > 0">
      <div>
        <div id="cabecalho">
          <div>Cliente:</div>
          <div>Massa:</div>
          <div>Carne:</div>
          <div>Molhos:</div>
          <div>Status:</div>
        </div>
      </div>
      <div v-for="(pedido, index) in pedidos" :key="index" id="cabecalho" class="dados">
        <div>
          <p>{{ pedido.nome }}</p>
        </div>
        <div>
          <p>{{ pedido.massa }}</p>
        </div>
        <div>
          <p>{{ pedido.carne }}</p>
        </div>
        <div>
          <p>{{ pedido.molho }}</p>
        </div> 
        <div class="botoes">
          <select v-model="pedido.status" @change="salvarPedidos">
            <option value="">Selecione</option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="pedido.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button @click="deletarPedido(pedido.id)" class="delete-btn">Remover</button>
        </div> 
      </div> 
    </div>
   
    <p v-else class="sem-pedido">{{ semPedido }}</p>
    
  </div>
</template>


<script>
export default {
  name: 'Pedidos',
  data() {
    return {
      semPedido: "Nenhum Pedido.",
      msg: "",
      pedidos: [],
      status: [
        { id: 1, tipo: "Solicitado" },
        { id: 2, tipo: "Em produção" },
        { id: 3, tipo: "Finalizado" }
      ]
    };
  },

  mounted() {
    const pedidosSalvos = localStorage.getItem('pedidos');
    if (pedidosSalvos) {
      this.pedidos = JSON.parse(pedidosSalvos).reverse(); //inverte a ordem
    }
  },

  methods: {
    deletarPedido(id) {
       // Perguntar ao usuário se ele realmente deseja remover
      const confirmacao = confirm("Realmente deseja remover o pedido?");
      
      if (!confirmacao) {
        return; // Sai da função se o usuário cancelar
      }

      // Encontrar o índice do pedido com base no id
      const index = this.pedidos.findIndex(pedido => pedido.id === id);

      // Se o pedido for encontrado, remova ele do array
      if (index !== -1) {
        this.pedidos.splice(index, 1); // Remove 1 item no índice encontrado
      }

      // Atualizar o localStorage com a lista de pedidos atualizada
      localStorage.setItem('pedidos', JSON.stringify(this.pedidos));

      this.msg = "Pedido removido com sucesso!";

      setTimeout(() => {
        this.msg = "";
      }, 3000);
    },

    salvarPedidos() {
      // Atualiza o localStorage sempre que o status for alterado
      localStorage.setItem('pedidos', JSON.stringify(this.pedidos));
    }
  }
};
</script>

<style scoped>
  #cabecalho {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
    display: flex;
    flex-wrap: wrap;  
  }


  #cabecalho div
   {
    width: 19%;
  }

  h1{
    margin-top: 50px;
  }

  .botoes{
    display: flex;
    flex-flow: wrap;
    justify-content: center;
    align-items: center;
    gap: 20px; 
  }

  select {
    padding-block: 12px;
    cursor: pointer;
    width: 100px;
    text-align: center;
  }

  
  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 12px 16px;
    width: 100px;
    font-size: 16px;
    /* margin: 0 auto; */
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }

  .dados{
    font-weight: 300 !important;
  }

  .sem-pedido{
    color: red;
    text-align: center;
    font-size: 22px;
    padding: 30px;
  }

  .msg {
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
    text-align: center;
  }

  .corpo{
    min-height: 60vh;
  }
  
</style>
