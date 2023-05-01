<script setup lang="ts">
</script>

<script lang="ts">
export default {

  data(){
    return{
      itensList:[
        {
          id: 1,
          name: "Placa de Video",
          valor: "13",
        },
        {
          id: 2,
          name: "Monitor", 
          valor: "11",  
        },
        {
          id: 4,
          name: "PC", 
          valor: "150",  
        },
        {
          id: 12,
          name: "Mother-Board", 
          valor: "30",  
        }
      ],
      itemSearch: ""
    }
  },
  methods:{
    add(){
      const body = {
        id: Math.random(),
        name: this.itemSearch,
        valor: "13"
      }
      this.itensList.push(body)
    }
  },
  watch:{
    
  }

}
</script>

<template>
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
        placeholder="Coloque aqui seu item" 
        class="searchBar"
        v-model="itemSearch"
      >
      <button class="btn" @click="add()">Adicionar Item</button>
      <button class="btn">Remover Item</button>
    </div>
    <div class="bodyList">
      <table style="color: black;">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Valor</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="list in itensList">
            <td>{{list.id}}</td>
            <td>{{list.name}}</td>
            <td>{{list.valor}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.greenBack{
  width: 100vw;
  height: 400px;
  background-color: #10393B;
  display: flex;
  justify-content: center;
  align-items: center;
}
.witheBack{
  width: 100vw;
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
.titleCard{
  color: white;
  width: 90%;
  margin: 0;
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

.searchBar{
  margin: 0 20px 0 0;
  width: 20%;
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
</style>
