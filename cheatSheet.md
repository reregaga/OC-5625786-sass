# Structure your CSS
How should you go about writing your CSS to make sure that it’s clean and maintainable? **CSS doesn’t have a rigid structure**, which can make it hard to keep a clean and maintainable codebase. By **creating and implementing your own structure**, you can keep keep an unwieldy CSS in check. Step one is **finding categories**. Scroll through your CSSand you will likely begin to notice heaps of repeated rules. For example, all of your buttons are using the same padding and font color, and nearly all of them have the same background color. This means that **you have repeated your code**. 

There’s a concept in programming known as the **DRY** principle, which goes like this: **Don’t repeat yourself**. Those piles of repeated CSS rules are preventing you from achieving a DRY codebase, and are wreaking havoc on its maintainability by making it **cumbersome to update values**. 

Begin by **refactoring**, or in other words, cleaning up your code. Start by looking through all of your selectors and **finding commonalities**.

## Example
Let’s say that you notice that **all your buttons have the same** background color, color, and padding. You might end up with something like:
```css
.btn {
    background-color: #001534;
    color: #15DEA5;
    padding: 1.5rem;
}
.btn-wide { width: 100%; }
.btn-rounded { border-radius: 3rem; }
```
So instead of your HTML looking like this:
```html
<button class="btn"> OK </button>
```
Your markup looks like: 
```html
<button class="btn btn-rounded btn-wide"> OK </button>
```

What we’ve just done is called **separation of concerns**. In the `.btn` selector, we’ve defined the very essence of our buttons, and nothing more. **One selector = one set of basic rules**. Every button in your code will have these qualities. In the `.btn-wide` and `.btn-rounded` selectors, we’ve added additional rules that, when combined with `.btn`, will modify the button. 

By separating concerns, your codebase instantly becomes **easier to maintain**; instead of relying on  `Ctrl+F` and Find-and-Replace to update your buttons’ padding, you **only need to change the value on a single rule set**.

## Note
There are no hard, set-fast rules for architecting your CSS - only educated opinions. The means and methods of this course are **battle-tested, highly adopted practices within the industry**, whose foundations will serve you well in creating a clean, maintainable CSS codebase on projects **of all scales**.  The most important takeaway in building a strong, maintainable front-end code is to **sit down, make a plan, and stick with it**.  Instead of looking through your existing code like we did in the example above, you need to think about how to structure your code **before you even write a line**. We showing you how to implement a **well-defined, highly-semantic naming convention for your selectors**. 

# What is specificity?
Let’s look at an example.  Say you have a button element with an  id  of submit-button  and a class of button:
```html
<div id="submit-button" class="button">Click Here!</div>
```
And in your CSS file, you’ve assigned a different background color to each, as well as the button element:
 CSS
```css
#submit-button { background-color: #15DEA5; }
.button { background-color: #DB464B; }
```
So, when you look at your button **in a browser, what color will it be**? The answer lies in each of the **selectors’ specificity**. When an element has conflicting rules applied, such as multiple background colors, the browser will apply the **rule from the most specific of the selectors**.
## The four horsemen of specificity
The browser lumps CSS rules into four categories:
- Inline styles: 
```html
<div style="background-color:#15DEA5;">Click Here!</div>
```
- IDs:
```html
<style> #submit-button { background-color: #15DEA5; } </style>
<div id="submit-button">Click Here!</div>
```
- Classes, pseudo-classes, attributes:
```html
<style> .button { background-color: #DB464B; } </style>
<div class="button">Click Here!</div>
```
- Elements and pseudo-elements:
```html
<style> div { background-color: #DB464B; } </style>
<div>Click Here!</div>
```
When the browser is deciding which of the conflicting rules to apply, it tallies up the number of categories being implemented by a selector. So our three selectors would be tallied as follows:
`#submit-button {...}` :
|Inline|ID|Class|Element|
|-|-|-|-|
|0|**1**|0|0|

Once the tallying is done, the browser starts by looking at the scores in the **left column**, because **inline selectors are the most specific**. If there’s a selector with a higher score, the browser will apply its style. **If there’s a tie, it moves right to the next column and does the same thing.** **Comparison column by column.**

**What if you were to add a second class to the button selector?**
```html
<style>.button.submit-button { background-color: #DB464B; }</style>
<div class="button submit-button">Click Here!</div>
```
That would change its specificity to:
|Inline|ID|Class|Element|
|-|-|-|-|
|0|0|**2**|0|

