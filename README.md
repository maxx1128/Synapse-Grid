# Synapse Grid

Synapse is a sass grid system with the fun and simplicity of Expressive CSS without the bloat and HTML classes.

[Expressive CSS](http://johnpolacek.github.io/expressive-css/) is a CSS philosophy that emphasizes, among many things, using utility classes to make layout and styling simpler, DRYer, and more modular. The classic drawbacks, however, are lots of CSS classes that likely won't all be used and lots of HTML classes on elements, which risks bloat and disorganization.

Synapse aims for the best of both worlds:
* Using Sass mixins to avoid unneeded CSS and HTML classes
* Still uses Expressive CSS utility classes and principles to make responsive layouts fun, simple, and easy to customize

Here are the basic steps to using Synapse

## Create your settings
Synapse lets you set your own columns, breakpoints, breakpoint labels, and spacing units. They're set by writing a Sass map like the following:

```
$synapse: (
  columns: 12,
  layouts: (
        xs:  0px,
        sm:  480px, 
        md:  787px,
        lg: 1024px,
        xlg: 1200px
    ),
  spaceUnits: (8px, 1em, 2em, 3em, 4em),
  side-margin: 1em

);
```

> Side margin is the margin on the right and right of every column that separates it from the others. This value will be split in half between both sides.

You can make the values whatever you want and add however many you want, so Synapse is very flexible. These are set as the defaults, but you can declare your own map to override them for a more custom Synapse grid.

> Note: Using a breakpoint set at 0 will simply assign regular styles without a media query. This helps keep the CSS files slimmer while helping coders use Synapse consistently.

## Use the Synapse mixin to create your grid

Simply use the mixin on an element to say how wide they should be at a breakpoint. You can also add offset to push or pull the column. Here are some examples:
```
@include syn(sm, 12, 0, ('')); // At 480px it's 12 columns wide
@include syn(md, 9, 3, ('')); // At 787px it's 9 columns wide and pushed 3 columns to the right
@include syn(lg, 8, -2, ('')); // At 1024px it's 8 columns wide and pulled 2 columns to the left
```

## Add utility classes 
You may be wondering what the empty mixin variable is at the end. That's where you put utility classes, a key part of Expressive CSS carried over here. These do things like align the text in your element, hide it, or add padding and margins. These will respond to the breakpoints as well. These classes can then make your text align differently at different screen sizes.

If you don't want any utilities in your element, use the same syntax as above.

Utility classes for padding and margin are set in your settings. With the spacing units above, the spacing utilities would be like this:
* **pad-1:** 8px of padding on all sides
* **pad-2:** 1em of padding on all sides
* **pad-3:** 2em of padding on all sides
* **pad-4:** 3em of padding on all sides
* **pad-5:** 4em of padding on all sides
* **marg-1:** 8px of margin on all sides
* **marg-2:** 1em of margin on all sides
* **marg-3:** 2em of margin on all sides
* **marg-4:** 3em of margin on all sides
* **marg-5:** 4em of margin on all sides

More can be added and the classes would increase to include pad-6, marg-7, etc. More classes like this are explained later.

Some examples explaining the utility classes follow:

```
@include syn(sm, 10, 2, (align-l, pad-0)); 
// In addition to the width and offset settings, text is aligned on the left with no padding

@include syn(md, 8, 2, (align-c, pad-2, marg-1)); 
// At this breakpoint text will then align to the center, have 1em padding and .5em margin on all sides

@include syn(lg, 'none', 0, (pad-4)); 
// The element will add extra padding without changing the width or offset

@include syn(xlg, 6, 0, (hide)); 
// The entire element will be hidden at this breakpoint
```

All the included utility classes are:
* **align-l**: Align text to the left
* **align-r**: Align text to the right
* **align-c**: Align text in center
* **float-l**: Float to left
* **float-r**: Float to right
* **float-n**: No float
* **float-n**: No float
* **border-b**: Add box-sizing: border-box
* **hide**: Hides elements with display:none
* **pad-#**: Adds custom padding to all sides
* **pad-t-#**: Adds custom padding to the top
* **pad-r-#**: Adds custom padding to the right
* **pad-b-#**: Adds custom padding to the bottom
* **pad-l-#**: Adds custom padding to the left


* **marg-#**: Adds custom margin to all sides
* **marg-t-#**: Adds custom margin to the top
* **marg-r-#**: Adds custom margin to the right
* **marg-b-#**: Adds custom margin to the bottom
* **marg-l-#**: Adds custom margin to the left

Custom utility classes can easily be added to the **$utilitiesList** map.

> Note: Want to add utility classes at certain breakpoints without changing the width? Simply put 0 for the columns, and they'll all be added without touching the width.

## Column Utilitity Classes

An element using the Synapse mixin isn't automatically treated as a column among many others. In order to give it the extra spacing and float properties, just add the 'col' utility class to it. This only needs to happen once and will carry over to all greater breakpoints.

```
article {
  @include syn(xs, 12, 0, (pad-1));
  @include syn(md, 6, 0, (pad-0, col));
  @include syn(lg, 3, 0, (marg-b-4));
}
```

If you want an element to stop acting as a column, include the 'no-col' utility class

## Extra Utility Classes

Include these two mixins to generate some fast utility classes for elements.

```
@include generate-padding();
@include generate-margin();
```

The resulting classes will be based on your spacing sizes, and are similarly named to what's used in the "syn" mixin. These are different since you add them directly to an element in the HTML, not in the Sass files. Useful if you have lots of elements that need general padding or margin changes consistent with your layout but not dependent on screen sizes.

* .pad-1
* .pad-top-1
* .pad-right-1
* .pad-bottom-1
* .pad-left-1
* .pad-vert-1
* .pad-sides-1
* .marg-1
* .marg-top-1
* .marg-right-1
* .marg-bottom-1
* .marg-left-1
* .marg-vert-1
* .marg-sides-1

> Note: you can use "0" to remove part or all of an element's padding or margin.

### Enjoy!