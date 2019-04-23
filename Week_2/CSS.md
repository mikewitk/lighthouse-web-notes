# CSS

## Flexbox Froggy

link: https://flexboxfroggy.com

**Property: justify-content**

* flex-start: item align to the left side of the container
* flex-end: items align to the right side of the container
* center: item align at the center of the container
* space-between: items align with equal spacing between them (doesn't care about the container)
* space-around: items display with equal spacing around them (and also with the container)

**Property: align-items**

* flex-start: items align to the top of the container
* flex-end: items align to the bottom of the container
* center: items align at the vertical center of the container
* baseline: items display at the baseline of the container
* stretch: items are stretched to fit the container

**Property: flex-direction**

* row: items are placed the same as the text direction
* row-reverse: items ar eplaced opposite to the text direction
* column: items ar eplace top to bottom
* column-reverse: items are placed bottom to top

**Property: order**

By default, item have a value of 0, but we can ue this property to set it to a positive or negative integer value

**Property: align-self**

This property accepts the same values as `align-items` and its value for the specific items

* flex-start: items align to the top of the container
* flex-end: items align to the bottom of the container
* center: items align at the vertical center of the container
* baseline: items display at the baseline of the container
* stretch: items are stretched to fit the container

**Property: flex-wrap**

* nowrap: every item is fit to a single line
* wrap: items wrap around to additional items
* wrap-reverse: items wrap around to additional lines in reverse

**Property: align-content**

* flex-start: lines are packed at the top of the container
* flex-end: lines are packed at the bottom of the container
* center: lines are packed at the vertical center of the container
* space-between: lines display with equal spacing between them
* space-around: lines display equal spacing around them
* stretch: lines are stretched to fit the container

`This can be confusing, but *align-content* determines the spacing between lines, while *align-items* determines how the items as a whole are aligned within the container. When there is only one line, *align-content* has no effect`



## Grid Garden

**Property: grid-column-start**

ex: grid-column-start: 3

**Property: grid-column-end**

Works together with `grid-column-start` to extend the item across mutiple columns

**Property: span**

Intead of defining a grid item based on the start and end positions of the grid lines, you can define it based on your desired column width using the `span` keyword.

ex
grid-column-end: span 2

**Property: grid-column**

It's the short version of *grid-column-start/end*. It takes two argument

ex: grid-column: 2 / 4

**Property: grid-row-start**
**Property: grid-row-end**
**Property: grid-row-start/end: span**
**Property: grid-row**

**Property: grid-area**

It acceps 4 values separated by slashes: grid-row-start / grid-column-start / grid-row-end / grid-column-end

ex: grid-area: 1 / 1 / 3 / 6

**Property: grid-template-columns**

Takes in the size of each column.

ex: grid-template-columns: 20% 20% 20% 20% 20%
(created 5 columns equally sized to be 20% of the total space available)