Although it might seem like the new double class selector of `.button.submit-button` would be more specific, it still loses out to `#submit-button`. Remember, **the browser works from left to right**, and since `#submit-button` has a **higher score in the ID column, the browser stops there**. It **doesn’t matter if a selector has two classes, or 200**, an ID selector will always be more specific than a selector of classes.

But what if you really want to use the color from the class selector? Instead of a second class, you could add the  id  to it as well:
```html
<style>
    #submit-button {background-color: #15DEA5;}
    #submit-button.button { background-color: #DB464B;}
</style>
<div id="submit-button" class="button">Click Here!</div>
```
Now you have: `#submit-button {...}`  :
|Inline|ID|Class|Element|
|-|-|-|-|
|0|**1**|0|0|

`#submit-button.button {...}` :
|Inline|ID|Class|Element|
|-|-|-|-|
|0|**1**|**1**|0|

Now **there is a tie for the ID column, so the browser moves right to the class column**, where  `.button` wins 1-0, and the browser applies its background color to the button.

You will often want to **override** certain attributes with a modifying selector, rather than writing out a ton of specific selectors. This helps make your code more **modular and reusable**. ID selectors are difficult and messy to override, thats why **avoid using ID's**. By sticking with classes to create your CSS selectors, you ensure that they have a low but consistent specificity. This makes conflicting rules easier to predict and manage.

**What happens if the browser goes through the columns and ends in a tie?**
```html
<style>
.submit {background-color: #15DEA5;}
.button { background-color: #DB464B;}
</style>
<div class="button submit">Click Here!</div>
```
Both `.submit` and `.button` have the same score, which selector wins out? In the case of a tie, the browser selects the **last selector to have been declared in css**, not last used in html code.

# BEM (Block Element Modifier) selectors naming
Being able to look at a class name and know what it does and how it interacts with other elements will save a lot of time and energy in the future. Enter BEM, a CSS naming methodology that will help you do just that. 

BEM is an acronym for **block, element, modifier**. By **assigning each selector you write to one of those three categories**, you are able to **define their functionality and hierarchical relationships**, while naming them appropriately.

## BLOCK
A **block is a component, or section, of a page that can stand alone and function independently** from the rest of the page. This could be a **header, container, menu, or button**. The key is that you could strip away all of the surrounding website and it would still make sense. For example: text string like "Project X"  wouldn't make much sense, but if it is string with picture of project and plus small annotation, and we have some this groups after another, then it is look like a blocks! You **name a block by describing its purpose**. Let’s name the block selector for our project preview  `.proj-prev`.
```css
.proj-prev { color: #fff; margin-bottom: .25rem; }
```
Now remember that text for the project title that wouldn’t work on its own? Since it **doesn’t function independently**, but rather forms an **integral part** of the block, it's an **element** of the **block**.

![fig 1](img/block-element.jpg)

The **name of an element should identify its parent block, followed by double underscores** (also known as “dunders”), and then the element’s purpose. Since it's the heading for the project preview, we'll name it  `.proj-prev__heading`  and assign the following rule set:
```css
.proj-prev__heading {
    font-size: 4rem;
    padding-left: 2.5rem;
    margin: 0;
    line-height: 6rem;
}
```
That leaves us with **modifiers** which, as its name indicates, **changes the appearance of a block or element**. Think of them as selectors that **produce different versions of blocks and elements**. Need to change the size, color, typography, etc., of an element, but otherwise, leave it as it is? That’s what modifiers are for! 

You’ll create a modifier for your `.proj-prev` block. To name the modifier, first identify what it’s modifying, followed by two dashes, and then the visual style of the modifier. Since you are modifying the `.proj-prev` block to have a mint font color, you can call it `.proj-prev--mint`, and style it as follows:
```css
.proj-prev--mint { color: #15DEA5; }
```
```html
<section class="proj-prev proj-prev--mint">
    <div class="proj-prev__image"><img src="/public/img/photography_1280w.jpg"></div>
    <h1 class="proj-prev__heading">Project Title</h1>
    <p class="proj-prev__byline">project keywords would go here</p>
</section>
```
Here is our entire contact page, broken down into its blocks, elements, and modifiers:

![fig 2](img/page-structure.jpg)

