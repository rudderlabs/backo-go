Backo [![GoDoc](http://godoc.org/github.com/segmentio/backo-go?status.png)](http://godoc.org/github.com/segmentio/backo-go)
-----

Exponential backoff for Go (Go port of segmentio/backo).


Usage
-----

```go
import "github.com/segmentio/backo-go"

// Create a Backo instance.
backo := backo.NewBacko(milliseconds(100), 2, 1, milliseconds(10*1000))
// OR with defaults.
backo := backo.DefaultBacko()

// Use the ticker API.
ticker := b.NewTicker()
for {
    timeout := time.After(5 * time.Minute)
    select {
    case  <-ticker.C:
        fmt.Println("ticked")
    case <- timeout:
        fmt.Println("timed out")
    }
}

// Or simply work with backoff intervals directly.
for i := 0; i < n; i++ {
    // Sleep the current goroutine.
    backo.Sleep(i)
    // Retrieve the duration manually.
    duration := backo.Duration(i)
}
```
