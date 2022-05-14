<template>
    <ol-vector-layer>
        <ol-source-vector :url="rokkakugawa" :format="geoJson">
        </ol-source-vector>
        <ol-style>
            <ol-style-stroke color="blue" :width="2"></ol-style-stroke>
            <ol-style-fill color="rgba(0,255,255,0.1)"></ol-style-fill>
        </ol-style>
    </ol-vector-layer>
</template>

<script lang="ts">
import {
    ref, inject
} from 'vue'
export default {
    setup() {
        const rokkakugawa = ref('src/data/六角川_20210815.geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();

        return {
            rokkakugawa,
            geoJson,
        }
    },
}
</script>

<style scoped>
</style>