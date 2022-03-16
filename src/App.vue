<template>
  <div id="app">
    <h1>Testador Vue ApexCharts</h1>
    <input 
      type="checkbox" 
      id="checkbox" 
      v-model="options.yaxis.reversed"
    >
    <label for="checkbox">Revertido</label>
    <select 
      v-model="selected" 
      @change="changeChart"
    >
      <option 
      v-for="(type, index) in chartTypes" 
      :selected="selected === type.Value"
      :value="type.Value"
      :key="index"
      >
        {{ type.Name }}
      </option>
    </select>
    <input
      v-model="options.title.text"
    >
    <div class="chart-wrapper">
      <apex-chart 
        width="800" :type="selected" 
        :options="options" :series="series">
      </apex-chart>  
    </div>
  </div> 
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    chartTypes: [
      { Name:"Barra", Value: "bar" },
      { Name:"Linha", Value: "line" },
      { Name:"Area", Value: "area" },
      { Name:"Radar", Value: "radar" }
    ],
    selected: "bar",
    reversed: false,
    options: {
      chart: {
        id: 'vuechart-example'
      },
      title: {
        text: 'Indicadores financeiros',
        align: 'center',
        style: {
          fontSize:  '20px',
        },
      },
      colors: ['#350FFB', '#00E396', '#FE0F00'],
      xaxis: {
        categories: [
         "Jan",
         "Fev",  
         "Mar",
         "Abr",
         "Mai",
         "Jun",
         "Jul",
         "Ago",
         "Set",
         "Oct",
         "Nov",
         "Dez"
        ]
      },

            yaxis: {
              reversed: false,
              axisTicks: {
                show: true
              }
            }
    },
    series: [{
            name: 'Lucro Líquido',
            data: [50,30,40,44, 55, 57, 56, 61, 58, 63, 60, 66],
          }, {
            name: 'Receita',
            data: [100,94,80,76, 85, 101, 98, 87, 105, 91, 114, 94],
          }, {
            name: 'Fluxo de Caixa Livre',
            data: [45,60,30,35, 41, 36, 26, 45, 48, 52, 53, 41],
          }]
  }),
  methods: {
    changeChart(e) {
      this.selected = e.target.value
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
div.chart-wrapper {
  display: flex;
  align-items: center;
  justify-content: center
}
</style>
