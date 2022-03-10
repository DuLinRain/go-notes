# Go: 三种将byte array转成string的方式

### 通过切片+ string构造函数的方式

```go
    package main
    import (
        "fmt"
    )
    func main() {
        byteArray := []byte{'H', 'E', 'L', 'L', 'O'}
        fmt.Printf("String = %s", string(byteArray[:]))
    }       
```

### 通过buffer -> string的思路

```go
    package main
    import (
        "bytes"
        "fmt"
    )
    
    func main () {
        byteArray := []byte{'H', 'E', 'L', 'L', 'O'}
        str := bytes.NewBuffer(byteArray).String()
        fmt.Printf("String = %s", str)
    }
```

### 通过fmt.Sprintf方法
这种方法会有点慢

```go
package main
import "fmt"

func main()  {
    byteArray := []byte{'H', 'E', 'L', 'L', 'O'}
    fmt.Sprintf("%s", byteArray)
}
```