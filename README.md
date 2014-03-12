
#XM RMD CSS Guide
Version:        1.0
Author:         Leon Ng
Last Updated:   Feb 2014



#####--------------------- NOTE: IE Browsers limitations ---------------------
* IE 6 - 9 - 4096 rule limit: 4096 selectors limit per CSS file
* IE 6 - 9 browsers may @import up to 31 CSS files
* IE 6 - 9 browsers @import nesting supports up to 4 levels deep

|Browser | HTTP/1.1 | HTTP/1.0 |
|----------------------|------------|------------|
|IE 6,7                | 2 | 4 |
|IE 8                  | 6 | 6 |
|Firefox 2             | 2 | 8 |
|Firefox 3             | 6 | 6 |
|Safari 3,4            | 4 | 4 |
|Chrome 1,2            | 6 | ? |
|Chrome 3              | 4 | 4 |
|Chrome 4+             | 6 | ? |
|iPhone 2              | 4 | ? |
|iPhone 3              | 6 | ? |
|iPhone 4              | 4 | ? |
|Opera 9.63,10.00alpha | 4 | 4 |
|Opera 10.51+          | 8 | ? |

The above shows how many CSS files are currently loaded at a time for different browsers.
How many CSS files should be loaded on any websites?

    1. one, two, or three ( ref: http://css-tricks.com/one-two-three/ )
    2. As little as possible, less then 20

Keep multiple files during development, and lesser files for deployment



##1 - Table of Contents
----
This will allow the developer(s) to know exactly what they to find in this CSS file.
Each item in the table of contents maps directly to a section.
This is a subjective point, good for bigger projects.

The **\$** prefixing the name of the section allows us to run a find **([Cmd|Ctrl]+F)** for **$[SECTION-NAME]** and limit our search scope to section titles only.

<pre><code>/*  -----------------------------------------------------
    $CONTENTS
    -----------------------------------------------------   */
/**
    * CONTENTS ..........................................
    * RESET .............................................
    * Module ............................................
    * Layout ............................................
    * Theme .............................................
*/
</code></pre>

##2 - CSS Files Source Order
----
1. Base / Reset – ground zero. They are almost exclusively single element selectors but it could include attribute selectors, pseudo-class selectors, child selectors or sibling selectors.
2. Layout – divide the page into sections. Layouts hold one or more modules together..
3. Module — the reusable, modular parts of our design. They are the callouts, the sidebar sections, the product lists and so on.
4. State – are ways to describe how our modules or layouts will look when in a particular state. Is it hidden or expanded? Is it active or inactive? They are about describing how a module or layout looks on screens that are smaller or bigger.
5. Theme – are similar to state rules in that they describe how modules or layouts might look.
    
Reference: [Jonathan Snook’s SMACSS](http://smacss.com/book/categorizing)
    


##3 - CSS Format
----
Reference from: [Idiomatic-css](https://github.com/necolas/idiomatic-css)

####3.1 - Use one discrete selector per line in multi-selector rulesets.
<pre><code>/*  --- Correct --- */
.selector-day:hover,
.selector-month:hover,
.selector-fullyear:hover,
.selector-year:hover{
    color: #7EA0E2;
}

/*  --- Wrong --- */
.selector-day:hover, .selector-month:hover, .selector-fullyear:hover, .selector-year:hover{
    color: #7EA0E2;
}
</code></pre>

####3.2 - Include a single space before the opening brace of a ruleset.
<pre><code>/*  --- Correct --- */
div.selector {
    margin: 10px 0 30px;
}

/*  --- Wrong --- */
div.selector{
    margin: 10px 0 30px;
}
</code></pre>

####3.3 - Include one declaration per line in a declaration block.
<pre><code>/* --- Correct --- */
div.selector {
    clear: both;
    padding: 20px;
    margin: 0 0 10px;
    text-align: left;
}

/*  --- Wrong --- */
div.selector {
    clear: both; padding: 20px; margin: 0 0 10px; text-align: left;
}
</code></pre>

####3.4 - Include a single space after the colon of a declaration.
<pre><code>/*  --- Correct --- */
.selector {
    display: block;
    margin-top: 15px;
}

/*  --- Wrong --- */
.selector {
    display:block;
    margin-top:15px;
}
</code></pre>

####3.5 - Use lowercase and shorthand hex values, e.g., #aaa.
<pre><code>/*  --- Correct --- */
.selector {
    color: #ddd;
    margin: 1em 0 2em 1em;
}

/*  --- Wrong --- */
.selector {
    color: #DDD;
    margin-top: 1em;
    margin-right: 0;
    margin-bottom: 2em;
    margin-left: 1em;
}

.selector {
    color: #DDDDDD;
}

</code></pre>

####3.6 - Use single or double quotes consistently. Preference is for double quotes, e.g., content: "".
<pre><code>.selector {
    content: "\e008";
}
</code></pre>

####3.7 - Quote attribute values in selectors, e.g., input[type="checkbox"].
<pre><code>.selector[type="text"]{
    border: 1px solid $pp-border-color;
    background-color: $pp-textfield-bg;
    color: $pp-text-color;
}
</code></pre>

####3.8 - Where allowed, avoid specifying units for zero-values, e.g., margin: 0.
<pre><code>/*  --- Correct --- */
.selector {
    display: block;
    margin-bottom: 0;
    padding: 0;
}

/*  --- Wrong --- */
.selector {
    display: block;
    margin-bottom: 0px;
    padding: 0px;
}
</code></pre>

####3.9 - Include a space after each comma in comma-separated property or function values.
####3.10 - Include a semi-colon at the end of the last declaration in a declaration block.
####3.11 - Place the closing brace of a ruleset in the same column as the first character of the ruleset.
####3.12 - Separate each ruleset by a blank line.
####3.13 - Magic numbers and absolutes
A magic number is a number which is used because it works to fix or align your styles to what you need.
These are bad, especially for responsive or fiuld layout, where they tend to fix symptoms but not problems. (Especially for IE browsers )

<pre>
For example, using .dropdown-nav li:hover ul { top: 37px; } to move a dropdown to the bottom of the nav on hover is bad, as 37px is a magic number. 37px only works here because in this particular scenario the .dropdown-nav happens to be 37px tall.

Instead you should use .dropdown-nav li:hover ul { top: 100%; } which means no matter how tall the .dropdown-nav gets, the dropdown will always sit 100% from the top.
</pre>

Everytime when you need to place a number, consider if it can be avoided or controlled by other elements instead of using a magic number. 

"Every hard-coded measurement you set is a commitment you might not necessarily want to keep."

####3.14 - 4 space tab indented ( configure in your IDE )
<pre><code>/*  --- Correct --- */
.bx-selector {
    left: 10px;
    @include spritebg($common-sprite-sheet, 30px, 29px, 0px, -1091px);
}

/*  --- Wrong --- */
.bx-selector {
    left: 10px
    @include spritebg($common-sprite-sheet,30px,29px,0px,-1091px)
    }
</code></pre>

####3.15 - Large blocks of single declarations can use a slightly different, single-line format.
In this case, a space should be included after the opening brace and before the closing brace.
<pre><code>/*  --- Example --- */
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
</code></pre>

####3.16 - Long, comma-separated property values - such as collections of gradients or shadows
Can be arranged across multiple lines in an effort to improve readability and produce more useful diffs.
<pre><code>/*  --- Example --- */
.selector {
    background:
        url('select2-spinner.gif') no-repeat 100%,
        -webkit-gradient(
            linear,
            left bottom,
            left top,
            color-stop(0.85, white),
        color-stop(0.99, #eeeeee));

    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
</code></pre>

####3.17 - OOCSS
When building a new component write markup before CSS.
This means you can visually see which CSS properties are naturally inherited and thus avoid reapplying redundant styles.
By writing markup first you can focus on data, content and semantics and then apply only the relevant classes and CSS afterwards.
[Reference link](https://github.com/csswizardry/CSS-Guidelines)

#####3.17.1 - Separate structure and skin
This means to define repeating visual features (like background and border styles)
as separate “skins” that you can mix-and-match with your various objects to achieve a large amount of visual variety without much code.
<pre><code>/*  --- Example --- */
.room {}

.room--kitchen {}
.room--bedroom {}
.room--bathroom {}
</code></pre>

#####3.17.2 - Separate container and content
Essentially, this means “rarely use location-dependent styles”. 
An object should look the same no matter where you put it.
So instead of styling a specific `<h2>` with .myObject h2 {...}, create and apply a class that describes the `<h2>` in question, like `<h2 class="category">`.

<pre><code>/*  --- Correct --- */
.category{
    font-weight: bold;
}

/*  --- Wrong --- */
.selector h2.category{
    font-weight: bold;
}
</code></pre>

####3.18 - For large stylesheet, leave five (5) carriage returns between each section
This large chunk of whitespace is quickly noticeable when scrolling quickly through larger files.
<pre><code>/*  -----------------------------------------------------
    $RESET
    -----------------------------------------------------   */
    .selector{
        some styles
    }





/*  -----------------------------------------------------
    $TYPOGRAPHY
    -----------------------------------------------------   */





</code></pre>

#####Other options:
Some uses 3 carriage returns instead.
Some uses the "START" & "END" comments:

<pre><code>/*  ----- Content Styles - START -----  */
    .selector{
        some styles
    }
/*  ----- Content Styles - END -----  */
</code></pre>

####3.19 - Using Classes instead of IDs.
Not implying that do not use CSS IDs at all, rather use them wisely.
There is nothing wrong with using all classes, or a mix of IDs & classes.
More to reusing existing styles for unqiue elements, thus there's no need for styling a ID. 

Furthermore the ID syntax # is also used in Jquery, which we can use ID as a form of indication that a script is binded to it. 

[Reference Link 1:](http://oli.jp/2011/ids/)
[Reference Link 2:](http://css-tricks.com/why-use-classes-or-ids-on-the-html-element/)
[Reference Link 3:](http://screwlewse.com/2010/07/dont-use-id-selectors-in-css/)


####3.20 - !important
Using `!important` on helper classes makes sense. To add `!important` preemptively is fine, e.g. .error { color: red !important }, as you know you will always want this rule to take precedence.

Do not use `!important` just for fast fix/overwite of existing styles.
Examine your existing styles and try to refactor your selectors instead. 



##4 - Declaration order
----
I've break Typography out as one group. [Reference link](https://github.com/necolas/idiomatic-css)

####4.1 - Always place @extend statements on the first lines of a declaration block.
####4.2 - Where possible, group @include statements at the top of a declaration block, after any @extend statements.
####4.3 - Limit nesting to 1 level deep. Reassess any nesting more than 2 levels deep. This prevents overly-specific CSS selectors.
####4.4 - Avoid large numbers of nested rules. Break them up when readability starts to be affected. Preference to avoid nesting that spreads over more than 20 lines.
<pre><code>.other-rule{}
.selector {
    /* --- @extend & @include statements always on top --- */
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);

    /* --- Display & Box Model --- */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    /* --- Positioning --- */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* --- Typography --- */
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;

    /* --- Others --- */
    background: #000;
    cursor: default;
}
</code></pre>



##5 - Naming Rules
----
Use lowercase & hyphen delimited class names (Should we use BEM notation, see [here](https://github.com/csswizardry/CSS-Guidelines#naming-conventions))
Sass mixins should use camelCase for their names, e.g: borderRadiusIdentical

[Reference link 1](http://thesassway.com/advanced/modular-css-naming-conventions)
[Reference link 2](https://github.com/csswizardry/CSS-Guidelines#naming-conventions)

[SMURF: Scalable, Modular, reUsable Rails Frontends](http://railslove.com/blog/2012/11/09/taking-sass-to-the-next-level-with-smurf-and-extend)

####5.1 - Learning to think in Objects (Think of your CSS as objects / modules)
    Objects are small little chunks of functionality. You can think of them as interface elements like headers, footers, buttons, and content areas.

####5.2 - Parent-Child relationships
<pre><code>/*  --- Example --- */
// Posts
.post {
    margin: 2em 0;
}

.post-title {
    font-size: 2em;
    font-weight: normal;
}
</code></pre>

####5.3 - Another pattern - Plural Parent Pattern
It's especially handy for a set of objects and their container.
<pre><code>/*  --- Example --- */
.tabs {
    border-bottom: 1px solid silver;
    text-align: center;
}

.tab {
    background: #e5e5e5;
    border: 1px solid silver;
    @include border-top-radius(3px);
    color: #666;
    display: inline-block;
    padding: 7px 18px 7px;
    text-decoration: none;
    position: relative;
    top: 1px;
}
</code></pre>

####5.4 - Subclassing objects
Most object-oriented systems have another concept for declaring that an object is a kind of another object.
<pre><code>/*  --- Example --- */
.button {
    background: linear-gradient(#eee, #ddd);
    border: 1px solid #999;
    @include border-radius(5px);
    color: #666;
    cursor: pointer;
    padding: 4px 10px 5px;

    &:hover {
        background: linear-gradient(#fff, #eee);
        color: #111;
    }
}

.dropdown-button {
    &::after { content: " \25BE"; }
}
</code></pre>

HTML codes:
`<button class="button dropdown-button">Dropdown</button>`


#####5.4.1 - If you prefer to only use one class in your markup, you can use the Sass @extend directive, as shown in the example below:
<pre><code>/*  --- Example --- */
.dropdown-button {
    @extend .button;
    &::after { content: " \25BE"; }
}
</code></pre>


####5.5 - Using modifiers
A modifier can be used to indicate that the object is in a certain state or to make small modifications on existing behavior.
<pre><code>/*  --- Example --- */
.tab {
    background: #e5e5e5;
    border: 1px solid silver;
    @include border-top-radius(3px);
    color: #666;
    display: inline-block;
    padding: 7px 18px 7px;
    text-decoration: none;
    position: relative;
    top: 1px;

    &.is-selected {
        background: white;
        border-bottom-color: white;
        color: #333;
    }
}

.textbox {
    font: 13px sans-serif;
    border: 1px solid #ccc;
    border-top: 1px solid #999;
    border-radius: 2px;
    padding: 2px 4px;

    &:focus { outline: none; border: 1px solid #69e; }

    &.large { font-size: 18px; }
    &.small { font-size: 11px; padding: 1px 2px; }
}
</code></pre>

#####5.5.1 - global modifier (Similar to helper Class)
There are times when it makes perfect sense to make a modifer a global modifier. Here are a couple of examples:
<pre><code>/*  --- Example --- */
.clearfix { @include clearfix; }

.is-hidden    { display:    none !important; }
.is-invisible { visibility: none !important; }

.block        { display: block        !important; }
.inline       { display: inline       !important; }
.inline-block { display: inline-block !important; }

.left  { float: left  !important; }
.right { float: right !important; }

.text-left   { text-align: left   !important; }
.text-center { text-align: center !important; }
.text-right  { text-align: right  !important; }

.mt0 { margin-top:    0   !important; }
.mt1 { margin-top:    1em !important; }
.mb0 { margin-bottom: 0   !important; }
.mb1 { margin-bottom: 1em !important; }
</code></pre>

####5.6 - JS hooks
If you need to bind to some markup use a JS specific CSS class. This is simply a class namespaced with .js-, e.g. .js-toggle, .js-drag-and-drop.
Makes it easier to debug and identify JS issues as well.

HTML codes:
`<th class="is-sortable  js-is-sortable"></th>`


####5.7 - Quasi-qualified selectors

---- *** This seems to apply to CSS only, using SASS defeats the point to follow this rule ----
We should never write qualified selectors, for example: ul.nav {} if you can just have .nav.
Qualifying selectors decreases selector performance, inhibits the potential for reusing a class on a different type of element
and it increases the selector’s specificity. These are all things that should be avoided at all costs.

However, sometimes it is useful to communicate to the next developer(s) where you intend a class to be used.
Let’s take .product-page for example;
this class sounds as though it would be used on a high-level container, perhaps the html or body element,
but with .product-page alone it is impossible to tell.

By quasi-qualifying this selector (i.e. commenting out the leading type selector) we can communicate where we wish to have this class applied, thus:
<pre><code>/*  --- Example --- */
/*html*/.product-page {}
/*ol*/.breadcrumb {}
/*p*/.intro {}
/*ul*/.image-thumbs {}
</code></pre>

###Other notes:
----
Descendant selectors (qualified selectors) are inefficient because, for each element that matches the key, the browser must also traverse up the DOM tree, evaluating every ancestor element until it finds a match or reaches the root element.
The less specific the key, the greater the number of nodes that need to be evaluated.

The :hover pseudo-selector on non-anchor elements is known to make IE7 and IE8 slow in some cases*.
When a strict doctype is not used, IE7 and IE8 will ignore :hover on any element other than anchors.
When a strict doctype is used, :hover on non-anchors may cause performance degradation.

[Reference Link](https://developers.google.com/speed/docs/best-practices/rendering?csw=1#UseEfficientCSSSelectors)
