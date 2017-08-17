## So you want to style your website

Here are 10 good things to know when starting your CSS journey.

### 0. The CSS Box Model

The box model is the foundation for how layout is determined on the web. Each element on the page is a virtual rectangle with radiating layers of padding, border, and margin (and in that order).

![Box-model](http://cdn.jsears.co/box-model.png "Box-model")

There are three main types of CSS boxes, which can be accessed with the 'display' property in CSS. These are:
  
  - 'Block': A box that stacks on other boxes. Example: standard 'div'
  - 'Inline': A box that flows with the elements text, and 'width' and 'height' properties aren't considered. Example: standard 'p' tags or span tags
  - 'Inline-block': A combination of the previous two, 'inline-block' acts like an inline element with 'width' and 'height' properties

### 1. ID vs. Class

**ID**s should be used for very specific, one-off elements. Example: a special submit button that needs a special styling.

**Class**es should be used for repeated styling across the application. Example: styling used throughout the website in different cases, like a font style you'd like to mix-and-match with various headers.

### 2. Including references to other stylesheets

Internal sheet

```html
<head>
<link rel="stylesheet" type="text/css" href="main.css">
</head>
```

External sheet

```html
<head>
  <link
    rel="stylesheet"
    type="text/css" 
    href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.13/components/modal.css"
  >
</head>
```

### 3. **Cascading** Style Sheets and what that means

In short, the highest priority declarations have the most power.

<img alt="CSS Cascade Order" src="http://cdn.jsears.co/css-cascade.gif" width="600px" />

The first sheet (i.e. the first one included in your HTML file) sets the stage for all of the CSS rules that occur after it, but it will be overwritten if new rules come into play later in the file. By this logic, inline styling hold the highest priority declaration and will generally overwrite rules that have come earlier in the CSS pipeline.

### 4. Overwriting with !important

A rule that has the **!important** property will always be applied no matter where that rule appears in the CSS document. This comes in very handy when you're using a framework that's already declared a wide breadth of rules that apply to many of the elements on a website. Make sure you only use this when necessary (and take particular cautious if you're working on a team), as the !important flag will prevent the applied style from being overwritten in the future.

### 5. Z-index

![Z-index](http://cdn.jsears.co/z-index.png "Z-index")

### 6. Media queries

Media queries are used to create unique CSS layouts and styling for different consumer devices. By using media queries, you can re-define how your website or web applications looks on a desktop, a tablet, or a phone, and thereby increase the user experience for a variety of consumer devices.

<img alt="Media Query Look" src="http://cdn.jsears.co/media-query-css.png" width="600px" />

<img alt="Media Query Declaration" src="http://cdn.jsears.co/media-query-declaration.png" width="500px" />

### 7. CSS units (fluid vs. static)

There are a variety of units you can use to declare the sizes of elements on your webpage. Some are absolute and others are relative.

![CSS Units](http://cdn.jsears.co/css-units.jpeg "CSS Units")

### 8. Positioning

There are two major types of positioning (which can be accessed with the 'position' property) that you should know straight out: 'relative' and 'absolute'. Other options include 'static', 'fixed', and 'sticky'. These properties define rules for elements being repositioned with the 'top', 'right', 'bottom' and 'left' properties.

**Absolute**ly positioned items are removed from the normal document flow and inserted relative to it's parent element's position; otherwise it is relative to the initial container block.

**Relative**ly positioned items are remain within the normal document flow and are positioned relative to itself.

For these 'position' properties to work, like with 'z-index', both elements in question need to have defined 'position' properties.

![CSS Position](http://cdn.jsears.co/css-position.png "CSS Position")

### 9. Next steps

The above barely scratches the surface on CSS in its entirety. I didn't touch on font selection or manipulation, color theory, or best practices of any sort.

I would suggest, if you're new to styling web applications, to begin by using a CSS framework like Bootstrap, Semantic UI or Materialize to get a bearing on how CSS flows. From there, I would suggest maniupulating your chosen framework's CSS with your own styling (likely making use of the !important flag) and taking it where you can from there: you can add your own CSS stylesheets as you become more familiar with popular properties and effects.
