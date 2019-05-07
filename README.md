# Positioning Elements in CSS

## Problem Statement

One powerful feature of CSS the ability to position content in a variety of
ways without having to write much HTML markup. There are a few different types
of positioning within CSS, some of which have multiple uses and applications.
When it comes to page layouts, CSS has become king, so what can be taken advantage
of to create user-friendly flows?

## Objectives

1. Use `float` to pull content left or right
2. Create `clearfix` to clear floated content
3. Use `position` to give fixed properties to elements
4. Use `z-index` to change the depth of elements
5. Use `margin: auto` to center block elements

## Use `float` to Pull Content Left or Right

One way to position elements on a page is with the `float` property. The `float` property
removes it from the normal flow of a page, and position it to the left or right of its 
parent element. All other elements on the page will then "wrap" around the floated element. 

The two most popular values for `float` are left and right, which allow elements to be
floated to the left or right inside of their parent element. Anytime you float an element
elements that come after are going to try fill into available whitespace next to the floating
elements. If there's room for a container to fit next to the some floated content, and that
not the intended affect, you can use the `clear` property. You can set it to clear, or reset from,
the element floated `left`, `right`, or elements floating with either using `both`. An example of
using `float` for layout structure can be seen in the snippet below:

<iframe width="100%" height="300" src="//jsfiddle.net/flatiron_school/VGue9/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

In this scenerio, we want the footer to cleanly display below all the column. In order to get the
footer to clear past the height of any floating content we can use the `clear` property. Using
`clear: both` for footer forces it to clear past the height of anything that's floating left and right,
and stay at the bottom of the columns, right where we want it.

In the next example, you can see `float` being utilized to wrap text around an image. 

<iframe width="100%" height="300" src="//jsfiddle.net/YXBnC/47/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

The image is given a `display` property of `block` (or `inline-block`) so that it can take
block properties such as `margin` to give it spacing. When the class `.fall-below` is removed,
the block of text continues to wrap around the image until there is a line-break in the text
that allows it to flow around. 

## Create `clearfix` to Clear Floated Content

When `float` is used with elements, there can be some unintended results. As elements are floated,
it is important to notice how they affect the flow of a page, and reset floats as necessary. Not
doing so can cause some headaches when dealing with structuring elements. To deal with these issues
the technique of using a `clearfix` can come in.

<iframe width="100%" height="300" src="//jsfiddle.net/eQRJM/17/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

In the above code snippet, if you remove the `clearfix` class from the containers, you can see that
the floated content is now falling outside of the parent element, because the parent element loses 
reference to its child elements as the parent element is not floating and its children have broken
out of the page flow.

The special `clearfix` class is a CSS "hack" that will allow the parent elements to be aware of its
children's height, even when they break the page flow. Sometimes the `clearfix` is referred to as
`group` to be more semantic to developers. There are a couple of different ways this hack can be
written. Both styles below provide the same outcome:

```
/*
  ========================================
  Clearfix
  ========================================
*/

.clearfix:after {
    content: ".";
    display: block;
    clear: both;
    visibility: hidden;
    height: 0;
    line-height: 0;
}

/*
  ========================================
  Group
  ========================================
*/
.group:after {
  content: "";
  display: table;
  clear: both;
}
```

As CSS3 techniques become more widely adapted, hacks such as the clearfix may soon become
obsolete. A new value of the display property has been launched.

```
.group {
  display: flow-root;
}
```

Using `display: flow-root` on an block element will perform the clearfix for us. Instead of needing
to apply the `clearfix` hack, we can use the `display` property on the container with a value of
`flow-root`. 

**NOTE: There may still be unintended results with this new property that could potentially
impact other properties like `z-index`, so use with caution!**

## Use `position` to Give Fixed Properties to Elements

Positioning allows you to place elements outside of the normal document flow. The `position` 
property can allow a UI element to float over the top of other parts of the page, or always 
sits in the same place inside of, or offset from the parent, regardless of the placement of
other elements. 

<iframe width="100%" height="300" src="//jsfiddle.net/flatiron_school/rgyPC/2/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

#### Using `relative` Positioning

The `relative` value for the `position` property allows elements to appear within the normal
flow of a page, however it gives us the ability to offset an element from the top, right, bottom,
or left that direction the number of units that is set without changing the positioning of the
elements around it.

