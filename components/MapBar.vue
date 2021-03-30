<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  data: () => ({
    chartdata: {
      labels: [],
      datasets: [
        {
          label: '',
          backgroundColor: '#088A08',
          data: [],
          labels: [],
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
    }
  }),

  props: ['dados', 'label', 'dadosRodape'],

  watch: {
        dados: function(val) {
          this.updateChart()
        },
        
  },  
  mounted () {
    this.updateChart()
  },
  methods: {
      updateChart() {
          if(this.dados) {
              this.chartdata.datasets[0].label = this.label;
              this.chartdata.datasets[0].data = this.dados;
              this.chartdata.labels = this.dadosRodape;
          }
          this.renderChart(this.chartdata, this.options);
      }
  }
}
</script>

<style>
</style>