<template>
  <div class="hello">
    <h1>Bem vindo a {{ Title }}</h1>

    <router-link
        active-class="active"
         tag="button"
         class="btn btn-primary btn-lg"
         :to="{name:'home'}"
       >Home</router-link>
       <router-link
         active-class="active"
         type="button"
         class="btn btn-primary btn-lg"
         style="margin-left:10px"
         :to="{name:'carrinho'}"
       >Carrinho: {{ quantidadeCarrinho }} filmes</router-link>
       
       

    <!-- Diretivas condicionais, pode-se mudar formatação de estilos--> 
    <h3 id="aberta" v-if="horas>=7 && horas<17"> Aberta </h3>
    <h3 id="quase" v-else-if="horas>= 17 && horas<18"> Perto de fechar </h3>
    <h3 id="fechada" v-else> Fechada </h3>

    


  </div>
</template>

<script>

export default {
  name: 'Header',
  props:{
    quantidadeCarrinho:Number
  },
  data: function (){
    return{
    Title:"Locadora de Filmes",
    horas : new Date().getHours(),
    minutos: new Date().getMinutes(),
    segundos: new Date().getSeconds()
    }
  },
  methods:{
    mostrarCarrinho(){
      this.$router.push({name:'carrinho'});
    },
    mostrarHome(){
      this.$router.push({name:'home'});
    }
  }
        
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  text-align: center;
  margin-top: 2%;
  color: black;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#aberta{
  color:blue;
  text-align: center;
  margin-top: 2%;
}
#fechada{
  color:red;
  text-align: center;
  margin-top: 2%;
}

#quase{
  color:orange;
  text-align: center;
  margin-top: 2%;
}




</style>