```html
<nav class="nav">
    <ul>
        <li class="nav__link nav__link--active">work</li>
        <li class="nav__link"> <a href="/about.html">about</a> </li>
        <li class="nav__link"> <a href="/contact.html">contact</a>  </li>
    </ul>
</nav>
```
**BEM selectors are always implemented as classes.** To be able to apply modifiers with consistent results, you need to ensure that **your selectors have as low a specificity as possible**. If you were to assign the block selector as an ID, rather than a class, its specificity would inherently trump all the modifying selectors assigned as a class.

```css
.nav {
    padding-right: 6rem;
    text-align: right;
}
.nav__link {
    display: inline;
    font-size: 3rem;
    padding-left: 1.5rem;
}
.nav__link a {
    text-decoration: none;
    color: #D6FFF5;
}
.nav__link--active { color: #001534; }
.nav__link a:hover { color: #fff; }
```
While we are attempting to keep the selector specificity low, pseudo-classes, such as `:hover` and combinators, like the descendant combinator, are perfectly acceptable to use. It’s true that they will increase the specificity of the selector, but they can help yield cleaner, more legible code by **reducing the need to assign a class to every single element on the page**.

# CSS Preprocessors
## Creating a hierarchy in your code
Wouldn’t it be awesome if you could **write your CSS like you write your HTML**? Rather than a long list of CSS selectors, you could **indent** your elements and modifiers within their parent block, like this:
```css
.nav {
    padding-right: 6rem;
    flex: 2 1 auto;
    text-align: right;
        .nav__link {
            display: inline;
            font-size: 3rem;
            padding-left: 1.5rem;
                .nav__link--active {
                    color: #001534;
                }
        }
}
```
Having a **visual hierarchy** not only makes things much easier to read, but it also helps to keep everything contained. By forcing an object to exist within **relative blocks**, it makes it much easier read and maintain your codebase; rather than scrolling around a document for random elements from a block of code, you simply need to locate that particular block and **all of its relative elements will be there with it**. With **CSS preprocessors**, you can write your code in a more visually coherent manner through features like **nesting**. Preprocessors give you the best of both worlds by **compiling its syntax into standard CSS for browsers to read and render**.
- **Variables** allow you to **store often repeated values**, such as colors and measurements, into a single element and reuse it throughout your code. Imagine that you’ve used a shade of green hundreds of times throughout a site, and now need to change it to red. With variables, you’d only have to change it once.
```scss
$mint: #15DEA5;
.header { background-color: $mint }
```
- **Loops**, which automate repetitive tasks such as creating a bunch of color modifiers, save you a lot of tedious coding while maintaining a much smaller codebase to manage.
```scss
$colours:(
    mint: #15DEA5,
    navy: #001534,
);
@each $colour, $hex in $colours {
    .btn--#{$colour} { background-color: $hex; }
}
```
```css
.btn--mint { background-color: #15DEA5; }
.btn--navy { background-color: #001534; }
```
- **Logical operations** allow you to write a single block of code that you can use in different circumstances and have it react accordingly, such as determining the font color based on a background color. For example, if the background color is dark blue, make the font white.
```scss
@if (lightness(#15DEA5) > 25%) {
    .header {
        color: #fff;
        background-color: $mint;
    }
}@else{
    .header {
        color: #000;
        background-color: $mint;
    }   
}
```
```css
.header {
    color: #fff;
    background-color: #15DEA5;
}
```
## Vendors
There are a lot of CSS preprocessors out there, but the three most prominent are **SASS** (Syntactically Awesome Style Sheets), **Less**, and **Stylus**. However, on the whole, **they all do the same thing in a very similar manner**. In this course, **we’ll be using Sass**, why?, you are far more likely to run into Sass in a professional environment, and it only makes sense to learn with the tool that you are most likely use in your day to day life.
### SASS
#### Syntax
There are **two different ways to write Sass**, which can be denoted by their file extensions:  `.sass`  and `.scss`. Up until now, all of the CSS precompiler snippets you have seen have been done using Sass' **`.scss`** syntax. It looks an awful lot **like regular CSS with some extra Sass sugar** sprinkled on top. The  `.scss`  syntax is rooted in the standard CSS syntax. In fact, **you can write standard CSS within a  `.scss`  file seamlessly**. The syntax that is specific to  `.scss`  only surfaces when you start to use Sass tools, such as variables and functions, where you **prefix variables with dollar signs ($)**, and **functionality keywords with at signs (@)**.
```scss
.class-selector{
    color: white;
    background-color: black;
}
```

