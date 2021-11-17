<template>
  <div id="map"></div>
</template>

<script>
import { Loader } from "@googlemaps/js-api-loader"
export default {
    props:['lat', 'lng', 'zoom'],
    mounted(){
    const loader = new Loader({
        apiKey: "AIzaSyBDLJHO_LGCc6KbmteH9bgcLheX9vfX05Y",
        version: "weekly"
});
    loader.load().then(() => {
        this.map = new google.maps.Map(document.getElementById("map"), {
        center: { lat: this.lat, lng: this.lng },
        zoom: this.zoom,
  });
});
    },
    data(){
        return {
            map: null
        }
    },
    watch: {
        lat(lat){
            this.map.panTo({lat: lat, lng:this.lng});
        },
        lng(lng){
            this.map.panTo({lat:this.lat, lng: lng});
        },
        zoom(zoom){
            this.map.setZoom(zoom);
        }
    }
}
</script>

<style scoped>
    #map{
        height: 800px;
        width:1800px;
    }
</style> 