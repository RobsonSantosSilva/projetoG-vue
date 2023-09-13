<template>
  <div class="home">
    <button @click="somaUm">Somar</button> 
    <button @click="subtraiUm">Subtrair</button> <br> <br>

    <input v-model="valor"> <br>
    <img src="../assets/logo.png" alt="Imagem" v-if="estaCerto"><br><br><br>

    <h1>{{titulo}}</h1>
    <input type="text" v-model="titulo">

    <h1 v-for="n in 10" :key="n">{{n}}</h1>
  </div>
</template>


<script>
// @ is an alias to /src

export default {
  data(){
    return {
      valor: 0,
      estaCerto: false,
      titulo: 'Insira o título aqui'
    }
  },

  methods: {
    somaUm(){
      this.valor++;
      this.atualizaCerto()
    },
    subtraiUm(){
      this.valor--;
      this.atualizaCerto()
    },
    atualizaCerto(){
      this.estaCerto = this.valor > 10;
    }
  }
}

</script>