But you also have the option of writing in the `.sass` syntax:
```sass
.class-selector
    color: white
    background-color: black
```
While  `.scss`  looks a lot like regular CSS,  **`.sass`  has a far more concise syntax**. `.scss`  syntax is similar to CSS syntax. `.scss`  is more commonly used than the more concise `.sass`  syntax, when someone talks about Sass, they are nearly always talking about `.scss`. The odds of ever needing to write `.sass` professionally are unlikely.
                                                                                           
#### Nesting
When you nest a block in Sass, it **creates an individual CSS selector with the parent selector appended**.
Sass:
```scss
ul {
    list-style: none;
    li {
        display: inline;
    }
}
```       
Resulting css:
```css
ul { list-style: none; }
ul li { display: inline; }
```              

```css
/*css*/
.parent { background-color: #15DEA5; }
.parent .descendant { color: #fff; } /* if descendand */
.parent > .child { color: #D6FFF5; } /* if child */
.parent + .adjacent { color: #001534; } /* if immediately preceded */
```                        
```scss
/*scss*/
.parent {
    background-color: #15DEA5;
    .descendant { color: #fff; }
    >.child { color: #D6FFF5; }
    +.adjacent { color: #001534; }
}
```             

You need to add a  `li:hover`  pseudo-class to your  `<li>`s to provide visual feedback and better the user experience:
```scss
/*sccs*/
li {
    display: inline;
    :hover { color: #001534; }
}
```                  
Well, that not work:
```css
/*result css*/
li :hover { color: #001534; }
```
**Nesting in Sass creates combinators** (with spaces). Sass has a **special character to concatenate** the parent and child selectors: the ampersand (**&**)!  Prefixing a nested selector with an ampersand will directly join it to the parent selector without any combinators.
```scss
/*scss*/
li {
    display: inline;
    &:hover { color: #001534; }
}
```                  
```css
/*result css*/
li:hover { color: #001534; }
```

There’s **no physical limit as to how deeply you can nest within Sass**. Remember, **when you nest selectors, you increase the specificity of the compiled selectors**. So, if you nest too deeply, you’ll end up with selectors of incredibly high specificity, making them extremely difficult to modify or override. It also greatly hinders the re-usability of your code. And that defeats the purpose of using a preprocessor at all!

Rather than trying to replicate the hierarchy of the HTML, it is **better to write nested selectors only relative to the root selector**. It **won’t represent the HTML structure as clearly**, but it helps to ensure a low specificity in your codebase while maintaining flexibility and modularity. In practice, **if you find yourself nesting more than two levels deep, stop and reassess how you are structuring your block**.

#### BEM with SASS
```scss
/*scss*/
.block{
    background-color: #15DEA5;
    .block__element { color: #fff; }
}
```
You end up with a `.block` selector with a specificity of `0/0/1/0`, and a `.block__element` selector with a specificity of `0/0/2/0`. Let’s say you then needed to create a variation of your  `block__element`  , changing its background color. This means creating a  `block__element--modifier`  selector, but since you’ve elevated the specificity of your element, you must also make sure that you are increasing your modifiers by at least as much, or they will fail to have any effect.
```scss
.block{
    background-color: #15DEA5;
    .block__element { color: #fff; }
    .block__element--modifier { background-color: #001534; }
}
```
```css
/*result css*/
.block { background-color: #15DEA5; }
.block .block__element { color: #fff; }
.block .block__element--modifier { background-color: #001534; }
```
What you need is a way to **nest in Sass without messing up the principles of BEM**? 

Child doesn’t have to be a selector; it can be plain old text as well! In our nest for `.block__element` , let’s replace the `block` part with an ampersand:
```scss
.block{
    background-color: #15DEA5;
    &__element { color: #fff; }
}
```
```css
/*result css*/
.block { background-color: #15DEA5; }
.block__element { color: #fff; }
```
Now we have an element selector with the flat specificity of `0/0/1/0`, just like we wanted.
```scss
.block{
    background-color: #15DEA5;
    &__element {
        color: #fff;
        &--modifier { background-color: #001534; }
    }
}
```

