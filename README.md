# css-clean-structured-short
Convention for structuring stylesheets and naming selectors (and people who don't like BEM ;)  
I began to hate having these BEM-style, amazing long selectors. They waste bandwidth and contain a lot of duplication.
Especially in combination they started owning my source code. They force me to use thousands of keystrokes while
editing. They are hard to find within LESS/SCSS if ```&``` was used a lot.  
So I tried to find a balance between specificity and code amount …

TL;TR
-----
Don't select tag names - give them classes!  
Use PascalCase for your 1st level scope and camelCase for the rest!

HTML example
```html
<article class="TeaserModule -variantLarge  grid-span-all">
  <header class="header">
    <p class="Headline -tertiary">Universe on panic</p>
    <h1 class="Headline -secondary">42 not the answer to life, the universe and everything!</h1>
  </header>
  <p class="body _expanded">
    Further studies revealed: 42 is not the answer to life, the universe and everything. It's 43!
    Someone made a off by one error within the calculation algorithm.
  </p>
  <a class="Link -arrowRight" href="article.html">Read more</a>
</article>
```

Structure
-----
We will define **primary selectors** (1st level scope) and **secondary selectors** (2nd level scope).  
Primary selectors are written in **PascalCase** and grouped into …

- **elements**  
  Uncomplex compounds like headlines, buttons, pictures with icons or action buttons.
- **components**  
  Less complex compounds without own context like article footers, form fields (including label & input)  
  May contain elements & components & secondary (custom) elements.
- **modules**  
  Complex compounds with own context.  
  May contain elements & components & secondary (custom) elements

Secondary selectors are written in **camelCase**.
Global helpers (e.g. grid classes) will also use **camelCase**.

```css
.PrimarySelector {}
.PrimarySelector .secondarySelector {}

```

Naming schema
-----

HTML:
```html
<div class="ComponentName -variantName _stateName"></div>
```
CSS:
```css
.ComponentName.-variantName._stateName {}
```

General Naming
-----
    .fooBar                    Foobar class
    .fooBar.-variant           Foobar class inheriting from .fooBar but with modifications
    .fooBar.-n-2               Foobar class inheriting from .fooBar but with counter as a helper selector
    .fooBar._collapsed         Foobar class in collapsed state
    .fooBar._active            Foobar class in active state
    #fooBar.-variant._active   Same rules for IDs
    #fooBar-variant_active     Similar rules for special IDs


Modules/Components/Elements Naming
----------------------------------
    .FooBar                    Foobar module/component
    .FooBar.-variant           Foobar module/component variant inheriting from .FooBar but with some different styles
    .LargeFooBar               Foobar module/component which is too different from .FooBar to use inheritance
    .FooBar .Headline          Headline of .FooBar using inheritance from global headline component
    .FooBar .headline          Headline of .FooBar without any inheritance
    #FooBar.-variant           Same rules for IDs
    #FooBar-variant_active     Similar rules for special IDs


Body-Switches
-------------
    .ifFooBarPresent_hide       Hide this element if HTML-Element has class "fooBarPresent"
    .ifFooBarError_show         Show this element if HTML-Element has class "fooBarError" (display: initial)
    .ifFooBarError_showInline   Show this element if HTML-Element has class "fooBarError" (display: inline)
    .ifFooBarError_showBlock    Show this element if HTML-Element has class "fooBarError" (display: block)


JS-Selectors
------------
Please use own selectors for JS so your scripts will never crash,
when layout is modified, classes renamed or moved etc.
You can use normal selectors if they can be configured inline with HTML.

    jsFoobar                   For selecting an element to handle with Foobar function/Plugin
    jsFoobarButtons


Order of things
---------------
Due to cascading/inheritance keep order of classes here like DOM-Tree.
- single/standalone elements (need default formattings, so keep them first)
- outer blocks (may contain same classes as their inner blocks …)
- inner blocks (… so to raise priority of latter blocks define them at the end)
