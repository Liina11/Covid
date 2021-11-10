<template>
  <div >
      <div class="columns is-multiline" >
          <div class="column is-one-quarter" v-for="result in results" :key="result.id">
            <character-card :character="result">
            </character-card>
          </div>
      </div>
      <h1 class="is-size-1" v-if="!info.next">There is no more results</h1>
  </div>
</template>

<script>
import CharacterCard from './CharacterCard.vue';
import Pagination from './Pagination.vue';
const axios = require('axios');
export default {
  components: { CharacterCard, Pagination },
    created(){
        axios.get('https://rickandmortyapi.com/api/character').then(response => {
            console.log(response.data);
            this.info = response.data.info;
            this.results = response.data.results;
        });
        
        window.addEventListener('scroll', this.scroll);
    },
    data(){
        return {
            info: {
                next: null,
                prev: null,
                pages: 0,
                count: 0
            },
            results: [],
            current: 1
        }
    },
    methods: {
        next(){
            axios.get(this.info.next).then(response => {
                console.log(response.data);
                this.info = response.data.info;
                this.results.push(...response.data.results);
            });
        },
        scroll(){
            console.log(window.scrollY + window.innerHeight, document.body.clientHeight);
            if(window.scrollY + window.innerHeight > document.body.clientHeight - 100 && this.info.next){
                this.next();
            }
        }
    }
}
</script>

<style>
</style>