**Save specify, when you need**:
```scss
.btn {
    display: inline-block;
    background: #15DEA5;
    &--disabled {
        background: grey;
    }
    &--outline {
        background: transparent;
        border: 2px solid #15DEA5;
        &.btn--disabled{
            border: 2px solid grey;
        }
    }
}
```
`.btn`,`.btn--outline`,`.btn--disabled`, `.btn--outline.btn--disabled`. Technically, selector #4 has a specificity of two, but `.btn--disabled` **also works without**  `.btn--outline`, making it a modular, reusable  system, where you can add or remove the class and have the element behave as we'd expect.
```html
<!-- make both buttons disabled -->
<div class="btn btn--disabled">Solid Button</div>
<div class="btn btn--outline btn--disabled">Outline Button</div>
```
Let’s say you decide that you want your first button to be outlined like the second. All you need to do is apply the outline modifier:
```html
<div class="btn btn--disabled btn--outline">Solid Button</div>
<div class="btn btn--outline btn--disabled">Outline Button</div>
```
Thanks to the **heightened specificity** of the outlined/disabled combo, **adding the same class in two situations produces two separate, but predictable results**.

#### Variables
Our site is using just a handful of colors. But we’re using them over and over again. Trying to remember hex values like `#16FFBD` and `#001534`, and what colors they represent doesn’t work. Instead, I scroll around my file, looking for another instance of that color, then copy and paste. This gets tedious, fast. And it’s dangerous. The client could request a color change out of the blue, and you now need to go through the file and update color values manually. This is where errors occur. Do you know what would make things so much easier and cleaner? **Setting a color once, and then referencing it** whenever you need to make something that color.

To **declare a variable** in Sass, you type a dollar sign (**$**), followed its name, then a colon, and the value that you want it to have: 
```scss
$mint: #15DEA5;
.form{ color: $mint;}
```
Note that **standard CSS also has variables**, though they’re called "**custom properties**".
```css
/*css*/
:root { --mint: #15DEA5; }
.form { color: var(--mint); }
```

A better approach would be to **name the variable by its role or purpose, rather than its contents**. Because:
```scss
$pink: pink;
/* If we need change color from pink to red, variable $pink: red; looks strange*/ 
```
Instead of `$mint`/`$pink`, something like `$color-primary` makes a more sense. The variable name tells you that its role is to store your primary color, whether it be mint-green, pink, or vermilion. Plus, when you revisit your code months, or years later, `$color-primary` will still make sense. 

There are eight data types in Sass:
- **Color**s: we’ve already seen these!
- **String**s: the programming term for text.
- **Number**s: well, just that: numbers.
- **List**s and **map**s: collections of any of the above.
- And three you shouldn’t worry too much about now: **Boolean**, **Null**s, and **Function Reference**s.

https://sass-lang.com/documentation/values

