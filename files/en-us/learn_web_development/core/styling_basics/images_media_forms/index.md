---
title: Images, media, and form elements
short-title: Images, media, forms
slug: Learn_web_development/Core/Styling_basics/Images_media_forms
page-type: learn-module-chapter
sidebar: learnsidebar
---

{{PreviousMenuNext("Learn_web_development/Core/Styling_basics/Overflow", "Learn_web_development/Core/Styling_basics/Tables", "Learn_web_development/Core/Styling_basics")}}

In this lesson we will take a look at how certain special elements are treated in CSS. Images, other media, and form elements behave a little differently from regular boxes in terms of your ability to style them with CSS. Understanding what is and isn't possible can save some frustration, and this lesson will highlight some of the main things that you need to know.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        HTML <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images"
          >images</a
        >, <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_video_and_audio"
          >video</a
        >, and <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_forms"
          >forms</a
        >. CSS <a href="/en-US/docs/Learn_web_development/Core/Styling_basics/Values_and_units">Values and units</a> and <a href="/en-US/docs/Learn_web_development/Core/Styling_basics/Sizing">Sizing</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Learning outcomes:</th>
      <td>
        <ul>
          <li>Understand how replaced elements are sized and laid out.</li>
          <li>Basic styling of easy-to-style form elements, like text inputs.</li>
          <li>Using a CSS reset as base on which to style tricky elements like forms.</li>
          <li>Understand that not all form elements are easy to style, and why.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Replaced elements

Images and video are described as **{{ glossary("replaced elements")}}**. This means that CSS cannot affect the internal layout of these elements — only their position on the page amongst other elements. As we will see however, there are various things that CSS can do with an image.

Certain replaced elements, such as images and video, are also described as having an **{{glossary("aspect ratio")}}**. This means that it has a size in both the horizontal (x) and vertical (y) dimensions, and will be displayed using the intrinsic dimensions of the file by default.

## Sizing images

As you already know from following these lessons, everything in CSS generates a box. If you place an image inside a box that is smaller or larger than the intrinsic dimensions of the image file in either direction, it will either appear smaller than the box, or overflow the box. You need to make a decision about what happens with the overflow.

In the example below we have two boxes, both 200 pixels in size:

- One contains an image that is smaller than 200 pixels — it is smaller than the box and doesn't stretch to fill it.
- The other is larger than 200 pixels and overflows the box.

```html live-sample___size
<div class="wrapper">
  <div class="box">
    <img
      alt="star"
      src="https://mdn.github.io/shared-assets/images/examples/big-star.png" />
  </div>
  <div class="box">
    <img
      alt="balloons"
      src="https://mdn.github.io/shared-assets/images/examples/balloons.jpg" />
  </div>
</div>
```

```css live-sample___size
.wrapper {
  display: flex;
  align-items: flex-start;
}

.wrapper > * {
  margin: 20px;
}

.box {
  border: 5px solid darkblue;
  width: 200px;
}

img {
}
```

{{EmbedLiveSample("size", "", "250px")}}

What can we do about the overflow issue?

As we learned in [Sizing items in CSS](/en-US/docs/Learn_web_development/Core/Styling_basics/Sizing), a common technique is to set the {{cssxref("max-width")}} of the image to `100%`. This will enable the image to become smaller in size than the box but not larger. This technique will also work with other replaced elements such as [`<video>`](/en-US/docs/Web/HTML/Reference/Elements/video)s, or [`<iframe>`](/en-US/docs/Web/HTML/Reference/Elements/iframe)s.

Try adding `max-width: 100%` to the `<img>` element rule in the example above. You will see that the smaller image remains unchanged, but the larger one becomes smaller to fit into the box.

### Handling image overflow with `object-fit`

You can make other choices about images inside containers. For example, you may want to size an image so it completely covers a box.

The {{cssxref("object-fit")}} property can help you here. When using `object-fit` the replaced element can be sized to fit a box in a variety of ways.

