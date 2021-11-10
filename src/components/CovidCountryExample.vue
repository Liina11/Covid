<template>
<div>
  <h1 class="has-text-primary is-size-1">{{$route.params.country}}</h1>
  <chart v-if="data" :data="confirmed" :labels="labels" type="line"></chart>
  </div>
</template>

<script>
import Chart from './Chart.vue'
const axios = require('axios')
export default {
  components: { Chart },
  created(){
    axios.get('https://api.covid19api.com/total/country/'+this.$route.params.country).then(response => {
    console.log(response);
    this.data = response.data;
  })
  },
  data(){
    return{
      data: null
    }
},
computed: {
    labels(){
      return this.data.map(value => value.Date);
    },
    confirmed(){
      return this.data.map(value => value.Confirmed);
    }
  }
}
</script>

<style>
</style>