## Поразрядная сортировка на php (RADIX-SORT)
Выполняется за линейное время.  
Нужно иметь представления о том что сортируется (максимальная разрядность и вариативность).  
Нужна доп. память на создание временных массивов.  


```php

//массив на вход
$ar = [101, 5, 200, 63, 990];
//кол-во разрядов
$redux = 3;
//вариативность одного разряда (цифры)
$variety = 10;


$tmp_ar_1 = $empty_ar = array_fill(0, $variety, []);

//сортировка
for ($i = 0; $i <= $redux; $i++) {
    if ($i === 0) { //первая итерация из массива сделать массив массивов
        foreach($ar as $item) {
            $tmp_ar_1[getElement($item, 0, $redux)][] = $item;
        }
    } else if ($i === $redux) {//последняя итерация наоборот из массива массивов сделать массив
        $count = 0;
        foreach($tmp_ar_1 as $items) {
            foreach ($items as $item) {
                $ar[$count] = $item;
                $count++;
            }
        }
    } else { //основные итерации посередине массива
        $tmp_ar_2 = $tmp_ar_1;
        $tmp_ar_1 = $empty_ar;
        foreach($tmp_ar_2 as $items) {
            foreach ($items as $item) {
                $square = getElement($item, $i, $redux);
                $tmp_ar_1[$square][] = $item;
            }
        }
    }
}

//возвращает номер разряда
function getElement($int, $iter, $redux)
{
    return str_pad($int, $redux, “0”, STR_PAD_LEFT)[$redux - $iter - 1];
}

var_dump($ar);
exit;
```
