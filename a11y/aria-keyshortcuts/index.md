---
title: "`aria-keyshortcuts`"
description: "Как рассказать пользователю вспомогательной технологии о вашем сочетании клавиш."
authors:
  - tatianafokina
related:
  - a11y/aria-intro
  - a11y/aria-attrs
  - js/element-addeventlistener
tags:
  - doka
---

## Кратко

[Глобальное свойство](/a11y/aria-attrs/) из [WAI-ARIA](/a11y/aria-intro/) для описания горячих клавиш, с помощью которых можно выполнить команду или сделать фокус на элементе.

<aside>

🚧 Атрибут `aria-keyshortcuts` пока не поддерживается в Firefox и никогда не работал в Internet Explorer.

</aside>

## Пример

```html
<button aria-keyshortcuts="Shift+F">
  Развернуть
</button>
```

<iframe title="Клавиатурное сокращение для кнопки" src="demos/button-with-shortcut/" height="210"></iframe>

Скринридер прочтёт код примерно так: «Развернуть, кнопка. Shift плюс F».

## Как пишется

Добавьте к тегу атрибут `aria-keyshortcuts` с нужным сочетанием клавиш в виде строки текста. `aria-keyshortcuts` можно использовать для всех тегов и ролей, кроме элементов с атрибутами [`disabled`](/html/disabled/) или [`aria-disabled`](/a11y/aria-disabled/).

Лучше добавлять сочетания клавиш для элементов, с которыми взаимодействуют пользователи. Например, для кнопок паузы, воспроизведения или включения субтитров в плеере, якорных ссылок и похожих элементов.

Названия клавиш из одного сочетания разделяйте знаком плюс — `+`.

```html
<button aria-keyshortcuts="Shift+D">Загрузить документ</button>
```

В сочетании на первом месте должны стоять [клавиши-модификаторы](https://www.w3.org/TR/uievents-key/#keys-modifier). Например <kbd>Alt</kbd>, <kbd>Shift</kbd> или <kbd>Control</kbd>. Их нельзя использовать без других клавиш с буквами, цифрами или знаками.

```html
<!-- ⛔ Неправильные сочетания клавиш -->
<button aria-keyshortcuts="S+Alt+Shift">Покричать в лесу</button>
<button aria-keyshortcuts="Alt">Покричать в лесу</button>

<!-- ✅ Правильные сочетания клавиш -->
<button aria-keyshortcuts="Alt+Shift+S">Покричать в лесу</button>
<button aria-keyshortcuts="Shift+Alt+S">Покричать в лесу</button>
```

Буквы в сочетаниях могут быть маленькими и большими.

```html
<!-- ✅ Оба варианта правильные -->
<button aria-keyshortcuts="Alt+Shift+s">Покричать в лесу</button>
<button aria-keyshortcuts="Shift+E">Покричать про себя</button>
```

Когда указываете несколько сочетаний горячих клавиш, разделяйте их пробелами.

```html
<button aria-keyshortcuts="Alt+Ctrl+S Shift+ArrowDown">Скачать файл</button>
```

Если используете знак, замените его на соответствующую цифру с клавиши. Например, вместо <kbd>%</kbd> укажите <kbd>5</kbd>.

```html
<a href="#main" aria-keyshortcuts="Alt+5">К основному содержимому</a>
```

Когда нужен знак с клавиши без цифры, лучше использовать [символ-мнемонику (HTML entity)](https://www.freeformatter.com/html-entities.html). Например, вместо апострофа указать `&#39;`.

```html
<a href="#main" aria-keyshortcuts="Alt+&#39;">К основному содержимому</a>
```

Список стандартных значений клавиш найдёте в [спецификации UI Events KeyboardEvent](https://www.w3.org/TR/uievents-key/).

Не забывайте слушать нажатия на клавиши с помощью [`.addEventListener()`](/js/element-addeventlistener/). Благодаря `aria-keyshortcuts` пользователи [скринридеров](/a11y/screenreaders/) узнают, что с элементом можно взаимодействовать как-то ещё. Атрибут не добавляет нужную функциональность.

Несколько важных правил при работе с `aria-keyshortcuts`:

- Не перезаписывайте сочетания клавиш, которые уже есть в браузерах, вспомогательных технологиях и операционных системах. Например, <kbd>Ctrl C</kbd> копирует выделенный текст.
- Учитывайте особенности раскладок и языков. Например, во французской раскладке нужно зажать <kbd>Shift</kbd> и нужную клавишу с цифрой, чтобы ввести число.
- Лучше рассказывать о горячих клавишах всем людям, не только пользователям вспомогательных технологий. К примеру, в тексте на странице или во всплывающей подсказке.
- Не используйте много сочетаний клавиш, это только усложнит взаимодействие с элементами на странице.

Подробнее про выбор горячих клавиш узнаете из [Developing a Keyboard Interface](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/).

## Как понять

Сочетание клавиш, горячие клавиши или шорткат — это способ выполнения команды, когда для неё зажимают одну или нескольких клавиш на клавиатуре.

Горячие клавиши ускоряют работу пользователей клавиатуры и даже тех, кто в основном пользуется мышкой и другими указателями.

`aria-keyshortcuts` пригодится в случаях, когда нужно рассказать пользователям вспомогательных технологий о том, что они могут взаимодействовать с элементом с помощью определённого сочетания клавиш. К примеру, видео часто разворачивается на весь экран при нажатии на <kbd>F</kbd>.

## Подсказки

💡 `aria-keyshortcuts` похож на HTML-атрибут `accesskey`, но поддержка ARIA-атрибута лучше, а поведение более предсказуемое и не отличается в зависимости от браузера.
