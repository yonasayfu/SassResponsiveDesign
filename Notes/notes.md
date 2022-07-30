## Sass Partials

used to split css file in multipple single file.

1.  create /scss/globals/\_boilerplate.scss
    => {
    html { # box-sizing: border-box;
    // insures that if we are adding border or padding in the website it include the finle height or width of the element
    e.g if we set a box size 300px wide if I add 20px padding on the side => the final width gone be 300

                # font-size: 100%;
                // set for accessiblity purpose now the system use 100% of the default size wich is set in the browser 16px
            }

            body {

    // We reset the default browser elments value
    // because they vary from browser to browser
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
    background-color: hsl(0, 0%, 11%);
    color: hsl(0, 0%, 100%);
    }
    }

2.  Create another boilerplate @ /global/\_typography.scss

h1,
h2,
h3 {
font-weight: 700;
line-height: 1.1;
margin-top: 0px;
}

p {
margin-top: 0px;
}

a,
a:visited,
a:active {
text-decoration: none;
}

3. Load the partial scss into main style.scss file

3.1) Create an global/\_index.scss file and export the two file from here

Add this two line

@forward 'boilerplate';
@forward 'typography';

3.2) @ Style.scss file just forward the global folder

@forward 'globals'; // it looks automatically the index file

## Variables

both css and Scss use variables

Css variables called => custome properties

Used for reffer
color value, font styles, spacing ....

1. in the global folder create a new file wich holde the color variable
   and update the index files

2. load font values /global/utils/

\*\* for scss variable the name began with $ sign

3. import the fonts inside body @ boilerplate

untill we add @use inside a boilerplate file we get an error

@use "../util";

// and we should use the name space as an object call like ( util.variableName)
// util.$font

// we can give the alias for @use importer ===> ( @use '../util' as u)

// if we use wildcard as alias ( as \* ) we did not supposed to prefix the //imported variable ( u.$font ==> $font only)

// but this lead as to name conflict into the program recomanded better to use aliass

## building a responsive layout

1. wrap with all inside a main tag aside tag

the main tage means the main content of the websites
and the aside means the secondary conten.

\*\* it is better to use Semantic tag like (h,p) they have their own padding and best for SEO on the website and easy for navigate into the page

it is not alike (span) tag.

## Sass and BEM

1. Create a new folder layout inside a scss dir
   and add afile index.scss and forward at main scss file

2. embaded the main and aside tage with div grid class for manging parent and child relation the main and aside will gone be a child of grid class

3. add a class name for main and side bar with double under score ( we call it
   BEM => block element modifier) it an approch of sass styling

   grid**main
   gird**sidebar

4. Create a grid css class under layout folder and forward to index

4.1) add a selector class for grid
.grid{
// add a selector for main and side bar
//use the ampersand & for nesting the two selcotr in one selection
// the benfit of using BEM is it keep the class name uniq and avoid style conflict
and are best for code organization

&\_\_main{

    }

    &__sidebar{

    }

}

## Build 2 column Responsive layout

media queries paly a master role in here

1. write the styled rule inside a Parent \_\_grid class

display: grid; // we should set the grid value

grid-template-columns:1fr; // we set 1 b/c we want 1 column
it divide to many column with the available space
since we set 1 column => the 100 % of 1 column == two column

the "fr" unit is used for css grid it means ( fractional units)

2. add space b/n grids write another style group

gap: 46px;

3. add a padding inside acompund selctor

&**main, &**sidebar{
padding: 40px;

}

4. add a media query insid parent grid selector
   \*\* in sass we can put the media query inside a parent selector alike an impure css
   it makes sass easier than css

- using media we can change the width of the web based on our view port

$$
we need set one column for mobils

$$ most mobiles are 370px wide and taplest are 800px wide and small screen start from 1024px

$# to set 2 columns for small screen start from 900px and up
this makes 1 columns in mobile portrite in taplet and 2 columns for landscape tablet

@media (min-width:900px){
grid-template-columns: 2fr 1fr;
gird-template-columns: auto; // means for 900px greater than the grid will only have one row

}

