# vue-colorpicker

## [LiveDemo](https://caohenghu.github.io/vue-colorpicker/)

![preview-dark](https://raw.githubusercontent.com/caohenghu/vue-colorpicker/master/src/img/preview-dark.jpg)
![preview-light](https://raw.githubusercontent.com/caohenghu/vue-colorpicker/master/src/img/preview-light.jpg)

## Install

```bash
$ yarn add @caohenghu/vue-colorpicker
```

## Example

```html
<template>
    <div :style="{background: color}">
        <color-picker
            theme="light"
            :color="color"
            :picker-hide="false"
            :picker-canvas="pickerCanvas"
            :picker-area="pickerArea"
            @changeColor="changeColor"
            @openPicker="openPicker"
        />
    </div>
</template>

<script>
    import colorPicker from '@caohenghu/vue-colorpicker'

    export default {
        components: {
            colorPicker,
        },
        data() {
            return {
                color: '#59c7f9',
                pickerCanvas: null,
                pickerArea: [],
                isPicking: false,
            }
        },
        methods: {
            changeColor(color) {
                const { r, g, b, a } = color.rgba
                this.color = `rgba(${r}, ${g}, ${b}, ${a})`
            },
            openPicker(isOpen) {
                if (isOpen) {
                    // ... canvas be created
                    // this.pickerCanvas = canvas
                    // this.pickerArea = [x1, y1, x2, y2]
                } else {
                    // this.pickerCanvas && this.pickerCanvas.remove
                }
            },
        },
    }
</script>
```

## Options

| Name               | Type              | Default                                                                                                                                                                                  | Description                             |
| ------------------ | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| theme              | String            | `dark`                                                                                                                                                                                   | `dark` or `light`                       |
| color              | String            | `#000000`                                                                                                                                                                                | `rgba` or `hex`                         |
| colors-default     | Array             | `['#000000', '#FFFFFF', '#FF1900', '#F47365', '#FFB243', '#FFE623', '#6EFF2A', '#1BC7B1', '#00BEFF', '#2E81FF', '#5D61FF', '#FF89CF', '#FC3CAD', '#BF3DCE', '#8E00A7', 'rgba(0,0,0,0)']` | like `['#ff00ff', '#0f0f0f', ...]`      |
| colors-history-key | String            | `vue-colorpicker-history`                                                                                                                                                                |
| picker-hide        | Boolean           | `true`                                                                                                                                                                                   | `true` or `false`                       |
| picker-canvas      | HTMLCanvasElement | `null`                                                                                                                                                                                   | like `document.createElement('canvas')` |
| picker-area        | Array             | `[]`                                                                                                                                                                                     | like `[x1, y1, x2, y2]`                 |

> `color` is one-way data flow, so you can't use `v-model`. why? because you'll listen `changeColor` event do more things, so i think it's not necessary here.

## Events

| Name        | Type     | Args   | Description                     |
| ----------- | -------- | ------ | ------------------------------- |
| changeColor | Function | color  | `{ rgba: {}, hsv: {}, hex: ''}` |
| openPicker  | Function | isOpen | `true` or `false`               |

> if you want use picker, then `openPicker`, `picker-hide`, `picker-canvas`, `picker-area` is necessary. when you click picker button, you can click it again or press key of `esc` to exit.
