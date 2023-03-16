# 📌 Vue Pin Image

An easy to use image marker library for vue3

## Installation

```shell
npm install --save vue-pin-image

or

yarn add vue-pin-image

or

pnpm i vue-pin-image
```

## Usage

### Import the magic zoom componet.

```js
import { PinImage } from "vue-pin-image"
```

### Use it in a Vue componens

```js
const markers = ref([]);
watchEffect(() => {
    console.log(markers.value);
})

<PinImage src="/default-image.jpg" v-model:markers="markers" />
```

This will render the image and when you hover over it, it will show a little lens with a zoomed in version

## The `MagicZoom` component accepts the following props:

| Prop        | Type             | Default        | Description                                                                                                                             |
| ----------- | ---------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| markers         | Array[{ x: number, y: number }]| - | Required. This will store all your markers                                                  |
| disable   | Boolean           | false              | Optional. This prop makes the pins disabled and removes pointer events.                                                  |

## Support

For any feedback or to report any issues or general implementation support, please reach out to [komi@yorgsoft.com](mailto:komi@yorgsoft.com)

## License

Released under the MIT license.
