<template>
  <div id="filmes" class="container">
    <Header :quantidadeCarrinho="quantidadeCarrinho"/>
    <b-row>

    </b-row>
   
      <div class="row">
     <div class="col">
       <h2>Filmes encontrados</h2>
       
     </div>
     </div>
      
    

  <div class="cards">
  <b-row v-if="mostrarFilmes"> 

    <b-col v-for="filme in filmes" v-bind:key="filme">
      <b-card  style="width:14rem" 
     
      :id="filme.id"
      :img-src="filme.imagem"
      img-top
      img-alt="Poster"
      tag = "article"
      class="mb-2"
      >

      <b-card-text>
        <router-link
              tag='h5'
              class="card-title"
              :to="{name:'filme', params:{id:filme.id}}">{{filme.titulo}}
        </router-link>
      </b-card-text>

        <span class="mensagem-estoque"
          v-if="filme.estoqueDisp-quantidadeNoCarrinhoPorFilme(filme)==0">
            Indisponível
        </span>

        <span class="mensagem-estoque"
          v-else-if="filme.estoqueDisp-quantidadeNoCarrinhoPorFilme(filme)<=5">
            Apenas {{filme.estoqueDisp - quantidadeNoCarrinhoPorFilme(filme)}} itens no estoque
        </span>

        <span class="mensagem-estoque"
          v-else>
            Alugue Agora
        </span>
        
        <b-card-text > {{filme.descricao}} </b-card-text>
        <b-card-text> {{filme.valor|formatarPreco("R$")}} </b-card-text>

         <div class="avaliacao">
              <span v-for="n in 5" :key="n"
                v-bind:class="{'avaliacao-active': checarAvaliacao(n,filme)}">
                <img src="../assets/star.jpg" height="20"/>
              </span>
         </div>

         
          <a href="#" 
          class="btn btn-primary" 
          @click="adicionarCarrinho(filme)" 
          v-if="validarPermissaoParaAdicionar(filme)">Alugar</a>
          <a href="#" 
          v-else
          class="btn btn-primary disabled"  
          >Alugar</a>
          
          
      </b-card>
    </b-col>
  
    
  </b-row>
 
  </div>
  </div>
</template>

<script>
import Header from './Header';
export default {
  name: 'Home',
  components:{
    Header
  },
  data:function (){
    return{
      mostrarFilmes:true,
      filmes: 
        [ {id:1, titulo: "Vingadores", descricao:"Um filme de heróis", valor:25, imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27141726%27&EntityType=%27Item%27&EntityId=%273863%27&Width=1080&Height=1600&device=web_browser&subscriptions=Anonymous",estoqueDisp: 3,avaliacao:3},
          {id:2, titulo: "Vingadores 2 ", descricao:"Um filme de heróis", valor:25,imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/2/22/OsVingadores2.jpg/250px-OsVingadores2.jpg",estoqueDisp:7},
          {id:3, titulo: "Pantera Negra", descricao:"Um filme de heróis", valor:25,imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27182460%27&EntityType=%27Item%27&EntityId=%2710148%27&Width=720&Height=1080&device=web_browser&subscriptions=Anonymous",estoqueDisp: 34,avaliacao:2},
          {id:4, titulo: "Capitã Marvel", descricao:"Um filme de heróis", valor:25, imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/5/59/Captain_Marvel_%282018%29.jpg/250px-Captain_Marvel_%282018%29.jpg",estoqueDisp: 4,avaliacao:1},
          {id:5, titulo: "Brightburn", descricao:"Um filme de heróis", valor:25, imagem:"https://s2.glbimg.com/ymb71yQSk38YMYeoe0717NTTisk=/e.glbimg.com/og/ed/f/original/2019/05/21/brightburn_regposter_brazil.jpg",estoqueDisp: 8,avaliacao:2}
        ],
        carrinho:[],
      pedido:{
        primeiroN:"",
        segundoN:"",
        endereco:"",
        cidade:"",
        estado:"",
        cep:"",
        pagoNaEntrega: "Não",
        simNaEntrega:"Sim",
        naoNaEntrega:"Não",
        entrega:"Manhã"
      },
      estados:{
        RJ:"Rio de Janeiro",
        MG:"Minas Gerais",
        SP:"São Paulo",
        ES:"Espirito Santo"
      }
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
    },
    submitFormulario(){
      alert("Pedido Finalizado");
    },
    checarAvaliacao(n,filme){
      return filme.avaliacao - n >= 0;
    },
    mostrarCarrinhoForm(){
      this.$router.push({name:'carrinho'});
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
.mensagem-estoque{
  font-weight: bold;
}

span.avaliacao-active {
  background-image:url('../assets/star-fill.jpg');
  background-repeat: no-repeat;
  background-position-y: 3px;
  background-position-x:1px;
  background-size: 20px;
  padding:1px;
}

</style>
