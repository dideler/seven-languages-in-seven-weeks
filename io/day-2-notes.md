### Conditionals and Loops

An infinite loop is as simple as
```io
loop("." print)
```

There are many options for conditional looping.

All loops can be broken out of.
```io
Io> i := 1
==> 1
Io> loop(if(i == 1, break))
==> nil
```

Or use a looping construct that accepts a conditional termination.

There is the `repeat` slot that any `Number` object will respond to.
```io
Io> 3 repeat("hi " println)
hi
hi
hi
==> hi
```

The `while(condition, )`

```io
while
```
