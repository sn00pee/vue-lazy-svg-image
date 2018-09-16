# Vue Lazy SVG image

use SVGs as a placeholder for lazy loading images.
### install
```bash
yarn install vue-lazy-svg-image
```

```javaScript
import Vue from 'vue'
import LazySvgImage from 'vue-lazy-svg-image'

Vue.use(LazySvgImage)
```

```javaScript
// SVGs should be imported with vue-svg-loader to import inline svgs
<LazySvgImage svg="svgfile" image="path/to/image"><LazySvgImage>
```

### css
```scss
// .lazy-transition (Vue transition) controls the image's transition when its ready
// by default the scss left blank (this is just an example)
.lazy-transition-enter, .lazy-transition-leave {
  opacity: 0;
}
.lazy-transition-enter-active, .lazy-transition-leave-to {
  transition: opacity 300ms;
}

// .lazy-svg uses animation to animate the svg's path
// .lazy-image is the image class
.lazy-svg, .lazy-image {
  position: absolute;
}

.lazy-svg {
  path {
    stroke: #000;
    stroke-miterlimit: 10;
    stroke-width: 1px;
    fill: transparent;
    stroke-dasharray: 610;
    stroke-dashoffset: 610;
    // stroke-width: 0;
    animation: dash 600ms cubic-bezier(0.1, 0.37, 0.2, 0.6) forwards;
  }
}

@keyframes dash {
  to {
    stroke-dashoffset: 0;
  }
}

.lazy-image {
  z-index: 2;
  transition: opacity 300ms;
  &:hover {
    opacity: .1;
  }
}
```

### Todo
 - make more versatile
 - alternative svg loading options?
