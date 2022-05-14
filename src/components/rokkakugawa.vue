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
        const center = ref([130.094129, 33.196412])
        const projection = ref('EPSG:4326')
        const zoom = ref(12)
        const rotation = ref(0)
        const rokkakugawa = ref('src/data/六角川_20210815.geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();
        const toggle = false

        return {
            center,
            projection,
            zoom,
            rotation,
            rokkakugawa,
            geoJson,
            toggle
        }
    },

    data() {
        return {
            checked: true
        }
    }
}
</script>

<style scoped>
.demo {
    font-family: sans-serif;
    border: 1px solid #eee;
    border-radius: 2px;
    padding: 20px 30px;
    margin-top: 1em;
    margin-bottom: 40px;
    user-select: none;
    overflow-x: auto;
}
</style>