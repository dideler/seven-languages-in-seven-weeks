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

#### List

`List` is the collection prototype for ordered objects.

```io
Io> List clone
==> list()
Io> List clone append(1, 2, 3)
==> list(1, 2, 3)
```

The shorthand syntax for creating a list is `list()`.

```io
Io> todo := list("wake up", "take over the world")
==> list(wake up, take over the world)
Io> todo append("sleep")
==> list(wake up, take over the world, sleep)
```

`List` has some convenience methods.

```io
Io> list(1, 2, 3) average
==> 2
Io> list(1, 2, 3) sum
==> 6
Io> list() isEmpty
==> true
```

In total there are 82 list methods<sup>2</sup>
```io
Io> List slotNames size
==> 82
```

You can see all the methods by viewing the slots on `List`.
```io
Io> List slotNames sort
==> list(ListCursor, append, appendIfAbsent, appendSeq, asEncodedList, asJson, asMap, asMessage, asSimpleString, asString, at, atInsert, atPut, average, capacity, contains, containsAll, containsAny, containsIdenticalTo, copy, cursor, detect, difference, empty, exSlice, first, flatten, foreach, fromEncodedList, groupBy, indexOf, insertAfter, insertAt, insertBefore, intersect, isEmpty, isNotEmpty, itemCopy, join, justSerialized, last, map, mapFromKey, mapInPlace, max, min, pop, preallocateToSize, prepend, push, reduce, remove, removeAll, removeAt, removeFirst, removeLast, removeSeq, rest, reverse, reverseForeach, reverseInPlace, reverseReduce, second, select, selectInPlace, setSize, size, slice, sliceInPlace, sort, sortBy, sortByKey, sortInPlace, sortInPlaceBy, sortKey, sum, swapIndices, third, union, unique, uniqueCount, with)
```

#### Map

`Map` is the collection prototypes for key-value pairs (e.g. Ruby hash).

It doesn't have a shorthand syntax like `list` does.

```io
Io> saba := Map clone
==>  Map_0x7fb7d8c3baf0:

Io> saba atPut("description", "island")
==>  Map_0x7fb7d8c3baf0:

Io> saba at("description")
==> island
Io> saba atPut("languages", "dutch, english")
==>  Map_0x7fb7d8c3baf0:

Io> saba asObject
==>  Object_0x7fb7d8c33c40:
  description      = "island"
  languages        = "dutch, english"

Io> saba asList
==> list(list(languages, dutch, english), list(description, island))
Io> saba keys
==> list(languages, description)
Io> saba size
==> 2
```

Maps are a lot like Io objects with slots as keys.
The difference is that maps have extra behaviour on them.

### Singletons

Every `Object` clone has its own object ID (which looks like a memory location).

```io
Io> Object clone
==>  Object_0x7fb7d8c65430:

Io> Object clone
==>  Object_0x7fb7d8c83b00:
```

Compare two `Object` clones, they are not equal.

```io
Io> one := Object clone
==>  Object_0x7fb7d8e499e0:

Io> two := Object clone
==>  Object_0x7fb7d8c50df0:

Io> one == two
==> false
```

But if we create a singleton object by overriding the `clone` method.
```io
Io> SomeSingleton := Object clone
==>  SomeSingleton_0x7fb7d8eb4060:
  type             = "SomeSingleton"

Io> SomeSingleton clone := SomeSingleton
==>  SomeSingleton_0x7fb7d8eb4060:
  clone            = SomeSingleton_0x7fb7d8eb4060
  type             = "SomeSingleton"

Io> foo := SomeSingleton clone
==>  SomeSingleton_0x7fb7d8eb4060:
  clone            = SomeSingleton_0x7fb7d8eb4060
  type             = "SomeSingleton"

Io> bar := SomeSingleton clone
==>  SomeSingleton_0x7fb7d8eb4060:
  clone            = SomeSingleton_0x7fb7d8eb4060
  type             = "SomeSingleton"

Io> foo == bar
==> true
```

Then only a single clone can exist for that object.
Trying to clone it results in the same object being returned!

Implementing the singleton pattern has never been easier!

Just be careful not to override the `clone` method on `Object`.
Cloning will break for all objects and the program will immediately hang until you kill it.

---

1. Even assignment is a message in Io.
2. In version 20140919 of the Io language.

[hash map]: https://en.wikipedia.org/wiki/Hash_table
