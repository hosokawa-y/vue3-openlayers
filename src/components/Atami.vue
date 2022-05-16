<template>
    <input type="checkbox" id="checkbox-atami" v-model="showLayer" @change="switchCenter" />
    <label for="checkbox">令和3年(2021年)7月1日 熱海地区 崩壊地当分布図</label>
    <div v-if="showLayer">
        <ol-vector-layer>
            <ol-source-vector :url="url" :format="geoJson">
            </ol-source-vector>
            <ol-style>
                <ol-style-stroke color="rgba(161,86,11,1)" :width="2"></ol-style-stroke>
                <ol-style-fill color="rgba(161,86,11,0.3)"></ol-style-fill>
            </ol-style>
        </ol-vector-layer>
        <ol-overlay :position="[139.063595, 35.096493]">
            <template v-slot="slotProps">
                <div class="overlay-content">
                    令和3年(2021年)7月1日 熱海地区 崩壊地当分布図<br>
                    Position: {{ slotProps.position }}
                </div>
            </template>
        </ol-overlay>
    </div>
</template>

<script lang="ts">
import {
    ref, inject
} from 'vue'
export default {
    emits: ['switch-center'],
    setup(_, { emit }) {
        const url = ref('src/data/崩壊地等分布図（熱海市伊豆山・逢初川）第３報(20210706).geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();
        const switchCenter = (e) => {
            console.log(e.target.checked)
            if (e.target.checked) {
                console.log("switch!")
                emit('switch-center', [139.063595, 35.096493])
            } 
        }

        return {
            url,
            geoJson,
            switchCenter
        }
    },
    data() {
        return {
            showLayer: false,
        }
    }
}
</script>

<style scoped>
</style>