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
* [链表反转](#链表反转)
* [获得上周一和上周日的日期](#获得上周一和上周日的日期)
* [去除数组中键值为空的元素](#去除数组中键值为空的元素)
* [去除数组中键值重复的元素](#去除数组中键值重复的元素)
* [重新建立数组索引](#重新建立数组索引)
* [对二维数组中多个键值相同的元素进行去重](#对二维数组中多个键值相同的元素进行去重)
* [使用正则表达式验证字符串不能为纯数字，不能为纯字母，并且不能包含彩票 / 广告等关键词](#使用正则表达式验证字符串不能为纯数字，不能为纯字母，并且不能包含彩票--广告等关键词)
* [复制一个数组 N 次](#复制一个数组-n-次)
* [抽象类和接口的区别](#抽象类和接口的区别)
* [猴子选大王](#猴子选大王)
* [发红包](#发红包)
* [斐波那契数列](#斐波那契数列)
* [二分查找](#二分查找)
* [读取大文件](#读取大文件)
* [如何实现多继承](#如何实现多继承)
* [PHP 执行流程](#php-执行流程)
* [自动加载的实现](#自动加载的实现)
* [单引号和双引号所包含的字符串的区别](#单引号和双引号所包含的字符串的区别)
* [递增递减运算符](#递增递减运算符)
* [类型转换的判别](#类型转换的判别)
* [字符串函数与大小写敏感](#字符串函数与大小写敏感)
* [变量范围](#变量范围)
* [三元运算符](#三元运算符)
* [传值和传引用的区别](#传值和传引用的区别)
* [从 URL 中获取文件的扩展名](#从-url-中获取文件的扩展名)
* [判断键名是否存在于数组中](#判断键名是否存在于数组中)
* [判断字符串是否是另一个字符串的子字符串](#判断字符串是否是另一个字符串的子字符串)
* [遍历目录中所有文件和子目录](#遍历目录中所有文件和子目录)
* [配置优化](#配置优化)

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

## 链表反转

###### 方法一：

```php
<?php

/**
 * Reverse list.
 *
 * @param  ListNode $pHead
 * @return ListNode
 */
function reverseList(ListNode $pHead): ?ListNode
{
    if ($pHead == null || $pHead->next == null) {
        return $pHead;
    }

    $p = null;
    while ($pHead != null) {
        $tmp = $pHead->next;
        $pHead->next = $p;
        $p = $pHead;
        $pHead = $tmp;
    }
    return $p;
}

```

###### 方法二：

```php
<?php

/**
 * Reverse list.
 *
 * @param  ListNode $pHead
 * @return ListNode
 */
function reverseList(ListNode $pHead): ?ListNode
{
    if ($pHead == null || $pHead->next == null) {
        return $pHead;
    }

    $p = reverseList($pHead->next);
    $pHead->next->next = $pHead;
    $pHead->next = null;
    return $p;
}

```

## 获得上周一和上周日的日期

```php
<?php

date('Y-m-d', strtotime('Monday Last Week'));
date('Y-m-d', strtotime('Sunday Last Week'));

```

## 去除数组中键值为空的元素

```php
<?php

array_filter($array);

```

## 去除数组中键值重复的元素

```php
<?php

array_unique($array);

```

## 重新建立数组索引

```php
<?php

array_values($array);

```

## 对二维数组中多个键值相同的元素进行去重

```php
<?php

/**
 * Unique array.
 *
 * @param  array  &$array
 * @param  string $key1
 * @param  string $key2
 * @return void
 */
function uniqueArray(array &$array, string $key1, string $key2)
{
    if (!is_array($array) || empty($array)) {
        return;
    }

    $tmp = [];
    foreach ($array as $key => $value) {
        if (isset($value[$key1]) && isset($value[$key2])) {
            $string = $value[$key1] . $value[$key2];
            if (in_array($string, $tmp)) {
                unset($array[$key]);
            } else {
                $tmp[] = $string;
            }
        }
    }
}

```

## 使用正则表达式验证字符串不能为纯数字，不能为纯字母，并且不能包含彩票 / 广告等关键词

```php
<?php

var_dump(preg_match('/^\d+$|^[a-zA-z]+$|彩票|广告/', $string));

```

## 复制一个数组 N 次

```php
<?php

/**
 * Repeat array.
 *
 * @param  array  &$array
 * @param  int    $count
 * @return void
 */
function repeatArray(array &$array, int $count)
{
    if (!is_array($array) || empty($array)) {
        return;
    }

    $tmp = $array;
    for ($i = 1; $i < $count; $i++) {
        $array = array_merge($array, $tmp);
    }
}

```

## 抽象类和接口的区别

> 抽象类用于不同的事物，而接口用于事物的行为。

## 猴子选大王

```php
<?php

/**
 * Monkey king.
 *
 * @param  int    $count
 * @param  int    $num
 * @return int
 */
function monkeyKing(int $count, int $num): int
{
    if ($count < 1 || $num <= 0) {
        return -1;
    }

    $array = range(1, $count);
    $i = 1;
    while (count($array) > 1) {
        if ($i % $num != 0) {
            $array[] = $array[$i - 1];
        }
        unset($array[$i - 1]);
        $i++;
    }
    return $array[$i - 1];
}

```

## 发红包

```php
<?php

/**
 * Red envelope.
 *
 * @param  float  $total
 * @param  int    $num
 * @param  float  $min
 * @param  float  $maxPercent
 * @return array
 */
function redEnvelope(float $total, int $num, float $min = 0.01, float $maxPercent = 0.6): array
{
    bcscale(2);
    if (bccomp($total, 0) <= 0 || bccomp($num, 0) <= 0 || bccomp($total, bcmul($num, $min)) < 0 || bccomp($maxPercent, 1) > 0) {
        return [];
    }

    $array = [];
    for (--$num; $num > 0; $num--) {
        $max = bcmul(bcsub($total, bcmul($num, $min)), $maxPercent);
        $tmp = bcdiv(mt_rand(bcmul($min, 100), bcmul($max, 100)), 100);
        $array[] = $tmp;
        $total = bcsub($total, $tmp);
    }
    $array[] = $total;
    return $array;
}

```

## 斐波那契数列

###### 方法一：

```php
<?php

/**
 * Fibonacci sequence.
 *
 * @param  int    $num
 * @return int
 */
function fib(int $num): int
{
    if ($num == 0 || $num == 1) {
        return $num;
    }

    return fib($num - 2) + fib($num - 1);
}

```

###### 方法二：

```php
<?php

/**
 * Fibonacci sequence.
 *
 * @param  int    $num
 * @return int
 */
function fib(int $num): int
{
    if ($num == 0 || $num == 1) {
        return $num;
    }

    $f0 = 0;
    $f1 = 1;
    $f2 = 0;
    for ($i = 2; $i <= $num; $i++) {
        $f2 = $f0 + $f1;
        $f0 = $f1;
        $f1 = $f2;
    }
    return $f2;
}

```

## 二分查找

```php
<?php

/**
 * Binary search.
 *
 * @param  array  $array
 * @param  int    $num
 * @return int
 */
function binarySearch(array $array, int $num): int
{
    if (!is_array($array) || empty($array)) {
        return -1;
    }

    $count = count($array);
    $left = 0;
    $right = $count - 1;
    while ($left <= $right) {
        $middle = (int) (($left + $right) / 2);
        if ($array[$middle] > $num) {
            $right = $middle - 1;
        } elseif ($array[$middle] < $num) {
            $left = $middle + 1;
        } else {
            return $middle;
        }
    }

    return -1;
}

```

## 读取大文件

[生成器总览](https://kuriv.github.io/manual-php/book/docs/语言参考/生成器/生成器总览.html)

## 如何实现多继承

[Trait](https://kuriv.github.io/manual-php/book/docs/语言参考/类与对象/Trait.html)

## PHP 执行流程

> * 词法分析，将 PHP 代码转换成语言片段。
> * 语法分析，将语言片段转换成简单有意义的表达式。
> * 编译，将表达式编译成操作码。
> * 执行，顺序执行操作码，从而实现 PHP 脚本的功能，和机器指令运行相似。

## 自动加载的实现

```php
<?php

spl_autoload_register();

```

## 单引号和双引号所包含的字符串的区别

> * 单引号处理速度相对较快，双引号处理速度相对较慢。
> * 双引号所包含的字符串会解析其中以 $ 开头的变量，而单引号则不解析。

## 递增递减运算符

```php
<?php

$x = 1;
++$x;
$y = $x++;
var_dump($x); // int(3)
var_dump($y); // int(2)

```

## 类型转换的判别

```php
<?php

$foo = "24linux" + 6;
var_dump($foo); // int(30)

```

## 字符串函数与大小写敏感

```php
<?php

var_dump(strstr('PHPlinux', 'L'));  // bool(false)
var_dump(stristr('PHPLinux', 'l')); // string(5) "Linux"

```

## 变量范围

```php
<?php

$foo = 'foo';

/**
 * Just a test function.
 *
 * @param  void
 * @return void
 */
function foo()
{
    $foo = 'Hello World!';
    global $foo;
    echo $foo;
}

echo $foo; // foo
foo();     // foo

```

## 三元运算符

```php
<?php

$foo = 201;
$bar = 40;
$baz = $foo > $bar ? 4 : 5;
echo $baz; // 4

```

## 传值和传引用的区别

> * 传值是将实参的值赋值给形参，对形参的修改不会影响到实参的值。
> * 传引用时传递的是实参的地址，对形参的修改将会影响到实参的值。

## 从 URL 中获取文件的扩展名

###### 方法一：

```php
<?php

/**
 * Get the extension name.
 *
 * @param  string $url
 * @return string
 */
function getExtensionName(string $url): string
{
    $path = urldecode(parse_url($url, PHP_URL_PATH));
    return trim(strrchr($path, '.'), '.');
}

```

###### 方法二：

```php
<?php

/**
 * Get the extension name.
 *
 * @param  string $url
 * @return string
 */
function getExtensionName(string $url): string
{
    return pathinfo($url, PATHINFO_EXTENSION);
}

```

###### 方法三：

```php
<?php

/**
 * Get the extension name.
 *
 * @param  string $url
 * @return string
 */
function getExtensionName(string $url): string
{
    return substr($url, strrpos($url, '.') + 1);
}

```

## 判断键名是否存在于数组中

###### 方法一：

```php
<?php

array_key_exists('foo', $array);

```

###### 方法二：

```php
<?php

in_array('foo', array_keys($array), true);

```

## 判断字符串是否是另一个字符串的子字符串

```php
<?php

/**
 * Check substring.
 *
 * @param  string $string1
 * @param  string $string2
 * @return bool
 */
function checkSubstring(string $string1, string $string2): bool
{
    if ($string1 === $string2) {
        return true;
    }

    if (strlen($string1) > strlen($string2)) {
        $tmp = $string1;
        $string1 = $string2;
        $string2 = $tmp;
    }
    return strpos($string2, $string1) !== false;
}

```

## 遍历目录中所有文件和子目录

```php
<?php

/**
 * Scan files.
 *
 * @param  string $dir
 * @return array
 */
function scanFiles(string $dir): array
{
    $dir = realpath($dir);
    if (!$dir || !is_dir($dir) || empty($files = array_slice(scandir($dir), 2))) {
        return [];
    }

    $array = [];
    foreach ($files as $value) {
        $tmp = realpath($dir . '/' . $value);
        is_dir($tmp) ? $array[$tmp] = scanFiles($tmp) : $array[] = $tmp;
    }
    return $array;
}

```

## 配置优化

```
;;;;;;;;;;;;;;;;;;;;
; Language Options ;
;;;;;;;;;;;;;;;;;;;;

output_buffering = 4096
realpath_cache_size = 4096K
realpath_cache_ttl = 120

;;;;;;;;;;;;;;;;;;;
; Resource Limits ;
;;;;;;;;;;;;;;;;;;;

max_execution_time = 30
memory_limit = 128M

;;;;;;;;;;;;;;;;
; File Uploads ;
;;;;;;;;;;;;;;;;

file_uploads = On
upload_max_filesize = 10M
max_file_uploads = 20

;;;;;;;;;;;;;;;;;;;
; Module Settings ;
;;;;;;;;;;;;;;;;;;;

[Session]
session.save_handler = redis

[opcache]
opcache.enable=1
```

