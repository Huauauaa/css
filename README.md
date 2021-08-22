# Airbnb CSS / Sass Styleguide

*A mostly reasonable approach to CSS and Sass*

*CSS and Sass 最佳实践*

## Table of Contents

1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)
1. [CSS](#css)
    - [Formatting](#formatting)
    - [Comments](#comments)
    - [OOCSS and BEM](#oocss-and-bem)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [Border](#border)
1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordering](#ordering-of-property-declarations)
    - [Variables](#variables)
    - [Mixins](#mixins)
    - [Extend directive](#extend-directive)
    - [Nested selectors](#nested-selectors)
1. [Translation](#translation)
1. [License](#license)

## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

"规则声明"是指伴随一组属性的一个（或一组）选择器。举个例子：

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

在规则声明中，“选择器” 决定 DOM 树中的元素如何被定义的属性所渲染。选择器可以匹配 HTML 元素，也可以匹配其 class、ID、属性。下面是一些选择器的例子

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

最后，属性是给被选择的元素声明样式。属性是 key-value 成对存在的，一个规则声明中可以包含一个或多个属性声明。属性声明就像这样：

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ back to top](#table-of-contents)**

## CSS

### Formatting

* Use soft tabs (2 spaces) for indentation.
* Prefer dashes over camelCasing in class names.
  - Underscores and PascalCasing are okay if you are using BEM (see [OOCSS and BEM](#oocss-and-bem) below).
* Do not use ID selectors.
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations.
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line.
* Put blank lines between rule declarations.


* 缩进使用 soft tabs （ 两个空格 ）。
* 类名用 破折号而不是驼峰
  - 如果使用 BEM (参见下面的 [OOCSS and BEM](#oocss-and-bem) )，下划线和大驼峰也是可以的
* 不要使用 ID 选择器
* 一个规则声明中，使用多个选择器时，每个选择器各占一行
* 左大括号 `{` 前面放一个空格
* 属性的冒号 `:` 后面加一个空格，前面不加
* 右大括号  `}` 放在新的一行
* 规则声明之间放一些空行

**Bad**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Good**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Comments

* Prefer line comments (`//` in Sass-land) to block comments.
* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks


* 用行注释 ( Sass 中是 `//` ) 代替块注释
* 独自一行注释。避免行末注释。
* 给不是自解释的代码添加详细的注释
  - z-index 的使用
  - 兼容或者特定浏览器的 hacks

### OOCSS and BEM

We encourage some combination of OOCSS and BEM for these reasons:

鼓励使用 OOCSS 和 BEM 的组合，因为：

  * It helps create clear, strict relationships between CSS and HTML
  * It helps us create reusable, composable components
  * It allows for less nesting and lower specificity
  * It helps in building scalable stylesheets


  * 可以创建 CSS 和 HTML 之前清晰严谨的关系
  * 可以创建可复用的、易重组的组件
  * 减少嵌套和降低耦合
  * 构建可扩展的样式表

**OOCSS**, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusable, repeatable snippets that can be used independently throughout a website.

**OOCSS**, or “Object Oriented CSS”, （面向对象的 CSS）是写 CSS 的一种方式，其鼓励你将你的样式表当成对象的集合： 在整个网站中可以被独立使用的可复用，可重用的代码段

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, or “Block-Element-Modifier”, is a _naming convention_ for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.

**BEM**, or “Block-Element-Modifier”, 是一种  HTML 和 CSS 类名的_命名约定_. 它最初由 Yandex 提出，拥有巨大的代码库和可扩展性, 被用来作为一系列遵循 OOCSS 的参考.

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

We recommend a variant of BEM with PascalCased “blocks”, which works particularly well when combined with components (e.g. React). Underscores and dashes are still used for modifiers and children.

建议搭配 PascalCased “blocks” 的 BEM 变体 , 与组件（如 React）结合时特别好用。 Underscores 和 dashes 依然被用作修改符和子节点。

**Example**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` is the “block” and represents the higher-level component
  * `.ListingCard__title` is an “element” and represents a descendant of `.ListingCard` that helps compose the block as a whole.
  * `.ListingCard--featured` is a “modifier” and represents a different state or variation on the `.ListingCard` block.

 * `.ListingCard` 是“块”，表示更高级的组件
 * `.ListingCard__title` 是一个“元素”，表示  `.ListingCard` 的后代， 用来组成“块”。
 * `.ListingCard--featured` 一个“修饰符”， 表示`.ListingCard`块的一个不同的状态或变化。

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

CSS 中按 ID 选择元素, 通常被认为是反模式的. ID 选择器为规则定义带来了不必须的高优先级的[特性](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) , 而且是不可复用的.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

想了解更多, 阅读 [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) 

### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

避免同时使用 CSS 和 JavaScript 绑定相同的类。合并两者在重构时容易导致问题, 轻者浪费时间对照寻找要修改的类名, 更糟糕的是，开发因害怕破坏功能而不敢修改代码。

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

建议在创建用于 JavaScript 的类名时，以 `.js-` 开头：

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Border

Use `0` instead of `none` to specify that a style has no border.

指定没有边框时，用 `0`代替 `none`。

**Bad**

```css
.foo {
  border: none;
}
```

**Good**

```css
.foo {
  border: 0;
}
```
**[⬆ back to top](#table-of-contents)**

## Sass

### Syntax

* Use the `.scss` syntax, never the original `.sass` syntax
* Order your regular CSS and `@include` declarations logically (see below)

* 用 `.scss` 语法，不要使用原始的 `.sass` 语法
* CSS 和 `@include`逻辑顺序 (见下文)

### Ordering of property declarations

1. Property declarations

    List all standard property declarations, anything that isn't an `@include` or a nested selector.
    列出所有不是 `@include` 或嵌套选择器的属性声明。

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector.
    分组 `@include` 在行末，使整个选择器更容易阅读

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.
    
    _如果一定要用_, 嵌套选择器放在最后，在规则声明和嵌套选择器之前添加空白。嵌套选择器也遵循此指引。

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

推荐破折号命名（如`$my-variable`）而不是驼峰或者蛇形。可以在变量名前添加下划线前缀（如`$_my-variable`），用以表示此变量只用于此文件。

### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

Mixins 可以用来 DRY 你的代码、增加清晰度或者抽象复杂度，和命名恰当的方法有异曲同工之妙。Mixins 不接收参数，但请注意，如果你不压缩 plyload(如 gzip), 可能会导致在结果样式中出现不必要的重复代码。

### Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins.

应该避免使用 `@extend`，因为它不直观并且可能有危险行为，特别是用在嵌套选择器上。即便是在顶层占位符选择器使用扩展，如果选择器的顺序最终会改变，也可能会导致问题。（比如，如果它们存在于其他文件，而加载顺序发生了变化）。其实，使用 @extend 所获得的大部分优化效果，gzip 压缩已经帮你做到了，因此你只需要通过 mixin 让样式表更符合 DRY 原则就足够了。
### Nested selectors

**Do not nest selectors more than three levels deep!**

**不要让嵌套选择器超过三层!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

When selectors become this long, you're likely writing CSS that is:
当选择器变得太长，可能是因为：

* Strongly coupled to the HTML (fragile) *—OR—*
* Overly specific (powerful) *—OR—*
* Not reusable


* 与 HTML 强耦合（易碎的）*—或者—*
* 过于具体（强大）*—或者—*
* 没有复用性

Again: **never nest ID selectors!**
再次： **不要嵌套 ID 选择器！**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

如果你必须使用 ID 选择器（尝试不要），它们不应该嵌套。如果你正这样做，你需要检查你的HTML 或者指明原因。如果你要写出良好的 HTML 和 CSS，你应该 **从不** 这样做。

**[⬆ back to top](#table-of-contents)**

## Translation

  This style guide is also available in other languages:

  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [rtplv/airbnb-css-ru](https://github.com/rtplv/airbnb-css-ru)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [tderflinger/css-styleguide](https://github.com/tderflinger/css-styleguide)

**[⬆ back to top](#table-of-contents)**

## License

(The MIT License)

Copyright (c) 2015 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
