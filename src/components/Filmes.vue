<template>
  <div id="filmes" class="container">
    <h2 id="enc"> Filmes Encontrados </h2>
    <!-- <b-row>
      <b-col >
        <b-card style="width:14rem id= "card" title="Vingadores" sub-title="Gênero:Ação">
        <b-card-text>
          Um filme de Heróis
        </b-card-text>

        <b-card-text>R$25,00</b-card-text>

        <a href="#" class="card-link">Clique aqui para alugar</a>
        
        </b-card>
      </b-col>
     <b-col >
        <b-card id= "card" title="Vingadores" sub-title="Gênero:Ação">
        <b-card-text>
          Um filme de Heróis
        </b-card-text>

        <b-card-text>R$25,00</b-card-text>

        <a href="#" class="card-link">Clique aqui para alugar</a>
        
        </b-card>
      </b-col>
       <b-col >
        <b-card id= "card" title="Vingadores" sub-title="Gênero:Ação">
        <b-card-text>
          Um filme de Heróis
        </b-card-text>

        <b-card-text>R$25,00</b-card-text>

        <a href="#" class="card-link">Clique aqui para alugar</a>
        
        </b-card>
      </b-col>
  </b-row> -->
  <b-row>
    <ul>
    <li v-for="filme in filmes" v-bind:key="filme">{{filme.titulo}} </li>
    </ul>
  </b-row>
    <div class="cards">
  <b-row>

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
        <b-card-text> {{filme.descricao}} </b-card-text>
        <b-card-text> R${{filme.valor}} </b-card-text>
        <a href="#" class="card-link">Clique aqui para alugar</a>
      </b-card>
    </b-col>
  
    
  </b-row>
  </div>
    
  </div>
</template>

<script>
export default {
  name: 'Filmes',
  data:function (){
    return{
      filmes: 
        [ {id:1, titulo: "Vingadores", descricao:"Um filme de heróis", valor:25, imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27141726%27&EntityType=%27Item%27&EntityId=%273863%27&Width=1080&Height=1600&device=web_browser&subscriptions=Anonymous"},
          {id:2, titulo: "Vingadores 2 ", descricao:"Um filme de heróis", valor:25,imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/2/22/OsVingadores2.jpg/250px-OsVingadores2.jpg"},
          {id:3, titulo: "Pantera Negra", descricao:"Um filme de heróis", valor:25,imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27182460%27&EntityType=%27Item%27&EntityId=%2710148%27&Width=720&Height=1080&device=web_browser&subscriptions=Anonymous"},
          {id:4, titulo: "Capitã Marvel", descricao:"Um filme de heróis", valor:25, imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/5/59/Captain_Marvel_%282018%29.jpg/250px-Captain_Marvel_%282018%29.jpg"},
          {id:5, titulo: "Brightburn", descricao:"Um filme de heróis", valor:25, imagem:"https://s2.glbimg.com/ymb71yQSk38YMYeoe0717NTTisk=/e.glbimg.com/og/ed/f/original/2019/05/21/brightburn_regposter_brazil.jpg"}

        ]
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
  text-align:center;
  margin-top:2%;
}
#enc{
  margin-top: 2%;
  text-align: center
}

#cards{
  display:flex;
  justify-content: space-between;

}

</style>
