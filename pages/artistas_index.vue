<script>
  import util from '~/assets/js/util'
  export default {
    async asyncData({ params, $axios }) {
      let artistas = await $axios.$get('https://api.typewriter.cloud/Cristobal2697/jazzsite/types/artista')
      artistas.forEach(artista => util.cmsToObj(artista))
      return {
        artistas
      }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <h3 style="margin-top: 15px">Artistas </h3>
   <ul class="ul">
     <li v-for="a of artistas" :key="a.slug">
       <div class="card">
          <div>
            <img class="card-img" :src=" a.image" />
          </div>
          <div class="card-text">
            <h4 class="card-title"><strong> {{ a.name }} </strong></h4>
            <p class="card-description">
              <span>Nacionalidad: {{a.nationality}}</span><br>
              <span>Nacimiento: {{a.birth_year}}</span><br>
            </p>
            <NuxtLink :to="{ name: 'artistas-slug', params: { slug: a.slug } }" class="button">
                Detalles
            </NuxtLink>
          </div>
        </div>
     </li>
   </ul>
   <FooterView />
 </div>
</template>