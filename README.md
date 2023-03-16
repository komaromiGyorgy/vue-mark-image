# 🔎 Vue Magic Zoom

An easy to use image zoom lens library for Vue.js 3

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

```
import { MagicZoom } from "vue-pin-image"
```

### Use it in a Vue componens

```js
<MagicZoom src="/default-image.jpg" />
```

This will render the image and when you hover over it, it will show a little lens with a zoomed in version

## The `MagicZoom` component accepts the following props:

| Prop        | Type             | Default        | Description                                                                                                                             |
| ----------- | ---------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| src         | String           | -              | Required. This is the path to the image that you want to have the ability to zoom on.                                                   |
| zoomScale   | Number           | 4              | Optional. This Prop is used to determin the magnification scale of the magnifing lens.                                                  |
| aspectRatio | Number           | 16/9           | Otpional. This can be provided as a fraction like: `16/9`                                                                               |
| fit         | String           | `contain`      | Otpional. Determines aspect ratio of image                                                                                              |
| lensSize    | Number           | 200            | Optional. Size of lens in pixels, lens will be a square                                                                                 |
| width       | Number`\|`String | `100%`         | Optional. Determines width of image                                                                                                     |
| height      | Number`\|`String | `100%`         | Optional. Determines height of image                                                                                                    |
| alt         | String           | `Zoomed Image` | Optional. alt of image                                                                                                                  |
| modifier    | String           | ''             | Optional. KeyCode of a KeyboardEvent (ex.:`ControlLeft`) this will make it so that the lens only appears if the modifier key is pressed |

## Support

For any feedback or to report any issues or general implementation support, please reach out to [komi@yorgsoft.com](mailto:komi@yorgsoft.com)

## License

Released under the MIT license.