#### Using `absolute` Positioning

If we set `position` to `absolute` it also gives us the same ability, however the values that
are applied for these properties will move the element within the relatively positioned parent, 
or within the entire browser window, instead of the element only moving relative to where it
was in the dom. The element will not appear within the normal flow of a document, and the
original space and position of the absolutely positioned element will not be preserved. A common
example of absolutely positioned elements in common UI are "close" buttons in a window. They are
typically docked to the top-right of a container (sometimes the top-left).

#### Using `fixed` Positioning

An element with `position` set to `fixed` shares all the rules of an absolutely positioned element,
except that the browser window positions the fixed element, as opposed to any parent element.
Additionally, a fixed element does not scroll with the document. It remains fixed within the window.
Commonly used fixed UI elements can be <a href="https://tympanus.net/Development/ModalWindowEffects/" target="_blank">modal windows</a>,
or <a href="https://tympanus.net/Development/HeaderEffects/" target="_blank">floating menus</a>. 

**NOTE: The value of `sticky` can also be used specifically for "sticky" elements like menus, but browser
support is limited.**

<iframe src="https://tympanus.net/codrops-playground/SaraSoueidan/BpnKahud/embed/result,html,css/" class="codrops-playground-embed" width="100%" height="300px" frameborder="0" scrolling="no" allowfullscreen="true" style="position: relative;"></iframe>

While positioning elements can allow for a lot of control in layout, be mindful that
it is not a method you would use for entire layouts. However, there are many tasks it
is suited for that enhances layout and functionality.

## Use `z-index` to Change the Depth of Elements

Positioning and `z-index` often go hand-in-hand. Have you ever noticed UI elements that overlap part of
the page, such as a drop down menu, tooltip, or a popover? When you click on a photo, a modal may pop
up with an enlarged version of it. These are a couple of common examples where you want to control the
placement of each layer on the page. This can be achieved using a property called `z-index`. 

The `z-index` property controls the stacking order of elements that overlap. A higher value means the
element will be closer to the top of the stacking order. `z-index` only effects
elements that have a position value other than `static`, the default. When the z-index property isn't
involved, the stacking order is prioritized by the following: 

1. The <html> (root) element, background and borders of the element that establish stacking context
2. Elements with negative stacking contexts, in order of appearance
3. Non-positioned, non-floated, block-level elements, in order of appearance
4. Non-positioned, floated elements, in order of appearance
5. Inline elements, in order of appearance
6. Positioned elements, in order of appearance

Observe the example below to see how elements are effected when positioning and `z-index` are applied:
<iframe width="100%" height="300" src="//jsfiddle.net/nWGts/132/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

Try changing the `z-index` property of individual elements to stack them in a different order. By
default, the top-most element would be the blue square, with the id of `c`, but the red square with
the id of `a` appears closest to you on the screen, since it has a higher `z-index` value.

## Use `margin: auto` to Center Block Elements

In constructing a layout and various layout elements, centering in the "unknown"
will be needed often to align elements in the center of a page without giving fixed
values that may not work for various screen sizes. With `margin: 0 auto;` it is possible!

<iframe width="100%" height="300" src="//jsfiddle.net/flatiron_school/VGue9/embedded/html,css,result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>


In the example above, we've wrapped all of content inside of one element, which is
the div with the class of wrapper. By setting the width of this wrapper element, it
will prevent it from stretching to the full width of a screen. Its `margin` is set to `0 auto`. The first value
is `0` meaning zero `margin` on the top and bottom, and the second value `auto` means
it will automatically calculate the left and right margin. If you drag the results
window larger or smaller, it will adjust the margin accordingly.

The only issue with this is when the element is wider than the browser window.
We will discuss later on how to adjust for this limitation.

## Conclusion

CSS enables us to choose from many options with positioning elements. Over the past
couple of years alone, CSS has dramatically changed as well as the way we develop
website front end. We need to understand the fundamentals in order to best make
a decision as to how to leverage these properties. With `float`, `clear`, `position`,
`z-index`, and `margin`, we're able to take control of CSS layouts and content
design--whether it's for alignment, spacing, and other design choices.
