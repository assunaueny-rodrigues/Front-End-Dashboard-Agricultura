<template>
  <div>

    <b-row class="justify-content-md-center">
      <b-col col lg="10" md="2">
        <div class="grafico-LP" style="border: 1px solid rgba(0, 0, 0);">
          <strong><h4 style="text-align:center; margin-top:2%;">Sinopse de Lavoura Permanente</h4></strong>
          <strong><h5>N° de estabelecimento: {{lp_numero_estabelecimentoRN}} estabelecimentos</h5></strong>
          <strong><h5>Área colhida: {{lp_area_colhidaRN}} hectares</h5></strong>
          <strong><h5>Valor da produção: {{lp_valor_producaoRN}} R$ x 1000</h5></strong>
        </div>


        <br>
        <br>

        <div class="grafico-LP">
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior número de estabelecimentos</h6></strong>
          <MapBar  :dados="lp_dados_numeros_estabelecimentoRN" label="Número de estabelecimento (Estabelecimentos)" :dadosRodape="lp_prod_estabelecimentoRN"/>
        </div>

        <br>
        <br>

        <div class="grafico-LP">
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior área colhida</h6></strong>
          <MapBar :dados="lp_dados_area_colhidaRN" label="Área colhida (Hectares)" :dadosRodape="lp_prod_area_colhidaRN"/>
        </div>
        
        <br>
        <br>

        <div class="grafico-LP">
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior valor de produção</h6></strong>
          <MapBar :dados="lp_dados_v_producaoRN" label="Valor da produção (R$ x 1000)" :dadosRodape="lp_prod_v_producaoRN"/> 
        </div>
      
      </b-col>
    </b-row>

    <br>

    
  </div>
</template>

<script>

import axios from 'axios'
import MapBar from "../components/MapBar.vue"

export default {
  components: {
    MapBar
  }, 
  data(){
    return{
      
      cor: "#088A08",
      borda: "black",

      lp_numero_estabelecimentoRN: null,
      lp_area_colhidaRN: null,
      lp_qtd_produzidaRN: null,
      lp_valor_producaoRN: null,

      // Garfico numero de estabelecimento
      lp_dados_numeros_estabelecimentoRN: [],
      lp_prod_estabelecimentoRN: [],
      
      // Grafico area colhida
      lp_dados_area_colhidaRN: [],
      lp_prod_area_colhidaRN: [],
      
       //Grafico valor de producao
      lp_dados_v_producaoRN: [],
      lp_prod_v_producaoRN: [],

    }
  },
    
  async mounted() {
    
    try {
      const resNumEstRNP = await axios.get('http://localhost:3333/numest/estpm');
      const resAreaColRNP = await axios.get('http://localhost:3333/areacol/estpm');
     const resValorProdRNP = await axios.get('http://localhost:3333/valorprod/estpm');
      const resG1RN = await axios.get('http://localhost:3333/numest/agrirnpm');
      const resG2RN = await axios.get('http://localhost:3333/areacol/agrirnpm');
      const resG3RN = await axios.get('http://localhost:3333/valorprod/agrirnpm');
      
      console.log(resG1RN.data.map(el => el.Indicador))

      this.lp_dados_numeros_estabelecimentoRN = resG1RN.data.map(el => el.numest); 
      this.lp_prod_estabelecimentoRN = resG1RN.data.map(el => el.Indicador);

      this.lp_numero_estabelecimentoRN = resNumEstRNP.data[18].numest.toLocaleString('pt-BR');
      /*for(var i = 0; i< resGeralRNP.data.length; i++){
          this.lp_numero_estabelecimentoRN += resGeralRNP.data[i].numest;
      }*/

      this.lp_dados_area_colhidaRN = resG2RN.data.map(el => el.areacol); // Aqui apenas esse esta correto
      this.lp_prod_area_colhidaRN = resG2RN.data.map(el => el.Indicador);

      this.lp_area_colhidaRN = resAreaColRNP.data[18].areacol.toLocaleString('pt-BR');
      /*
      for(var i = 0; i< resGeralRNP.data.length; i++){
          this.lp_area_colhidaRN += resGeralRNP.data[i].areacol;
      }*/

      this.lp_dados_v_producaoRN = resG3RN.data.map(el => el.valorprod); // Aqui apenas esse esta correto
      this.lp_prod_v_producaoRN = resG3RN.data.map(el => el.Indicador);
      
      this.lp_valor_producaoRN = resValorProdRNP.data[18].valorprod.toLocaleString('pt-BR');
      /*
      for(var i = 0; i< resGeralRNP.data.length; i++){
          this.lp_valor_producaoRN += resGeralRNP.data[i].valorprod;
      }*/
      
        
      } catch (erro) {
        console.log("Erro de leitura", erro)       
    }
  },
  
  

  
}
</script>

<style>

.grafico-LP{
  box-shadow: 5px 5px 5px rgba(0,0,0,0.5);
  border-radius: 5px;
  background: rgb(255, 255, 255);
  border: 1px solid rgba(0, 0, 0); 
}

h5{
  padding-top: 2%;
  padding-left: 10px;
  font-size: 15px;
}

.background-dados{
  
}



</style>
