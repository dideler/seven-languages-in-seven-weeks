Io is a programming language focused on expressiveness through simplicity.
Its syntax is minimal and pure, as you'll soon see.

Io is a message-passing language.
Everything is a message.
Each message is sent to a receiver (object).
Each message returns another receiver (object).
Its syntax chains messages together.

Receivers go on the left, messages go on the right.

```io
Io> "hello" println
hello
```

All values are objects in Io.
The value "hello" is an object, it's also the receiver of the message `println`.

That's it. You just send messages to objects.

You create new objects by cloning existing objects, which are called prototypes.

```io
Io> Person := Object clone
==>  Person_0x7fb1a50124c0:
  type             = "Person"
```

`Object` is the root-level object. We sent it the `clone` message.
That message returned a new object, which we assign to `Person`.<sup>1</sup>

There are no classes in Io; `Person` is not a class, it's an object, based on the `Object` prototype.

Objects have _slots_. We can give our `Person` a `name` slot, and assign a value to that slot.

```io
Io> Person name := "Dennis"
==> Dennis
```

Slots are key-value pairs. Objects are a collection of slots.
The collection can be thought of as a [hash map].

Reading a value from a slot is straight forward: send the slot's name to the object.

```io
Io> Person name
==> Dennis
```

We can look at all the slots on the object.
```io
Io> Person slotNames
==> list(type, name)
```

Look at that, we have another slot! The `type` slot exists on all objects.

```io
Io> Person type
==> Person
Io> Object type
==> Object
```

---

1. Even assignment is a message in Io.

[hash map]: https://en.wikipedia.org/wiki/Hash_table
