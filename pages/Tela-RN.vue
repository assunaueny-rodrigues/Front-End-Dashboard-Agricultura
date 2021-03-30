<template>
  <div id="principal"> 
    
    <Cabecalho></Cabecalho>
    
    <br>
    <br>

     <b-row>
      <b-col>
       <graficoP></graficoP>
       <GraficoPCidadeP></GraficoPCidadeP>
      </b-col>
        
      <b-col>
        <graficoT></graficoT>
        <GraficoPCidadeT></GraficoPCidadeT>
      </b-col>
    </b-row>
  
  </div>
</template>

<script>
import Cabecalho from '~/components/Cabecalho-RN.vue'
import GraficoT from '~/components/Grafico-LTemporariaRN.vue'
import GraficoP from '~/components/Grafico-LPermanenteRN.vue'
import GraficoPCidadeP from '~/components/G-CidadeLP-RN.vue'
import GraficoPCidadeT from '~/components/G-CidadeLT-RN.vue'

export default {
  components: {
    Cabecalho,
    GraficoT,
    GraficoP,
    GraficoPCidadeP,
    GraficoPCidadeT
  }
}
</script>

<style>

body{
  background: url('../assets/background/background1.jpg');
  background-size: 100%;
  background-repeat: no-repeat;
  background-attachment: fixed;
}


</style>
