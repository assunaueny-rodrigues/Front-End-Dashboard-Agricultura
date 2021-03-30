<template>
  <div id="principal"> 
    
    <Cabecalho></Cabecalho>

    <br>
    <br>

    <b-row>
      <b-col>
       <graficoP></graficoP>
      </b-col>
    
      <b-col>
        <graficoT></graficoT>
      </b-col>
    </b-row>
    
    <br>
    <br>

    <b-row>
      <b-col>
        
        <div  class="cabecalho-mapas">
        <h5>Lavoura Permanente<br>N° de Estabelecimentos (Estabelecimentos) dos Estados</h5>
        <br>
        <MapaLPNumeroEst></MapaLPNumeroEst>
        
        </div>

        <br>
        <br>
        
        <div  class="cabecalho-mapas">
        <h5>Lavoura Permanente<br>Área Colhida (Hectares) dos Estados</h5>
        <br>
        <MapaLPAreaCol></MapaLPAreaCol>
        </div>
        
        <br>        
        <br>

        <div class="cabecalho-mapas">
        <h5>Lavoura Permanente<br>Valor de Produção (R$ x 1000) dos Estados</h5>
        <br>
        <MapaLPValorProd></MapaLPValorProd>
        </div>

      </b-col>

      <b-col>
        
        <div class="cabecalho-mapas">
        <h5>Lavoura Temporária<br>N° de Estabelecimento (Estabelecimentos) dos Estados</h5>
        <br>
        <MapaLTNumeroEst></MapaLTNumeroEst>
        </div>

        <br>
        <br>
        
        <div class="cabecalho-mapas"> 
        <h5>Lavoura Temporária<br>Área Colhida (Hectares) dos Estados</h5>
        <br>
        <MapaLTAreaCol></MapaLTAreaCol>
        </div> 
        
        <br>
        <br>

        <div class="cabecalho-mapas">
        <h5>Lavoura Temporária<br>Valor de Produção (R$ x 1000) dos Estados</h5>
        <br>
        <MapaLTValorProd></MapaLTValorProd>
        </div>

      </b-col>
    
    
    </b-row>  
  
  </div>
</template>

<script>
import Cabecalho from '~/components/Cabecalho-Brasil.vue'
import GraficoP from '~/components/Grafico-LPermanente.vue'
import GraficoT from '~/components/Grafico-LTemporaria.vue'
import MapaLPNumeroEst from '~/components/Mapa-LP-NumeroEst.vue'
import MapaLPAreaCol from '~/components/Mapa-LP-AreaCol.vue'
import MapaLPValorProd from '~/components/Mapa-LP-ValorProd.vue'
import MapaLTNumeroEst from '~/components/Mapa-LT-NumeroEst.vue'
import MapaLTAreaCol from '~/components/Mapa-LT-AreaCol.vue'
import MapaLTValorProd from '~/components/Mapa-LT-ValorProd.vue'


export default {
  components: {
    Cabecalho,
    GraficoP,
    GraficoT,
    MapaLPNumeroEst,
    MapaLPAreaCol,
    MapaLPValorProd,
    MapaLTNumeroEst,
    MapaLTAreaCol,
    MapaLTValorProd
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

.cabecalho-mapas{
  border: 1px solid rgba(0, 0, 0);
  width: 82%;
  margin-left: 9%;
  border-radius: 5px;
  padding-bottom: 2px;
  text-align: center;
  background: white;
}

</style>
