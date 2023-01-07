<template>
  <msg :msg="msg" v-show="msg" />
  <div id="acai-tab">
    <div id="acai-tab-heading">
      <div class="order-id">#</div>
      <div>Cliente:</div>
      <div>Batida:</div>
      <div>Tamanho:</div>
      <div>Opcionais</div>
      <div>Ações</div>
    </div>
  </div>
  <div id="acai-rows">
      <div class="acai-row" v-for="acai in acais" :key="acai.id">
        <div class="order-number">{{ acai.id }}</div>
        <div>{{acai.nome}}</div>
        <div>{{acai.batida}}</div>
        <div>{{acai.tamanho}}</div>
        <div>
          <ul>
            <li v-for="opcional, index in acai.opcionais" :key="index">{{ opcional }}</li>
            
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updateAcai($event, acai.id)">
              <option v-for="stts in status" :key="stts.id" :value="stts.tipo" :selected="acai.status == stts.tipo">{{ stts.tipo }}</option>
          </select>
          <button @click="deleteAcai(acai.id)" class="deleteBTN">Cancelar</button>
        </div>
      </div>
  </div>
</template>



<script>
import msg from './msg.vue'
export default {
    name: 'Dashboard',

    data(){
      return{
        acais: null,
        acai_id: null,
        status: [],
        msg: null
      }
    },

    components:{
      msg
    },

    methods: {
      async getPedidos(){
            const req = await fetch('http://localhost:3000/Acais')
            const pedidos = await req.json()
            this.acais = pedidos
            this.getStatus()
            
        },
      async getStatus(){
            const req = await fetch('http://localhost:3000/status')
            const status = await req.json()
            this.status = status
      },
      
      async deleteAcai(id){
        const req = await fetch(`http://localhost:3000/acais/${id}`, {
          method: "DELETE"
        });

        const res = await req.json()
        this.msg = 'Pedido removido com sucesso'
        setTimeout(()=> this.msg = '', 2000);
        this.getPedidos()
      },

      async updateAcai(event, id){
        const option = event.target.value;
        const dataJson = JSON.stringify({status: option});

            const req = await fetch(`http://localhost:3000/acais/${id}`, {
              method: "PATCH",
              headers: { "Content-Type" : "application/json" },
              body: dataJson
            });

            const req2 = await fetch(`http://localhost:3000/acais/${id}`)
            const nomeCliente = await req2.json()


            this.msg = `O pedido do cliente do cliente ${nomeCliente.nome} está ${option}!`
            setTimeout(()=> this.msg = '', 2000);
           
      }
    },

    mounted(){
      this.getPedidos()
      
    }
     
    
}
</script>

<style scoped>
  #acai-tab{
    max-width: 1200px;
    margin: 0 auto;
  }

  #acai-tab-heading, #acai-rows, .acai-row{
    display: flex;
    flex-wrap: wrap;
  }

  #acai-tab-heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }
 
  .acai-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }
  #acai-tab-heading div,
  .acai-row div {
    width: 19%;
  }
  #acai-tab-heading .order-id,
  .acai-row .order-number {
    width: 5%;
  }
  select {
    padding: 12px 6px;
    margin-right: 12px;
  }
  .deleteBTN {
    background-color: #222;
    color:rgb(224, 69, 69);
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .deleteBTN:hover {
    background-color: transparent;
    color: #222;
  }
</style>

