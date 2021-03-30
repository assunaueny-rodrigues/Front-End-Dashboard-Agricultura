<template>
  <div>

    <b-row class="justify-content-md-center">
      <b-col col lg="10" md="2">

        <br>
        
        <div class="grafico-LT">
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 cidades com maior número de estabelecimentos</h6></strong>
          <MapBar :dados="lt_dados_numeros_estabelecimentoRN" label="Número de estabelecimento (Estabelecimentos)" :dadosRodape="lt_prod_estabelecimentoRN"/>
        </div>
        
        <br>
        <br>

        <div class="grafico-LT">
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 cidades com maior área colhida</h6></strong>
          <MapBar :dados="lt_dados_area_colhidaRN" label="Área colhida (Hectares)" :dadosRodape="lt_prod_area_colhidaRN"/>
        </div>
        
        <br>
        <br>

        <div class="grafico-LT" > 
          <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 cidades com maior valor de produção</h6></strong>
          <MapBar :dados="lt_dados_v_producaoRN" label="Valor da produção (R$ x 1000)" :dadosRodape="lt_prod_v_producaoRN"/> 
        </div>
      
      </b-col>
    </b-row>

    <br>
    <!--
    <b-row>
      <b-col>
        <MapBar :dados="lt_dados_quant_produzida" label="Quantidade produzida" :dadosRodape="lt_prod_quant_produzida" />
      </b-col>
    
      <b-col>
        <MapBar :dados="lt_dados_v_producao" label="Valor da producao" :dadosRodape="lt_prod_v_producao"/> 
      </b-col>
    </b-row>
    -->
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
      
      cor: "linear-gradient(to top, #33cc33 0%, #00ff99 37%)",
      borda: "black",

      lt_numero_estabelecimentoRN: null,
      lt_area_colhidaRN: null,
      lt_qtd_produzidaRN: null,
      lt_valor_producaoRN: null,

      // Garfico numero de estabelecimento
      lt_dados_numeros_estabelecimentoRN: [],
      lt_prod_estabelecimentoRN: [],
      
      // Grafico area colhida
      lt_dados_area_colhidaRN: [],
      lt_prod_area_colhidaRN: [],
      
      //Grafico valor de producao
      lt_dados_v_producaoRN: [],
      lt_prod_v_producaoRN: [],
      
    }
  },

  async mounted() {
    
    try {
      
      const resG1Todo = await axios.get('http://localhost:3333/numest/cidrntttemp');
      const resG2Todo = await axios.get('http://localhost:3333/areacol/cidrntttemp');
      const resG3Todo = await axios.get('http://localhost:3333/valorprod/cidrntttemp');
      
      console.log(resG1Todo.data.map(el => el.Indicador))
      
      this.lt_dados_numeros_estabelecimentoRN = resG1Todo.data.map(el => el.numest); // Aqui apenas esse esta correto
      this.lt_prod_estabelecimentoRN = resG1Todo.data.map(el => el.cidade);


      this.lt_dados_area_colhidaRN = resG2Todo.data.map(el => el.areacol); // Aqui apenas esse esta correto
      this.lt_prod_area_colhidaRN = resG2Todo.data.map(el => el.cidade);


      this.lt_dados_v_producaoRN = resG3Todo.data.map(el => el.valorprod); // Aqui apenas esse esta correto
      this.lt_prod_v_producaoRN = resG3Todo.data.map(el => el.cidade);
      
        
      } catch (erro) {
        console.log("Erro de leitura", erro)       
    }
  }
}
</script>

<style>

.tamanho-de-grafico{
  width: 70%;
  margin-left: 10%;
}

.grafico-LT{
  box-shadow: 5px 5px 5px rgba(0,0,0,0.5);
  border-radius: 5px;
  background: rgb(255, 255, 255);
  border: 1px solid rgba(0, 0, 0); 
}


#sinopse{
  
}

</style>
