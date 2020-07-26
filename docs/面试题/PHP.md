# PHP

* [垃圾回收机制](#垃圾回收机制)
* [设置 Session 的生存时间](#设置-session-的生存时间)
* [页面重定向的方法](#页面重定向的方法)
* [使用正则表达式匹配 HTML 页面中所有 a 标签的 href 属性](#使用正则表达式匹配-html-页面中所有-a-标签的-href-属性)
* [验证 Email 格式](#验证-email-格式)
* [预定义变量](#预定义变量)
* [魔术变量](#魔术变量)
* [魔术方法](#魔术方法)
* [设计模式](#设计模式)
* [类型比较表](#类型比较表)
* [echo (int) ((0.1 + 0.7) * 10)](#echo-int-01--07--10)
* [使用单例模式建立数据库连接](#使用单例模式建立数据库连接)
* [冒泡排序](#冒泡排序)
* [选择排序](#选择排序)
* [插入排序](#插入排序)
* [快速排序](#快速排序)

## 垃圾回收机制

[垃圾回收机制](https://kuriv.github.io/manual-php/book/docs/垃圾回收机制.html)

## 设置 Session 的生存时间

###### 方法一：

Memcache / Redis

###### 方法二：

* 设置 session.cookie_lifetime
* 设置 session.gc_maxlifetime
* 设置 session.gc_probability 和 session.gc_divisor

###### 方法三：

为每个 Session 的值添加一个对应的时间戳作为生存时间，在每次访问该值之前对时间戳进行判断。

## 页面重定向的方法

```php
<?php

header('Location: http://www.example.com');

```

```php
<?php

echo '<meta http-equiv="refresh" content="0; url=http://www.example.com">';

```

```php
<?php

echo '<script type="text/javascript">window.location.href="http://www.example.com"</script>';

```

## 使用正则表达式匹配 HTML 页面中所有 a 标签的 href 属性

```php
<?php

preg_match_all('/<a.*?href="(.*?)".*?>.*?<\/a>/i', file_get_contents('https://github.com/'), $matches);
var_dump($matches[1]);

```

## 验证 Email 格式

###### 方法一：

```php
<?php

var_dump(preg_match('/^[a-z0-9]+(\.[a-z0-9]+)*@[a-z0-9]+(\.[a-z0-9]+)*(\.[a-z]{2,})$/', $email));

```

###### 方法二：

```php
<?php

var_dump(filter_var($email, FILTER_VALIDATE_EMAIL));

```

## 预定义变量

[预定义变量](https://kuriv.github.io/manual-php/book/docs/语言参考/预定义变量.html)

## 魔术变量

[魔术常量](https://kuriv.github.io/manual-php/book/docs/语言参考/常量/魔术常量.html)

## 魔术方法

[魔术方法](https://kuriv.github.io/manual-php/book/docs/语言参考/类与对象/魔术方法.html)

## 设计模式

[phpdp](https://github.com/kuriv/phpdp)

## 类型比较表

[类型比较表](https://kuriv.github.io/manual-php/book/docs/PHP 类型比较表.html)

## echo (int) ((0.1 + 0.7) * 10)

```php
<?php

echo (int) ((0.1 + 0.7) * 10); // 7

```

浮点数只能表示一个实数的近似值。

```php
<?php

printf('%0.16f', 0.1 + 0.7); // 0.7999999999999999

```

## 使用单例模式建立数据库连接

```php
<?php

final class DB
{
    /**
     * Store the database instance.
     *
     * @var PDO
     */
    private static PDO $instance;

    /**
     * Prevent the instance from being constructed.
     *
     * @param  void
     * @return void
     */
    private function __construct()
    {
        //
    }

    /**
     * Prevent the instance from being cloned.
     *
     * @param  void
     * @return void
     */
    private function __clone()
    {
        //
    }

    /**
     * Prevent the instance from being unserialized.
     *
     * @param  void
     * @return void
     */
    private function __wakeup()
    {
        //
    }

    /**
     * Get the instance via lazy initialization.
     *
     * @param  void
     * @return PDO
     */
    public static function getInstance(): PDO
    {
        return static::$instance ??= new PDO('mysql:host=127.0.0.1;port=3306;dbname=test', 'root', 'root');
    }
}

$foo = DB::getInstance();
$bar = DB::getInstance();
var_dump($foo === $bar); // bool(true)

```

## 冒泡排序

> 依次比较相邻的两个元素，并根据元素的大小来进行排序，由于在排序的过程中总是较小的元素放在前面，较大的元素放在后面，类似于气泡往上升，所以称之为冒泡排序。

```php
<?php

/**
 * Bubble sort.
 *
 * @param  array  &$array
 * @return void
 */
function bubbleSort(array &$array)
{
    if (!is_array($array) || empty($array)) {
        return;
    }

    for ($i = 1, $x = count($array); $i < $x; $i++) {
        for ($j = 0, $y = $x - $i; $j < $y; $j++) {
            if ($array[$j] > $array[$j + 1]) {
                $tmp = $array[$j + 1];
                $array[$j + 1] = $array[$j];
                $array[$j] = $tmp;
            }
        }
    }
}

```

## 选择排序

> 首先找到最小的元素，并将最小的元素放到最前面，然后再从剩余未排序的元素中继续寻找最小的元素进行排序，直到所有元素排序完毕。

```php
<?php

/**
 * Selection sort.
 *
 * @param  array  &$array
 * @return void
 */
function selectionSort(array &$array)
{
    if (!is_array($array) || empty($array)) {
        return;
    }

    for ($i = 0, $count = count($array); $i < $count; $i++) {
        $min = $i;
        for ($j = $i + 1; $j < $count; $j++) {
            if ($array[$min] > $array[$j]) {
                $min = $j;
            }
        }
        if ($min != $i) {
            $tmp = $array[$min];
            $array[$min] = $array[$i];
            $array[$i] = $tmp;
        }
    }
}

```

## 插入排序

> 每次将一个等待排序的元素按其大小插入到前面已经排好序的适当的位置中，直到全部元素插入完成。

```php
<?php

/**
 * Insertion sort.
 *
 * @param  array  &$array
 * @return void
 */
function insertionSort(array &$array)
{
    if (!is_array($array) || empty($array)) {
        return;
    }

    for ($i = 1, $count = count($array); $i < $count; $i++) {
        $tmp = $array[$i];
        for ($j = $i - 1; $j >= 0; $j--) {
            if ($array[$j] > $tmp) {
                $array[$j + 1] = $array[$j];
                $array[$j] = $tmp;
            }
        }
    }
}

```

## 快速排序

> 快速排序是对冒泡排序的改进，首先通过一次排序将元素分成独立的两部分，其中一部分的元素均比另一部分的元素小，然后分别对这两部分继续进行快速排序，整个排序过程可以递归进行。

```php
<?php

/**
 * Quick sort.
 *
 * @param  array  &$array
 * @return void
 */
function quickSort(array &$array)
{
    if (!is_array($array) || empty($array) || ($count = count($array)) == 1) {
        return;
    }

    $left = $right = [];
    for ($i = 1; $i < $count; $i++) {
        $array[$i] > $array[0] ? $right[] = $array[$i] : $left[] = $array[$i];
    }

    quickSort($left);
    quickSort($right);
    $array = array_merge($left, [$array[0]], $right);
}

```