---
title: "HTML: A good basis for accessibility"
short-title: Accessible HTML
slug: Learn_web_development/Core/Accessibility/HTML
page-type: learn-module-chapter
sidebar: learnsidebar
---

{{PreviousMenuNext("Learn_web_development/Core/Accessibility/Tooling","Learn_web_development/Core/Accessibility/CSS_and_JavaScript", "Learn_web_development/Core/Accessibility")}}

A great deal of web content can be made accessible just by making sure the correct Hypertext Markup Language elements are used for the correct purpose at all times. This article looks in detail at how HTML can be used to ensure maximum accessibility.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>Familiarity with <a href="/en-US/docs/Learn_web_development/Core/Structuring_content">HTML</a>, <a href="/en-US/docs/Learn_web_development/Core/Styling_basics">CSS</a>, a <a href="/en-US/docs/Learn_web_development/Core/Accessibility/What_is_accessibility">basic understanding of accessibility concepts</a>.</td>
    </tr>
    <tr>
      <th scope="row">Learning outcomes:</th>
      <td>
        <ul>
          <li>Use semantic HTML, aka "The right element for the right job", because the browser provides so many built-in accessibility hooks.</li>
          <li>Accessible best practices such as alt text, good link best, form labels, and table row and column headings and scoping.</li>
          <li>Using simple plain language, steering clear of slang and abbreviations where possible, and providing definitions where it is not possible.</li>
          <li>The concept and practice of keyboard accessibility.</li>
          <li>The importance of source order.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## HTML and accessibility

As you learn more about HTML — read more resources, look at more examples, etc. — you'll keep seeing a common theme: the importance of using semantic HTML (sometimes called POSH, or Plain Old Semantic HTML). This means using the correct HTML elements for their intended purpose as much as possible.

You might wonder why this is so important. After all, you can use a combination of CSS and JavaScript to make just about any HTML element behave in whatever way you want. For example, a control button to play a video on your site could be marked up like this:

```html
<div>Play video</div>
```

But as you'll see in greater detail later on, it makes sense to use the correct element for the job:

```html
<button>Play video</button>
```

Not only do HTML `<button>`s have some suitable styling applied by default (which you will probably want to override), they also have built-in keyboard accessibility — users can navigate between buttons using the <kbd>Tab</kbd> key and activate their selection using <kbd>Space</kbd>, <kbd>Return</kbd> or <kbd>Enter</kbd>.

Semantic HTML doesn't take any longer to write than non-semantic (bad) markup if you do it consistently from the start of your project. Even better, semantic markup has other benefits beyond accessibility:

1. **Easier to develop with** — as mentioned above, you get some functionality for free, plus it is arguably easier to understand.
2. **Better on mobile** — semantic HTML is arguably lighter in file size than non-semantic spaghetti code, and easier to make responsive.
3. **Good for SEO** — search engines give more importance to keywords inside headings, links, etc. than keywords included in non-semantic `<div>`s, etc., so your documents will be more findable by customers.

Let's get on and look at accessible HTML in more detail.

## Good semantics

We've already talked about the importance of proper semantics, and why we should use the right HTML element for the job. This cannot be ignored, as it is one of the main places that accessibility is badly broken if not handled properly.

Out there on the web, the truth is that people do some very strange things with HTML markup. Often, misuse of HTML is because of legacy practices that haven't gone away yet, but sometimes it occurs because authors don't know any better. Whatever the case, you should replace bad code with good semantic markup wherever possible, in both static HTML pages and dynamically-generated HTML from [server-side](/en-US/docs/Learn_web_development/Extensions/Server-side) code or [client-side JavaScript frameworks](/en-US/docs/Learn_web_development/Core/Frameworks_libraries) such as React.

Sometimes you are not in a position to get rid of lousy markup — your pages might be dependant on server-side code or web/framework components that you have no control over, or you might have third-party content on your page (such as ad banners).

The goal isn't "all or nothing"; every improvement you can make will help the cause of accessibility.

### Use well-structured text content

One of the best accessibility aids a screen reader user can have is an excellent text structure with headings, paragraphs, lists, etc. A good semantic example might look something like the following:

```html example-good
<h1>My heading</h1>

<p>This is the first section of my document.</p>

<p>I'll add another paragraph here too.</p>

<ol>
  <li>Here is</li>
  <li>a list for</li>
  <li>you to read</li>
</ol>

<h2>My subheading</h2>

<p>
  This is the first subsection of my document. I'd love people to be able to
  find this content!
</p>

<h2>My 2nd subheading</h2>

<p>
  This is the second subsection of my content, which I think is more interesting
  than the last one.
</p>
```

