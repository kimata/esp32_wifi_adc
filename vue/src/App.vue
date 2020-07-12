<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-12 text-center">
        <MeterValue :value="value" :unit="unit" />
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <MeterGraph :chart-data="graph_data" :unit="unit" />
      </div>
    </div>
  </div>
</template>

<script>
import MeterValue from './components/MeterValue.vue'
import MeterGraph from './components/MeterGraph.vue'

const MAX_HIST = 5 * 60;

export default {
    name: 'App',
    components: {
        MeterValue,
        MeterGraph
    },
    computed: {
        graph_data: function() {
            return {
                labels: this.hist_labels,
                datasets: [{
                    label: 'Voltage',
                    borderColor: '#999999',
                    backgroundColor: '#EEEEEE',
                    data: this.hist_values,
                }],
            };
        }
    },
    data() {
        return  {
            unit: 'mV',
            value: NaN,
            hist_labels: [new Date()],
            hist_values: [100],
        };
    },
    methods: {
        update_hist: function(value) {
            this.hist_labels.push(new Date());
            this.hist_values.push(value);

            if (this.hist_labels.length > MAX_HIST) {
                this.hist_labels.shift();
                this.hist_values.shift();
            }
        }
    },
    mounted () {
        setInterval(() => {
            this.value = Math.random() * 100;
            this.update_hist(this.hist_values.slice(-1)[0]+this.hist_values.slice(-1)[0]*(Math.random()-0.4)*0.1);
        }, 1000);
    },
}
</script>

<style>
#app {

}
#graph {
    
}
</style>
