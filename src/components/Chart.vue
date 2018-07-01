<template>
  <div>
    <div id="chart-area"></div>    
  </div>
</template>

<script>
import Vue from 'vue'
import tuiChart from 'tui-chart'
import axios from 'axios'

vue.use(tuiChart)

var container = document.getElementById('chart-area');

export default {
    name: 'Chart',
    mounted() {
        this.getWeightDataAndSetGraph()
    },
    methods: {
    
        getWeightDataAndSetGraph: function() {
            const baseURI = 'http://localhost:3000/api';
            axios.get('${baseURI}/weights')
                .then((response) => {
                    console.log(response);
                    setGraph(response);
                })
                .catch( response => { console.log(response); });
        },
        setGraph(weights){
            var weight_categories = [];
            var weight_data = [];
            for(var i=0; i<weights.length; i++){
                weight_categories.push(weights[i].register_ymdt);
                weight_data.push(weights[i].weight);
            }

            var data = {
                categories: weight_categories, 
                series: [
                    {
                        name: '체중',
                        data: weight_data
                    }
                ]
            };
            var options = {
                chart: {width: 700, height: 400}
            };

            var chart = tui.chart.lineChart(container, data, options);
        }
    }
}
</script>