[Quiz](https://openclassrooms.com/en/courses/5625786-produce-maintainable-css-with-sass/exercises/3171)
# Apply advanced Sass techniques to your code

## Question 1
**Which of the following directory names are not part of the 7-1 file system?**
- [ ] Base
- [x] _variables.scss
- [ ] Themes
- [ ] Utils

_The seven directory names used in the 7-1 file system are:

Base
Utils
Layout
Components
Pages
Themes
Vendors

_variables.scss is the name of a Sass partial, which can be imported into the main.scss file, and should be placed within the Util directory._

## Question 2
**Which of the following are properly formatted Sass maps?**
- [ ] $map: (key1,$value1,key2,$value2,key3,$value3);
- [x] $map: (key1:$value1, key2:$value2, key3:$value3);
- [ ] $map: value1, value2, value3;
- [ ] $map: $value1 $value2 $value3;

_Sass maps must contain key/value pairs, where the key is formatted using the dollar sign ($) as a prefix, and the value is separated by a colon ( : ). Each key/value pair must be separated by commas, and they all must sit inside a set of parenthesis._

## Question 3
**Autoprefixer creates cross-browser compatible CSS by:**
- [ ] Removing non-compliant code.
- [ ] Placing non-compliant code in a separate file.
- [x] Automatically adding the necessary prefixes to our CSS.
- [ ] Alerts the user to upgrade their browser to the current version.

_Vendors don’t necessarily want to wait for the new properties to be standardized before they implement them in browsers. So, until they become standardized, each browser has it's own version of those properties, which can be identified by their specific presets. Rather than manually entering all of the prefixes yourself, you can use Autoprefixer to generate them automatically._

## Question 4
**$map: (
    pink: &num;f442f1,
    mint: &num;15dea5,
    navy: &num;2a2760,
);

@each $key, $value in $map {
    .btn--&num;{$key} {
        background-color: $value;
    }
}

Which of the following selectors would be generated from the @each loop above?**
- [x] .btn--pink {
    background-color: &num;f442f1;
}
- [x] .btn--mint {
    background-color: &num;15dea5;
}
- [ ] .btn .navy {
    background-color: &num;2a2760;
}
- [ ] .mint {
    background-color: &num;15dea5;
}

_The  @each  loop will generate a selector with the prefix of  .btn-- followed by the name of each key in  $map . It will create a background color property with the color from that key's value inside each selector._

## Question 5
**Which of the following .sccs snippets is properly formatted to import the _variables.scss partial into main.scss given the following file-structure:**
- [x] @import "./Utils/variables";
- [ ] @import "variables";
- [ ] @import ./Utils/variables;
- [ ] import "./Utils/variables";

_To import the variables partial, you need to type  @import  followed by a set of quotes. Inside of the quotes, type out the path to your variables partial. The leading period . of the path tells Sass that the partial’s path starts in the same directory as main.scss. Then  /Utils/  leads Sass to the utils directory, where it will find the variables partial.
When typing the name of the partial, don’t use an underscore or file extension in the partial’s filename. Sass knows to look for a file beginning with an underscore, and that it will be a Sass file, so you can skip that extra bit of typing._

## Question 6
**Which of the following are validly formatted Sass lists?**
- [x] $list: $value1, $value2, $value3;
- [x] $list: ($value1, $value2, $value3);
- [x] $list: $value1 $value2 $value3;
- [ ] $list: $value1$value2$value3;

_The syntax for writing lists is extremely flexible. You can wrap them in parenthesis or leave them open. You must, however, separate the values, either with spaces or commas. Answer &num;4 isn't properly formatted because the values aren't separated from one either._

## Question 7
**What will the margin of  .block  be if the browser width is 480px?
@mixin mobile-only {
    @media screen and (max-width: 599px){
        @content;
    }
}

.block {
    margin: 1.5rem;
    @include mobile-only {
        margin: .5rem;
    }
}**
- [ ] 1.5rem
- [ ] 2rem
- [x] .5rem
- [ ] 0

_The  mobile-only  mixin contains a media query for a screen with a  max-width  of 599px, so if the screen is 599px wide or less, the browser will apply the rules contained within the media query, which we can set on a use-by-use basis using the  @content  directive.
Since the browser width is 480px, it will apply the ruleset that we have written when we included the  mobile-only  mixin with  .block , which, in this case, is a  margin  of  .5rem_

## Question 8
**Which of the following snippets will return a value of 3rem from the following Sass list?
$list: 1rem, 2rem, 3rem, 4rem;**
- [ ] nth($list, 2);
- [x] nth($list, 3);
- [ ] $map-get($list, 2);
- [ ] nth(3, $list);

_To access individual values from a Sass list, call the nth() function with two arguments:

The first argument is the name of the list that you want to access.
The second argument is the index of the value you want to return, where the first item in the list has an index of 1.

In the case of the list provided in the question, the name of the list is  $list  , and  3rem  has an index of 3, so to return the value of  3rem  from the list, you would call thenth() function as follows:
nth($list, 3);_

## Question 9
**$map: (
    small: 1rem,
    medium: 5rem,
    large: 10rem
);

Given the map above, which of the Sass loops would produce the following selectors:
.btn--small {
    font-size: 1rem;
}
.btn--medium {
    font-size: 5rem;
}
.btn--large {
    font-size: 10rem;
}**
- [ ] @each $size, $measurement in $map {
    .btn--&num;{$measurement} {
        font-size: $size;
    }
}
- [ ] @each $size, $measurement in $map {
    .btn--$size {
        font-size: $measurement;
    }
}
- [x] @each $size, $measurement in $map {
    .btn--&num;{$size} {
        font-size: $measurement;
    }
}
- [ ] @each $size, $measurement in $map {
    .btn--${size} {
        font-size: $measurement;
    }
}

_We're starting with a Sass map with three keys/value pairs, and need to produce three selectors, where each key is incorporated into the name of the selector, and it's value is assigned to a font-size property. In an @each  loop, the first variable declared is for a map's keys and the second for its values. The loops used in this question's options,  $size , is the variable assigned to  $map 's  keys, and  $measurement  to its values.
That means that you want to use $size in the selector name. To use it within a string, you need to use the interpolation syntax, where you wrap it within a hashtag and curly braces:  &num;{$size} . And then use that key's value to set the font size of the selector: 
@each $size, $measurement in $map {
    // include key's name within the selector's name
    .btn--&num;{$size} {
        // use the key's value as the selector's font size
        font-size: $measurement;
    }
}_

## Question 10
**$font-sizes: (
    heading: 3rem,
    byline: 1.75rem,
    caption: 1rem
);

Given the Sass map above, which code snippet would return the value for the  byline  key?**
- [x] .article__byline {
    font-size: map-get($font-sizes, byline);
}
- [ ] .article__byline {
    font-size: map-get(byline, $font-sizes);
}
- [ ] .article__byline {
    font-size: nth($font-sizes), byline);
}
- [ ] .article__byline {
    font-size: map-get($font-sizes, 2);
}

