<template>
    <ol-map :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:800px">

        <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>

        <div id="v-model-checkbox" class="demo">
            <input type="checkbox" id="checkbox" v-model="checked" />
            <label for="checkbox">六角川</label>
            <p v-if="checked">
                <Rokkakugawa />
            </p>
        </div>
    </ol-map>
</template>

<script lang="ts">
import {
    ref, inject
} from 'vue'
import Rokkakugawa from './rokkakugawa.vue'
export default {
    setup() {
        const center = ref([130.094129, 33.196412]);
        const projection = ref("EPSG:4326");
        const zoom = ref(12);
        const rotation = ref(0);
        const rokkakugawa = ref("../data/六角川_20210815.geojson");
        const format = inject("ol-format");
        const geoJson = new format.GeoJSON();
        const toggle = false;
        const checked = ref(true)

        return {
            center,
            projection,
            zoom,
            rotation,
            rokkakugawa,
            geoJson,
            toggle,
            checked
        };
    },
    components: { Rokkakugawa }
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
