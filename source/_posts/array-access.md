---
title: PHP数组访问

date: 2019-10-17 15:42:43

tags:
 - php
 - 面向对象
 
categories:
  - php
  
thumbnail: ../images/php.png
 
---

# `ArrayAccess` 接口

平常使用的 [Laravel](https://laravel.com/) 框架的模型对象既可以使用箭头来进行赋值, 又可以使用数组方式进行赋值.

```php
<?php

$user = new Users();

$user->name = "RandyChan";
$user['email'] = "M17607475471@163.com";
```

通过以上两种方式都能给对象赋值, 这个功能主要是实现了 `ArrayAccess` 接口和 `__get` 和 `__set` 这两个魔术方法.

![ArrayAccess](/../images/arrayAccess.jpg)

实现 `ArrayAccess` 接口需要实现四个方法.

- `offsetExists(mixed $offset): boolean` : 检查一个偏移位置是否存在
- `offsetGet(mixed $offset): mixed`: 获取一个偏移位置的值
- `offsetSet(mixed $offset, mixed $value): void`: 设置一个偏移位置的值
- `offsetUnset(mixed $offset)`: 复位一个偏移位置的值

> 其中 `$offset` 参数代表数组的键, `$value` 参数代表数组的值

## 实现 `ArrayAccess` 接口
```php
<?php

class User implements \ArrayAccess
{
    /**
     * 声明一个数组存储数据
     * @var array
     */
    private $data = [];

    /**
     * 检查一个偏移位置是否存在, 只需判断这个键是否存在定义好的data变量里面
     * @param mixed $offset
     * @return bool|mixed
     */
    public function offsetExists($offset)
    {
        return isset($this->data[$offset]);
    }

    /**
     * 获取一个偏移位置的值, 实现该方法只需要返回 data 数组对应的值就行
     * @param mixed $offset
     * @return mixed
     */
    public function offsetGet($offset)
    {
        return $this->data[$offset];
    }

    /**
     * 设置一个偏移位置的值, 往 data 里面设置就行
     * @param mixed $offset
     * @param mixed $value
     */
    public function offsetSet($offset, $value)
    {
        $this->data[$offset] = $value;
    }

    /**
     * 复位一个偏移位置的值, 删除数组里面的值, 这里先判断一下值是否存在
     * @param mixed $offset
     */
    public function offsetUnset($offset)
    {
        if ($this->offsetExists($offset)) {
            unset($this->data[$offset]);
        }
    }

    /**
     * 当设置一个不存在的属性时触发
     * @param mixed $offset
     * @param mixed $value
     */
    public function __set($offset, $value)
    {
        $this->data[$offset] = $value;
    }

    /**
     * 当获取一个不存在的属性是触发
     * @param mixed $offset
     * @return mixed
     */
    public function __get($offset)
    {
        return $this->data[$offset];
    }
}

$user = new User();
$user['name'] = "RandyChan";
$user->email = "M17607475471@163.com";

echo $user->name . "\n" . $user['email'];

```

执行结果
```bash
RandyChan
M17607475471@163.com
```


