<template>
  <div>

    <b-row class="justify-content-md-center">
      <b-col col lg="10" md="2">
        <div class="grafico-LP" style="border: 1px solid rgba(0, 0, 0);">
          <strong><h4 style="text-align:center; margin-top:2%;">Sinopse de Lavoura Permanente</h4></strong>
          <strong><h5>N° de estabelecimentos: {{lp_numero_estabelecimento}} estabelecimentos </h5></strong>
          <strong><h5>Área colhida: {{lp_area_colhida}} hectares</h5></strong>
          <strong><h5>Valor da produção: {{lp_valor_producao}} R$ x 1000</h5></strong>
        </div>


        <br>
        <br>
        
        <div class="grafico-LP">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior número de estabelecimentos</h6></strong>
        <MapBar :dados="lp_dados_numeros_estabelecimento" label="Número de estabelecimento (Estabelecimentos)" :dadosRodape="lp_prod_estabelecimento"/>
        </div>

        <br>
        <br>

        <div class="grafico-LP">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior área colhida</h6></strong>
        <MapBar :dados="lp_dados_area_colhida" label="Área colhida (Hectares)" :dadosRodape="lp_prod_area_colhida"/>
        </div>

        <br>
        <br>

        <div class="grafico-LP">
        <strong><h6 style="text-align:center; margin-top:2%;">Lavoura Permanente<br>10 produtos com maior valor de produção</h6></strong>
        <MapBar :dados="lp_dados_v_producao" label="Valor da produção (R$ x 1000)" :dadosRodape="lp_prod_v_producao"/> 
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

      lp_numero_estabelecimento: null,
      lp_area_colhida: null,
      lp_qtd_produzida: null,
      lp_valor_producao: null,

      // Garfico numero de estabelecimento
      lp_dados_numeros_estabelecimento: [],
      lp_prod_estabelecimento: [],
      
      // Grafico area colhida
      lp_dados_area_colhida: [],
      lp_prod_area_colhida: [],
      
       //Grafico valor de producao
      lp_dados_v_producao: [],
      lp_prod_v_producao: [],

    }
  },
  /*
  async mounted() {
      try {
        const res = await axios.get('https://agribrpm-backend.herokuapp.com/numest/brpm');

        this.lp_dados_numeros_estabelecimento = res.data.map(el => el.numest); // Aqui apenas esse esta correto
        this.lp_prod_estabelecimentos = res.data.map(el => el.Indicador);
        console.log(res.data.map(el => el.Indicador))
      
      } catch (erro) {
        console.log("Erro de leitura", erro)       
    }
  },*/
  
  async mounted() {
    
    try {
      const resGeralP = await axios.get('http://localhost:3333/tudo/brpm');
      const resG1 = await axios.get('http://localhost:3333/numest/brpm');
      const resG2 = await axios.get('http://localhost:3333/areacol/brpm');
      const resG3 = await axios.get('http://localhost:3333/valorprod/brpm');
      
      this.lp_dados_numeros_estabelecimento = resG1.data.map(el => el.numest); // Aqui apenas esse esta correto
      this.lp_prod_estabelecimento = resG1.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralP.data.length; i++){
          this.lp_numero_estabelecimento += resGeralP.data[i].numest;
      }
      this.lp_numero_estabelecimento = this.lp_numero_estabelecimento.toLocaleString('pt-BR');

      this.lp_dados_area_colhida = resG2.data.map(el => el.areacol); // Aqui apenas esse esta correto
      this.lp_prod_area_colhida = resG2.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralP.data.length; i++){
          this.lp_area_colhida += resGeralP.data[i].areacol;
      }
      this.lp_area_colhida = this.lp_area_colhida.toLocaleString('pt-BR')

      this.lp_dados_v_producao = resG3.data.map(el => el.valorprod); // Aqui apenas esse esta correto
      this.lp_prod_v_producao = resG3.data.map(el => el.Indicador);

      for(var i = 0; i<resGeralP.data.length; i++){
          this.lp_valor_producao += resGeralP.data[i].valorprod;
      }
      this.lp_valor_producao = this.lp_valor_producao.toLocaleString('pt-BR')
        
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


</style>
