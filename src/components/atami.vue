<template>
    <ol-vector-layer>
        <ol-source-vector :url="atamiHoukai" :format="geoJson">
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
        const atamiHoukai = ref('src/data/崩壊地等分布図（熱海市伊豆山・逢初川）第３報(20210706).geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();

        return {
            atamiHoukai,
            geoJson,
        }
    },
}
</script>

<style scoped>
</style>