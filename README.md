<p align="center">
  <a href="https://medium-zoom.francoischalifour.com"><img src="logo.svg" alt="Demo" width="64"></a>
  <h3 align="center">medium-zoom</h3>
  <p align="center">A JavaScript library for zooming images like Medium</p>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/medium-zoom">
    <img src="https://img.shields.io/npm/v/medium-zoom.svg?style=flat-square" alt="version">
  </a>
  <a href="https://github.com/francoischalifour/medium-zoom/blob/master/LICENSE">
    <img src="https://img.shields.io/npm/l/medium-zoom.svg?style=flat-square" alt="MIT license">
  </a>
  <a href="http://npmcharts.com/compare/medium-zoom">
    <img src="https://img.shields.io/npm/dm/medium-zoom.svg?style=flat-square" alt="downloads">
  </a>
  <br>
  <a href="https://unpkg.com/medium-zoom/dist/">
    <img src="http://img.badgesize.io/https://unpkg.com/medium-zoom/dist/medium-zoom.min.js?label=size&style=flat-square" alt="size">
  </a>
  <a href="https://unpkg.com/medium-zoom/dist/">
    <img src="http://img.badgesize.io/https://unpkg.com/medium-zoom/dist/medium-zoom.min.js?compression=gzip&label=gzip%20size&style=flat-square" alt="gzip size">
  </a>
  <a href="https://github.com/francoischalifour/medium-zoom/blob/master/package.json">
    <img src="https://img.shields.io/badge/dependencies-none-lightgrey.svg?style=flat-square" alt="no dependencies">
  </a>
</p>

<p align="center">
  <a href="https://medium-zoom.francoischalifour.com">
    <img src="https://user-images.githubusercontent.com/6137112/43369906-7623239a-9376-11e8-978b-6e089be499fb.gif" alt="Medium Zoom Demo">
  </a>
  <br>
  <br>
  <strong>
  <a href="https://codesandbox.io/s/github/francoischalifour/medium-zoom/tree/master/website">🔬 Playground</a> ・
  <a href="https://medium-zoom.francoischalifour.com">🔎 Demo</a> ・
  <a href="https://medium-zoom.francoischalifour.com/storybook">📚 Storybook</a>
  </strong>
</p>

