## So you want to style your website

Here are 10 good things to know when starting your CSS journey.

0. The CSS Box Model

The box model is the foundation for how layout is determined on the web. Each element on the page is a virtual rectangle with radiating layers of padding, border, and margin (and in that order).

There are three main types of CSS boxes, which can be accessed with the 'display' attribute in CSS. These are:
  
  - 'Block': A box that stacks on other boxes. Example: standard 'div'
  - 'Inline': A box that flows with the elements text, and 'width' and 'height' attributes aren't considered. Example: standard 'p' tags or span tags
  - 'Inline-block': A combination of the previous two, 'inline-block' acts like an inline element with 'width' and 'height' attributes

1. ID vs. Class

**ID**s should be used for very specific, one-off elements. Example: a special submit button that needs a special styling.

**Class**es should be used for repeated styling across the application. Example: styling used throughout the website in different cases, like a font style you'd like to mix-and-match with various headers.

2. Including references to other stylesheets

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

3. **Cascading** Style Sheets and what that means

In short, the highest priority declarations have the most power.

The first sheet (i.e. the first one included in your HTML file) sets the stage for all of the CSS rules that occur after it, but it will be overwritten if new rules come into play later in the file. By this logic, inline styling hold the highest priority declaration and will generally overwrite rules that have come earlier in the CSS pipeline.

4. Overwriting with !important



5. Background sizing

6. Media queries

7. CSS units (fluid vs. static)

8. Positioning

9. Next steps