We've prepared a version with longer text for you to try out with a screen reader (see [good-semantics.html](https://mdn.github.io/learning-area/accessibility/html/good-semantics.html)). If you try navigating through this, you'll see that this is pretty easy to navigate:

1. The screen reader reads each header out as you progress through the content, notifying you what a heading is, what is a paragraph, etc.
2. It stops after each element, letting you go at whatever pace is comfortable for you.
3. You can jump to the next/previous heading in many screen readers.
4. You can also bring up a list of all headings in many screen readers, allowing you to use them as a handy table of contents to find specific content.

People sometimes write headings, paragraphs, etc. using line breaks and adding HTML elements purely for styling, something like the following:

```html example-bad
<span style="font-size: 3em">My heading</span> <br /><br />
This is the first section of my document.
<br /><br />
I'll add another paragraph here too.
<br /><br />
1. Here is
<br /><br />
2. a list for
<br /><br />
3. you to read
<br /><br />
<span style="font-size: 2.5em">My subheading</span>
<br /><br />
This is the first subsection of my document. I'd love people to be able to find
this content!
<br /><br />
<span style="font-size: 2.5em">My 2nd subheading</span>
<br /><br />
This is the second subsection of my content. I think is more interesting than
the last one.
```

If you try our longer version out with a screen reader (see [bad-semantics.html](https://mdn.github.io/learning-area/accessibility/html/bad-semantics.html)), you'll not have a very good experience — the screen reader hasn't got anything to use as signposts, so you can't retrieve a useful table of contents, and the whole page is seen as a single giant block, so it is just read out in one go, all at once.

There are other issues too beyond accessibility — it is harder to style the content using CSS, or manipulate it with JavaScript, for example, because there are no elements to use as selectors.

### Use clear language

The language you use can also affect accessibility. In general, you should use clear language that is not overly complex and doesn't use unnecessary jargon or slang terms. This not only benefits people with cognitive or other disabilities; it benefits readers for whom the text is not written in their first language, younger people…, everyone, in fact! Apart from this, you should try to avoid using language and characters that don't get read out clearly by the screen reader. For example:

- Don't use dashes if you can avoid it. Instead of writing 5–7, write 5 to 7.
- Expand abbreviations — instead of writing Jan, write January.
- Expand acronyms, at least once or twice, then use the [`<abbr>`](/en-US/docs/Web/HTML/Reference/Elements/abbr) tag to describe them.

### Structure page sections logically

You should use appropriate [sectioning elements](/en-US/docs/Web/HTML/Reference/Elements#content_sectioning) to structure your webpages, for example navigation ({{htmlelement("nav")}}), footer ({{htmlelement("footer")}}), and repeating content units ({{htmlelement("article")}}). These provide extra semantics for screen readers (and other tools) to give users extra clues about the content they are navigating.

For example, a modern content structure could look something like this:

```html
<header>
  <h1>Header</h1>
</header>

<nav>
  <!-- main navigation in here -->
</nav>

<!-- Here is our page's main content -->
<main>
  <!-- It contains an article -->
  <article>
    <h2>Article heading</h2>

    <!-- article content in here -->
  </article>

  <aside>
    <h2>Related</h2>

    <!-- aside content in here -->
  </aside>
</main>

<!-- And here is our main footer that is used across all the pages of our website -->

<footer>
  <!-- footer content in here -->
</footer>
```

You can find a [full example here](https://mdn.github.io/learning-area/html/introduction-to-html/document_and_website_structure/).

In addition to having good semantics and an attractive layout, your content should make logical sense in its source order — you can always place it where you want using CSS later on, but you should get the source order right to start with, so what screen reader users get read out to them will make sense.

### Use semantic UI controls where possible

By UI controls, we mean the main parts of web documents that users interact with — most commonly buttons, links, and form controls. In this section, we'll look at the basic accessibility concerns to be aware of when creating such controls. Later articles on WAI-ARIA and multimedia will look at other aspects of UI accessibility.

One key aspect of the accessibility of UI controls is that by default, browsers allow them to be manipulated by the keyboard. You can try this out using our [native-keyboard-accessibility.html](https://mdn.github.io/learning-area/tools-testing/cross-browser-testing/accessibility/native-keyboard-accessibility.html) example (see the [source code](https://github.com/mdn/learning-area/blob/main/tools-testing/cross-browser-testing/accessibility/native-keyboard-accessibility.html)). Open this in a new tab, and try pressing the tab key; after a few presses, you should see the tab focus start to move through the different focusable elements. The focused elements are given a highlighted default style in every browser (it differs slightly between different browsers) so that you can tell what element is focused.

![Three buttons with the text "Click me!", "Click me too!", and "And me!" inside them respectively. The third button has a blue outline around it to indicate current tab focus.](button-focused-unfocused.png)

> [!NOTE]
> You can enable an overlay that shows the page tabbing order in your developer tools. For more information see: [Accessibility Inspector > Show web page tabbing order](https://firefox-source-docs.mozilla.org/devtools-user/accessibility_inspector/index.html#show-web-page-tabbing-order).

You can then press Enter/Return to follow a focused link or press a button (we've included some JavaScript to make the buttons alert a message), or start typing to enter text in a text input. Other form elements have different controls; for example, the {{htmlelement("select")}} element can have its options displayed and cycled between using the up and down arrow keys.

You essentially get this behavior for free, just by using the appropriate elements, for example:

```html example-good
<h1>Links</h1>

<p>This is a link to <a href="https://www.mozilla.org">Mozilla</a>.</p>

<p>
  Another link, to the
  <a href="https://developer.mozilla.org">Mozilla Developer Network</a>.
</p>

<h2>Buttons</h2>

<p>
  <button data-message="This is from the first button">Click me!</button>
  <button data-message="This is from the second button">Click me too!</button>
  <button data-message="This is from the third button">And me!</button>
</p>

<h2>Form</h2>

<form>
  <div>
    <label for="name">Fill in your name:</label>
    <input type="text" id="name" name="name" />
  </div>
  <div>
    <label for="age">Enter your age:</label>
    <input type="text" id="age" name="age" />
  </div>
  <div>
    <label for="mood">Choose your mood:</label>
    <select id="mood" name="mood">
      <option>Happy</option>
      <option>Sad</option>
      <option>Angry</option>
      <option>Worried</option>
    </select>
  </div>
</form>
```

This means using links, buttons, form elements, and labels appropriately (including the {{htmlelement("label")}} element for form controls).

However, this is another case where people sometimes do strange things with HTML. For example, you sometimes see buttons marked up using {{htmlelement("div")}}s, for example:

```html example-bad
<div data-message="This is from the first button">Click me!</div>
<div data-message="This is from the second button">Click me too!</div>
<div data-message="This is from the third button">And me!</div>
```

But using such code is not advised — you immediately lose the native keyboard accessibility you would have had if you'd just used {{htmlelement("button")}} elements, plus you don't get any of the default CSS styling that buttons get. In the rare to non-existent case when you need to use a non-button element for a button, use the [`button` role](/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/button_role) and implement all the default button behaviors, including keyboard and mouse button support.

#### Building keyboard accessibility back in

Adding such advantages back in takes a bit of work (you can see an example in our [fake-div-buttons.html](https://mdn.github.io/learning-area/tools-testing/cross-browser-testing/accessibility/fake-div-buttons.html) example — also see the [source code](https://github.com/mdn/learning-area/blob/main/tools-testing/cross-browser-testing/accessibility/fake-div-buttons.html)). Here we've given our fake `<div>` buttons the ability to be focused (including via tab) by giving each one the attribute `tabindex="0"`. We also include `role="button"` so screen reader users know they can focus on and interact with the element:

```html
<div data-message="This is from the first button" tabindex="0" role="button">
  Click me!
</div>
<div data-message="This is from the second button" tabindex="0" role="button">
  Click me too!
</div>
<div data-message="This is from the third button" tabindex="0" role="button">
  And me!
</div>
```

Basically, the [`tabindex`](/en-US/docs/Web/HTML/Reference/Global_attributes/tabindex) attribute is primarily intended to allow tabbable elements to have a custom tab order (specified in positive numerical order), instead of just being tabbed through in their default source order. This is nearly always a bad idea, as it can cause major confusion. Use it only if you really need to, for example, if the layout shows things in a very different visual order to the source code, and you want to make things work more logically. There are two other options for `tabindex`:

- `tabindex="0"` — as indicated above, this value allows elements that are not normally tabbable to become tabbable. This is the most useful value of `tabindex`.
- `tabindex="-1"` — this allows not normally tabbable elements to receive focus programmatically, e.g., via JavaScript, or as the target of links.

While the above addition allows us to tab to the buttons, it does not allow us to activate them via the <kbd>Enter</kbd>/<kbd>Return</kbd> key. To do that, we had to add the following bit of JavaScript:

```js
document.onkeydown = (e) => {
  // The Enter/Return key
  if (e.key === "Enter") {
    document.activeElement.click();
  }
};
```

Here we add a listener to the `document` object to detect when a button has been pressed on the keyboard. We check what button was pressed via the event object's [`key`](/en-US/docs/Web/API/KeyboardEvent/key) property; if the key pressed is <kbd>Enter</kbd>/<kbd>Return</kbd>, we run the function stored in the button's `onclick` handler using `document.activeElement.click()`. [`activeElement`](/en-US/docs/Web/API/Document/activeElement) which gives us the element that is currently focused on the page.

This is a lot of extra hassle to build the functionality back in. And there's bound to be other problems with it. **Better to just use the right element for the right job in the first place.**

#### Use meaningful text labels

UI control text labels are very useful to all users, but getting them right is particularly important to users with disabilities.

You should make sure that your button and link text labels are understandable and distinctive. Don't just use "Click here" for your labels, as screen reader users sometimes get up a list of buttons and form controls. The following screenshot shows our controls being listed by VoiceOver on Mac.

![List of form input labels being listed by VoiceOver software on Mac. This list contains meaningless labels like 'happy menu button` given to various form controls like button, textfield and link](voiceover-formcontrols.png)

Make sure your labels make sense out of context, read on their own, as well as in the context of the paragraph they are in. For example, the following shows an example of good link text:

```html example-good
<p>
  Whales are really awesome creatures.
  <a href="whales.html">Find out more about whales</a>.
</p>
```

but this is bad link text:

```html example-bad
<p>
  Whales are really awesome creatures. To find out more about whales,
  <a href="whales.html">click here</a>.
</p>
```

> [!NOTE]
> You can find a lot more about link implementation and best practices in our [Creating links](/en-US/docs/Learn_web_development/Core/Structuring_content/Creating_links) article. You can also see some good and bad examples at [good-links.html](https://mdn.github.io/learning-area/accessibility/html/good-links.html) and [bad-links.html](https://mdn.github.io/learning-area/accessibility/html/bad-links.html).

Form labels are also important for giving you a clue about what you need to enter into each form input. The following seems like a reasonable enough example:

```html example-bad
Fill in your name: <input type="text" id="name" name="name" />
```

However, this is not so useful for disabled users. There is nothing in the above example to associate the label unambiguously with the form input and make it clear how to fill it in if you cannot see it. If you access this with some screen readers, you may only be given a description along the lines of "edit text."

The following is a much better example:

```html example-good
<div>
  <label for="name">Fill in your name:</label>
  <input type="text" id="name" name="name" />
</div>
```

With code like this, the label will be clearly associated with the input; the description will be more like "Fill in your name: edit text."

![A good form label that reads 'Fill in your name' is given to a text input form control. ](voiceover-good-form-label.png)

As an added bonus, in most browsers associating a label with a form input means that you can click the label to select or activate the form element. This gives the input a bigger hit area, making it easier to select.

> [!NOTE]
> You can see some good and bad form examples in [good-form.html](https://mdn.github.io/learning-area/accessibility/html/good-form.html) and [bad-form.html](https://mdn.github.io/learning-area/accessibility/html/bad-form.html).

You can find a nice explanation of the importance of proper text labels, and how to investigate text label issues using the [Firefox Accessibility Inspector](https://firefox-source-docs.mozilla.org/devtools-user/accessibility_inspector/index.html), in the following video:

{{EmbedYouTube("YhlAVlfH0rQ")}}

## Accessible data tables

A basic data table can be written with very simple markup, for example:

```html
<table>
  <tr>
    <td>Name</td>
    <td>Age</td>
    <td>Pronouns</td>
  </tr>
  <tr>
    <td>Gabriel</td>
    <td>13</td>
    <td>he/him</td>
  </tr>
  <tr>
    <td>Elva</td>
    <td>8</td>
    <td>she/her</td>
  </tr>
  <tr>
    <td>Freida</td>
    <td>5</td>
    <td>she/her</td>
  </tr>
</table>
```

But this has problems — there is no way for a screen reader user to associate rows or columns together as groupings of data. To do this, you need to know what the header rows are and if they are heading up rows, columns, etc. This can only be done visually for the above table (see [bad-table.html](https://mdn.github.io/learning-area/accessibility/html/bad-table.html) and try the example out yourself).

Now have a look at our [punk bands table example](https://github.com/mdn/learning-area/blob/main/css/styling-boxes/styling-tables/punk-bands-complete.html) — you can see a few accessibility aids at work here:

- Table headers are defined using {{htmlelement("th")}} elements — you can also specify if they are headers for rows or columns using the `scope` attribute. This gives you complete groups of data that can be consumed by screen readers as single units.
- The {{htmlelement("caption")}} element and the `<table>` element's `summary` attribute both do similar jobs — they act as alt text for a table, giving a screen reader user a useful quick summary of the table's contents. The `<caption>` element is generally preferred as it makes its content accessible to sighted users too, who might also find it useful. You don't really need both.

> [!NOTE]
> See our [HTML table accessibility](/en-US/docs/Learn_web_development/Core/Structuring_content/Table_accessibility) article for more details about accessible data tables.

## Text alternatives

Whereas textual content is inherently accessible, the same cannot necessarily be said for multimedia content — image and video content cannot be seen by visually-impaired people, and audio content cannot be heard by hearing-impaired people. We cover video and audio content in detail in the [Accessible multimedia](/en-US/docs/Learn_web_development/Core/Accessibility/Multimedia), but for this article we'll look at accessibility for the humble {{htmlelement("img")}} element.

We have a simple example written up, [accessible-image.html](https://mdn.github.io/learning-area/accessibility/html/accessible-image.html), which features four copies of the same image:

```html
<img src="dinosaur.png" />

<img
  src="dinosaur.png"
  alt="A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth." />

<img
  src="dinosaur.png"
  alt="A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth."
  title="The Mozilla red dinosaur" />

<img src="dinosaur.png" aria-labelledby="dino-label" />

<p id="dino-label">
  The Mozilla red Tyrannosaurus Rex: A two legged dinosaur standing upright like
  a human, with small arms, and a large head with lots of sharp teeth.
</p>
```

The first image, when viewed by a screen reader, doesn't really offer the user much help — VoiceOver for example reads out "/dinosaur.png, image". It reads out the filename to try to provide some help. In this example the user will at least know it is a dinosaur of some kind, but often files may be uploaded with machine-generated file names (e.g., from a digital camera) and these file names would likely provide no context to the image's content.

> [!NOTE]
> This is why you should never include text content inside an image — screen readers can't access it. There are other disadvantages too — you can't select it and copy/paste it. Just don't do it!

When a screen reader encounters the second image, it reads out the full alt attribute — "A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a human, with small arms, and a large head with lots of sharp teeth.".

This highlights the importance of not only using meaningful file names in case so-called **alt text** is not available, but also making sure that alt text is provided in `alt` attributes wherever possible.

Note that the contents of the `alt` attribute should always provide a direct representation of the image and what it conveys visually. The alt should be brief and concise and include all the information conveyed in the image that is not duplicated in the surrounding text.

The content of the `alt` attribute for a single image differs based on the context. For example, if the photo of Fluffy is an avatar next to a review for Yuckymeat dog food, `alt="Fluffy"` is appropriate. If the photo is part of Fluffy's adoption page for the animal rescue society, information conveyed in the image that is relevant for a prospective dog parent that is not duplicated in the surrounding text should be included. A longer description, such as `alt="Fluffy, a tri-color terrier with very short hair, with a tennis ball in her mouth."` is appropriate. As the surrounding text likely has Fluffy's size and breed, that is not included in the `alt`. However, as the dog's biography likely doesn't include hair length, colors, or toy preferences, which the potential parent needs to know, it is included. Is the image outdoors, or does Fluffy have a red collar with a blue leash? Not important in terms of adopting the pet and therefore not included. All information image conveys that a sighted user can access and is relevant to the context is what needs to be conveyed; nothing more. Keep it short, precise, and useful.

Any personal knowledge or extra description shouldn't be included here, as it is not useful for people who have not seen the image before. If the ball is Fluffy's favorite toy or if a sighted user can't know that from the image, then don't include it.

One thing to consider is whether your images have meaning inside your content, or whether they are purely for visual decoration, and thus have no meaning. If they are decorative, it is better to write an empty text as a value for `alt` attribute (see [Empty alt attributes](#empty_alt_attributes)) or to just include them in the page as CSS background images.

> [!NOTE]
> Read [HTML images](/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images) and [Responsive images](/en-US/docs/Web/HTML/Guides/Responsive_images) for a lot more information about image implementation and best practices.
> You can also check [An alt Decision Tree](https://www.w3.org/WAI/tutorials/images/decision-tree/) to learn how to use an alt attribute for images in various situations.

If you do want to provide extra contextual information, you should put it in the text surrounding the image, or inside a `title` attribute, as shown above. In this case, most screen readers will read out the alt text, the title attribute, and the filename. In addition, browsers display title text as tooltips when moused over.

![Screenshot of a red Tyrannosaurus Rex with the text "The mozilla red dinosaur" displayed as tooltip on mouseover.](title-attribute.png)

Let's have another quick look at the fourth method:

```html
<img src="dinosaur.png" aria-labelledby="dino-label" />

<p id="dino-label">The Mozilla red Tyrannosaurus…</p>
```

In this case, we are not using the `alt` attribute at all — instead, we have presented our description of the image as a regular text paragraph, given it an `id`, and then used the `aria-labelledby` attribute to refer to that `id`, which causes screen readers to use that paragraph as the alt text/label for that image. This is especially useful if you want to use the same text as a label for multiple images — something that isn't possible with `alt`.

> [!NOTE]
> [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) is part of the [WAI-ARIA](https://w3c.github.io/aria/) spec, which allows developers to add in extra semantics to their markup to improve screen reader accessibility where needed.

### Figures and figure captions

HTML includes two elements — {{htmlelement("figure")}} and {{htmlelement("figcaption")}} — which associate a figure of some kind (it could be anything, not necessarily an image) with a figure caption:

```html
<figure>
  <img
    src="dinosaur.png"
    alt="The Mozilla Tyrannosaurus"
    aria-describedby="dinodescr" />
  <figcaption id="dinodescr">
    A red Tyrannosaurus Rex: A two legged dinosaur standing upright like a
    human, with small arms, and a large head with lots of sharp teeth.
  </figcaption>
</figure>
```

While there is mixed screen reader support of associating figure captions with their figures, including [`aria-labelledby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) or [`aria-describedby`](/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-describedby) creates the association if none is present. That said, the element structure is useful for CSS styling, plus it provides a way to place a description of the image next to it in the source.

### Empty alt attributes

```html
<h3>
  <img src="article-icon.png" alt="" />
  Tyrannosaurus Rex: the king of the dinosaurs
</h3>
```

There may be times where an image is included in a page's design, but its primary purpose is for visual decoration. You'll notice in the code example above that the image's `alt` attribute is empty — this is to make screen readers recognize the image, but not attempt to describe the image (instead they'd just say "image", or similar).

The reason to use an empty `alt` instead of not including it is because many screen readers announce the whole image URL if no `alt` is provided. In the above example, the image is acting as a visual decoration to the heading it's associated with. In cases like this, and in cases where an image is only decoration and has no content value, you should include an empty `alt` in your `img` elements. Another alternative is to use the aria [`role`](/en-US/docs/Web/Accessibility/ARIA/Reference/Roles) attribute [`role="presentation"`](/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/presentation_role) as this also stops screen readers from reading out alternative text.

> [!NOTE]
> If possible you should use CSS to display images that are only decorative.

## More on links

Links (the [`<a>`](/en-US/docs/Web/HTML/Reference/Elements/a) element with an `href` attribute), depending on how they are used, can help or harm accessibility. By default, links are accessible in appearance. They can improve accessibility by helping a user quickly navigate to different sections of a document. They can also harm accessibility if their accessible styling is removed or if JavaScript causes them to behave in unexpected ways.

### Link styling

By default, links are visually different from other text in both color and [text-decoration](/en-US/docs/Web/CSS/text-decoration), with links being blue and underlined by default, purple and underlined if visited, and with a [focus-ring](/en-US/docs/Web/CSS/:focus) when they receive keyboard focus.

Color should not be used as the sole method of distinguishing links from non-linking content. Link text color, like all text, has to be significantly different from the background color ([a 4.5:1 contrast](/en-US/docs/Web/Accessibility/Guides/Understanding_WCAG/Perceivable/Color_contrast)). In addition, links should visually be significantly different from non-linking text, with a minimum contrast requirement of 3:1 between link text and surrounding text and between default, visited, and focus/active states and a 4.5:1 contrast between all those state colors and the background color.

### `onclick` events

Anchor tags are often abused with the `onclick` event to create pseudo-buttons by setting **href** to `"#"` or `"javascript:void(0)"` to prevent the page from refreshing.

These values cause unexpected behavior when copying or dragging links, opening links in a new tab or window, bookmarking, and when JavaScript is still downloading, errors out, or is disabled. This also conveys incorrect semantics to assistive technologies (e.g., screen readers). In these cases, it is recommended to use a {{HTMLElement("button")}} instead. In general you should only use an anchor for navigation using a proper URL.

### External links and linking to non-HTML resources

Links that open in a new tab or window via the `target="_blank"` declaration and links to whose `href` value points to a file resource should include an indicator about the behavior that will occur when the link is activated.

People experiencing low vision conditions, who are navigating with the aid of screen reading technology, or who have cognitive concerns may become confused when the new tab, window, or application is opened unexpectedly. Older versions of screen reading software may not even announce the behavior.

#### Link that opens a new tab or window

```html
<a target="_blank" href="https://www.wikipedia.org/"
  >Wikipedia (opens in a new window)</a
>
```

#### Link to a non-HTML resource

```html
<a target="_blank" href="2017-annual-report.ppt"
  >2017 Annual Report (PowerPoint)</a
>
```

If an icon is used in place of text to signify this kind of links behavior, make sure it includes an [alternate description](/en-US/docs/Web/HTML/Reference/Elements/img#alt).

- [WebAIM: Links and Hypertext - Hypertext Links](https://webaim.org/techniques/hypertext/hypertext_links)
- [MDN Understanding WCAG, Guideline 3.2 explanations](/en-US/docs/Web/Accessibility/Guides/Understanding_WCAG/Understandable#guideline_3.2_—_predictable_make_web_pages_appear_and_operate_in_predictable_ways)
- [G200: Opening new windows and tabs from a link only when necessary | W3C Techniques for WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/G200.html)
- [G201: Giving users advanced warning when opening a new window | W3C Techniques for WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/G201.html)

### Skip links

A skip link, also known as skipnav, is an `a` element placed as close as possible to the opening {{HTMLElement("body")}} element that links to the beginning of the page's main content. This link allows people to bypass content repeated throughout multiple pages on a website, such as a website's header and primary navigation.

Skip links are especially useful for people who navigate with the aid of assistive technology such as switch control, voice command, or mouth sticks/head wands, where the act of moving through repetitive links can be a laborious task.

- [WebAIM: "Skip Navigation" Links](https://webaim.org/techniques/skipnav/)
- [How–to: Use Skip Navigation links - The A11Y Project](https://www.a11yproject.com/posts/skip-nav-links/)
- [MDN Understanding WCAG, Guideline 2.4 explanations](/en-US/docs/Web/Accessibility/Guides/Understanding_WCAG/Operable#guideline_2.4_%e2%80%94_navigable_provide_ways_to_help_users_navigate_find_content_and_determine_where_they_are)
- [Understanding Success Criterion 2.4.1 | W3C Understanding WCAG 2.0](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html)

### Proximity

Large amounts of interactive content—including anchors—placed in close visual proximity to each other should have space inserted to separate them. This spacing is beneficial for people who suffer from fine motor control issues and may accidentally activate the wrong interactive content while navigating.

Spacing may be created using CSS properties such as {{CSSxRef("margin")}}.

- [Hand tremors and the giant-button-problem - Axess Lab](https://axesslab.com/hand-tremors/)

## Test your skills

You've reached the end of this article, but can you remember the most important information? See [Test your skills: HTML Accessibility](/en-US/docs/Learn_web_development/Core/Accessibility/Test_your_skills/HTML) to verify that you've retained this information before you move on.

## Summary

You should now be well-versed in writing accessible HTML for most occasions. Our WAI-ARIA basics article will help to fill gaps in this knowledge, but this article has taken care of the basics. Next up we'll explore CSS and JavaScript, and how accessibility is affected by their good or bad use.

{{PreviousMenuNext("Learn_web_development/Core/Accessibility/Tooling","Learn_web_development/Core/Accessibility/CSS_and_JavaScript", "Learn_web_development/Core/Accessibility")}}
