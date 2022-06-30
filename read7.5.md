Домашнее задание к занятию "7.5. Введение в Golang"

##  задача 1 Установите golang.

    Воспользуйтесь инструкций с официального сайта: https://golang.org/.
    Так же для тестирования кода можно использовать песочницу: https://play.golang.org/.

Ответ:
```bash
root@ubuntuserv:/home/adm1/gitrep/devops-netology# go version
go version go1.13.8 linux/amd64
```
##  задача 2 Знакомство с gotour

Ответ:
```bash
У Golang есть обучающая интерактивная консоль https://tour.golang.org/. Рекомендуется изучить максимальное количество примеров. В консоли уже написан необходимый код, осталось только с ним ознакомиться и поэкспериментировать как написано в инструкции в левой части экрана.
```
## Задача 3 Написание кода
Напишите программу для перевода метров в футы (1 фут = 0.3048 метр). Можно запросить исходные данные у пользователя, а можно статически задать в коде. Для взаимодействия с пользователем можно использовать функцию Scanf:
Ответ:
```bash
package main

  import "fmt"

  func main() {
    var foot float64
      fmt.Print("Type foot: ")
      fmt.Scanf("%f", &foot)
      result := foot * 0.3048
      fmt.Println("Meters:", result )
        }

root@ubuntuserv:/home/adm1/hello# go run foot.go
Type foot: 2
Meters: 0.6096
root@ubuntuserv:/home/adm1/hello#
```
## Задача 4 Написание кода
Напишите программу, которая найдет наименьший элемент в любом заданном списке, например:

x := []int{48,96,86,68,57,82,63,70,37,34,83,27,19,97,9,17,}

Ответ: 
```bash
package main

  import "fmt"

  func main() {
    x := []int{48,96,86,3,68,57,82,63,70,37,34,83,27,19,97,9,17}
    zero := 0
    for i, less := range x {
      if (i == 0) {
        zero = less
      } else {
        if (less < zero) {
          zero = less
        }
      }
      }
    fmt.Println("Min zero: ", zero)
  }
root@ubuntuserv:/home/adm1/hello# go run zero.go
Min zero:  3
root@ubuntuserv:/home/adm1/hello#
```
## Задача 5 Написание кода
Напишите программу, которая выводит числа от 1 до 100, которые делятся на 3. То есть (3, 6, 9, …).

Ответ:
```bash
package main

  import "fmt"

   func main() {
    for i := 1; i <= 100; i++ {
      if (i%3) == 0 {
        fmt.Print("[",i,"]")
      }
    }
  }

root@ubuntuserv:/home/adm1/hello# go run chiclo3.go
[3][6][9][12][15][18][21][24][27][30][33][36][39][42][45][48][51][54][57][60][63][66][69][72][75][78][81][84][87][90][93][96][99]
root@ubuntuserv:/home/adm1/hello#
```
