<template>
    <div>
        <msg  :msg="msg" v-show="msg" :msgBAD="msgBAD"/>
        <div>
            <form @submit="CreateAcai($event)" id="acaiForm">
                <div class="input-container">
                    <label for="name">Nome do cliente</label>
                    <input type="text" name="name" v-model="nome" placeholder="Digite seu nome:">
                </div>

                <div class="input-container">
                    <label for="batidas">Escolha a batida do seu açai</label>
                    <select name="batidas" id="batidas" v-model="batida">
                            <option value="">Selecione a sua batida:</option>
                            <option v-for="batida in batidas" :key="batida.id" :value="batida.tipo">{{ batida.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="tamanho">Escolha o tamanho do seu açai</label>
                    <select name="tamanho" id="tamanho" v-model="tamanho">
                        <option>Selecione o tamanho</option>
                        <option v-for="tamanho in tamanhos" :key="tamanho.id" :value="tamanho.qntd">{{ tamanho.qntd }}</option>
                    </select>
                </div>

                <div id="opcionais-container" class="input-container">
                    <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
                    <div v-for="opcs in opcionaisBD" :key="opcs.id" class="checkbox-container">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" :value="opcs.tipo">
                        <span>{{ opcs.tipo }}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Montar seu açai!">
                </div>
            </form>
        </div>
    </div>
  
</template>

<script>
import msg from '../components/msg.vue'
export default {
    name: 'FormPed',

    data(){
        return{
            batidas: null,
            tamanhos:null,
            opcionaisBD: null,
            nome: null,
            batida: null,
            tamanho: null,
            opcionais: [],
            msg: null,
            msgBAD: false
        }
    },

    components: {
        msg
    },

    methods: {
        async getIngredientes(){
            const req = await fetch('http://localhost:3000/ingredientes')
            const ingredientes = await req.json()
            console.log(ingredientes)
            this.batidas = ingredientes.batidas
            this.tamanhos = ingredientes.tamanhos
            this.opcionaisBD = ingredientes.opcionais
        },
        
        async CreateAcai($event){
           $event.preventDefault()
           

         if(this.nome == '' || this.nome == null || this.batida == '' || this.batida == null || this.tamanho == '' || this.tamanho == null){

            this.msgBAD = true
            this.msg = 'Preencha todos os campos'
            setTimeout(()=> location.reload(), 1000)
            

         }else{
                    const data = {
                        nome: this.nome,
                        batida: this.batida,
                        tamanho: this.tamanho,
                        opcionais: Array.from(this.opcionais),
                        status: 'Solicitado' 
                    }
      
                this.msgBAD = false
                const dataJson = JSON.stringify(data)
                const req = await fetch("http://localhost:3000/Acais", {
                    method: "POST",
                    headers: { "Content-Type" : "application/json" },
                    body: dataJson
                });

                this.msg = 'O pedido foi realizado com sucesso'

                setTimeout(()=> location.reload(), 1000)
                // setTimeout(()=> this.msg = '', 3000);

                this.nome = ''
                this.batida = ''
                this.tamanho = ''
                this.opcionais = ''
                console.log(opcionais + tamanho)

          } 
         

        }
    },

    mounted(){
        this.getIngredientes()
    }
       
    
}
</script>

<style scoped>

#acaiForm {
    /* QUANDO A DIV TEM WIDTH FIXA VOCE PODE CENTRALIZAR COM MARGIN 0 AUTO */
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

.input-container label {
    font-weight: bold;
    margin-bottom: 15px;
    padding: 5px 10px;
    color: #222;
    border-left: solid 4px rgb(224, 69, 69);;
}

input, select{
    padding: 5px 10px;
    width: 300px;
    border: 1px solid black;
}

#opcionais-container{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}
#opcionais-title{
    width: 100%;
   
}

.checkbox-container{
    width: 50%;
    display: flex;
    justify-content: flex-start;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
    
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
    background-color: #222;
    color: rgb(224, 69, 69);;
    font-weight: bold;
    border: 2px solid #111;
    padding: 10px;
    font-size: 1rem;
    cursor: pointer;
    margin: 0 auto;
    transition: .5s;
}

.submit-btn:hover{
    background-color: transparent;
    color: #222;
}

@media screen and (max-width: 600px){
    
}

</style>