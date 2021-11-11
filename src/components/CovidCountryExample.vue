<template>
<div>
  <h1 class="has-text-primary is-size-1">{{$route.params.country}}</h1>
  <button class="button is-warning" @click="active='confirmed'">Confirmed</button>
  <button class="button is-danger" @click="active='deaths'">Deaths</button>
  <chart v-if="data" :data="this[active]" :labels="labels" type="line"></chart>
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
      data: null,
      active: 'confirmed'
    }
},
computed: {
    labels(){
      return this.data.map(value => value.Date);
    },
    confirmed(){
      return this.data.map(value => value.Confirmed);
    },
    deaths(){
      return this.data.map(value => value.Deaths);
    }
  }
}
</script>

<style>
</style>