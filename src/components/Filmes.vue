<template>
  <div id="filmes" class="container">
    <b-row>
      <b-col>
      <h2 id="enc"> Filmes Encontrados </h2>
      </b-col>
    </b-row>
    <b-row>
     
      <b-col align="center" >
      <b-button variant="outline-primary" @click="mostrarCarrinho"> Carrinho: {{ quantidadeCarrinho}} filmes</b-button>
      </b-col>
    </b-row>

  <div class="cards">
  <b-row v-if="mostrarFilmes"> 

    <b-col v-for="filme in filmes" v-bind:key="filme">
      <b-card  style="width:14rem" 
      :title="filme.titulo"
      :id="filme.id"
      :img-src="filme.imagem"
      img-top
      img-alt="Poster"
      
      tag = "article"
      class="mb-2"
      >
        <b-card-text > {{filme.descricao}} </b-card-text>
        <b-card-text> {{filme.valor|formatarPreco("R$")}} </b-card-text>
         <b-button variant="outline-primary">
          <a href="#" class="card-link" @click="adicionarCarrinho(filme)" v-if="validarPermissaoParaAdicionar(filme)">Alugar</a>
          <a href="#" class="card-link" @click="adicionarCarrinho(filme)" v-else type="disabled">Alugar</a>
          </b-button>
      </b-card>
    </b-col>
  
    
  </b-row>
  <b-row v-else>
    <h2> Carrinho </h2>
  </b-row>
  </div>

    
  </div>
</template>

<script>
export default {
  name: 'Filmes',
  data:function (){
    return{
      mostrarFilmes:true,
      filmes: 
        [ {id:1, titulo: "Vingadores", descricao:"Um filme de heróis", valor:25, imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27141726%27&EntityType=%27Item%27&EntityId=%273863%27&Width=1080&Height=1600&device=web_browser&subscriptions=Anonymous",estoqueDisp: 3},
          {id:2, titulo: "Vingadores 2 ", descricao:"Um filme de heróis", valor:25,imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/2/22/OsVingadores2.jpg/250px-OsVingadores2.jpg",estoqueDisp:7},
          {id:3, titulo: "Pantera Negra", descricao:"Um filme de heróis", valor:25,imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27182460%27&EntityType=%27Item%27&EntityId=%2710148%27&Width=720&Height=1080&device=web_browser&subscriptions=Anonymous",estoqueDisp: 34},
          {id:4, titulo: "Capitã Marvel", descricao:"Um filme de heróis", valor:25, imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/5/59/Captain_Marvel_%282018%29.jpg/250px-Captain_Marvel_%282018%29.jpg",estoqueDisp: 4},
          {id:5, titulo: "Brightburn", descricao:"Um filme de heróis", valor:25, imagem:"https://s2.glbimg.com/ymb71yQSk38YMYeoe0717NTTisk=/e.glbimg.com/og/ed/f/original/2019/05/21/brightburn_regposter_brazil.jpg",estoqueDisp: 8}
        ],
        carrinho:[]
      
    }
  },
  methods : {
    adicionarCarrinho: function (filme){
      this.carrinho.push(filme.id);
    },
    quantidadeNoCarrinhoPorFilme: function (filme){
      var quantidade = 0;
      for(var i=0;i<this.carrinho.length; i++){
        if (filme.id==this.carrinho[i]){
          quantidade++;
        }
      }
      return quantidade;
    },
    validarPermissaoParaAdicionar: function(filme){
      return filme.estoqueDisp > this.quantidadeNoCarrinhoPorFilme(filme);
    },
    mostrarCarrinho(){
      this.mostrarFilmes = this.mostrarFilmes ? false:true;
    }
  },
  computed: {
    quantidadeCarrinho: function(){
      return this.carrinho.length;
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


a {
  color: #42b983;
}

.card{
  display: flex;
  justify-content: center;
  align-content: space-around;
  text-align:center;
  margin-top:2%;
}
#enc{
  margin-top: 2%;
  text-align: center
}

#cards{
  display:flex;
  justify-content: space-around;;

}

</style>
