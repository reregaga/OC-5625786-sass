[Quiz](https://openclassrooms.com/en/courses/5625786-produce-maintainable-css-with-sass/exercises/3169)
# Structure your code efficiently

## Question 1
**Which of the following selectors is a BEM modifier?**
- [ ] .block-modifier {...}
- [x] .block--modifier {...}
- [ ] .block__modifier {...}
- [ ] .block .modifier {...}

_When you name modifiers, you always use the name of the block or element that is being modified, followed by a pair of dashes, and then the manner in which you are modifying it. So, to name a modifier that turns the background of  .btn  green, you would right it as follows:  .btn--green_

## Question 2
**Some benefits of using CSS preprocessors, such as Sass, are:**
- [x] Storing often-repeated values with variables.
- [x] Creating visual hierarchies through nesting
- [x] Creating code that reacts differently depending on the circumstance with loops.
- [x] Automating repetitive CSS with logical operations.
- [ ] Providing a guideline that ensures the proper use of specificity.

_CSS preprocessors make your life easier by letting you create hierarchies in your code via nesting. They also let you store often-repeated values, such as colors, as variables, help make your code more flexible by reacting to different circumstances with logical operations, and can help save your carpal tunnels by automating the creation of repetitive code via loops._

## Question 3
**Given the following HTML:
&lt;div id="header" class=".header"&gt;
    Header Content!
&lt;/div&gt;

And CSS:
#header {
    background-color: #e0a788;
}

.header {
    background-color: #72cbd8;
}

What colour will the background of the &lt;div&gt; be?**
- [x] #e0a788
- [ ] #72cbd8
- [ ] All of the above

_The  #header  selector carries a specificity of:



Inline
ID
Class
Element


 0
1
0
0



And the .header selector carries a specificity of:



Inline
ID
Class
Element


0
0
1
0



When there are conflicting CSS properties within selectors, the browser works across the specificity table from left to right until it finds a winner. In this case, they tie in the inline column, each with a score of 0, so the browser goes to the next column, where #header wins with a score of 1 vs  .header 's score of 0, so the browser uses the background color from #header , making it #e0a788_

## Question 4
**A selector named .recipe-card falls into which BEM category?**
- [x] Block
- [ ] Element
- [ ] Modifier

_The names that you give blocks should describe that block's purpose, or role on the site, such as the contents of a recipe. To name the elements that form the block, use the name of the block, followed by a pair of underscores, and that element's role within the block. Therefore, the element for a recipe ingredient could be written as  .recipe-card__ingredient .  To modify a block or element, use the name of the block, or element, followed by a set of dashes, and the manner in which you are modifying it, such as  .recipe-card--selected .
Since the selector from the question doesn't contain any double underscores or dashes, you can tell that it is a block selector._

## Question 5
**Which of the following snippets are written with the valid  .scss  syntax?**
- [x] .block {
    background-color: #15dea5;
    div {
        margin: 1rem;
    }
}
- [ ] .block
    background-color: #15dea5
    div
        margin: 1rem
- [x] .block {
    background-color: #15dea5;
}

.block div {
    margin: 1rem;
}
- [x] .block {
    background-color: #15dea5;
    &__element{
        background-color: #de15d0;
    }
}

_The  .scss  syntax requires that you use a selector, and whatever rules you want to assign the selector to be wrapped within a set of curly braces ( { } ). You can also choose to nest other selectors within those curly braces via combinators or the ampersand, but nesting is completely optional within Sass._

## Question 6
**.block {
    &__element {
        background-color: #15dea5;
    }
}

The above Sass snippet would compile as which of the following CSS snippets?**
- [ ] .block&__element {
    background-color: #15dea5;
}
- [x] .block__element {
    background-color: #15dea5;
}
- [ ] .block .__element {
    background-color: #15dea5;
}
- [ ] .block-element {
    background-color: #15dea5;
}

_When nesting in Sass, the ampersand symbol ( & ) will be replaced with the the name of the parent when it is compiled into CSS, so the & in the question's code will be replaced with  .block  when it compiles, creating a selector named  .block__element._

