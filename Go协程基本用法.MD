
### 使用waitGroup进行协程同步

```go
package main
import (
"fmt"
"runtime"
"sync"
)

func main()  {
    runtime.GOMAXPROCS(4)
    var wg sync.WaitGroup
    var counter = 1
    for i:=0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            counter++
            wg.Done()
        }()
    }
    wg.Wait()
    fmt.Println(counter)
}
```

### 锁

```go
package main
import (
"fmt"
"runtime"
"sync"
)

func main()  {
    runtime.GOMAXPROCS(4)
    var wg sync.WaitGroup
    var ml sync.Mutex
    var counter = 1
    for i:=0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            ml.Lock()
            counter++
            ml.Unlock()
            wg.Done()
        }()
    }
    wg.Wait()
    fmt.Println(counter)
}
```

### 使用管道进行协程同步


### 从空管道内读数据，且管道未关闭，导致deadlock

### 使用无限循环读取管道数据

```go
package main
import "fmt"

func main () {
	ch := make(chan int)
	go func() {
		ch <- 7
		ch <- 0
		close(ch)
	}()
	for {
        // 管道已关闭，可以继续读取
		if n, ok := <-ch; ok {
			fmt.Println(n)
		} else {
			break
		}
	}
	var input string
	fmt.Scanln(&input)
}


```

### 使用for...range读取管道数据

```go
package main

import "fmt"

func main()  {
    ch := make(chan int)
    go func() {
        ch <- 7
        ch <- 0
        close(ch)
    }()
    // 使用for...range 读
    for n := range ch {
        fmt.Println(n)
    }
}
```
