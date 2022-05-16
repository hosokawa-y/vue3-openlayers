<template>
    <input type="checkbox" id="checkbox-rokkakugawa" v-model="switchRokkakugawa" @change="switchCenter" />
    <label for="checkbox">令和3年(2021年)8月 六角川 浸水想定図</label>
    <p v-if="switchRokkakugawa">
        <ol-vector-layer>
            <ol-source-vector :url="rokkakugawa" :format="geoJson">
            </ol-source-vector>
            <ol-style>
                <ol-style-stroke color="blue" :width="2"></ol-style-stroke>
                <ol-style-fill color="rgba(0,255,255,0.1)"></ol-style-fill>
            </ol-style>
        </ol-vector-layer>
    </p>
</template>

<script lang="ts">
import {
    ref, inject
} from 'vue'
export default {
    emits: ['switch-center'],
    setup(_, { emit }) {
        const rokkakugawa = ref('src/data/六角川_20210815.geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();
        const switchCenter = () => {
            console.log("switch")
            emit('switch-center', [130.094129, 33.196412])
        }

        return {
            rokkakugawa,
            geoJson,
            switchCenter
        }
    },
    data() {
        return {
            switchRokkakugawa: false
        }
    }
}
</script>

<style scoped>
</style>