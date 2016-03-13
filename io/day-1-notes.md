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

### Inheritance

```io
Io> Vehicle := Object clone
==>  Vehicle_0x7fb7d8e1ece0:
  type             = "Vehicle"

Io> Vehicle description := "a vehicle"
==> a vehicle
Io> Car := Vehicle clone
==>  Car_0x7fb7d8e35e80:
  type             = "Car"

Io> Car description
==> a vehicle
Io> Car slotNames
==> list(type)
```

The `Car` object itself does not have a `description` slot but is able to
access the `description` slot on `Vehicle`. Io forwards the `description`
message up the prototype chain until it finds a matching slot.

Now let's create a specific car.

```io
Io> tesla := Car clone
==>  Car_0x7fb7d8d56760:

Io> tesla slotNames
==> list()
Io> tesla type
==> Car
```

Whoa! Our `tesla` has no slotNames and its type is `Car` (its prototype).  
By convention, types in Io begin with an uppercase letter.

Objects are containers for slots. When an object receives a message,
it searches for a matching slot. If that slot doesn't exist, it will
search its prototype. If it hasn't found the slot in the parent, you
get an error that the object doesn't respond to the message.

```
+-----------------+
|Object           |
|                 |
|                 |
+--------+--------+
         ^
         |
         |
+--------+--------+
|Vehicle          |
|                 |
|    description  |
+--------+--------+
         ^
         |
         |
+--------+--------+
|Car              |
|                 |
|                 |
+--------+--------+
         ^
         |
         |
+--------+--------+
|tesla            |
|                 |
+-----------------+
```

Both `tesla` and `Car` are objects, but only `Car` is a type (meaning it gets the `type` slot)
since it starts with an uppercase letter. The wo objects are pretty much identical otherwise.

### Methods

Methods in Io are objects. Methods have `Block` as its (proto)type.

```io
Io> method type
==> Block
```

We can create a method with optional parentheses where we specify its behaviour.

```io
Io> method("hello" println)
==> method(
    "hello" println
)
```

If we treat a method as a message, we can assign it to a slot, and invoke it by calling the slot.

```io
Io> tesla charge := method("charging..." println)
==> method(
    "charging..." println
)
Io> tesla charge
charging...
```

Those are the basic principles of Io. The rest is learning its libraries.

We can view the contents of a slot:

```io
Io> tesla getSlot("charge")
==> method(
    "charging..." println
)
```

We can get an object's prototype (and conveniently the slots of that prototype):

```io
Io> Car proto
==>  Vehicle_0x7fb7d8e1ece0:
  description      = "a vehicle"
  type             = "Vehicle"
```

We can view all named objects that exist by calling the `Lobby` object:

```io
Io> Lobby
==>  Object_0x7fb7d8f17b80:
  Car              = Car_0x7fb7d8e35e80
  Lobby            = Object_0x7fb7d8f17b80
  Protos           = Object_0x7fb7d8f17aa0
  Vehicle          = Vehicle_0x7fb7d8e1ece0
  _                = Object_0x7fb7d8f17b80
  exit             = method(...)
  forward          = method(...)
  set_             = method(...)
  tesla            = Car_0x7fb7d8d56760
```

### Collections

TODO

---

1. Even assignment is a message in Io.

[hash map]: https://en.wikipedia.org/wiki/Hash_table
