<script>
import { Line, mixins } from 'vue-chartjs';

export default {
    extends: Line,
    mixins: [mixins.reactiveProp],
    name: 'MeterGraph',
    props: {
        unit: String
    },
    data() {
        return {
            options: {
                legend: {
                    display: false
                },
                scales: {
                    xAxes: [{
                        type: 'time',
                        time: {
                            unit: 'minute'
                        },
                        ticks: {
                            fontSize: 20
                        }
                    }],
                    yAxes: [{
                        scaleLabel: {
                            display: true,
                            labelString: 'voltage (' + this.unit + ')',
                            fontSize: '20',
                        },
                        ticks: {
                            fontSize: 20
                        }
                    }]
                },
                responsive: true,
                maintainAspectRatio: false
            },
        }
    },
    mounted () {
        this.renderChart(this.chartData, this.options);
    }
}
</script>
