# Go 语言中的运算符、流程控制与循环

## 运算符

### 算数运算

| 操作符 | 描述 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |

### 关系运算

| 操作符 | 描述                                           |
| ------ | ---------------------------------------------- |
| ==     | 两边相等则返回 `true` 否则返回 `false`         |
| !=     | 两边不相等则返回 `true` 否则返回 `false`       |
| >      | 左值大于右值则返回 `true` 否则返回 `false`     |
| >=     | 左值大于等于右值则返回 `true` 否则返回 `false` |
| <      | 左值小于则返回 `true` 否则返回 `false`         |
| <=     | 左值小于等于右值则返回 `true` 否则返回 `false` |

### 逻辑运算符

| 操作符 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| &&     | AND 运算符，两边表达式结果都为 `true` 则为 `true` 否则为 `false` |
| \|\|   | OR 运算符，两边表达式有一个为 `true` 则为 `true` 否则为 `false` |
| !      | NOT 运算符，取反；如果条件为 `true` 则为 `false` 否则为 `true` |

#### 位运算

| 操作符 | 描述                                       |
| ------ | ------------------------------------------ |
| &      | 按位与，二进制位都为 1 则为1，否则 为 0    |
| \|     | 按位或，二进制位有一个为 1 则为 1 否则为 0 |
| ^      | 按位异或，二进制位不一样就为 1 否则为 0    |
| <<     | 左移，左移 n 为就是乘以 2 的 n 次方        |
| >>     | 右移，右移n位就是除以2的n次方              |

例如

```go
package main

import "fmt"

func main(){
	two := 2
	four := 4
	fmt.Println(two & four)
	fmt.Println(two | four)
	fmt.Println(two ^ four)
	fmt.Println(two >> four)
	fmt.Println(two << four)
}
```

<img src="mac-vim/img/image-20241216210942780.png" alt="image-20241216210942780" style="zoom:33%;" />



## 流程控制

- if语句
- if-else语句
- if-else嵌套
- switch语句

### if语句

> - `if` 语句的布尔表达式整体不需要用括号包裹。
> - 可以用多个逻辑操作符连接起多个条件判断表达式。
> - `if` 关键字后面的条件判断表达式的求值结果必须是布尔类型，即要么是 `true`，要么是 `false。`
> - `if` 语句的分支代码块的左大括号与 `if` 关键字在同一行上，这也是 Go 代码风格的统一要求，`gofmt` 工具会帮助我们实现这一点。

```go
package main

import "fmt"

func main(){
	var a = 1
	var b = 0
	if a > b {
	fmt.Println(a)
	}
}

```

<img src="mac-vim/img/image-20241216211427530.png" alt="image-20241216211427530" style="zoom:33%;" />

### if-else语句

```go
package main

import "fmt"

func main(){
	var a = 2 
	if a > 0 {
		if a > 1{
		fmt.Println(a)
		}
		else{
		fmt.Println("小于0")
		}
	}
}
```

<img src="mac-vim/img/image-20241216214541363.png" alt="image-20241216214541363" style="zoom:33%;" />



### switch语句

```
package main

import "fmt"

func main(){
	var a = 1
	switch a {
	case 1:
		fmt.Println(1)
	default:
		fmt.Println(a)
	}
}
```

<img src="mac-vim/img/image-20241216214844603.png" alt="image-20241216214844603" style="zoom:33%;" />

> - `switch` 后面的大括号内是一个个代码执行分支，每个分支以 `case` 关键字开始，每个 `case` 后面是一个表达式或是一个逗号分隔的表达式列表。这里还有一个以 `default` 关键字开始的特殊分支，被称为默认分支。且**每个** **`switch`** **只能有一个** **`default`** **分支**
> - **Go 先对 switch expr 表达式进行求值，然后再按** **`case`** **语句的出现顺序，从上到下进行逐一求值**。
> - 无论 `default` 分支出现在什么位置，它都只会在所有 `case` 都没有匹配上的情况下才会被执行的。
> - Go 取消了每个 `case` 后面显示调用 `break`，默认会在每个 `case` 后面调用 `break`，**如果需要执行下一个** **`case`** **的代码逻辑，可以显式使用 Go 提供的关键字** **`fallthrough`** **来实现**。

