<template>
    <div class="mapContainer">
        <div id="map"></div>
        <div class="coordinates">Latitude: {{ lat }}, Longitude: {{ lng }}</div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import "leaflet/dist/leaflet.css";
import * as L from 'leaflet';
import 'leaflet-iiif';
import { JsonMapDelimiter } from '../data/JsonMapDelimiter';

const initialMap = ref(null);

onMounted(() => {
    const iiifUrl = "https://iiif.oldmapsonline.org/export/40c9d955-d5e1-42ca-9531-93ae5d81bc75/info.json";

    const bounds = L.latLngBounds(
        [41.92382812500001, 9.102096738726456], 
        [11.523087506868514, 51.8554687500000]  
    );

    initialMap.value = L.map('map', {
        zoomControl: true,
        zoomAnimation: true,
        fadeAnimation: true,
        markerZoomAnimation: true,
        maxBounds: bounds,
        maxBoundsViscosity: 4.0,
        minZoom: 5,
        maxZoom: 10,
    }).setView([23.8041, 90.4152], 10);

    initialMap.value.on('click', (e) => {
        lat.value = e.latlng.lat;
        lng.value = e.latlng.lng;
        const marker = L.marker(e.latlng).addTo(initialMap.value);
        console.log(lat.value, lng.value);
    });


    L.tileLayer.iiif(iiifUrl).addTo(initialMap.value);

    initialMap.value.setMaxBounds(bounds);
});
</script>

<style scoped>
.mapContainer {
    height: 100vh;
    width: 100vw;
    margin: 0;
    padding: 0;
    position: relative;
    
}

#map {
    height: 100%;
    width: 100%;
}

.coordinates {
    position: absolute;
    bottom: 10px;
    left: 10px;
    background-color: rgba(255, 255, 255, 0.8);
    padding: 5px 10px;
    border-radius: 5px;
    font-size: 14px;
}
</style>
