<template>
<div>
    <button class="button is-primary" @click="goToHome">Go to home</button>
    <!-- <google-maps :lat="this.lat" :lng="this.lng" :zoom="this.zoom"></google-maps> -->
    <leaflet-map :lat="lat" :lng="lng" :zoom="zoom" :geoJson="covidGeoJson"></leaflet-map>
</div>
</template>

<script>
import GoogleMaps from './GoogleMaps.vue';
import LeafletMap from './LeafletMap.vue';
import axios from 'axios';
export default {
  components: { GoogleMaps, LeafletMap },
    created(){
        let url = 'https://raw.githubusercontent.com/johan/world.geo.json/master/countries.geo.json'
        axios.get(url).then(response =>{
            console.log(response.data);
            this.geoJson = response.data;
        });
        axios.get('https://api.covid19api.com/summary').then(response => {
            console.log(response);
            this.countries=response.data.Countries;
        })
    },
    data(){
        return {
            lat: 59.4265182,
            lng: 24.7431717,
            zoom: 18.25,
            geoJson: null,
            countries: null
        }
    },
    methods: {
        goToHome(){
            this.lat=59.4113121;
            this.lng=24.7031906;
            this.zoom=18;
        }
    },
    computed: {
        covidGeoJson(){
            if(this.geoJson && this.countries){
                let covidGeoJson = {...this.geoJson};
                covidGeoJson.features = this.geoJson.features.map(feature => {
                    let country = this.countries.find(country => country.Country == feature.properties.name);
                    feature.properties.confirmed=-1;
                    feature.properties.deaths=-1;
            if(country){
                feature.properties.confirmed = country.TotalConfirmed;
                feature.properties.deaths = country.TotalDeaths;
            }
                return feature;
            });
            return covidGeoJson;
            }
            return null;
        }
    }
}
</script>

<style>
</style>