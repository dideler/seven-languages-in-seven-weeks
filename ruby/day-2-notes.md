### Functions

Defining functions is very simple compared to languages like Java or C#.
You don't need to build a whole class to define a function.
Every function returns a value, whatever was last executed.

```ruby
def always_true
  true
end
```

---

### Arrays

Arrays are Ruby's primary ordered collection.

```ruby
>> names = ['john', 'mary']
["john", "mary"]
>> puts names
john
mary
nil
>> names[0]
"john"
>> names[-1]
"mary"
>> names[0..1]
["john", "mary"]
>> names[9001]
nil
>> names << 1
["john", "mary", 1]
```

Ruby arrays are incredibly flexible, thanks to its rich API.
You can use them as a queue, linked list, stack, or set.

---

### Hashes

Hashes are key-value pairs. In other languages you may know this data structure
as a map, dictionary, associative array, table, or even object. _\*shudders\*_

```ruby
>> hash = { foo: 'bar', one: :two, :three => 4 }
{:foo=>"bar", :one=>:two, :three=>4}
>> hash[:foo]
"bar"
```

The above example contains `:symbols`. Think of them like strings, except cheaper.
Unlike strings, Ruby does not create a new object for the same symbol.
This makes them great as identifiers, for example, keys in a hash.

```ruby
>> :foo.object_id == :foo.object_id
true
>> 'foo'.object_id == 'foo'.object_id
false
```

---

### Code blocks

Code blocks are anonymous functions that can take parameters.

```ruby
3.times { puts 'naaaaaaaa naa naa nana na, hey jude' }
```

They're quite powerful and are the basis of many DSLs written in Ruby.

Blocks can also be passed as first-class parameters.

```ruby
def call
  yield if block_given?
end

def pass(&block)
 call(&block)
end

>> call { puts 'hey' }
hey
>> pass { puts 'hey' }
hey
```

---

### Defining Classes

TODO

### Mixins

TODO

### Modules, Enumerables, and Sets

TODO
