---
title: "`:user-invalid`, `:user-valid`"
description: "Ненавязчиво валидируем форму с помощью CSS."
authors:
  - fpetrakov
keywords:
  - invalid
  - user-invalid
  - valid
  - user-valid
  - валидация
  - форма
  - филдсет
related:
  - html/form
tags:
  - doka
---

## Кратко

Псевдоклассы помогают стилизовать [`<input>`](/html/input), [`<textarea>`](/html/textarea/) или [`<select>`](/html/select/):

- `:user-valid` для допустимого значения;
- `:user-invalid` для недопустимого значения.

В отличии от [`:invalid`](/css/invalid-valid/) и [`:valid`](/css/invalid-valid/), эти псевдоклассы срабатывают только если пользователь повзаимодействовал с элементом ввода, а затем перешел к другому элементу (сменил фокус).

## Пример

```html
<form>
  <label>
    Имя:
    <input type="text" name="name" autocomplete="name" />
  </label>
  <label>
    Почта:
    <input type="email" name="email" autocomplete="email" required />
  </label>
  <label>
    <input type="checkbox" name="agree" required />
    В целом я с вами согласен
  </label>
  <button>Отправить</button>
</form>
```

```css
input:user-invalid {
  border: 2px solid oklch(62.5% 0.2 30);
}

input:user-valid {
  border: 2px solid oklch(62.5% 0.2 144);
}

[type="checkbox"]:user-invalid {
  outline: 2px solid oklch(62.5% 0.2 30);
  outline-offset: 2px;
}
```

## Как понять

Часто поля формы имеют требования к заполнению. Например, в форме регистрации может быть обязательным поле для пароля. Если пользователь оставит поле пустым, то можно привлечь его внимание к полю, например, покрасив рамку поля красным. Для этого может подойти [псевдокласс `:invalid`](/css/invalid-valid/).

Однако у такого подхода есть один минус - псевдокласс `:invalid` применится сразу же, хотя пользователь даже не успел коснуться поля ввода. Зачем отвлекать пользователя и указывать ему на ошибки, которых он не совершал? Для более приятного пользовательского опыта используйте псевдокласс `:user-invalid` чтобы указать на поля, которые не прошли валидацию, а `:user-valid` - для тех, что прошли.

Его отличие в том, что он применяется только после того как пользователь написал что-то в поле, а затем сменил фокус, например, перешел к другому полю. Посмотрим на примере:

<iframe title="Стилизация элементов формы" src="demos/form-inputs/" height="390"></iframe>

