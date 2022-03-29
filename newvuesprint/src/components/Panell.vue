<template>
  <div v-if="clicatWeb">
    <h4>Has clicat a web. qué vols fer ara?</h4>

    <label for="pagina">Número de pàgines</label>
    <button @click="calctotalPaginasSumar" type="button">+</button>
    <input @keypress="filtraNumeros" @keyup="calctotalPaginas" type="text" v-model.number="paginas" name="pag" >
    <button @click="calcTotalPaginasRestar" type="button">-</button>
  <hr>
    <label for="idioma" >Número d'idiomes</label>
    <button @click="calctotalIdiomaSumar" type="button">+</button>
    <input @keypress="filtraNumeros" @keyup="calctotalIdiomas" type="text" v-model.number="idiomas" name="lang" >
    <button @click="calcTotalIdiomaRestar" type="button">-</button>
  

  <p v-if="paginas == 1">Vols només {{paginas}} pàgina</p>
        <p v-if="paginas>1" > Vols un total de {{paginas}} pàgines.</p>

        <p v-if="idiomas == 1">Vols només {{idiomas}} idioma</p>
        <p v-if="idiomas>1" > Vols un total de {{idiomas}} idiomes.</p>

  </div>
  
</template>

<script>
export default {
  name: 'panellView',
  props: {
    clicatWeb: Boolean,
    numPaginas:Number,
    numIdiomas:Number,
    cantidad:Number
  },data(){
    return{
      
      idiomas:this.numIdiomas,
      paginas:this.numPaginas,
      
      
    }
  },
    methods:{
     
      filtraNumeros(filtra) {
          if(filtra.keyCode < 48 || filtra.keyCode > 57) {
            filtra.preventDefault();
          }
      },
      calctotalPaginas(){
       
        if(this.paginas.length==0|| this.paginas==0){
          this.paginas=1;
        }else{
           this.$emit('totalPags',parseInt(this.paginas)) 
        }
      },calctotalIdiomas(){
        if(this.idiomas.length==0 || this.idiomas==0){
          this.idiomas=1;
        }else{
            this.$emit('totalidioms',parseInt(this.idiomas)) 
        }
      },calctotalIdiomaSumar(){
        this.idiomas++;
        this.$emit('sumarIdioma',parseInt(this.idiomas)) 
      },calcTotalIdiomaRestar(){
        if(this.idiomas>1){
          this.idiomas--;
          this.$emit('restarIdioma',parseInt(this.idiomas))
        }   
      },calctotalPaginasSumar(){
        this.paginas++;
        this.$emit('sumarPagina',parseInt(this.paginas)) 
      },calcTotalPaginasRestar(){
        if(this.paginas>1){
          this.paginas--;
          this.$emit('restarPagina',parseInt(this.paginas))
        }
         
      }
  
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