* Styles outside of media queriy use the default styles
if they use the same property for d/t value
* better to use min than max

@media (min-width:900px) and (max-width: 1920px){

}
$# if we use the and at media it means the style rule apply b/n the two given
value.

$# but it is not recomanded to use this method b/c we will write another rull for
device that are larger than 1920px


## Setting Widths

** we can create column layout with flex-box too.

CSS Grid Layout
The CSS Grid Layout is a two-dimensional grid-based layout system with rows and columns. It is useful in creating more complex and organized layouts.

To define a grid container, you will have to pass a display: grid property to your element.

CSS Flexbox
The CSS Flexbox is a one-dimensional layout. It is useful in allocating and aligning the space among items in a grid container. It works with various kinds of display devices and screen sizes. Flex layout makes it easier to design and build responsive web pages without using many float and position properties in the CSS code.

To start using Flexbox, you have to create a flex container using the display: flex property. Every element inside the particular flex container will act as a flex item.

*$# stop using static width for style rules since all divaice have d/t sizes
best to use like 1fr

*$# bess to set max-width in the parent elemnt like

max-width: 1000px; // the size it will not go over for the x-larger devicess

// use margin-left and margin-right : auto;

// or use the shortcut margin: 0 auto;

$# it is better use the new property ( margin-inline:auto;)
b/c it only set the right and left elments it did not affect the ( top and bottom)
elments.
// inside the dom it set ( margin-inline-start: auto; and margin-inline-end:auto)
// it set when it reach the max size the content placed in the middle of
// the screen

$### or we can use the body tag if we add the property
display: grid or flex; and
jsustify-content: center;

and comment out the margin-inline from grid file it work the same as the previous
but do not forget the ( max-width)

$# to set the width dynamic use the min()

width:min(100%, 1000px); // the 100% fit the mobile device and the max will be 1000

// to set the left and right padding for mobile device which did not affect for larger screen add the minus 40px inside min();

width: min(100%-40px, 100px);


## Sass Mixins and Built-in Modules

uses for re-work media qureris

1) create a new file inside util folder and rename it _breackpoints.scss

// create a breack points for mobile, tablets and Desktops
// 700px,(mobile will be 700 and less) 900px (taplate), 1440px (small screen and larger)

$# To set the ui we can use the map built sass moudel 
better for set the alias name for each size 

// it is best practice to use em units 
// to convert px to em use calculate relative to parrnt elments
// which is 16px ==> 1em == 16px

2) Create a mixn with map-get function

@mixin breakpoint($size ) {
    @media (min-width: map-get($breakpoints-up, $size)){
        @content;
    }

3) To use mixin in the project add into the file grid.scss
using @include then the name of the mixin
$# it need to load the util module inside the grid it self
like we did in the boilerplate.scss

@include breackpoint(large){
   // some code here
}

4) let say we want our text centered on mobile and tablet only 
the desktop used the default align

#$ on the side bar selector at grid.scss add a media query

the default => text-align: center;

then use the include media

@include u.breakpoints(large){
   text-align: left;
}

or we can use the max-width with media query

@media (max-width: 56.25em // large device){
   text-align: center;
}

to avoid unkonwn beaviour of the app creat the max-width ruls on breakpoints
b/c small change of pixles can make our app wiered

// 699.98, 899.98, 1439.98
// the bootstrap team used this method and it avoid the overlap

$breakpoints-down(
   "small" : 43.7485em;
   "large" : 56.24875em;
   "xlarge" : 89.99875em;
);

#$ Orders of the Media Queris matters

## Responsive Design Typography

on the typography.scss section add a mixn (do not forget use the util calss on top)

@use '../util' as u;


h1 {
  font-size: 28px;

  @include u.breakpoint(medium) {
    font-size: 36px;
  }

  @include u.breakpoint(large) {
    font-size: 46px;
  }
}

#$ to simplify with one linke of code we can use vw (view width) port

1 view port unit is == 1% of the device view port

on the mobile phone 375 px wide === 3.75px vp

and there is the same as vw ==> vh (repersents the hight)