<details>
  <summary><strong>Contents</strong></summary>

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Import the library](#1-import-the-library)
  - [Use the library](#2-use-the-library)
- [API](#api)
  - [Options](#options)
  - [Methods](#methods)
  - [Data attributes](#data-attributes)
  - [Events](#events)
- [Examples](#examples)
- [Demo](#demo)
- [Browser support](#browser-support)
- [Development](#development)
- [Contributing](#contributing)
- [License](#license)
  </details>

## Features

- 📱 **Responsive** — _scale on mobile and desktop_
- 🚀 **Performant and lightweight** — _should be able to reach 60 [fps](https://en.wikipedia.org/wiki/Frame_rate)_
- ⚡️ **High definition support** — _load the HD version of your image on zoom_
- 🔎 **Flexibility** — _apply the zoom to a selection of images_
- 🖱 **Mouse, keyboard and gesture friendly** — _click anywhere, press a key or scroll away to close the zoom_
- 🎂 **Event handling** — _trigger events when the zoom enters a new state_
- 📦 **Customization** — _set your own margin, background and scroll offset_
- 🔧 **Pluggable** — _add your own features to the zoom_
- 💎 **Custom templates** — _extend the default look to match your app UI_

## Installation

This module is available on the [npm](https://www.npmjs.com) registry, with no dependencies.

```sh
npm install medium-zoom
# or
yarn add medium-zoom
```

###### Download

- [Normal](https://cdn.jsdelivr.net/npm/medium-zoom/dist/medium-zoom.js)
- [Minified](https://cdn.jsdelivr.net/npm/medium-zoom/dist/medium-zoom.min.js)

###### CDN

- [jsDelivr](https://www.jsdelivr.com/package/npm/medium-zoom)
- [unpkg](https://unpkg.com/medium-zoom/)

## Usage

### 1. Import the library

Using imports:

```js
import mediumZoom from 'medium-zoom'
```

Using script tags:

```html
<script src="node_modules/medium-zoom/dist/medium-zoom.min.js"></script>
```

That's it! You don't need to import any CSS styles.

### 2. Use the library

```js
mediumZoom(selector?, options?)
```

You can specify the zoomable images with a [CSS selector](http://www.w3schools.com/cssref/css_selectors.asp) and add [options](#options).

The selector can also be an [HTML Element](https://developer.mozilla.org/en-US/docs/Web/API/Element), a [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList), an [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection) or an array of images.

```js
// CSS selector
mediumZoom('#cover')

// HTML Element
mediumZoom(document.getElementById('cover'))

// NodeList
mediumZoom(document.querySelectorAll('[data-action="zoom"]'))

// HTMLCollection
mediumZoom(document.images)

// Array
const imagesToZoom = [
  document.querySelector('#cover'),
  ...document.querySelectorAll('[data-action="zoom"]'),
]

mediumZoom(imagesToZoom)
```

## API

### Options

Options can be passed as an object to the second argument of the `mediumZoom` function.

| Property       | Type                          | Default  | Description                                                                                      |
| -------------- | ----------------------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `margin`       | `number`                      | `0`      | The space outside the zoomed image                                                               |
| `background`   | `string`                      | `"#fff"` | The color of the overlay                                                                         |
| `scrollOffset` | `number`                      | `48`     | The number of pixels to scroll to close the zoom                                                 |
| `container`    | `string`\|`Element`\|`object` |          | The element to render the zoom in or a viewport object. [Read more →](#using-a-custom-container) |
| `template`     | `string`\|`Element`           |          | The template element to show on zoom. [Read more →](#using-a-custom-template)                    |

```js
mediumZoom('[data-action="zoom"]', {
  margin: 24,
  background: '#000',
  scrollOffset: 0,
  container: '#zoom-container',
  template: '#zoom-template',
})
```

#### Using a custom `container`

The zoom is by default rendered in the window viewport. You can also render your image in any element of the DOM, or any custom coordinates with the `container` option.

##### Rendering in a DOM Element

```html
<article>
  <p>My article...</p>
  <img src="image.jpg" alt="My image">
  <div id="zoom-container"></div>
</article>

<script>
  mediumZoom('img', {
    container: '#zoom-container' // or document.querySelector('#zoom-container')
  })
</script>
```

##### Rendering with coordinates

If you don't already have an element in your DOM to specify the position of the zoom, you can pass an object with the following `number` properties:

```js
mediumZoom('img', {
  container: {
    width: 720,
    height: 480,
    top: 64,
    bottom: 64,
    right: 0,
    left: 0,
  },
})
```

These properties behave very much like [`Element.getBoundingClientRect()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect). They will get merged with the default ones so you don't need to specify all of them.

The default `width` and `height` are `window.innerWidth` and `window.innerHeight`. Others are set to `0`.

#### Using a custom `template`

You might want to render the zoom in your own template. You could reproduce zooms as seen on [Facebook](examples/facebook-template) or [Dropbox Paper](examples/dropbox-paper-template). This is possible with the `template` option.

1.  Create a [`template`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template) element matching the `template` option value
2.  If you'd like your image to appear at a specific position in your template, specify the `container` option and add it in your template (`#zoom-container` here)

```html
<template id="zoom-template">
  <div>
    <header>My image zoom template</header>
    <div id="zoom-container"></div>
    <aside>Comment on my image</aside>
  </div>
</template>

<script>
  mediumZoom('[data-action="zoom"]', {
    template: '#zoom-template',
    container: '#zoom-container'
  })
</script>
```

Go to the [`examples/`](examples) folder for more details.

### Methods

#### `.open({ target? })`

Opens and returns a promise resolving the zoom.

```js
const zoom = mediumZoom('#my-image')

zoom.open()
```

_Emits an event [`open`](#events) on animation start and [`opened`](#events) when completed._

#### `.close()`

Closes and returns a promise resolving the zoom.

```js
const zoom = mediumZoom('#my-image')

zoom.close()
```

_Emits an event [`close`](#events) on animation start and [`closed`](#events) when completed._

#### `.toggle({ target? })`

Opens the zoom when closed / dismisses the zoom when opened, and returns a promise resolving the zoom.

```js
const zoom = mediumZoom('#my-image')

zoom.toggle()
```

#### `.attach(...selectors)`

Attaches the images to the zoom and returns the zoom.

```js
const zoom = mediumZoom()

zoom.attach('#image-1', '#image-2')
zoom.attach(
  document.querySelector('#image-3'),
  document.querySelectorAll('aside img')
)
```

#### `.detach(...selectors?)`

Releases the images attached to the zoom and returns the zoom.

```js
const zoom = mediumZoom('.content img')

zoom.detach('#image-1', document.querySelector('#image-2')) // detach two images
zoom.detach() // detach all images
```

_Emits an event [`detach`](#events)._

#### `.update(options)`

Updates the options and returns the zoom.

```js
const zoom = mediumZoom('#my-image')

zoom.update({
  background: '#000',
})
```

_Emits an event [`update`](#events)._

#### `.extend(options?)`

Clones the zoom with new options to merge with the current ones, and returns the zoom.

```js
const zoom = mediumZoom('#my-image', { background: '#000' })

const extendedZoom = zoom.extend({
  margin: 48,
})
```

#### `.on(type, listener, options?)`

Registers the specified listener on each target of the zoom.

```js
const zoom = mediumZoom('[data-action="zoom"]')

zoom.on('closed', event => {
  // the image has been closed
})

zoom.on(
  'open',
  event => {
    // the image has been opened (tracked only once)
  },
  { once: true }
)
```

You can use the same `options` as the [`addEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#Parameters) method.

#### `.off(type, listener, options?)`

Removes the previously registered listener on each target of the zoom.

```js
const zoom = mediumZoom('[data-action="zoom"]')

const listener = event => {
  /* ... */
}

zoom.on('closed', listener)
// ...
zoom.off('closed', listener)
```

You can use the same `options` as the [`removeEventListener`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener#Parameters) method.

#### `.getOptions()`

Returns the zoom options.

#### `.getImages()`

Returns the images attached to the zoom.

#### `.getZoomedTarget()`

Returns the current zoomed target.

### Data attributes

#### `data-zoom-target`

Specifies the high definition image to show on zoom. This image loads when the user clicks on the source image, only once.

```html
<img
  src="image-thumb.jpg"
  data-zoom-target="image-hd.jpg"
  alt="My image"
>
```

### Events

| Event  | Description                                         |
| ------ | --------------------------------------------------- |
| open   | Fired immediately when the `open` method is called  |
| opened | Fired when the zoom has finished being animated     |
| close  | Fired immediately when the `close` method is called |
| closed | Fired when the zoom out has finished being animated |
| detach | Fired when the `detach` method is called            |
| update | Fired when the `update` method is called            |

```js
const zoom = mediumZoom('#image-tracked')

zoom.on('open', event => {
  // track when the image is zoomed...
})
```

You can access the zoom object in `event.detail.zoom`.

## Examples

<details>
 <summary>Declare zoomable images with data attributes</summary>

A common pattern to declare images as zoomable is to use [data attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*).

```js
mediumZoom('[data-action="zoom"]')
```

</details>

<details>
 <summary>Attach a zoom to external images</summary>

```js
mediumZoom('img[src^="http"]')
```

</details>

<details>
 <summary>Attach a zoom to images from a database</summary>

```js
fetch(`https://myapi.com/posts/${postId}`)
  .then(response => response.json())
  .then(post => {
    const imagesToZoom = post.images.map(imgSrc =>
      document.querySelector(`img[src=${imgSrc}]`)
    )

    mediumZoom(imagesToZoom)
  })
```

</details>

<details>
 <summary>Attach a zoom using React refs</summary>

```js
import React, { Component } from 'react'
import mediumZoom from 'medium-zoom'

const zoom = mediumZoom({ background: '#000' })

class ZommableImage extends Component {
  constructor(props) {
    this.zoom = this.props.zoom.extend({
      background: props.color,
    })
  }

  attachZoom = image => {
    this.zoom.attach(image)
  }

  render() {
    return <img src={props.src} alt={props.alt} ref={this.attachZoom} />
  }
}

class App extends Component {
  render() {
    return (
      <ZommableImage src="image.jpg" alt="Image" zoom={zoom} color="#fff" />
    )
  }
}
```

</details>

<details>
 <summary>Trigger a zoom from another element</summary>

You sometimes want to trigger a zoom when the user clicks somewhere else.

```js
const button = document.querySelector('#btn-zoom')
const zoom = mediumZoom('#image')

button.addEventListener('click', () => zoom.open())
```

</details>

<details>
 <summary>Track an event (for analytics)</summary>

You can use the `open` event to keep track of how many times a user interacts with your image. This can be useful if you want to gather some analytics on user engagement.

```js
let counter = 0
const zoom = mediumZoom('#image-tracked')

zoom.on('open', event => {
  console.log(`"${event.target.alt}" has been zoomed ${++counter} times`)
})
```

</details>

<details>
 <summary>Detach a zoom once closed</summary>

```js
const zoom = mediumZoom('#image-detach')

zoom.on('closed', () => zoom.detach(), { once: true })
```

</details>
<br>

You can see [more examples](examples/) including [React](examples/react) and [Vue](examples/vue), or check out the [storybook](https://medium-zoom.francoischalifour.com/storybook).

## Demo

[Check out the demo](https://medium-zoom.francoischalifour.com), go to the [examples folder](examples/), see the [storybook](https://medium-zoom.francoischalifour.com/storybook) or [read the article](https://francoischalifour.com/lab/medium-image-zoom).

## Browser support

| IE              | Edge            | Chrome | Firefox | Safari |
| --------------- | --------------- | ------ | ------- | ------ |
| 10<sup>\*</sup> | 12<sup>\*</sup> | 36     | 34      | 9      |

<sup>\*</sup> _These browsers require a [`<template>` polyfill](https://github.com/webcomponents/template) when using [custom templates](#using-a-custom-template)_.

## Development

- Run `yarn` to install Node dev dependencies
- Run `yarn run dev` to build the `medium-zoom` library in watch mode
- Run `yarn run storybook` to see your changes at http://localhost:9001
- Add a story in the [storybook](stories) when you add a new feature
- Add your tests and run `yarn run test` to make sure it works

_You can also use [npm](https://www.npmjs.com)._

## Contributing

Need more options? Send a pull request!

1.  [Fork the repository](https://help.github.com/articles/fork-a-repo/)
2.  [Create a new branch](https://help.github.com/articles/creating-and-deleting-branches-within-your-repository/#creating-a-branch)
3.  [Send a pull request](https://help.github.com/articles/creating-a-pull-request/) 👌

## License

MIT © [François Chalifour](https://francoischalifour.com)
