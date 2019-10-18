---
title: 十个推荐使用的Laravel函数

image: ../images/food.png 

tags:
- Laravel
- function

categories:
- PHP
 
thumbnail: ../images/food.png
 
---


Laravel中包含各种全局辅助函数。可以使用它们来简化开发流程。在这里，我将编写10个最好用的laravel帮助函，数用于使我的开发更容易。 您必须考虑在必要时使用它们。

您还可以查看中文文档发现更多的辅助函数[Laravel help functions](https://learnku.com/docs/laravel/5.8/helpers/3919)


# array_dot()
---

`array_dot()` 辅助函数允许你将多维数组转换为使用点符号的一维数组。

```php
$array = [
    'user' => ['username' => 'something'],
    'app' => ['creator' => ['name' => 'someone'], 'created' => 'today']
];

$dot_array = array_dot($array);

// [user.username] => something, [app.creator.name] => someone, [app.created] => today
```

# array_get()
---

`array_get()` 函数使用点符号从多维数组中检索值。
```php
$array = [
    'user' => ['username' => 'something'],
    'app' => ['creator' => ['name' => 'someone'], 'created' => 'today']
];

$name = array_get($array, 'app.creator.name');

// someone
```

如果key不存在, `array_get()` 函数还接受可选的第三个参数作为默认值。
                       
```php
$name = array_get($array, 'app.creator.name', 'anonymous');

// anonymous
```

# public_path()
---

`public_path()` 返回 Laravel 应用程序中公共目录的完全限定的绝对路径。 你还可以将路径传递到公共目录中的文件或目录以获取该资源的绝对路径。 它将简单地将 public_path() 添加到你的参数中。

```php

$public_path  = public_puth();

$path = public_path('js/app.js');
```

# Str::orderedUuid()
---

`Str::orderedUuid()`函数首先生成一个时间戳 uuid。 这个 uuid 可以存储在索引数据库列中。 这些 uuid 是基于时间戳创建的，因此它们会保留你的内容索引。 在 Laravel 5.6 中使用它时，会引发 `Ramsey\Uuid\Exception\UnsatisfiedDependencyException`。 要解决此问题，只需运行以下命令即可使用 `moontoast/math` 包：

```sheel
composer require "moontoast/math"
```

```php
use Illuminate\Support\Str;

return (string) Str::orderByUuid()

// A timestamp first uuid
```

# str_plural()
---

`str_plural()` 函数将字符串转换为复数形式。该功能只支持英文。

```php
echo str_plural('bank');

// banks

echo str_plural('developer');

// developers
```

# route()
---

`route()` 函数为指定的路由生成路由 URL。

```php
$url = route('login');
```

如果路由接受参数，你可以简单地将它们作为第二个参数传递给一个数组。

```php
$url = route('products', ['id' => 1]);
```

如果你想产生一个相对的 URL 而不是一个绝对的 URL，你可以传递 false 作为第三个参数。

```php
$url = route('products', ['id' => 1], false);
```

# tap()
---

`tap()` 函数接受两个参数：一个值和一个闭包。该值将被传递给闭包，然后该值将被返回。闭包返回值无关紧要。
```php
$user = App\User::find(1);

return tap($user, function($user) {
    $user->update([
        'name' => 'Random'
    ]);
});
```

它不会返回布尔值，而是返回 `User Model`。

如果你没有传递闭包，你也可以使用 `User Model` 的任何方法。 无论实际返回的方法如何，返回值都将始终为值。 在下面的例子中，它将返回 `User Model` 而不是布尔值。 `update` 方法返回布尔值，但由于用了 `tap` ，所以它将返回 `User Model`。

```php
$user = App\User::find(1);

return tap($user)->update([
    'name' => 'SomeName'
]);
```

# dump()
---

`dump()` 函数会 dump 给定的变量，同时也支持同时传入多个变量。这对调试非常有用。

```php
dump($var1);
dump($var1, $var2, $var3);
```

# str_slug()
--- 

`str_slug()` 函数将给定的字符串生成一个 URL 友好的 slug。 你可以使用此功能为帖子或产品标题创建一个 slug。

```php
$slug = str_slug('Helpers in Laravel', '-');

// helpers-in-laravel
```

# optional()
---

`optional()` 函数接受一个参数，你可以调用参数的方法或访问属性。 如果传递的对象为 null，则方法和属性将返回 null，而不是导致错误或抛出异常。

```php
$user = User::find(1);

return optional($user)->name;
```

> 原文地址: https://tutsforweb.com/10-best-laravel-helpers/