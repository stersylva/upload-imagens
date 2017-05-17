<template>

  <div class="corpo">
    <h1 class="titulo">{{ titulo }}</h1>

    <input type="search" class="filtro" placeholder="filtro por foto">

    <ul class="lista-fotos">

        <li class="lista-fotos-item" v-for="foto in fotos">

            <meu-painel :titulo="foto.titulo">
                <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
            </meu-painel>   
        </li>
    </ul>
  </div>

</template>



<script>

// agora temos apenas a propriedade `fotos` que é um array que possui dois objetos que possuem as propriedades 
//`url` e `titulo`, cada um com seu valor.
import Painel from './components/shared/painel/Painel.vue'
export default {

  components: {
    'meu-painel': Painel
  },
  data() {
    return {
      titulo: 'Imagens',
      fotos: [],

      filtro: ''
    }
  },

  computed: {
    fotoComFiltro(){

      if(this.filtro){

        /* se tiver filtro */
        return[];
        
      } else{
        return this.fotos;
        /* se não tiver ele vai retonar a lista de fotos completa*/
      }
    }
  },

  //detro do created que eu carrego a api das fotos
  created(){
    this.$http
      .get ('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));

  }
}
</script>
<style>
  .titulo{
    text-align: center;
  }

  .corpo{
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .lista-fotos{
    list-style:nome;
  }

  .lista-fotos .lista-fotos-item{
    display: inline-block;
  }

  .imagem-responsiva{
    width: 100%;
  }
  .filtro {
    display: block;
    width:25%;
  }
</style>