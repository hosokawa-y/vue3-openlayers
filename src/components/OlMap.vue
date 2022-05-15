<template>
    <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:800px">

        <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />
        <ol-fullscreen-control />
        <ol-mouseposition-control />
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>
        <li class="layerPanel">
            <ul>
                <input type="checkbox" id="checkbox-rokkakugawa" v-model="switchrokkakugawa" />
                <label for="checkbox">令和3年(2021年)8月 六角川 浸水想定図</label>
                <p v-if="switchrokkakugawa">
                    <Rokkakugawa />
                </p>
            </ul>
            <ul>
                <input type="checkbox" id="checkbox-atami" v-model="switchatami" @change="switchCenter" />
                <label for="checkbox">令和3年(2021年)7月1日 熱海地区 崩壊地当分布図</label>
                <p v-if="switchatami">
                    <Atami />
                </p>
            </ul>
        </li>
    </ol-map>
</template>

<script lang="ts">
import {
    ref
} from 'vue'
import Rokkakugawa from './rokkakugawa.vue'
import Atami from './atami.vue'
export default {
    setup() {
        const center = ref([130.094129, 33.196412]);
        // const center = ref([139.063595, 35.096493]);
        const projection = ref("EPSG:4326");
        const zoom = ref(12);
        const rotation = ref(0);
        const switchCenter = (e) => {
            if (e.target.checked) {
                center.value = [139.063595, 35.096493]
            }
        }


        return {
            center,
            projection,
            zoom,
            rotation,
            switchCenter,
        };
    },
    data() {
        return{
            switchatami: false,
            switchrokkakugawa: false,
        }
    },
    components: { Rokkakugawa, Atami }
}
</script>

<style scoped>
.layerPanel {
    font-family: sans-serif;
    border: 1px solid #eee;
    border-radius: 2px;
    padding: 20px 30px;
    margin-top: 1em;
    margin-bottom: 40px;
    user-select: none;
    overflow-x: auto;
    list-style: none;
}
</style>
