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
![alt text](../img/block-element.jpg)