<script setup lang="ts">
import axios from 'axios';
</script>

<script lang="ts">
export default {

  data(){
    return{
      itensList:[],
      itemSearch: "",
      itemNumber: ""
    }
  },
  methods:{
    async getList() {
      const options = {
        method: 'GET',
        url: 'http://localhost:8002/notes/',
      };

      const data = await axios.request(options).then(function (response) {
        console.log("Response da api",response.data)
        let resposta = response.data;
        return resposta;
      }).catch( (error)=> {
        console.error(error);
        return []
      });

      this.itensList = data
    },
    async addItem(){
      const options = {
        method: 'POST',
        url: 'http://localhost:8002/notes/',
        headers: {'Content-Type': 'application/json'},
        data: JSON.stringify({title: this.itemSearch, description: this.itemNumber})
      };

      axios.request(options).then(function (response) {
        console.log(response.data);
      }).catch(function (error) {
        console.error(error);
      });

      this.getList()
    },
    delItem(list){
      const options = {
        method: 'DELETE',
        url: 'http://localhost:8002/notes/'+ list.id,
        headers: {'Content-Type': 'application/json'}
      };

      axios.request(options).then(function (response) {
        console.log(response.data);
      }).catch(function (error) {
        console.error(error);
      });

      this.getList()
    }

  },
  created(){
    this.getList()
  }

}
</script>

<template>
  <div style="height: 100vh; width: 100vw;">
    <div class="greenBack">
      <div class="leftSide">
          <div class="titlePrev">Promoções</div>
          <h1 class="titleCard">Loja de Eletrônicos</h1>
          <div class="titleLegend">Se a sua vida for a melhor coisa que já te aconteceu, acredite, você tem mais sorte do que pode imaginar.</div>
        </div>
      <div class="rightSide">
        <img src="../src/assets/images/pcGamer.png" class="img">
      </div>    
    </div>
    <div class="witheBack">
      <div class="headList">
        <input 
          type="text" 
          placeholder="Coloque o nome do item" 
          class="nameBar"
          v-model="itemSearch"
        >
        <input 
          type="text" 
          placeholder="Coloque o valor" 
          class="valueBar"
          v-model="itemNumber"
        >
        <button class="btn" @click="addItem()">Adicionar Item</button>
      </div>
      <div class="bodyList">
        <table style="color: black; border: 1px;" >
          <thead>
            <tr>
              <th>ID</th>
              <th>Nome</th>
              <th>Valor</th>
              <th>Ação</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="list in itensList">
              <td>{{list?.id}}</td>
              <td>{{list?.title}}</td>
              <td>{{list?.description}}</td>
              <td>
                <span class="material-icons-outlined" @click="delItem(list)">delete</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
.greenBack{
  width: 100%;
  height: 50%;
  background-color: #10393B;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px;
}
.witheBack{
  width: 100%;
  min-height: 400px;
  height: 100%;
  background-color: white;
}
.rightSide{
  width: 40%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.leftSide{
  width: 40%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap:10px;
}
.img{
  width: 70%;
}
.titleCard {
  color: #fff;
  margin: 0;
  font-size: 60px;
  text-shadow:
    /* brilho branco */
  0 0 7px #fff,
  0 0 10px #fff,
  0 0 21px #fff,
    /* brilho verde */
  0 0 32px #0fa,
  0 0 62px #0fa,
  0 0 52px #0fa,
  0 0 72px #0fa,
  0 0 81px #0fa;

  animation: flicker 1.5s infinite alternate;
}

 /* Configuração do efeito */
@keyframes flicker {
    
    0%, 18%, 22%, 25%, 53%, 57%, 100% {
  
        text-shadow:
        0 0 4px #fff,
        0 0 11px #fff,
        0 0 19px #fff,
        0 0 40px #0fa,
        0 0 80px #0fa,
        0 0 90px #0fa,
        0 0 100px #0fa,
        0 0 150px #0fa;
    
    }
    
    20%, 24%, 55% {        
        text-shadow: none;
    }    
  }
.titlePrev{
  color: rgb(180, 141, 10);
  width: 50%;
}
.titleLegend{
  color: rgb(230, 226, 216);
  width: 50%;
  text-align: left;
}

.nameBar{
  margin: 0 20px 0 0;
  width: 20%;
  height: 30px;
  background-color: white;
  color: black;
}
.valueBar{
  margin: 0 20px 0 0;
  width: 10%;
  height: 30px;
  background-color: white;
  color: black;
}

.headList{
  padding-top: 20px;
}
.btn{
  height: 35px;
  margin-left: 5px;
}
.bodyList{
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 20px 0 0 0;
}

table, th, td {
border: 1px solid black;
}

table {
border-collapse: collapse;
margin: auto;
}

th, td{
padding: 10px;
text-align: center;
width: 120px;
}

th{
font-weight: bold;
}

tr:nth-child(even) {
background-color: #DCEBE6;
}
.material-icons-outlined{
  color: rgb(202, 65, 65);
}
.material-icons-outlined:hover{
  color: rgb(202, 65, 65);
  cursor: pointer;
}
</style>
