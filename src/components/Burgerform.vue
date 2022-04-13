<template>
  <div id="todo-form">
      <Message :msg="msg" v-show="msg" />
      <div>
          <form id="burger-fom" @submit="createBurger">
              <div class="input-container">
                  <label for="nome">Client name:</label>
                  <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">     
              </div>
              <div class="input-container">
                  <label for="pao">Choose your bread:</label>
                  <select name="pao" id="pao" v-model="pao">
                      <option value="">Select your bread</option>
                      <option v-for="pao in breads" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                  </select>
              </div>

              <div class="input-container">
                  <label for="carne">Choose meet for your burger:</label>
                  <select name="carne" id="carne" v-model="carne">
                      <option value="">Select type of meat</option>
                      <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                  </select>
              </div>
              <div id="opcionais-container" class="input-container">
        <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
        <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
          <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
          <span>{{ opcional.tipo }}</span>
        </div>
      </div>
              <div class="input-container">
                  <input type="submit" class="submit-btn" value="Make Burger">
              </div>
          </form>
      </div>
  </div>
</template>

<script>
import Message from "./Message.vue"
export default {
    name:"BurgerForm",
    components:{
        Message,
    },
    data(){
        return {
            breads: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null

        }
    },
    methods:{
        // GET INFREDIENTES
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            
            // console.log(data);
            // console.log(data.opcionais);
            this.breads = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },

        // POST CREATE BURGER
        async createBurger(e){
            e.preventDefault();
            const data = {
                nome : this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }
            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers",{
                method: "POST",
                headers: { "Content-Type" : "application/json" },
                body: dataJson
            });
            const res = await req.json();
            // console.log(res);
            this.msg = `Pedido N.${res.id} Enviado com Successo`;

            // apos 3min depois de enviar o pedido a msg apaga
            setTimeout(() => this.msg = "", 3000);
            
            // CLEAR 
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";
        }
            
    },
    mounted(){
        this.getIngredientes();
    }
}
</script>

<style scoped>
    #burger-form{
        max-width: 400px;
        margin: 0 auto;
        align-content: center;
        display: inline-block;
    }
    #todo-form{
        margin: 0 auto;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
        align-items: center;
        /* margin-left: center; */
    }
    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 6px 10px;
        border-left: 4px solid #FCBA03;
        
    }
    input,select{
        padding: 5px 10px;
        width: 300px;
    }
    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;     
    }
    #opcionais-title{
        width: 100%;
        align-content: center;
    }

    .checkbox-container{
        display:flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
        /* height: 900px; */
    }
    .checkbox-container span,
    .checkbox-container input{
        width: auto;
        align-items: center;
    }
    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }
    .submit-btn{
        background-color: darkgreen;
        color: #fff;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: auto;
        cursor: pointer;
        transition: .5s;
        border-radius: 10px;
    }
    .submit-btn:hover{
        background-color: transparent;
        color: darkgreen;
        border: 4px solid;
    }
        
        
</style>