<template>
    <li v-for="layer in layers" :key="layer.id">
        <input type="checkbox" :id="layer.id" @change="switchCenter(layer.center, $event, layer)" />
        <label for="checkbox">{{ layer.label }}</label>
        <p v-if="layer.flg">{{ layer.label }}</p>
        <div v-if="layer.flg">
            <ol-vector-layer>
                <ol-source-vector :url="layer.url" :format="geoJson">
                </ol-source-vector>
                <ol-style>
                    <ol-style-stroke :color="layer.strokeColor" :width="2"></ol-style-stroke>
                    <ol-style-fill :color="layer.fillColor"></ol-style-fill>
                </ol-style>
            </ol-vector-layer>
        </div>
    </li>
</template>

<script lang="ts">
import {
    ref, inject
} from 'vue'

type Layer = {
    id: number,
    url: string,
    center: Array<number>,
    strokeColor: string,
    fillColor: string,
    label: string
}
type Props = {
    layers: Layer[]
}

export default {
    props: ['layers'],
    emits: ['switch-center'],
    setup(_, { emit }) {
        const id = ref(0)
        const url = ref('src/data/六角川_20210815.geojson')
        const format = inject('ol-format');
        const geoJson = new format.GeoJSON();
        const strokeColor = ref("red")
        const fillColor = ref("rgba(0,255,255,0.1)")
        const switchCenter = (center, e, layer) => {
            console.log("e: " + e.target.checked)
            console.log("center:" + center)
            layer.flg = e.target.checked
            if (e.target.checked) {
                emit('switch-center', center)
            }
        }

        return {
            id,
            url,
            geoJson,
            switchCenter,
            strokeColor,
            fillColor
        }
    }
}
</script>

<style scoped>
</style>