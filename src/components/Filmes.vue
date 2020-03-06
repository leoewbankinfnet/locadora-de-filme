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
  <b-row v-else>
      <h2> Carrinho </h2>
       <div class="col-12">
       <form>
         <div class="form-group">
           <label for="pedido.primeiroNome">Primeiro nome</label>
           <input
             type="text"
             class="form-control"
             id="primeiroNome"
             placeholder="Digita o primeiro nome"
             v-model.trim.lazy="pedido.primeiroNome"
           >
         </div>
         <div class="form-group">
           <label for="ultimoNome">Último nome</label>
           <input
             type="text"
             class="form-control"
             id="ultimoNome"
             placeholder="Digite o último nome"
             v-model.trim.lazy="pedido.ultimoNome"
           >
         </div>
         <div class="form-group">
           <label for="endereco">Endereço</label>
           <input
             type="text"
             class="form-control"
             id="endereco"
             placeholder="Digita o endereço"
             v-model.trim.lazy="pedido.endereco"
           >
         </div>
         <div class="form-group">
           <label for="cidade">Cidade</label>
           <input
             type="text"
             class="form-control"
             id="cidade"
             placeholder="Digita a cidade"
             v-model.trim="pedido.cidade"
           >
         </div>
         <div class="form-group">
           <label for="estado">Estado</label>
           <select class="form-control" id="estado" v-model="pedido.estado">
            <option disabled value> Escolha um estado </option>
            <option 
              v-for="(estado,key) in estados"
              v-bind:value="estado"
              v-bind:key="key">
              {{key}}
            </option>
             
           </select>
         </div>
         <div class="form-group">
           <label for="cep">CEP</label>
           <input
             type="number"
             class="form-control"
             id="cep"
             placeholder="Digita o CEP"
             v-model.number.trim="pedido.cep"
           >
         </div>
        
         <div class="form-group form-check">
           <input
              type="checkbox"
              class="form-check-input"
              id="pagoNaEntrega"
              v-bind:true-value="pedido.simNaEntrega"
              v-bind:false-value="pedido.naoNaEntrega"
              v-model="pedido.pagoNaEntrega">
            <label class="form-check-label" for="pagoNaEntrega"> Pago na Entrega?</label>
         </div>
         <div class = "form-group form-check-inline">
           <input
              type="radio"
              class="form-check-input"
              id="manha"
              value="Manhã"
              v-model="pedido.entrega">
            <label class="form-check-label" for="manha"> Manhã</label>
         </div>
          <div class = "form-group form-check-inline">
           <input
              type="radio"
              class="form-check-input"
              id="tarde"
              value="Tarde"
              v-model="pedido.entrega">
            <label class="form-check-label" for="Tarde"> Tarde</label>
         </div>
          <div class = "form-group form-check-inline">
           <input
              type="radio"
              class="form-check-input"
              id="noite"
              value="Noite"
              v-model="pedido.entrega">
            <label class="form-check-label" for="noite"> Noite</label>
         </div>
         <div class="form-group">
            <button type="submit" class="btn btn-primary" v-on:click="submitFormulario">
              Finalizar pedido
            </button>
         </div>

       </form>
     </div>
    

     <div class="col-12">
       <pre>
         Primeiro nome: {{ pedido.primeiroNome }}
         Último nome: {{ pedido.ultimoNome }}
         Endereço: {{ pedido.endereco }}
         Cidade: {{ pedido.cidade }}
         Estado: {{ pedido.estado }}
         CEP: {{ pedido.cep }}
         Pago na entrega?: {{pedido.pagoNaEntrega}}
         Entrega: {{pedido.entrega}}
       </pre>
     </div>
   
      
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