## 循环

- 经典模式

- ```
  for init; condition; post{
  
  }
  - init：控制变量赋初始值
  - condition：循环控制条件
  - post：给控制变量增量或减量
  ```

- ```Go
  package main
  
  func main() {
          var sum int
          for i := 0; i < 10; i++ {
                  sum += i
          }
          println(sum) // 45
  }
  ```

- 进保留循环判断条件表达式

```Go
i := 0
for i < 10 {
    println(i)
    i++
}
```

- 无限循环，

```
for { 
   // 循环体代码
}
```

`for...range` 循环结构，可以遍历数组、切片、字符串、`map` 及 `channel`，语法如下：

```Go
for key, value := range 复合变量值 {
    // ...
}
```

`注意`

```
package main

import "fmt"
import "time"

func main(){
	var v1 []int = []int{1,2,3,4,5}
	for k,v := range v1 {
		go func(i,v int){
				time.Sleep(time.Second * 3)
				fmt.Println(k,v)
		}(k,v)
	}
	time.Sleep(time.Second * 10)
}

//
```

break 与 continue

## label

> 带 label 的 continue 语句，通常出现于嵌套循环语句中，被用于跳转到外层循环并继续执行外层循环语句的下一个迭代

```
package main

import "fmt"

func main() {
        var sl = [][]int{
                {1, 34, 26, 35, 78},
                {3, 45, 13, 24, 99},
                {101, 13, 38, 7, 127},
                {54, 27, 40, 83, 81},
        }

outerloop:
        for i := 0; i < len(sl); i++ {
                for j := 0; j < len(sl[i]); j++ {
                // 一旦内层循环发现 13 这个值，便中断内层 for 循环，回到外层 for 循环继续执行
                        if sl[i][j] == 13 {
                                fmt.Printf("found 13 at [%d, %d]\n", i, j)
                                continue outerloop
                        }
                }
        }
}
```

## 练习

- 九九乘法表

- ```
  package main
  
  import "fmt"
  
  func main(){
  for i:=1;i<=9;i++{
  	for j:=1;j<=i;j++{
  	fmt.Print("%d * %d = %d",i,j,i*j)
  	}
  	fmt.Println("\n")
  }
  }
  ```

- 字符串遍历

- ```go
  package main
  
  import (
          "fmt"
          "unicode/utf8"
  )
  
  func main() {
          str := "this is a string"
          len := utf8.RuneCountInString(str)
          fmt.Println("字符串的长度：", len)
          for i := 0; i < len; i++ {
                  fmt.Printf("%s\n", string(str[i]))
          }
  }
  ```

- 数组遍历

- ```go
  package main
  
  import (
          "fmt"
  )
  
  func main() {
          arr := [5]int{1, 2, 3, 4, 5}
          for _, value := range arr {
                  fmt.Printf("value: %d\n", value)
          }
  }
  ```

- 切片遍历

- ```go
  package main
  
  import (
          "fmt"
  )
  
  func main() {
          arr := []int{1, 2, 3, 4, 5}
          for _, value := range arr {
                  fmt.Printf("value: %d\n", value)
          }
  }
  ```

- 多层map遍历

- ```go
  package main
  
  import (
          "fmt"
          "strings"
  )
  
  func main() {
          books := map[string]map[string]int{
                  "四书": map[string]int{"论语": 80, "大学": 66, "中庸": 60, "孟子": 70},
                  "五经": map[string]int{"周易": 90, "诗书": 80, "礼记": 88, "尚书": 78, "春秋": 99},
                  "书法": map[string]int{"兰亭集序": 66, "九成宫碑": 68, "多宝塔": 56},
          }
          for key, value := range books {
                  slice := []string{}
                  for v := range value {
                          slice = append(slice, v)
                  }
                  fmt.Printf("%s: %s\n", key, strings.Join(slice, ", "))
          }
  }
  ```