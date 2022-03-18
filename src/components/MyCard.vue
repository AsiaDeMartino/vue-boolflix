<template>
<li class="d-flex flex-column">
    <img class="poster" v-if="item.poster_path" :src="locandina(item.poster_path)" alt="">
    <img class="poster_placeholder" v-else src="../assets/poster-placeholder.png" alt="">
    <div class="primo" v-if="item.title">Titolo: {{item.title}}</div>
    <div v-if="item.name">Titolo: {{item.name}}</div>
    <div v-if="item.original_title">Titolo originale: {{item.original_title}}</div>
    <div v-if="item.original_name">Titolo originale: {{item.original_name}}</div>
    <div ><img :src="bandiera(item.original_language)" :alt="item.original_language"></div>
    <div class="stella">
        <span class="titolo">Voto: </span>
        <span v-html="stellaPiena(item.vote_average)"></span>  <!-- piena -->
        <span v-html="stellaVuota(item.vote_average)"></span>   <!-- vuota -->
    </div>
    <div>Overview: {{item.overview}}</div>
</li>
</template>

<script>
export default {
    name: 'MyCard',
    props: {
        item: {}
    },
    methods: {
    bandiera: function(lingua){
      if (lingua == 'en') {
        lingua = 'gb';
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      } else {
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      }
    },
    locandina: function(immagine){
      return ('https://image.tmdb.org/t/p/w342' + immagine);
    },
    stellaPiena: function(voto){
      let stelle;
      stelle = parseInt(voto/2)
      return ('&#9733; '.repeat(stelle))
    },
    stellaVuota: function(voto){
      let stelle;
      stelle = 5 - parseInt(voto/2)
      return ('&#9734; '.repeat(stelle))
    }
    }
}
</script>

<style scoped lang="scss">
li{
  list-style: none;
  overflow: scroll;

    .poster_placeholder{
    width: 342px;
    }

    .stella{
    color: gold;
    display: flex;
        .titolo{
            color: white;
            margin-right: 10px;
        }
    }

    div{
        margin-left: 20px;
    }

    .primo{
        margin-top: 35px;
    }

    div, span {
        display: none;
    }

    &:hover{
        .poster{
            display: none;
        }
        .poster_placeholder{
            display: none;
        }
        div, span {
            display: initial;
        }

        
        background-color: rgba( #262626,1.0);
        width: 342px;
        height: 510px;
    }
}


</style>