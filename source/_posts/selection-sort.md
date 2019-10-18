---
title: PHP实现选择排序

date: 2019-05-10 21:28:32

tags:
 - php
 - 算法
 - 排序
 
categories:
  - 算法
 
thumbnail: ../images/qiao.png
 
---

# 排序算法(Selection Sort)

选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。以此类推，直到全部待排序的数据元素排完。 选择排序是不稳定的排序方法。

动画演示：

![选择排序](/../images/selectioSort.gif)

PHP代码实现:

```php
<?php

/**
 * main
 * @return void
 */
function main()
{
    $array = [3, -1, 4, 5, 8, 7, 9, 6, 4, 2, 3];
    selectionSort($array, count($array));

    fwrite(STDOUT, "排序结果： \n");
    foreach ($array as $value) {
        fwrite(STDOUT, $value . "\n");
    }
}

/**
 * 选择排序
 * @param array $array
 * @param int $length
 * @return void
 */
function selectionSort(array &$array, int $length)
{
    for ($i = 0; $i < $length - 1; $i ++) { // 由于每次都是和最后面的数字进行比较，所以最后一位不需要循环
        $min = $i;
        for ($j = $i + 1; $j < $length; $j ++) { // 循环未排序号的数字
            if ($array[$j] < $array[$min]) {
                $min = $j;
            }
        }
        swap($array[$i], $array[$min]);
    }
}

/**
 *
 * @param mixed $firstVariable
 * @param mixed $lastVariable
 */
function swap(&$firstVariable, &$lastVariable)
{
    $temp = $firstVariable;
    $firstVariable = $lastVariable;
    $lastVariable = $temp;
}

main();
```

