<template>
  <h1 class="is-size-1">{{ joke }}</h1>
</template>

<script>
const axios = require('axios');
export default {
    created(){
        axios.get('https://api.chucknorris.io/jokes/random').then(response => {
            console.log(response.data);
            this.joke = response.data.value;
        });
    },
    data(){
        return {
            joke: ''
        }
    }
}
</script>

<style>
</style>