## Question 7
**Sass creates a visual hierarchy through the use of:**
- [ ] Combinators
- [x] Nesting
- [ ] Loops
- [ ] Specificity

_Sass allows you to group related code and establish visual hierarchies through nesting. You can use combinators when you create nested selectors, which increase their specificity, but the hierarchy itself is created through nesting._

## Question 8
**Which Sass snippet generates the most specific CSS selector?**
- [ ] .block {
    &__element {
        color: #fff;
    }
}
- [x] .block {
    .element {
        color: #fff;
    }
}
- [ ] .block {
    &__element {
        div {
            color: #fff;
        }
    }
}
- [ ] The three snippets all generate CSS selectors with the same level of specificity.

_The selector for Answer #1 would compile as  .block__element {...}  and would have a specificity of:



0
0
1
0



The selector for Answer #2 would compile as  .block .element {...} and would have a specificity of:



0
0
2
0



The selector for Answer #3 would compile as .block__element div {...} and would have a specificity of:



0
0
1
1



Since Answer #2 has a class score of 2, vs #1 & #3's 1, it has the highest specificity of the three.
When nesting is performed without an ampersand or other CSS combinator, it will compile as a descendent combinator, as opposed to the ampersand, which concatenates the parent's name before the given name of the nested selector._

## Question 9
**Existing CSS codebases can be easily integrated into a file using Sass'  .scss  syntax because:**
- [ ] Sass turns the CSS code into  .scss  when it compiles.
- [ ] Sass doesn't have a standardized syntax.
- [x] CSS syntax is also valid  .scss  syntax.
- [ ] CSS has a vastly different syntax and doesn't easily integrate into a  .scss  file.

_Sass's  .scss  syntax is based on the standard CSS syntax. The advanced functionality that Sass provides, such as nesting, requires additional ways of formatting the code. But valid CSS is completely valid  .scss  as well._

## Question 10
**Which Sass snippet would yield the following CSS code:
.block {
    background-color: #15dea5;
}

.block__element {
    background-color: #de15d0;
}**
- [ ] .block {
    background-color: #15dea5;
    &-element {
        background-color: #de15d0;
    }
}
- [ ] .block {
    background-color: #15dea5;
    .element {
        background-color: #de15d0;
    }
}
- [ ] .block {
    background-color: #15dea5;
    __element {
        background-color: #de15d0;
    }
}
- [x] .block {
    background-color: #15dea5;
    &__element {
        background-color: #de15d0;
    }
}

_To achieve a nested selector that compiles as  .block__element   , you need to have a parent selector named .block and a child selector that uses the ampersand to join the parent's name of  .block  with the desired prefix,   __element  .
Answer #1 would compile as:
.block {
    background-color: #15dea5;
}

.block-element {
    background-color: #de15d0;
}

Answer #2 would compile as:
.block {
    background-color: #15dea5;
}

.block .element {
    background-color: #de15d0;
}

Answer #3 would compile as invalid CSS:
.block {
    background-color: #15dea5;
}

.block __element {
    background-color: #de15d0;
}

And answer #4 would compile as the code from the question:
.block {
    background-color: #15dea5;
}

.block__element {
    background-color: #de15d0;
}_

## Question 11
**The greatest danger of nesting in Sass is that:**
- [ ] It generates excessive code.
- [x] It can create overly specific selectors.
- [ ] It's impossible to use BEM while nesting.
- [ ] It generates CSS that is difficult to read.

_When you nest selectors, you can create heightened specificity. So, if you nest too deeply, you’ll end up with selectors of incredibly high specificity, making them extremely difficult to modify or override._

## Question 12
**In Sass, what does the ampersand symbol ( & ) compile to?**
- [x] The selector's parent in the hierarchy
- [ ] The adjacent sibling combinator
- [ ] The ampersand symbol ( & )
- [ ] The root selector in the hierarchy

_In Sass, the ampersand symbol compiles as the parent selector, making it easier to build and maintain complex naming structures like BEM, as well as nest pseudo-selectors like  :hover._