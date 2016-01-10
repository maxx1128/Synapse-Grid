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
* **block**: Display as block
* **i-block**: Display as inline block
* **inline**: Display as inline
* **center-m**: Sets margin to "0 auto"
* **hide**: Hides elements with display:none
* **pad-#**: Adds custom padding to all sides
* **pad-t-#**: Adds custom padding to all top
* **pad-r-#**: Adds custom padding to all right
* **pad-b-#**: Adds custom padding to all bottom
* **pad-l-#**: Adds custom padding to all left
* **pad-vert-#**: Adds custom padding to the top and bottom (left and right are set to 0, this can be overridden)
* **pad-sides-#**: Adds custom padding to the right and left (top and bottom are set to 0, this can be overridden)
* **marg-#**: Adds custom margin to all sides
* **marg-t-#**: Adds custom margin to all top
* **marg-r-#**: Adds custom margin to all right
* **marg-b-#**: Adds custom margin to all bottom
* **marg-l-#**: Adds custom margin to all left
* **marg-vert-#**: Adds custom margin to the top and bottom (left and right are set to 0, this can be overridden)
* **marg-sides-#**: Adds custom margin to the right and left (top and bottom are set to 0, this can be overridden)

Custom utility classes can easily be added to the **$utilitiesList** map.

## Enjoy!