# Циклы

Циклы нужны для того, чтобы в зависимости от некоторого условия или задачи выполнять некоторые действия множество раз.

В отличии от других языков программирования, единственной конструкцией для создания циклов является `for`, который может принимать разные формы. Базовая конструкция цикла `for` вяглядит следующим образом:

```
for [инициализация счетчика]; [условие]; [изменение счетчика]{
    // действия
}
```

Давайте теперь рассмотрим пример программы с циклом `for`. Например, нам нужно проссумировать все числа от 1 до 10. Такую программу с легостью можно написать, используя цикл `for`:

```
package main
import "fmt"

func main() {
	sum := 0    // создаем переменную, в которой будет суммировать значения
	for i := 1; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)    // 45  (все проссумированные значения от 1 до 10)
}
```

Теперь давайте подробно разберем конструкцию цикла в нашей программе. Вначале происходит инциализация (присваивание) счетчика: `i := 1` (начальное значение). По сути она представляет объявление переменной, которую мы будем использовать внутри цикла.

Условие `i < 10` означает, что пока это условие выполняется, то мы будем инкремировать (3-я часть цикла - `i++`) наше значение `i` на 1 (`i++` эквивалентно `i += 1`).

Соответственно, цикл прекращается тогда, когда значение `i` равно 11 (`i == 11`).

## Вариации конструкции цикла for

На самом деле необязательно указывать все условия при объявлении цикла. Например, можно объявить перменную `i` раньше самой конструкции цикла:

```
package main
import "fmt"

func main() {
	var i int = 1

	for ; i < 5; i++ {
    	fmt.Println(i * i)
	}
}
```

Можно оставить и вовсе только одно условие, тогда цикл `for` будет являться, по сути, аналогом цикла `while` из других языков программирование (самого слова `while` нет в Go):

```
package main
import "fmt"

func main() {
	var i int = 1

	for i < 5 {
    	fmt.Println(i * i)
		i++
	}
}
```

Однако, в этом случае необходимо будет обозначить условие выхода цикла (условие завершения), т.к. в противном случае программа будет выполняться бесконечно. В данном случае, `i++` является условием выхода, так как при каждой итерации (т.е. при каждом шаге выполнения цикла) мы увеличиваем `i` на 1.

Пример бесконечного цикла:

```
package main
import "fmt"

func main() {
	var i int = 1

	for i < 5 {
    	fmt.Println(i * i)
	}
}
```

Еще бесконечный цикл можно указать таким образом:

```
for {

}
```

## Вложенные циклы

Вложенный цикл расположен в еще одном цикле:

```
package main
import "fmt"

func main() {

	for i := 1; i < 3; i++ {
		fmt.Println("i равно", i)
    	for j := 1; j < 3; j++ {
			fmt.Println("J равно", j)
		}
	}
}
```

В результате мы получим следующий вывод на консоль:

```
i равно 1
J равно 1
J равно 2
i равно 2
J равно 1
J равно 2
```

Из результата мы видим что, для каждого значения `i` значение `j` выводилось ровно 2 раза!

Чтобы лучше понять работу вложенных циклов, вспомним по какому принципу работают наши часы. Мы знаем, что секундная, минутная и часовая стрелки вращаются вокруг циферблата. Часовая стрелка смещается всего на 1 шаг для каждых 60 шагов минутной стрелки. Минутная же стрелка вращается на 1 шаг для каждых 60 шагов секундных стрелок. Таким образом, это означает, что для каждого полного оборота часовой стрелки (12 шагов, т.е. часов), минутная стрелка сделает 720 шагов, а секундная 43200 шагов!

<p align="center">
    <img width="350" src="https://upload.wikimedia.org/wikipedia/commons/8/8a/AnalogClockAnimation1_2hands_1h_in_6sec.gif" alt="Clock logo">
</p>

```
package main
import "fmt"

func main() {

	for hours := 0; hours < 12; hours++ {
		for minutes := 0; minutes < 60; minutes++ {
			for seconds := 0; seconds < 60; seconds++{
				fmt.Println(hours, ":", minutes, ":", seconds)
			}
		}
	}
}
```

Результатом работы такого кода будет:

```
0 : 0 : 0
0 : 0 : 1
0 : 0 : 2
...
11 : 59 : 57
11 : 59 : 58
11 : 59 : 59
```

## Цикл for и массивы/срезы

Для перебора массивов или срезов можно использовать следующую форму цикла `for`:

```
for индекс, значение := range массив/срез {
    // действия
}
```

Давайте теперь рассмотрим более подробный пример. Допустим у нас есть массив некоторых чисел и нужно создать срез, в котором будут только четные значение:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	var even []int

	for i, v := range numbs {   // i, v сокр. от index, value
		if v % 2 == 0 {
			even = append(even, numbs[i])
		}
	}
	fmt.Println(even)	// [2 4 6 8 10]
}
```

Если мы не планируем использовать значения или индексы элементов, то мы можем вместо них указать прочерк. Например, в данной задаче нам вовсе не нужны индексы:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	var even []int

	for _, v := range numbs {
		if v % 2 == 0 {
			even = append(even, v)
		}
	}
	fmt.Println(even)	// [2 4 6 8 10]
}
```

Но также для перебора массива или среза можно использовать и стандартную версию цикла `for`:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	var even []int

	for i := 0; i < len(numbs); i++ {
		if numbs[i] % 2 == 0 {
			even = append(even, numbs[i])
		}
	}
	fmt.Println(even)	// [2 4 6 8 10]
}
```

В этом примере счетчик `i` играет роль индекса массива. Цикл выполняется, пока счетчик `i` не станет равным длине массива. Как мы помним из предыдущего материала, значение длины массива возвращает функция **len()**.

## Операторы break и continue

Часто в цикле `for` используют такие операторы как `break` и `continue`. Начнем с оператора break.

### break

Данный оператор полностью осуществляет выход. из цикла, несмотря даже на само условие в цикле. Например, нам неопходимо найти опредленное чилсо в массиве. Если это число найдено, то последующие итерации нас уже не интересует, а поэтому, можно (и даже нужно) использовать оператора `break`. Допустим, нам надо найти число 5 и вывести его:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

	for i := 0; i < len(numbs); i++ {
		if numbs[i] == 5 {
			fmt.Println(numbs[i])   // 5
			break   // цикл останавливается
		}
	}
}
```

Да, во втором случае результат будет абсолютно таким же:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

	for i := 0; i < len(numbs); i++ {
		if numbs[i] == 5 {
			fmt.Println(numbs[i])   // 5
		}
	}
}
```

Однако программа продолжит дальше итерироваться, не смотря на то, что мы уже нашли число 5. А это негативно сказывается на быстродействие программы.

### continue

Оператор `continue` позволяет нам пропускать те значения, которые нас не интересуют или которые необходимо проигнорировать. Например, дан массив положительных и отрицательных чисел и нужно просуммировать только положительные значения:

```
package main
import "fmt"

func main() {
	var numbs = [10]int{-1, 2, -3, 4, 5, 6, 7, 8, -9, -10}
	sum := 0

	for i := 0; i < len(numbs); i++ {
		if numbs[i] < 0 {
			continue
		}
		sum += numbs[i]
	}
	fmt.Println(sum)	// 32
}
```

Т.е. в данном случае, если выполняется условие `numbs[i] < 0` (отрицательное значение), то срабатывает оператор `continue` которыей пропускает отрицательое значение.