#### Mixin
```scss
.heading__header { text-shadow: 0.55rem 0.55rem #fff; }
$heading-shadow: text-shadow: 0.55rem 0.55rem #15DEA5; /*ERROR*/
```
Instead being limited to values, **mixins store entire blocks of code**.
```scss
@mixin mixin-name { css-property: value; }
```
```scss
@mixin heading-shadow{
    text-shadow: .55rem .55rem #15DEA5;
}
.form {
    &__heading {
        @include heading-shadow;
    }
}
```
```css
/*result css*/
.form__heading {
    text-shadow: .55rem .55rem #15DEA5;
}
```
Mixins will behave differently based on its **inputs**. `$colour` looks like a variable, right? That’s the **argument**. Think of arguments as empty variables that **only live within the mixin**. You set their value each time you include the mixin in your code, and that value is used within the mixin block when it is compiled to CSS:
```scss
@mixin heading-shadow($colour){
    text-shadow: .55rem .55rem $colour;
}
 .heading{
    &__header {
        @include heading-shadow(#fff);
    }
 }
```
You can set the **default value for the argument**.  Now, if you omit the argument and don’t set a color value when you include it, Sass will assume that you want the shadow to be the default color.
```scss
@mixin heading-shadow($colour: $colour-primary){
    text-shadow: .55rem .55rem $colour;
}
 .heading{
    &__header {
        @include heading-shadow($colour-white);
    }
 }
 .form{
    &__heading {
        @include heading-shadow;
    }
 }
```
```scss
$heading-shadow-size: 0.55rem;
@mixin heading-shadow($colour: $colour-primary, $size: $heading-shadow-size;){
    text-shadow: $size $size $colour;
}
```
#### Extensions
Mixin:
```scss
@mixin typography {
    color: $colour-primary;
    font-size: 2rem;
    font-weight: 100;
    line-height: 1.7;
}
h1 { @include typography; }
textarea { @include typography; }
```
```css
/*result css*/
h1 {
  color: #15dea5;
  font-size: 2rem;
  font-weight: 100;
  line-height: 1.7;
}
textarea {
  color: #15dea5;
  font-size: 2rem;
  font-weight: 100;
  line-height: 1.7;
}
```
Lot of duplicate code in CSS file! To avoid that use: **Extensions** are **a lot like mixins**: you **write a block of code and leverage Sass to reuse it**, saving you from retyping it over and over again. Unlike mixins, **you don’t need to declare it with a special identifier** - just write it as a simple selector:
```scss
.typography {
    color: $colour-primary;
    font-size: 2rem;
    font-weight: 100;
}
h1 {
  @extend .typography; /*TODO: openclassrooms have not dot for this string in example, but dot needed here*/
}
```
```css
/*result css*/
.typography, h1 {
    color: red;
    font-size: 2rem;
    font-weight: 100;
}
```
Sure, you could rename `.typography` to something like `.placeholder-typography`, but **having selectors in your CSS file that aren’t actually being used anywhere is a bad idea**. Unused selectors needlessly increase file size, and clutter things up. Instead, **Sass has a built-in placeholder** that you can use to hold your ruleset, rather than a standard selector:
```scss
%typography {
    color: $colour-primary;
    font-size: 2rem;
}
h1 {
  @extend %typography;
}
```
Prefixing the selector with a percent sign (**%**), rather than the standard period of class selectors, creates a Sass **placeholder**. Also called “silent classes” and "placeholder classes".
#### Mixins or Extensions ?
You **use arguments or not**? **If you need to introduce any sort of argument, use mixins**; there’s no other choice.

The difference between the two is that you end up with **duplicate rules** with mixins, and with extensions, you end up with **duplicate selectors**.

Well, when it's put that way, the answer is actually pretty simple: **don’t use extensions**.

Mixins produce a bunch of duplicate code! Yes, they do. But they don’t affect the organization of your CSS. Extensions destroy the order and predictability of your codebase to save you from repetitive code. It’s not worth it.

#### Function
They are pre-built blocks of code that perform tasks, such as taking an argument, changing it, then spitting out the new value. Sass has functions to desaturate,  invert, compliment, and even darken colors (among many other things).

This function takes two arguments: a color value, and the amount that you want to darken it by. To darken `$colour-primary` for the `text-shadow`, use the function where you would normally place a color value:
```scss
@mixin heading-shadow($colour:$colour-primary, $size: $heading-shadow-size){
        text-shadow: $size $size darken($colour, 10%);
}
```
```css
/*result css*/
.form__heading { text-shadow: 0.55rem 0.55rem #11af82; }
```
Built-in fucntions: http://sass-lang.com/documentation/Sass/Script/Functions

#### Conditionals
Start by typing `@if`. Then follow it up with your conditional statement: the lightness percentage is less than 25% and a set of curly braces. To get the lightness of ` $colour`, we are using Sass'  `lightness()`  function, which returns the color's `lightness` value:
```scss
@if ( lightness($colour) < 25% ) {
    $colour: lighten($colour, 10%);
}@else{
     $colour: darken($colour, 10%);
}
```
```scss
@mixin heading-shadow($colour: $colour-primary, $size: $heading-shadow-size){
    @if ( lightness($colour) < 25% ) {
      $colour: lighten($colour, 10%);
    }
    @else{
      $colour: darken($colour, 10%);
    }
    text-shadow: $size $size $colour;
}
.form {
    &__heading { @include heading-shadow($colour-secondary); }
}
```
```css
/*result css*/
.form__heading { text-shadow: 0.55rem 0.55rem #002a67; }
```

```scss
/*my variant to solve exercise*/
@mixin hover($color) {
  @if (hue($color)<180) {
    background: adjust-hue($color, 50)
  }
  @else{
    background: adjust-hue($color, -60);
  }
}
.btn:hover{
    @include hover($color-primary);
}
/*openclassrooms variant*/
@mixin hover($color) {
  @if (hue($color) < 180) {
    $color: adjust-hue($color, 30);
  }@else{
    $color: adjust-hue($color, -60);
  }
  background: $color;
}
```
Logical operators:
```scss
@if ( lightness($colour) < 25% ) and ( lightness($colour) > 10% {...}
@if ( lightness($colour) < 25% ) or ( lightness($colour) > 10% {...}
```

