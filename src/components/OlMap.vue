<template>
    <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:800px">

        <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />
        <ol-fullscreen-control />
        <ol-mouseposition-control />
        <ol-attribution-control :collapsible="collapsible" />
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>
        <ol-tile-layer>
            <ol-source-xyz :url="chiriin" :crossOrigin="crossOrigin" />
        </ol-tile-layer>
        <div class="layerPanel">
            <vectorLayer :layers="layers" @switch-center="switchCenter" />
        </div>
    </ol-map>
</template>

<script lang="ts">
import {
    ref,
} from 'vue'
import vectorLayer from './VectorLayer.vue'

export default {
    setup() {
        const atami = {
            id: 1,
            url: "src/data/崩壊地等分布図（熱海市伊豆山・逢初川）第３報(20210706).geojson",
            center: [139.063595, 35.096493],
            strokeColor: "rgba(161,86,11,1)",
            fillColor: "rgba(161,86,11,0.3)",
            label: "令和3年(2021年)7月1日 熱海地区 崩壊地当分布図",
            flg: false
        }
        const rokkakugawa = {
            id: 2,
            url: "src/data/六角川_20210815.geojson",
            center: [130.094129, 33.196412],
            strokeColor: "blue",
            fillColor: "rgba(0,255,255,0.1)",
            label: "令和3年(2021年)8月 六角川 浸水想定図",
            flg: false
        }
        const layers = ref([atami, rokkakugawa])
        const center = ref([130.094129, 33.196412]);
        const projection = ref("EPSG:4326");
        const zoom = ref(12);
        const rotation = ref(0);
        const collapsible = true
        const switchCenter = (point: Array<number>) => {
            console.log("switch center!!!!")
            center.value = point
        }
        const chiriin = ref("https://cyberjapandata.gsi.go.jp/xyz/20140711dol/{z}/{x}/{y}.png")
        const crossOrigin = "anonymous"
        return {
            center,
            projection,
            zoom,
            rotation,
            switchCenter,
            collapsible,
            chiriin,
            crossOrigin,
            layers
        };
    },
    components: { vectorLayer }
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
