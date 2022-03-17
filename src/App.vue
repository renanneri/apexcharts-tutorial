<template>
  <div id="app">
    <h1>Testador Vue ApexCharts</h1>
    <div id="options">
    <div>
      <input 
        type="checkbox" 
        id="checkbox" 
        v-model="options.yaxis.reversed"
        @change.prevent="changeReversed"
      >
      <label 
        for="checkbox"
      >
        Revertido
      </label>
    </div>
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
      @input="changeTitle"
    >
    </div>
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
      { Name:"Radar", Value: "radar" },
      { Name:"Pontos", Value: "scatter" }
    ],
    selected: "bar",
    options: {
      chart: {
        id: 'vuechart-example'
      },
      /*
      dataLabels: {
        enabled: false
      },
      */
      title: {
        text: 'Indicadores financeiros',
        align: 'center',
        style: {
            fontSize:  '20px',
            fontWeight:  'bold',
            fontFamily:  undefined,
            color:  '#263238'
        },
      },
      colors: ['#003f5c', '#bc5090', '#ffa600'],
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
        reversed: true,
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
    },
    changeReversed(e) {
      this.options = {
        ...this.options,
        yaxis: {
          ...this.options.yaxis,
          reversed: e.target.checked
        }
      }
      this.$forceUpdate();
    },
    changeTitle(e) {
      console.log(e.target.value)
      this.options = {
        ...this.options,
        title: {
          ...this.options.title,
          text: e.target.value
        }
      }
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

#options {
  display: flex;
  text-align: justify;
  flex-direction: row;
  justify-content: center;
  margin: 40px 40px;
  gap: 20px;
}

div.chart-wrapper {
  display: flex;
  align-items: center;
  justify-content: center
}
</style>