#### Functions
A function is a block of code that performs a task when executed, like darkening a color, or retrieving its lightness, or converting RGB values into hexadecimal:  `rgb(21, 222,165)`. That’s right, whenever you write your colors as `rgb()` in `.scss`, you’re calling a function. 

**Define a function** by using the `@function` keyword, followed by its name, a pair of parentheses for arguments, and a set of curly braces to contain your code:
```scss
@function lightness-shift($colour){
    @if ( lightness($colour) < 25% ) {
        $colour: lighten($colour, 10%);
    }@else{
        $colour: darken($colour, 10%);
    }
}
```
Right now, the function only updates the `$colour` with a lighter or darker value. For `lightness-shift()` to return a value, you need to tell the function what you want it to return when it’s executed. 
```scss
@function lightness-shift($colour){
    @if ( lightness($colour) < 25% ) {
        @return lighten($colour, 10%);
    }@else{
        @return darken($colour, 10%);
    }
}
```
Now the function is done! Let’s plug it into our mixin, like when you call one of Sass' built-in functions:
```scss
@mixin heading-shadow($colour: lightness-shift($colour-primary), $size: $heading-shadow-size){
    @if ( lightness($colour) < 25% ) {
        $colour: lighten($colour, 10%);
    }@else{
        $colour: darken($colour, 10%);
    }
    text-shadow: $size $size $colour;
}
```
```scss
@function pastel($clr){
  $hue: hue($clr);
  $sat: 100%;
  $light: 90%;
  $pastel: hsl($hue, $sat, $light);
  @return $pastel;
}
```

# 7-1 Structure of files
Create the following seven directories within our sass directory, each of which represents a category of Sass code:
- Base
- Utils
- Layout
- Components
- Pages
- Themes
- Vendors

