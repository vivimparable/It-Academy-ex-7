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

        <p v-if="paginas == 1">Vols només {{paginas}} pàgina</p>
        <p v-if="paginas>1" > Vols un total de {{paginas}} pàgines.</p>

        <p v-if="idiomas == 1">Vols només {{idiomas}} idioma</p>
        <p v-if="idiomas>1" > Vols un total de {{idiomas}} idiomes.</p>
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
      preuWeb: 500,
      preuSeo:300,
      preuAds:200,
      paginas:0,
      idiomas:0,
      
    }
  },methods:{

    //inputs calcular
    calctotalpaginas(a){
        this.paginas=a;
    },
    calctotalidiomas(b){
        this.idiomas=b;   
    },
    //butons calcular idioma
    calcRestarIdioma(d){
        this.idiomas=d; 
    },
    calcSumarIdioma(c){
        this.idiomas=c;
    },
    //butons calcular paginas
    calcSumarPaginas(e){
        this.paginas=e;
      },
    calcRestarPaginas(f){
        this.paginas=f;
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
