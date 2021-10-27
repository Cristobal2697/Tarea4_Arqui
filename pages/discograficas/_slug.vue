<script>
  import util from '~/assets/js/util'
  export default {
    async asyncData({params, $axios }) {
      const cmsUrl = 'https://api.typewriter.cloud/Cristobal2697/jazzsite/types'
      let discografica = await $axios.$get(cmsUrl+'/discografica/'+params.slug)
      discografica = util.cmsToObj(discografica)

      let albumes = await $axios.$get('https://api.typewriter.cloud/Cristobal2697/jazzsite/types/album')
      albumes.forEach(album => util.cmsToObj(album))
      let album = new Array();
      albumes.forEach(a => {
        if(a.discograficaid == params.slug){
            album.push(a);
        }
      });
      return { discografica, album }
    }
  }
</script>

<template>
  <div class="container">
   <HeaderView />
   <div class="row">
     <div class="three columns">
       <img class="u-max-full-width" :src=" discografica.image">
     </div>
     <div class="six columns">
       <h4>{{discografica.name}}</h4>
        Fundación: {{discografica.founded}}<br>
        País: {{discografica.country}} <br><br>
	   
	    <b>Historia</b><br>
	    <nuxt-content :document="discografica" />
	  </div>
	 <div class="three columns"></div>
	   <h5>Álbumes Publicados</h5>
	   <ul>
	     <li v-for="a of album" :key="a.slug">
	       <NuxtLink :to="{ name: 'album-slug', params: { slug: a.slug } }">{{a.title}}</NuxtLink>
	     </li>
	   </ul>
	   
	   
	   
	   
   </div>
   <FooterView />
 </div>
</template>