[Quiz](https://openclassrooms.com/en/courses/5625786-produce-maintainable-css-with-sass/exercises/3799)
# Create efficient, maintainable code with intermediate Sass techniques

## Question 1
**.btn{
   color: &num;0c2461;
   font-size: 2rem;
}
.article{
   color: &num;0c2461;
   background-color: &num;fff;
}

If you want to refactor the code above, and for this you want to store the color  &num;0c2461  in a variable so that you can reuse it several times in your code, how will you change the code?**
- [ ] $blue = &num;0c2461;
- [ ] $colour = b;
- [ ] pink = $&num;0c2461;
- [x] $blue: &num;0c2461;

_The variables enable the storing of values so that they can be reused anywhere in the code. In order to declare a variable:  $name_of_the_variable: value;
In our case, the correct answer is 4: $blue: &num;0c2461;_

## Question 2
**$blue-border: border: solid 5px &num;0c2461;

Starting from the code above, what happens if I declare a variable like this to store border and apply it to a .btn selector?**
- [x] A compilation error
- [ ] The button will have a blue border
- [ ] The button will not have a border

_The variables enable the storing of values, but not of sets of rules. The code will not work and will trigger an error. It is however possible to store the values of the border property as follows:
$blue-border: solid 5px &num;0c2461;_

## Question 3
**Using the code from the previous exercise:
$blue-border: border: solid 5px &num;0c2461;

If you create the appropriate mixin to contain the border and you call it blue-border, what would be considered good writing among the following?**
- [ ] $blue-border: border: solid 5px &num;0c2461;
- [ ] @mixin $blue-border: border: solid 5px &num;0c2461;
- [x] @mixin blue-border {
  border: solid 5px &num;0c2461;
}
- [ ] @mixin $blue-border {
  border: solid 5px &num;0c2461;
}

_In order to declare a mixin, it needs to be in the following form:
@mixin mixin-name {
  css-property: value;
}

 The first two answers will give you a compilation error; this syntax is not valid.
Answer 4 has an extra $. We declare that the name of a variable with the symbol $, for a mixin  @mixin  + the name of the mixin, is enough. So 3 is the correct answer._

## Question 4
**You have created your blue-border mixin. It is time to use it in your selectors. If you were to use your new mixin in the following class selector:
.article {
display: flex;
padding: 5px 10px;
color: black;
background-color: $white;
// write your code here
}

 What form would it take?**
- [ ] @include $blue-border;
- [ ] @mixin blue-border;
- [x] @include blue-border;
- [ ] @extend %blue-border;

_In order to use a mixin, you have to include it in this way:  @include + name_of_the_mixin.
The first can not work because there is a $ in front of the blue-border. Overview: An $ enables the declaring of a variable.
Answer 2 will not work because  @mixin is used to declare a mixin and not to use it.
Finally, @extend% blue-border  ;  is correct in terms of syntax, but it serves to use a placeholder and not a mixin._

## Question 5
**What is the difference between mixins and extensions?**
- [ ] There is no difference
- [ ] Mixins duplicate selectors and extensions duplicate rules
- [x] Mixins duplicate rules and extensions duplicate selectors

_The main difference between mixins and extensions is that with mixins you get duplicate rules, while with extensions you get duplicate selectors._

## Question 6
**If you had to name a placeholder to replace the .content-color class selector, how would you do it?**
- [ ] $content-colour
- [x] %content-colour
- [ ] .content-colour
- [ ] &content-colour

_To name a placeholder, you need to type the % symbol followed by the placeholder name. In our case,  %content-color._

## Question 7
**.content-colour {
  color: blue;
  font-size: 2rem;
}
h1 {
  @extend .content-colour;
}
textarea {
  @extend .content-colour;
}

Using the code above as a starting point, how will you compile your code?**
- [ ] textarea {
 color: blue;
 font-size: 2rem;
}
- [ ] .content-colour {
 color: blue;
 font-size: 2rem;
}
- [ ] .content-colour {
 color: blue;
 font-size: 2rem;
}

h1 {
 color: blue;
 font-size: 2rem;
}

textarea {
 color: blue;
 font-size: 2rem;
}
- [x] .content-colour, h1, textarea {
 color: blue;
 font-size: 2rem;
}

_Remember, extensions provide duplicate selectors. Answers 1 and 2 apply the result to a single selector, without extensions.
Answer 3 shows that when the rules have been duplicated, this would rather be the result of a mixin.
The correct answer is 4._

## Question 8
**.btn {
  border: 5px solid blue;
}

What would be considered an appropriate mixin to get the result compiled above?**
- [ ] mixin border-colour {
  border: 5px solid blue;
}
- [x] @mixin border-colour {   
  border: 5px solid blue;
}
- [ ] @include border-colour {
  border: 5px solid blue;
}

_A mixin can be declared in the following way:
@mixin mixin-name {
  css-property: value;
}

The first answer has no @ before the mixin and it will not compile; you will get an error. The third answer does have an @ but is followed by include; @include is used to call the mixin in your selector and not to declare it. In our case, if we had to use our mixin, it would give a result similar to this:
.btn {
  @include border-colour;
}

The correct answer is 2!_

## Question 9
**$white: &num;fff;
$pastel-blue: &num;0097e6;
$dark-blue: &num;192a56;

@mixin border-colour($colour){
  @if ( lightness($colour) &gt; 25% ) {
      $colour: darken($colour, 30%);
  } @else {
      $colour: lighten($colour, 30%);
  }

  border: 5px solid $colour;
}

.article {
  display: flex;
  padding: 5px 10px;
  color: black;
  background-color: $white;

  @include border-colour($dark-blue);
}

&lt;div class="article"&gt;Read me!&lt;/div&gt;

Using the code above as a starting point, what color will the border of .article be if you replace $dark-blue with $pastel-blue?**
- [ ] White
- [ ] Black
- [x] Dark blue
- [ ] Light blue

_Let's take all the code of our mixin into consideration: If the brightness of the color that is considered a parameter is less than 25%, then we have to darken it by 30%; otherwise, we need to lighten it by 30%. If we take light blue as a parameter, the brightness will be greater than 25%, so we need to darken it and the mixin will apply these changes directly in the  border._

## Question 10
**$white: &num;fff;
$pastel-blue: &num;0097e6;
$text-color: &num;192a56;

@function background($text-color) {
  @if ( $text-color == $white ) {
      @return $pastel-blue;
  } @else {
      @return $white;
  }
}

.btn {
  color: $text-color;
  background-color: background($text-color);
}

Using the code above as a starting point, what would be the  background-color  of  .btn?**
- [ ] None, there will be a syntax error
- [ ] &num;0097e6
- [x] &num;fff
- [ ] &num;192a56

_The function applied to background-color indicates that if $text-color  (the color of the text) is the same as the one of the $white  variable (&num;fff, which is white), then the return value is $pastel-blue (pastel blue). In addition, if the  text color is not white, the return value will be $white  .
In this case, our text color is not white, but dark blue (  &num;192a56  ), so the return value of the function will be $white  !
We indicate in our CSS that the result ofbackground($text-color) will be the color of the background, which is white here._