<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    
    
    <form>
      <label for="web">Pàgina web: 500€</label>
      <input v-model="checkedWeb"  type="checkbox" name="web">
        
        <panellView  
        v-on:totalidioms="calctotalidiomas" 
        v-on:totalPags="calctotalpaginas"  :numPaginas="paginas"  
        :numIdiomas="idiomas"  
        :clicatWeb="checkedWeb"
        v-on:sumarIdioma="calcSumarIdioma" 
        v-on:restarIdioma="calcRestarIdioma" 
        v-on:sumarPagina="calcSumarPaginas"
        v-on:restarPagina="calcRestarPaginas"
         />

        
      <hr>

      
      <label for="seo">Consultoria SEO: 300€</label>
      <input v-model="checkedSeo" type="checkbox" name="seo">

      <hr>

      <label for="ads">Campanya de ADS: 200€ </label>
      <input v-model ="checkedAds" type="checkbox" name="ads">

    </form>

    
    <p>El preu total es de: {{preuTotalNou}}€</p>
    
   <router-link to="/"><!--ruta base!!!!!-->
     <button>Tornar enrere</button>
  </router-link>
     

  </div>
</template>

<script>
// @ is an alias to /src
import panellView from '@/components/Panell.vue'

export default {
  name: 'HomeView',
  components: {
    panellView
  },data(){
    return{
      
      checkedWeb:false,
      checkedSeo:false,
      checkedAds:false,
      preuWeb: 500, //Posar en array
      preuSeo:300,
      preuAds:200,
      paginas:1, //Posar en array
      idiomas:1,
      
    }
  },methods:{

    //inputs calcular
    calctotalpaginas(paginaInput){
        this.paginas=paginaInput;
    },
    calctotalidiomas(idiomaInput){
        this.idiomas=idiomaInput;   
    },
    //butons calcular idioma
    calcRestarIdioma(idiomaResta){
        this.idiomas=idiomaResta; 
    },
    calcSumarIdioma(idiomaSuma){
        this.idiomas=idiomaSuma;
    },
    //butons calcular paginas
    calcSumarPaginas(paginaSuma){
        this.paginas=paginaSuma;
      },
    calcRestarPaginas(paginaResta){
        this.paginas=paginaResta;
    }

  },computed:{
    preuTotalNou(){
      let total = 0;
      
      if(this.checkedWeb){
         total+= this.preuWeb + (this.idiomas*this.paginas*30);
        
      }
      if(this.checkedSeo){
        total+=this.preuSeo;
      }
      if(this.checkedAds){
        total+=this.preuAds;

      }
        
          return total;
        
          
      },
      
  }
  
}
</script>
