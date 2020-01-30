# Темы

## Введение

Тема позволяет полностью настроить внешний вид сайта с помощью Azuriom.

Для установки темы, просто поместите ее в папку `resources/themes/` в корне вашего сайта.

## Создание темы

### Структурирование темы

```
themes/ <-- Папка, содержащая все установленные темы
| example/ <-- Slug вашей темы (название вашей темы в нижнем регистре)
| | theme.json <-- Основной файл вашей темы, содержащий различную информацию
| |  assets/  <-- Папка с активами вашей темы (css, js, images, svg, и т.д.)
| | views/ <-- Папка, содержащая представления вашей темы.
| | config/
| | | config.json
| | | config.blade.php
| | | rules.php
```

### Файл theme.json

У всех тем должен быть файл `theme.json` в корне, то есть
единственный существенный элемент для темы, который выглядит следующим образом:
```json
{
    "name": "Example",
    "version": "1.0.0",
    "description": "A great theme.",
    "url": "https://azuriom.com",
    "authors": [
        "Azuriom"
    ]
}
```

> {инфо} Для создания темы Вы также можете использовать следующую команду, которая
автоматически создаст каталог темы и файл `theme.json`:
```
php artisan theme:create <theme name>
```

### Представления

Представления являются сердцем темы, они представляют собой файлы содержимого HTML
темы для разных частей сайта.

В Azuriom, использующим представления [Laravel](https://laravel.com/), представления могуть быть сделаны при помощи Blade.
Если Вы еще не владеете Blade, то мы настоятельно рекомендуем ознакомиться с информацией по ссылке [its documentation](https://laravel.com/docs/6.x/blade).

> {предупреждение} Настоятельно рекомендуется НЕ ИСПОЛЬЗОВАТЬ синтаксис PHP
при работе с Blade, поскольку это лишь усложнит дальнейшую работу.

Что касается CSS, рекомендуется использовать стандартную структуру CMS, которая является [Bootstrap 4] (https://getbootstrap.com).
Это облегчит реализацию темы и будет совместимо с новыми плагинами,
так что Вам не нужно делать постоянные обновления.
Но Вы, конечно, можете использовать CSS-фреймворк по вашему выбору.

Что касается Javascript, jQuery не является обязательным, только [Axios] (https://github.com/axios/axios) необходим в качестве зависимости.

#### Макет

Макет создает структуру страниц темы. Он содержит
метаданные, активы темы, заголовки, колонтитулы и т.д..

Для отображения контента на текущей странице используйте
`@yield('content')`, а для отображения заголовка текущей страницы `@yield('title')`.

Вы также можете интегрировать различные элементы с помощью
`@include('<название представления>')`, например `@include('element.navbar')` для добавления элемента navbar.

### Методы

#### Активы

Для получения ссылки на актив в теме, используйте функцию
`theme_asset`: 
```html
<link rel="stylesheet" href="{{ theme_asset('css/style.css') }}">
```

#### Переводы

В тему, при необходимости, можно загрузить перевод.

Для этого создайте файл `messages.php` в дирекции `lang/<language>` (пример: `lang/en`).
вашей темы. Затем Вы можете отобразить перевод через команду
trans: `{{ trans('theme::messages.hello') }}` или через `@lang`: 
`@lang('theme::messages.hello')`.
Вы можете также использовать `trans_choice` 
для переводов с цифрами, и `trans_bool` для перевода с двоичными переменными (возвращает на русский`Да`
/`Нет`).

Для более подробной информации о переводах Вы можете перейти по ссылке
[Laravel documentation](https://laravel.com/docs/6.x/localization).

#### Пользователь

Текущий пользователь может быть вычислен с помощью функции `auth()->user()`.
Более подробная информация по аутентификации представлена по ссылке
[Laravel documentation](https://laravel.com/docs/6.x/authentication).

#### Полезные функции

Вы можете получить определенное количество параметров с веб-сайта с помощью представленных функций:

|    Функция       |              Описание                           |
| ---------------- | ------------------------------------------------|
| `site_name()`    | Извлекает имя сайта                             |
| `site_logo()`    | Позволяет получить ссылку на лого веб-сайта     |
| `favicon()`      | Позволяет получить ссылку на значок веб-сайта   |
| `format_date()`  | Отображает дату, отформатированную на текущем языке. Эта функция принимает случай `Carbon \ Carbon` в качестве параметра |
| `money_name()`   | Возвращает имя валюты веб-сайта                 |
| `format_money()` | Возвращает сумму в формате валюты сайта         |

### Установка темы

Вы можете добавить в тему конфигурацию. Для этого, создайте в корне темы:
* Представление `config/config.blade.php` содержащее форму для конфигурации.
* Файл `config/rules.php` с различными правилами валидации для
конфигурации темы.
* Файл `config.json` с конфигурацией темы и исходными значениями. 

##### Пример:

config.blade.php
```html
<form action="{{ route('admin.themes.update', $theme) }}" method="POST">
    @csrf

    <div class="form-group">
        <label for="discordInput">{{ trans('theme::carbon.config.discord') }}</label>
        <input type="text" class="form-control @error('discord-id') is-invalid @enderror" id="discordInput" name="discord-id" required value="{{ old('discord-id', config('theme.discord-id')) }}">

        @error('discord-id')
        <span class="invalid-feedback" role="alert"><strong>{{ $message }}</strong></span>
        @enderror
    </div>

    <button type="submit" class="btn btn-primary"><i class="fas fa-save"></i> {{ trans('messages.actions.save') }}</button>
</form>
```

config.json
```json
{
    "discord-id": "625774284823986183."
}
```