
A *goroutine* is a lightweight thread managed by the Go runtime.

for example

```
go f(x, y, z) 
```
starts a new goroutine running the function 


```
f(x, y, z) 
```

Goroutines run in the same address space, so access to shared memory must be synchronized to prevent threads from writing over each other. The sync package provides useful primitives, although you wont need them much in Go as there are other primitives.


# Channels

Channels are a types conduit through which you can send and receive values with the channel operator <-.

```
ch <- v    // Send v to channel ch.
v := <-ch  // Receive from ch, and
           // assign value to v.
```

(The data flows in the direction of the arrow) 

Like maps and slides, channels must be created before use

```
ch := make(chan int)
```

by default,, sends and receives block until the other side is ready. This allows goroutines to synchronize without explicit locks or condition variables.

The example code sums the numbers in a slice, distributing the work between two goroutines. Once both goroutines have completed their computation it calculates the final result.