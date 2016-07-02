Evaluate `1 + 1`
```io
Io> 1 + 1
==> 2
```

Evaluate `1 + "one"`
```io
Io> 1 + "one"

  Exception: argument 0 to method '+' must be a Number, not a 'Sequence'
  ---------
  message '+' in 'Command Line' on line 1
```

Is IO strongly typed or weakly typed?

It's strongly typed. The above snippet generated an error. In a weakly typed language it would result in
some unexpected behaviour like `2` or `"1one"`.

---

Is 0 true or false?

```io
Io> 0 isTrue
==> true
```

Is empty string true or false?
```io
Io> "" isTrue
==> true
```

Is nil true or false?  
Neither, nil is nil (used to indicate an unset or missing value).
```io
Io> nil isTrue
==> false
Io> nil isNil
==> true
```

---

How can you tell what slots a prototype supports?  
Use the `slotNames` method.
```io
Io> Map slotNames
==> list(map, values, empty, foreach, addKeysAndValues, atPut, justSerialized, removeAt, hasValue, asList, hasKey, mergeInPlace, reverseMap, keys, with, asJson, merge, detect, asObject, select, isNotEmpty, size, atIfAbsentPut, isEmpty, at)
```

---

What is the difference between `=`, `:=`, and `::=`. When would you use which?

All three are **assignment operators**.

| operator | action |
| -------- | ------ |
| `=`      | Assigns value to slot if it exists, otherwise raises exception |
| `:=`     | Creates slot, assigns value |
| `::=`    | Creates slot, creates setter, assigns value |

For example

Using `=` raises on a fresh prototype because it has no slots yet.  
Use it when you only want to update a slot, not (accidentally) create new slots.
```io
Io> Foo := Object clone
==>  Foo_0x7fb9a9fd0ec0:
  type             = "Foo"

Io> Foo bar = "some value"

  Exception: Slot bar not found. Must define slot using := operator before updating.
  ---------
  message 'updateSlot' in 'Command Line' on line 1
Io> Foo slotNames
==> list(type)
```

Using `:=` creates a slot if none exists and assigns the value.  
Use it when you want to update a slot or create one if it doesn't exist (instead of raising an exception).
```io
Io> Foo := Object clone
==>  Foo_0x7fb9a9f6e4e0:
type             = "Foo"

Io> Foo bar := "some value"
==> some value
Io> Foo bar := "another value"
==> another value
Io> Foo slotNames
==> list(type, bar)
```

Using `::=` goes one step further and also adds a setter method.  
Use it when you want a new slot and want to set it via a method (instead of an assignment operator).
```io
Io> Foo := Object clone
==>  Foo_0x7fb9ab9aff80:
  type             = "Foo"

Io> Foo bar ::= "some value"
==> some value
Io> Foo slotNames
==> list(type, setBar, bar)
```

Note that the assignment operators are syntax sugar for methods.

| source | compiles to |
| ------ | ----------- |
| `a ::= 1`	| `newSlot("a", 1)` |
| `a := 1` | `setSlot("a", 1)` |
| `a = 1` | `updateSlot("a", 1)` |

---

How do you run an Io program from file?

```shell
$ io filename.io
```

Without arguments, `io` starts a REPL.