Below, the first example uses the value `cover`, which sizes the image down, maintaining the aspect ratio so that it neatly fills the box. As the aspect ratio is maintained, some parts of the image will be cropped by the box. The second example uses `contain` as a value: this scales the image down until it is small enough to fit inside the box. This results in "letterboxing" as it is not the same aspect ratio as the box.

```html live-sample___object-fit
<div class="wrapper">
  <div class="box">
    <img
      alt="balloons"
      class="cover"
      src="https://mdn.github.io/shared-assets/images/examples/balloons.jpg" />
  </div>
  <div class="box">
    <img
      alt="balloons"
      class="contain"
      src="https://mdn.github.io/shared-assets/images/examples/balloons.jpg" />
  </div>
</div>
```

```css live-sample___object-fit
.wrapper {
  display: flex;
  align-items: flex-start;
}

.wrapper > * {
  margin: 20px;
}

.box {
  border: 5px solid darkblue;
  width: 200px;
  height: 200px;
}

img {
  height: 100%;
  width: 100%;
}

.cover {
  object-fit: cover;
}

.contain {
  object-fit: contain;
}
```

{{EmbedLiveSample("object-fit", "", "250px")}}

You could also try the value of `fill`, which will fill the box but not maintain the aspect ratio.

## Replaced elements in layout

When using various CSS layout techniques on replaced elements, you may well find that they behave slightly differently from other elements. For example, in a grid layout, elements are stretched by default to fill their entire [grid areas](/en-US/docs/Glossary/Grid_Areas). Images do not stretch; instead, they are aligned to the start of their grid areas.

You can see this happening in the example below where we have a two column, two row grid container, which has four items in it. All of the `<div>` elements have a background color and stretch to fill the row and column. The image, however, does not stretch.

```html live-sample___layout
<div class="wrapper">
  <img
    alt="star"
    src="https://mdn.github.io/shared-assets/images/examples/big-star.png" />
  <div></div>
  <div></div>
  <div></div>
</div>
```

```css live-sample___layout
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 100px 100px;
  gap: 20px;
}

.wrapper > div {
  background-color: rebeccapurple;
  border-radius: 0.5em;
}
```

{{EmbedLiveSample("layout", "", "220px")}}

You won't study layout until a later module. For now, just keep in mind that replaced elements, when they become part of a specific layout system such as grid or flexbox, have different default behaviors, essentially to avoid them being stretched strangely by the layout.

## Form elements

Form elements have issues when it comes to styling with CSS. The [Web Forms extensions module](/en-US/docs/Learn_web_development/Extensions/Forms) covers the trickier aspects of styling certain form input types, which we will not go into here. There are, however, a few key basics worth highlighting in this section.

Many form controls are added to your page by way of the [`<input>`](/en-US/docs/Web/HTML/Reference/Elements/input) element — this defines simple form fields such as text inputs, through to more complex fields such as color and date pickers. There are some additional elements, such as [`<textarea>`](/en-US/docs/Web/HTML/Reference/Elements/textarea) for multiline text input, and also elements used to contain and label parts of forms such as [`<fieldset>`](/en-US/docs/Web/HTML/Reference/Elements/fieldset) and [`<legend>`](/en-US/docs/Web/HTML/Reference/Elements/legend).

HTML also contains attributes that enable web developers to indicate which fields are required, and even the type of content that needs to be entered. If the user enters something unexpected, or leaves a required field blank, the browser can show an error message. Different browsers vary with one another in how much styling and customization they allow for such items.

## Styling text input elements

Elements that allow for text input such as `<input type="text">`, the more specific `<input type="email">`, and the `<textarea>` element, are quite easy to style and tend to behave just like other boxes on your page. The default styling of these elements will differ, however, based on the operating system and browser that your user visits the site with.

In the example below, we have styled some text inputs using CSS. You can see that things such as borders, margins and padding all apply as you would expect. We are using attribute selectors to target the different input types.