- The **base/** directory contains the files that define the foundation of your site, such as the typography and norms you want applied site-wide, like box-sizing.
- **utils/** is where you store **variables, functions, mixins, and %placeholders** for extensions (if you use them).
- **layouts/** is where you store BEM blocks which contain things that can be reused, such as a form or header for large layouts.
- **components/** is where you store BEM blocks that are more self-contained, such as buttons.
- **pages/**  contains blocks of code that only apply to a single page. While you use buttons all over the site, your home page has a quote section and a project grid that isn’t used anywhere else. In other words, pages/ are rules specific to a single page and won't be reused elsewhere.
- **themes/** is where you store thematic code, such as custom styling for Christmas or Halloween. This doesn't apply to the site we're creating. 
- **vendors/**  is a directory for third-party library style sheets such as Bootstrap or jquery UI. It's essentially for any CSS that has originated from outside of the project. Using third party frameworks, such as Bootstrap, are common as they speed up site development with predefined style sheets for things like buttons and forms. 

Inside `layouts/`, make a new partial named  `_form.scss`, then cut and paste the form block from `main.scss`. We must now import it into our main file to make use of it:
```scss
@import "./utils/variables";
@import "./layouts/form";
```
Once all of the code has been split into proper partials and imported, the `main.scss` file should only contain imports; rule sets will be contained in their appropriate partials:
```scss
@import "./utils/variables";
@import "./utils/functions";
@import "./utils/mixins";
@import "./utils/extensions";

@import "./base/base";
@import "./base/typography";

@import "./components/buttons";

@import "./layouts/header";
@import "./layouts/nav";
@import "./layouts/container";
@import "./layouts/form";

@import "./pages/work";
@import "./pages/about";
@import "./pages/project";
```

# Install SASS Locally and Run
- Go to your folder with sass files.
- Initiate a `npm package.json` file. `package.json`  is a file that stores info about your project: its name, version number, author, licensing info, external dependencies, and more importantly, short snippets of code to execute! Think of `package.json` as an instruction manual for npm to use to re-assemble and run the site.  Let’s create a package file by typing  `$ npm init`.
- Install SASS: `$ npm install sass -g`

To test that you’ve got Sass installed on your system, type  `sass --version`.

Going back to the `package.json` file, you may have noticed a `"scripts"` object:
```json
{
  "name": "writting-sass",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```
This is where you’ll put your script to run Sass. 
```json
"scripts" : {
    "sass": "sass --watch ./sass/main.scss:./css/style.css"
  }
```
- `sass`  is telling npm where to look to find the script to execute.
- `--watch`  is a flag that npm uses to look for any changes in the Sass file.  If it sees a change made, it will recompile and update the CSS file. Without the watch flag, you’d have to run the script every time you hit save. With the flag, it will automatically update as long as you have the script running in your terminal window.
- `./sass/main.scss` is telling the script located in node-sass where to find the Sass file to compile.
- A colon  `:`  separates the source path from the destination path.
- `./css/style.css` tells the script where to compile the CSS to, and what to name it.

Time to **run SASS** `$ npm run sass`. `npm` tells the command line that you want to execute a `npm` command.  `run` is the command. And  `sass` is the name of the script that you want to run.

Now, as long as you don’t stop the process, either by typing `Ctrl+C` within the terminal, or clicking the trash can, **the script will wait and watch for any changes to compile**. 

**Sass has four different compile modes, each rendering the CSS in a different fashion**. The first, and default, is what you’ve just seen: **Nested** mode. The second compile mode is called **expanded**. The third mode is **compact**. It renders the CSS with one ruleset per line. The fourth and final compile mode is **compressed**. When Sass compiles the CSS sheet in compressed mode, it removes any unnecessary whitespace and line breaks. This is also known as a **minified CSS** file. Enable modes:
```json
"scripts": {
    "sass": "sass --watch ./sass/main.scss:./css/style.css --style compressed"
},
```

# SASS Lists and Maps
```css
/*css*/
.block { padding: 1rem 2rem 3rem 4rem; }
```
```scss
$padding-dimensions: 1rem 2rem 3rem 4rem; /*list*/
.block {
    padding: $padding-dimensions;
}
```
Lists allow you to group values together in a single variable.
```scss
$syntax-01: 1rem 2rem 3rem 4rem;
$syntax-02: 1rem, 2rem, 3rem, 4rem;
$syntax-03: (1rem 2rem 3rem 4rem);
$syntax-04: (1rem, 2rem, 3rem, 4rem);
```
You can use values from list individually:
```scss
$font-size: 7rem 5rem 4rem 2rem;
.form{
    font-size: nth($font-size, 4); /* use the 2rem value from $font-size */
}
```
Lists can be difficult to read and remember because there’s no real context to list contents; just values grouped together. That's why you have Sass **maps**! They are a lot like lists, but give each value a name in the form of **key/value pairs**:
```scss
$font-size: (logo:7rem, heading:5rem, project-heading:4rem, label:2rem);
.form{
    font-size: map-get($font-size, label);
}
```
**The values in maps (and lists) can be any valid Sass data type, maps included.** 
```scss
$colour-primary: #15DEA5;
$colour-secondary: #001534;
$colour-white: #fff;
$txt-input-palette: (
    active: (
        bg: $colour-primary,
        txt: $colour-white,
    ),
    focus: (
        bg: $colour-primary,
        txt: $colour-white,
    )
);
```
# Mixin and map:
```scss
@mixin txt-input-palette($state) {
    $palette: map-get($txt-input-palette, $state);
    border: .1rem solid map-get($palette, border);
    background-color: map-get($palette, bg);
    color: map-get($palette, txt);
}
.form {
    @include txt-input-palette(focus);
}
```
# Loops
```scss
@mixin txt-input-palette($palettes) {
    @each $state, $palette in $palettes{
        &:#{$state}{
            border: .1rem solid map-get($palette, border);
            background-color: map-get($palette, bg);
            color: map-get($palette, txt);
        }
    }
}
```
# Responsive with SASS
```scss
.proj-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    @media (max-width: 599px) {
        grid-template-columns: 1fr;
    }
}
```

To make things a bit more maintainable, let’s create a `$breakpoints` map to store our breakpoints in. Let’s add our mobile breakpoint value while we’re at it:
```scss
$breakpoints: (
    mobile: 599px
);
@mixin mobile-only {
    @media screen and (max-width: map-get($breakpoints, mobile)){
        grid-template-columns: 1fr;
    }
}
.proj-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    @include mobile-only;
}
```
```css
/*result css*/
.proj-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
@media screen and (max-width: 599px) {
  .proj-grid {
    grid-template-columns: 1fr;
  }
}
```