---
title: offset-anchor
slug: Web/CSS/offset-anchor
page-type: css-property
browser-compat: css.properties.offset-anchor
sidebar: cssref
---

The **`offset-anchor`** [CSS](/en-US/docs/Web/CSS) property specifies the point inside the box of an element traveling along an {{cssxref("offset-path")}} that is actually moving along the path.

{{InteractiveExample("CSS Demo: offset-anchor")}}

```css interactive-example-choice
offset-anchor: auto;
```

```css interactive-example-choice
offset-anchor: right top;
```

```css interactive-example-choice
offset-anchor: left bottom;
```

```css interactive-example-choice
offset-anchor: 20% 80%;
```

```html interactive-example
<section class="default-example" id="default-example">
  <div class="wrapper">
    <div id="example-element"></div>
  </div>
  <button id="playback" type="button">Play</button>
</section>
```

```css interactive-example
#example-element {
  offset-path: path("M 0,20 L 200,20");
  animation: distance 3000ms infinite alternate ease-in-out;
  width: 40px;
  height: 40px;
  background: cyan;
  animation-play-state: paused;
}

#example-element.running {
  animation-play-state: running;
}

.wrapper {
  background-image: linear-gradient(
    to bottom,
    transparent,
    transparent 49%,
    #000 50%,
    #000 51%,
    transparent 52%
  );
  border: 1px solid #ccc;
  width: 90%;
}

@keyframes distance {
  0% {
    offset-distance: 0%;
  }
  100% {
    offset-distance: 100%;
  }
}

#playback {
  position: absolute;
  top: 0;
  left: 0;
  font-size: 1em;
}
```

```js interactive-example
window.addEventListener("load", () => {
  const example = document.getElementById("example-element");
  const button = document.getElementById("playback");

  button.addEventListener("click", () => {
    if (example.classList.contains("running")) {
      example.classList.remove("running");
      button.textContent = "Play";
    } else {
      example.classList.add("running");
      button.textContent = "Pause";
    }
  });
});
```

## Syntax

```css
/* Keyword values */
offset-anchor: top;
offset-anchor: bottom;
offset-anchor: left;
offset-anchor: right;
offset-anchor: center;
offset-anchor: auto;

/* <percentage> values */
offset-anchor: 25% 75%;

/* <length> values */
offset-anchor: 0 0;
offset-anchor: 1cm 2cm;
offset-anchor: 10ch 8em;

/* Edge offsets values */
offset-anchor: bottom 10px right 20px;
offset-anchor: right 3em bottom 10px;

/* Global values */
offset-anchor: inherit;
offset-anchor: initial;
offset-anchor: revert;
offset-anchor: revert-layer;
offset-anchor: unset;
```

### Values

- `auto`
  - : `offset-anchor` is given the same value as the element's {{cssxref("transform-origin")}}, unless {{cssxref("offset-path")}} is `none`, in which case it takes its value from {{cssxref("offset-position")}}.
- `<position>`
  - : A {{cssxref("&lt;position&gt;")}} defines an x/y coordinate, to place an item relative to the edges of an element's box. It can be defined using one to four values. For more specifics, see the {{cssxref("&lt;position&gt;")}} and {{cssxref("background-position")}} reference pages. Note that the 3-value position syntax does not work for any usage of `<position>`, except for in `background(-position)`.

## Formal definition

{{cssinfo}}

## Formal syntax

{{csssyntax}}

## Examples

### Setting various offset-anchor values

In the following example, we have three {{htmlelement("div")}} elements nested in {{htmlelement("section")}} elements. Each `<div>` is given the same {{cssxref("offset-path")}} (a horizontal line 200 pixels long) and animated to move along it. The three are then given different {{cssxref("background-color")}} and `offset-anchor` values.

Each `<section>` has been styled with a linear gradient to give it a horizontal line running through its center, to give you a visual display of where the `<div>`'s offset paths are running.

This allows you to see what effect the different `offset-anchor` values have — the first one, `auto`, causes the `<div>`'s center point to move along the path. The other two cause the `<div>`'s top-right and bottom-left points to move along the path, respectively.

#### HTML

```html
<section>
  <div class="offset-anchor1"></div>
</section>
<section>
  <div class="offset-anchor2"></div>
</section>
<section>
  <div class="offset-anchor3"></div>
</section>
```

#### CSS

```css
div {
  offset-path: path("M 0,20 L 200,20");
  animation: move 3000ms infinite alternate ease-in-out;
  width: 40px;
  height: 40px;
}

section {
  background-image: linear-gradient(
    to bottom,
    transparent,
    transparent 49%,
    #000 50%,
    #000 51%,
    transparent 52%
  );
  border: 1px solid #ccc;
  margin-bottom: 10px;
}

.offset-anchor1 {
  offset-anchor: auto;
  background: cyan;
}

.offset-anchor2 {
  offset-anchor: right top;
  background: purple;
}

.offset-anchor3 {
  offset-anchor: left bottom;
  background: magenta;
}

@keyframes move {
  0% {
    offset-distance: 0%;
  }
  100% {
    offset-distance: 100%;
  }
}
```

#### Result

{{EmbedLiveSample('Setting_various_offset-anchor_values', '100%', '300')}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{cssxref("offset")}}
- {{cssxref("offset-distance")}}
- {{cssxref("offset-rotate")}}
- [SVG `<path>`](/en-US/docs/Web/SVG/Tutorials/SVG_from_scratch/Paths)
