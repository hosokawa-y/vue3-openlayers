<template>
    <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:800px">

        <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />
        <ol-fullscreen-control />
        <ol-mouseposition-control />
        <ol-attribution-control :collapsible="collapsible" />
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>
        <!-- <ol-tile-layer>
            <ol-source-xyz :url="chiriin" :crossOrigin="crossOrigin"/>
        </ol-tile-layer> -->
        <li class="layerPanel">
            <ul>
                <Rokkakugawa @switch-center="switchCenter" />
            </ul>
            <ul>
                <Atami @switch-center="switchCenter" />
            </ul>
        </li>
    </ol-map>
</template>

<script lang="ts">
import {
    ref
} from 'vue'
import Rokkakugawa from './Rokkakugawa.vue'
import Atami from './Atami.vue'
export default {
    setup() {
        const center = ref([130.094129, 33.196412]);
        const projection = ref("EPSG:4326");
        const zoom = ref(12);
        const rotation = ref(0);
        const collapsible = true
        const switchCenter = (point: Array<number>) => {
            console.log("switch center!!!!")
            center.value = point
        }
        const chiriin = ref('https://cyberjapandata.gsi.go.jp/xyz/std/{z}/{x}/{y}.png')
        const crossOrigin = 'anonymous'
        return {
            center,
            projection,
            zoom,
            rotation,
            switchCenter,
            collapsible,
            chiriin,
            crossOrigin
        };
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
