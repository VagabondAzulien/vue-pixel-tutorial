<template>
    <div id="app">
        <ColorPicker :color=color />
        <Canvas :pixels=pixels />
    </div>
</template>

<script>
import Canvas from './components/Canvas.vue'
import ColorPicker from './components/ColorPicker'

const defaultPixelColor = 'white'

export default {
    name: 'app',
    data: function() {
        return {
            color: defaultPixelColor,
            pixels: Array(30 * 30).fill().map(() => defaultPixelColor)
        }
    },
    components: {
        Canvas,
        ColorPicker
    },
    mounted() {
        this.$root.$on('updatecolor', color => {
            this.color = color
        })
        this.$root.$on('clickedpixel', index => {
            this.pixels.splice(index, 1, this.color)
        })
    }
}
</script>

<style>

#app {
    background-color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}
</style>
