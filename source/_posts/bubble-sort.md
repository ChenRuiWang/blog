---
title: PHP实现冒泡排序


tags: 
 - php
 - 算法
 - 排序

categories:
 - 算法

 
thumbnail: ../images/mac.png

---

# 冒泡排序 (Bubble Sort)

冒泡排序（英语：Bubble Sort）是一种简单的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序（如从大到小、首字母从A到Z）错误就把他们交换过来。 

演示动画:
![冒泡排序](/../images/BubbleSort.gif)

PHP代码实现：
```php
<?php

/**
 * main
 * @return void
 */
function main()
{
    $array = [3, 1, 4, 5, 8, -1, 7, 6, 4, 2, 3];
    bubbleSort($array, count($array) - 1);
    fwrite(STDOUT, "排序结果: " . PHP_EOL);
    foreach ($array as $value) {
        fwrite(STDOUT, $value . PHP_EOL);
    }
}

/**
 * 冒泡排序
 * @param $array
 * @param $length
 * @return void
 */
function bubbleSort(array &$array, int $length)
{
    for ($i = 0; $i < $length; ++$i) {
        for ($j = 0; $j < $length - $i; ++$j) {
            if ($array[$j] > $array[$j + 1]) {
                swap($array[$j], $array[$j + 1]);
            }
        }
    }
}

/**
 * 交换两个值
 * @param mixed $firstVariable
 * @param mixed $lastVariable
 * @return void
 */
function swap(&$firstVariable, &$lastVariable)
{
    $temp = $firstVariable;
    $firstVariable = $lastVariable;
    $lastVariable = $temp;
}

main();
```


