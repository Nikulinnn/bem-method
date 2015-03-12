# Вы спрашиваете, мы отвечаем

## Почему для хранения информации об именах блоков в БЭМ-методологии используются именно CSS-классы?

В ответе пойдем от обратного:

**Почему не используем ID**

Привязка к ID подразумевает уникальность блока на странице. Изначально в БЭМ пробовали использовать ID. Для блоков (например, формы поиска) запись была примерно следующей:

**HTML**

```html
<div id="search"> ... </div>
```

**CSS**

```css
#search { ... }
```

Потом стало понятно, что хочется иметь возможность использовать повторно любой блок, даже, казалось бы, уникальный для страницы (нпример, шапку) блоки могут повторяться на странице. И при этом хотелось делать как можно меньше изменений в коде. Так, например, форма поиска однажды появлялась внизу выдачи, чтобы было удобнее перезадавать запрос по прочтении результатов. И мы приняли решение, всегда использовать классы, чтобы лишний раз не менять CSS, если блок будет повторяться:
HTML:
<div class="search"> ... верхняя форма поиска ... </div>
...
<div class="search"> ... нижняя форма поиска ... </div>

CSS:
.search { ... }



## Why do I need CSS classes for block instead of using semantic custom tags?

Blocks can be represented as custom tags which we may define CSS rules for. Looks like we do not need CSS classes for blocks at all. They can be used for modifiers only, like <button class="mod"/>.
Using custom tags as block selectors is indeed one of the BEMish solutions and can be used. However this variant is less flexible than the recommended "class" approach.

This is more likely that you would need to prefix modifier classes with their block name to provide them namespace. The details are uncovered in "Why the modifier CSS classes are prefixed with their parent block name?" question. So, finally the custom-tag version of a block is like <block class="block_mod"/>. This does not look very different from <div class="block block_mod"> especially assuming that being tag-independent you can use any custom node and stay with <block class="block block_mod">.

Second drawback is that "tag" version makes using the mixes of blocks impossible whereas the "class" version represent that naturally by <div class="block1 block2">.

And the last clench against such an approach is that in many cases you are not able to represent your blocks with custom tags at all. For a link block you definitely need <a> tag, and the same for <input>.

Why do I need to combine block and prefixed modifier class for a modified block?
Why does both block's and modifier's class sit together in the modified block like <div class=”block block_mod”>? Everything about a modified block can be decribed in .block_mod. If there is something common between 2 modifiers, it's possible to use preprocessor's mixins to avoid copy-paste.
This approach is possible thanks to preprocessors. However it brings some drawbacks which you should be aware of.

In case of combining 2 or more modifiers at the same block <div class="block_theme_christmas block_size_big"> you would get the core block's styles twice. However this depends on the preprocessor algorythms.

When operating modifiers dynamically with JavaScript, additional modifier is more handy. Switching it off would mean only removing one CSS class from the DOM node with no need to add the core block CSS class back as it sits there forever.


Изначально были id-шники, и для блоков (например, формы поиска) мы писали как-то так:
HTML:
<div id="search"> ... </div>

CSS:
#search { ... }


Потом мы поняли, что блоки могут повторяться на странице и нам хочется как можно меньше делать изменений при этом. Так например форма поиска однажды появлялась внизу выдачи, чтобы было удобнее перезадавать запрос по прочтении результатов. И мы приняли решение, всегда использовать классы, чтобы лишний раз не менять css, если блок будет повторяться:
HTML:
<div class="search"> ... верхняя форма поиска ... </div>
...
<div class="search"> ... нижняя форма поиска ... </div>

CSS:
.search { ... }