_To access an individual value located in a map, use the map-get() function with two arguments, the first being the name of the map, and the second the name of the value's key. In the case of  byline , it is part of the$fonts map. To access  byline via map-get() , use  $fonts as the first argument andbyline as the second:
.article__byline {
    font-size: map-get($font-sizes, byline);
}_

## Question 11
**.form{width:100%;padding-bottom:1.5rem}.form__heading{width:100%;color:&num;fff;text-shadow:.55rem .55rem &num;11af82;background:&num;15DEA5;line-height:5rem;padding:1.5rem}.form__field label{color:&num;D6FFF5;display:block;font-size:2rem;line-height:2rem;padding-top:1.5rem}.form__field input{width:100%;background:&num;001534;border:0.1rem solid &num;15DEA5;padding:1.5rem;color:&num;D6FFF5;font-weight:900;font-style:italic;font-size:2.75rem}.form__field textarea{width:100%;color:&num;15DEA5;background:&num;001534;border:0.1rem solid &num;15DEA5;outline:none;padding:1.5rem;margin-bottom:.75rem}

To prepare for deployment, which of the following snippets will compile Sass code to minified CSS, as seen in the code above?**
- [ ] --style nested
- [ ] --style expanded
- [ ] --style compact
- [x] --style compressed

_Sass has four different compile modes available at compile time, via the  --style  flag:

Nested: mimics Sass nesting while maintaining valid CSS syntax.
Expanded: most similar to how we typically write CSS by hand, and therefore can be the easiest to read for some.
Compact: fits each selector and its ruleset on its own line.
Compressed: removes any whitespace and line returns, creating a smaller file sizes better suited for deployment, and is often referred to as minified code.

In order to prepare for deployment, the best practice is to compile Sass into minified CSS via the compressed mode._

## Question 12
**What must you add to your package.json file to ensure Autoprefixer adds prefixes to cover the previous three versions of the major browsers?**
- [ ] "browser-history": "3 versions"
- [x] "browserslist": "last 3 versions"
- [ ] "browsers": "last 3 versions"
- [ ] "browserslist": "last 3"

_To have Autoprefixer add prefixes for properties going back further than a single version, you need to add the key"browserslist" to your package.json with "last XX versions" as the value, where  XX is the number of versions you want included. In the case of this question, you want to include the last three versions of browsers in your prefixing, so you need to big  "browserslist" a value of  "last 3 versions"_