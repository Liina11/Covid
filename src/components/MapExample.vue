<template>
<div>
    <button class="button is-primary" @click="goToHome">Go to home</button>
    <google-maps :lat="this.lat" :lng="this.lng" :zoom="this.zoom"></google-maps>
</div>
</template>

<script>
import GoogleMaps from './GoogleMaps.vue'
export default {
  components: { GoogleMaps },
    data(){
        return {
            lat: 59.4265182,
            lng: 24.7431717,
            zoom: 18.25
        }
    },
    methods: {
        goToHome(){
            this.lat=59.32471411,
            this.lng=24.5557187,
            this.zoom=18
        }
    }
}
</script>

<style>
</style> 