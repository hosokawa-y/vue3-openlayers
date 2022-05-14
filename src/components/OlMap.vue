<template>
    <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:800px">

        <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>
        <li class="layerCheckbox">
            <ul>
                <input type="checkbox" id="checkbox-rokkakugawa" v-model="checkedR" />
                <label for="checkbox">令和3年(2021年)8月 六角川 浸水想定図</label>
                <p v-if="checkedR">
                    <Rokkakugawa />
                </p>
            </ul>
            <ul>
                <input type="checkbox" id="checkbox-atami" v-model="checkedA" />
                <label for="checkbox">令和3年(2021年)7月1日 熱海地区 崩壊地当分布図</label>
                <p v-if="checkedA">
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
        const projection = ref("EPSG:4326");
        const zoom = ref(12);
        const rotation = ref(0);
        const toggle = false;
        const checkedR = ref(true)
        const checkedA = ref(true)

        return {
            center,
            projection,
            zoom,
            rotation,
            toggle,
            checkedR,
            checkedA
        };
    },
    components: { Rokkakugawa, Atami }
}
</script>

<style scoped>
.layerCheckbox {
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
