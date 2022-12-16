# Переменные

Переменная представляет собой именованный участок в памяти, который может хранить определенное значение. В Go для определения (создания) переменной применяется ключевое слово **var**, после которого идет имя переменной, а затем указывается ее тип (подробно о типах данных рассмотрим в следующем пункте). Общий синтаксис выглядит следующим образом:

```
var имя_переменной тип_данных
```

Пример создания переменной в Go:

```
var greeting string
```

В данном примере мы создали переменную с именем **greeting**, которая может хранить тип данных **string**.

Также возможно одновременно объявить несколько переменных через запятую:

```
var name, surname string
```

Здесь уже определены сразу две переменные **name** и **surname**, которые имеют тип **string** и которые принадлежат типу **string**.

## Примеры программ с переменными

Теперь мы можем объявить переменную типа **string** и присвоить ей любое значение, а затем её вывести.

```
package main
import "fmt"

func main() {

    var name, surname string

    name = "Ivan"
    surname = "Ivanov"

    fmt.Println(name) // Ivan
    fmt.Println(surname) // Ivanov
}
```

Поскольку переменные **name** и **surname** имеют тип данных **string**, им можно присвоить строку. В данном случае переменная **name** хранит строку `"Ivan"`, a **surname** хранит `"Ivanov"`. С помощью функции Println значение этих переменных выводится на консоль.

_Важно! Go - регистрозависимый язык. Это значит, что переменные с именами **name** и **Name** будут представлять собой разные переменные._

```
package main
import "fmt"

func main() {
    var name string
    name = "Ivan"

    fmt.Println(Name) // Ошибка! Переменной Name не существует, есть переменная name
}
```

Также возможно сразу при объявлении переменной присвоить ей начальное значение. Данный прием называется инциализацией:

```
package main
import "fmt"

func main() {
    var name string = "Ivan"

    fmt.Println(name)
}
```

Если мы хотим сразу определить несколько переменных и присвоить им начальные значения, то можно обернуть их в скобки:

```
package main
import "fmt"

func main() {
    var (
        name string = "Ivan"
        surname string = "Ivanov"
    )

    fmt.Println(name)       // Ivan
    fmt.Println(surname)    // Ivanov
```

Одной из особенностей переменных является то, что их значение можно многократно изменять:

```
package main
import "fmt"

func main() {
    var name string = "Ivan"
    fmt.Println(name)  // Ivan

    name = "Petr"
    fmt.Println(name)  // Petr

    name = "Oleg"
    fmt.Println(hello)  // Oleg
}
```

## Краткая инициализация переменных

Существует более краткий способ объявить переменную:

```
name := "Ivan"
```

В этом случае тип данных явным образом не указывается, он выводится автоматически из присваиваемого значения. Это равносильно следующему примеру:

```
var name string = "Ivan"
```

Также возможно объявить таким способом (пример неявной типизации):

```
var name = "Ivan"
```

## Комментарии

Комментарии служат для описания действий, которые производит программа или какие-то ее части. При компиляции комментарии не учитываются и не оказывают никакого влияния на работу приложения. Комментарии бывают однострочными и многострочными.

В вышеперечилсенных примерах мы уже использовали комментарии. Однострочный комментарий располагается в одну строку после двойного слеша (`//`). Все, что идет после этих символов, воспринимается компилятором как комментарий. Многострочный комментарий заключается между символами `/*` и `*/` и может занимать несколько строк, например:

```
/*
    The first porgramm
    in the Golang
*/

package main // определение пакета для файла main.go
import "fmt" // подключение пакета "fmt"

// определение функции main

fun main() {
    fmt.Println("Hello there!")  // вывод строки на консоль
}
```