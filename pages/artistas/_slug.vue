<script>
  import util from '~/assets/js/util'
  export default {
    async asyncData({params, $axios }) {
      const cmsUrl = 'https://api.typewriter.cloud/Cristobal2697/jazzsite/types'
      let artista = await $axios.$get(cmsUrl+'/artista/'+params.slug)
      artista = util.cmsToObj(artista)

      let albumes = await $axios.$get('https://api.typewriter.cloud/Cristobal2697/jazzsite/types/album')
      albumes.forEach(album => util.cmsToObj(album))
      let album = new Array();
      albumes.forEach(a => {
        if(a.artistaid == params.slug){
            album.push(a);
        }
      });
      return { artista, album }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <div class="row">
     <div class="three columns">
       <img class="u-max-full-width" :src=" artista.image" alt="Italian Trulli">
     </div>
     <div class="six columns">
       <h4>{{artista.name}}</h4>
	    Nacionalidad: {{artista.nationality}}.<br>
      Año Nacimiento: {{artista.birth_year}}<br>
	    Estilos: {{artista.estilos}}<br><br>
	    <b>Biografía</b><br><br>
     <span v-html="artista.content"></span>
	 </div>
	 <div class="three columns"></div>
	   <h5>Álbumes</h5>
	   <ul>
	     <li v-for="a of album" :key="a.slug">
	       <NuxtLink :to="{ name: 'album-slug', params: { slug: a.slug } }">{{a.title}}</NuxtLink>
	     </li>
	   </ul>
   </div>
   <FooterView />
 </div>
</template>