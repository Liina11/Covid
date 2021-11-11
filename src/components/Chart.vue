<template>
  <div>
        <canvas ref="myChart" width="1800px" height="800px"></canvas>
</div>
</template>
<script>
import { Chart, registerables } from 'chart.js';
Chart.register(...registerables);
export default {
    props:['data', 'labels', 'type'],
    mounted(){
        const ctx = this.$refs['myChart']; 
        this.myChart = new Chart(ctx, {
    type: this.type,
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        labels: this.labels,
        datasets: [{
            label: '# of Votes',
            data: this.data,
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        responsive: false,
        scales: {
            y: {
                beginAtZero: true
            }
        }
    }
});
console.log(this.myChart);
    },
    data(){
        return{
            myChart: null,
        }
    },
    watch: {
        data: {
            handler(data){
            this.myChart.data.datasets[0].data = data;
            this.myChart.update();
            },
            deep:true,
        }
    },
    labels: {
            handler(labels){
            this.myChart.data.labels = labels;
            this.myChart.update();
            },
            deep:true,
        },
        type: {
            handler(type){
            this.myChart.type = type;
            this.myChart.update();
            console.log(this.myChart);
            },
            deep:true,
        }
}
    </script>
<style>
</style>