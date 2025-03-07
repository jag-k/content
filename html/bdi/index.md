---
title: "`<bdi>`"
authors:
  - xpleesid
keywords:
  - двунаправленный текст
tags:
  - doka
---

## Кратко

Тег `<bdi>` используется, когда нам нужно изолировать блок с текстом от направления текста, заданного у его родителя. Это полезно, когда в тексте встречаются несколько языков, некоторые из которых читаются и пишутся слева направо, а другие — справа налево.

## Как пишется

Здесь используется тег [`<bdo>`](/html/bdo) с атрибутом `dir="rtl"`, поэтому текст в нем будет идти справа налево.

```html
<p>
  <bdo dir="rtl">
    <bdi>Обычный текст</bdi> |
    Зеркальный текст
  </bdo>
</p>
```

<iframe title="Базовый пример" src="demos/basic/" height="120"></iframe>

## Как понять

Тег `<bdi>` стоит использовать, если мы выводим сгенерированный пользователями контент, такой как логин или комментарий, и мы не уверены, в каком направлении будет идти этот текст. Многие языки имеют направление письменности справа налево, например, арабский, иврит или персидский.

Тег `<bdi>` игнорирует значения атрибута `dir`, установленные у родителя, и для текста внутри задаёт `dir="auto"`. Таким образом создаётся изоляция — контент внутри `<bdi>` не зависит от направления текста снаружи.

## Пример

Предположим, мы разрабатываем международный сайт и хотим вывести список самых активных пользователей. Для этого нам может пригодиться такой подход:

```html
<ul>
  <li>
    Пользователь <bdi>john_smith78</bdi>:
    167 комментариев.
  </li>
  <li>
    Пользователь
    <bdi>superPanda</bdi>:
    152 комментария.
  </li>
  <li>
    Пользователь <bdi>شاب رائع</bdi>:
    133 комментария.
  </li>
</ul>
```

<iframe title="Список пользователей с bdi" src="demos/userlist-bdi/" height="170"></iframe>

Однако, если мы заменим `<bdi>` на, скажем, [`<b>`](/html/b), то мы столкнёмся с неожиданным поведением:

```html
<ul>
  <li>
    Пользователь <b>john_smith78</b>:
    167 комментариев.
  </li>
  <li>
    Пользователь <b>superPanda</b>:
    152 комментария.
  </li>
  <li>
    Пользователь <b>شاب رائع</b>:
    133 комментария.
  </li>
</ul>
```

<iframe title="Список пользователей с b" src="demos/userlist-b/" height="170"></iframe>

У третьего пользователя логин на арабском языке, поэтому он направлен справа налево. Из-за этого браузер считает, что следующие за ним символы также нужно вывести справа налево. Скорее всего, мы бы хотели избавиться от такого непредсказуемого поведения, поэтому в подобных ситуациях стоит изолировать логины или иной генерируемый пользователем контент при помощи тега `<bdi>`.
