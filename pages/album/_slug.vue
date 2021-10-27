<script>
  import util from '~/assets/js/util'
  export default {
    async asyncData({ params, $axios }) {
      const cmsUrl = 'https://api.typewriter.cloud/Cristobal2697/jazzsite/types'
      let album = await $axios.$get(cmsUrl+'/album/'+params.slug)
      album = util.cmsToObj(album)
      let artista = await $axios.$get(cmsUrl+'/artista/'+album.artistaid)
      artista = util.cmsToObj(artista)
      let discografica = await $axios.$get(cmsUrl+'/discografica/'+album.discograficaid)
      discografica = util.cmsToObj(discografica)
      return { cmsUrl, album, artista, discografica }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <div class="row">
     <div class="three columns">
       <img class="u-max-full-width" :src="album.image">
     </div>
     <div class="six columns">
      <h4>{{album.title}}</h4>
	   Artista: <NuxtLink :to="{ name: 'artistas-slug', params: { slug: album.artistaid } }">{{artista.name}}</NuxtLink><br> 

	   Duración: {{album.duracion}}<br> 
     Año de publicación: {{album.copyright}}<br> 
	   Publicado por <NuxtLink :to="{ name: 'discograficas-slug', params: { slug: album.discograficaid } }">{{discografica.name}}</NuxtLink><br><br>

	   <b>Canciones</b><br>
     <span v-html="album.content"></span>
	 </div>
	 <div class="two columns"></div>
   </div>
   <FooterView />
 </div>
</template>