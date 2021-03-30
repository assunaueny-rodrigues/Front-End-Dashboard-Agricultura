<template>
  <div>

    <b-row class="justify-content-md-center">
      <b-col col lg="10" md="2">
        <div class="grafico-LT" style="border: 1px solid rgba(0, 0, 0);">
          <strong><h4 style="text-align:center; margin-top:2%;">Sinopse de Lavoura Temporária</h4></strong>
          <strong><h5>N° de estabelecimentos: {{lt_numero_estabelecimento}} estabelecimentos</h5></strong>
          <strong><h5>Área colhida: {{lt_area_colhida}} hectares</h5></strong>
          <strong><h5>Valor da produção: {{lt_valor_producao}} R$ x 1000</h5></strong>
        </div>

        <br>
        <br>

        <div class="grafico-LT">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 produtos com maior número de estabelecimentos</h6></strong>
        <MapBar  :dados="lt_dados_numeros_estabelecimento" label="Número de estabelecimento (Estabelecimentos)" :dadosRodape="lt_prod_estabelecimento"/>
        </div>

        <br>
        <br>
        
        <div class="grafico-LT">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 produtos com maior área colhida</h6></strong>
        <MapBar :dados="lt_dados_area_colhida" label="Área colhida (Hectares)" :dadosRodape="lt_prod_area_colhida"/>
        </div>

        <br>
        <br>
       
        <div class="grafico-LT">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Temporária<br>10 produtos com maior valor de produção</h6></strong>
        <MapBar  :dados="lt_dados_v_producao" label="Valor da produção (R$ x 1000)" :dadosRodape="lt_prod_v_producao"/> 
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

      lt_numero_estabelecimento: null,
      lt_area_colhida: null,
      lt_qtd_produzida: null,
      lt_valor_producao: null,

      // Garfico numero de estabelecimento
      lt_dados_numeros_estabelecimento: [],
      lt_prod_estabelecimento: [],
      
      // Grafico area colhida
      lt_dados_area_colhida: [],
      lt_prod_area_colhida: [],
      
      //Grafico valor de producao
      lt_dados_v_producao: [],
      lt_prod_v_producao: [],
      
    }
  },

  async mounted() {
    
    try {

      const resGeralT = await axios.get('http://localhost:3333/tudo/brtemp');
      const resG1 = await axios.get('http://localhost:3333/numest/brtemp');
      const resG2 = await axios.get('http://localhost:3333/areacol/brtemp');
      const resG3 = await axios.get('http://localhost:3333/valorprod/brtemp');
      
      this.lt_dados_numeros_estabelecimento = resG1.data.map(el => el.numest); // Aqui apenas esse esta correto
      this.lt_prod_estabelecimento = resG1.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralT.data.length; i++){
          this.lt_numero_estabelecimento += resGeralT.data[i].numest;
      }
      this.lt_numero_estabelecimento = this.lt_numero_estabelecimento.toLocaleString('pt-BR')

      this.lt_dados_area_colhida = resG2.data.map(el => el.areacol); // Aqui apenas esse esta correto
      this.lt_prod_area_colhida = resG2.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralT.data.length; i++){
          this.lt_area_colhida += resGeralT.data[i].areacol;
      }
      this.lt_area_colhida = this.lt_area_colhida.toLocaleString('pt-BR')

      this.lt_dados_v_producao = resG3.data.map(el => el.valorprod); // Aqui apenas esse esta correto
      this.lt_prod_v_producao = resG3.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralT.data.length; i++){
          this.lt_valor_producao += resGeralT.data[i].valorprod;
      }
      this.lt_valor_producao = this.lt_valor_producao.toLocaleString('pt-BR')
        
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