Try editing the example to change how the form looks by adjusting the borders, adding background colors to the fields, and changing fonts and padding.

```html live-sample___form
<form>
  <div><label for="name">Name</label> <input id="name" type="text" /></div>
  <div><label for="email">Email</label> <input id="email" type="email" /></div>

  <div class="buttons"><input type="submit" value="Submit" /></div>
</form>
```

```css hidden live-sample___form
body {
  font-family: sans-serif;
}
form > div {
  display: flex;
}

label {
  width: 10em;
}

.buttons {
  justify-content: center;
}
```

```css live-sample___form
input[type="text"],
input[type="email"] {
  border: 2px solid #000;
  margin: 0 0 1em 0;
  padding: 10px;
  width: 80%;
}

input[type="submit"] {
  border: 3px solid #333;
  background-color: #999;
  border-radius: 5px;
  padding: 10px 2em;
  font-weight: bold;
  color: #fff;
}

input[type="submit"]:hover,
input[type="submit"]:focus {
  background-color: #333;
}
```

{{EmbedLiveSample("form")}}

> [!WARNING]
> You should take care when changing the styling of form elements to make sure it is still obvious to the user they are form elements. You could create a form input with no borders and background that is almost indistinguishable from the content around it, but this would make it very hard to recognize and interact with.

Many of the more complex input types are rendered by the operating system and are inaccessible to styling. You should, therefore, always assume that forms are going to look quite different for different visitors and test complex forms in a number of browsers.

## Normalizing form behavior

Form elements behave differently across different browsers and operating systems. This section looks at a few of the most common issues and provides strategies for dealing with them.

### Inheritance and form elements

In some browsers, form elements do not inherit font styling by default. Therefore, if you want to be sure that your form fields use the font defined on the body, or on a parent element, you should add this rule to your CSS.

```css
button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
}
```

### Form elements and box-sizing

Across browsers, form elements use different box sizing rules for different widgets. You learned about the `box-sizing` property in [our box model lesson](/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model) and you can use this knowledge when styling forms to ensure a consistent experience when setting widths and heights on form elements.

For consistency, it is a good idea to set margins and padding to `0` on all elements, then add these back in when styling particular controls:

```css
button,
input,
select,
textarea {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
```

### Other useful settings

In addition to the rules mentioned above, you should also set `overflow: auto` on `<textarea>` elements to stop some older browsers from showing a scrollbar when there is no need for one:

```css
textarea {
  overflow: auto;
}
```

### Putting it all together into a "reset"

As a final step, we can wrap up the various properties discussed above into the following "form reset" to provide a consistent base to work from. This includes all the items mentioned in the last three sections:

```css
button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

textarea {
  overflow: auto;
}
```

> [!NOTE]
> Normalizing stylesheets are used by many developers to create a set of baseline styles to use on all projects. Typically these do similar things to those described above, making sure that anything different across browsers is set to a consistent default before you do your own work on the CSS. They are not as important as they once were, as browsers are typically more consistent than in the past. However, if you want to take a look at an example, check out [Normalize.css](https://necolas.github.io/normalize.css/), which is a very popular stylesheet used as a base by many projects.

## Test your skills!

You've reached the end of this article, but can you remember the most important information? You can find some further tests to verify that you've retained this information before you move on — see [Test your skills: Images and form elements](/en-US/docs/Learn_web_development/Core/Styling_basics/Test_your_skills/Images).

## Summary

This lesson has highlighted some of the differences you will encounter when working with images, media, and other unusual elements in CSS.

In the next article, we'll learn how to style HTML tables.

## See also

- [Styling web forms](/en-US/docs/Learn_web_development/Extensions/Forms/Styling_web_forms)
- [Advanced form styling](/en-US/docs/Learn_web_development/Extensions/Forms/Advanced_form_styling)

{{PreviousMenuNext("Learn_web_development/Core/Styling_basics/Overflow", "Learn_web_development/Core/Styling_basics/Tables", "Learn_web_development/Core/Styling_basics")}}
