<template>
  <div id="filme-id">
      <h1> Filme</h1>
     
      <b-row align-v="center">
        <b-col cols=4>
                  <b-img :src=filme.imagem fluid alt="Foto"></b-img>
        </b-col>
        <b-col cols=8>
            <b-card :title=filme.titulo :sub-title=filme.descricao>
                <b-card-text>
                    id:  {{ $route.params.id}}
                </b-card-text>

                <b-card-text>Título : {{ filme.titulo}}</b-card-text>
                <b-card-text>Descrição : {{ filme.descricao}}</b-card-text>
                <b-card-text>Valor : {{ filme.valor}}</b-card-text>
                <b-card-text>Estoque Disponível : {{ filme.estoqueDisp}}</b-card-text>

            </b-card>
        </b-col>
    </b-row>
      
  </div>
</template>
 
<script>

 
export default {
  name:"Filme",
   data:function() {
    return {
      filmes: 
          [ {id:1, titulo: "Vingadores", descricao:"Um filme de heróis", valor:25, imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27141726%27&EntityType=%27Item%27&EntityId=%273863%27&Width=1080&Height=1600&device=web_browser&subscriptions=Anonymous",estoqueDisp: 3,avaliacao:3},
            {id:2, titulo: "Vingadores 2 ", descricao:"Um filme de heróis", valor:25,imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/2/22/OsVingadores2.jpg/250px-OsVingadores2.jpg",estoqueDisp:7},
            {id:3, titulo: "Pantera Negra", descricao:"Um filme de heróis", valor:25,imagem:"https://cdn.telecineplay.com.br/isl/api/v1/dataservice/ResizeImage/$value?Format=%27jpg%27&Quality=85&ImageId=%27182460%27&EntityType=%27Item%27&EntityId=%2710148%27&Width=720&Height=1080&device=web_browser&subscriptions=Anonymous",estoqueDisp: 34,avaliacao:2},
            {id:4, titulo: "Capitã Marvel", descricao:"Um filme de heróis", valor:25, imagem:"https://upload.wikimedia.org/wikipedia/pt/thumb/5/59/Captain_Marvel_%282018%29.jpg/250px-Captain_Marvel_%282018%29.jpg",estoqueDisp: 4,avaliacao:1},
            {id:5, titulo: "Brightburn", descricao:"Um filme de heróis", valor:25, imagem:"https://s2.glbimg.com/ymb71yQSk38YMYeoe0717NTTisk=/e.glbimg.com/og/ed/f/original/2019/05/21/brightburn_regposter_brazil.jpg",estoqueDisp: 8,avaliacao:2}
          ]
      }
    },

      computed:{
        filme: function(){
          return this.filmes[this.$route.params.id -1]
        }
      },
     
  }


</script>
 
<style scoped>
</style>