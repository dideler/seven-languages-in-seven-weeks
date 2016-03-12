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

Being an OO language, Ruby has classes.
Ruby has no support for multi-inheritance, only single-inheritance.

Here's an example of empty classes and inheritance.

```ruby
>> class A; end
>> class B < A; end
>> class C < B; end
>> C.superclass
B
>> C.ancestors
[C, B, A, Object, Kernel, BasicObject]
```

In Ruby, pretty much every object inherits from [`BasicObject`](http://ruby-doc.org/core/BasicObject.html).
As its name implies, it's intentionally basic, an almost blank class.
It provides a small set of basic behaviour that is useful to all classes.

```ruby
>> BasicObject.instance_methods.sort
[:!, :!=, :==, :__id__, :__send__, :equal?, :instance_eval, :instance_exec]
```

The `Object` class, which inherits from `BasicObject`, provides a lot more behaviour to all classes.
Here is a list of all the extra instance methods defined in `Object`.

```ruby
>> (Object.instance_methods - BasicObject.instance_methods).sort
[:!~, :<=>, :===, :=~, :class, :clone, :define_singleton_method, :display, :dup, :enum_for, :eql?, :extend, :freeze, :frozen?, :hash, :inspect, :instance_of?, :instance_variable_defined?, :instance_variable_get, :instance_variable_set, :instance_variables, :is_a?, :itself, :kind_of?, :local_methods, :method, :methods, :nil?, :object_id, :private_methods, :protected_methods, :public_method, :public_methods, :public_send, :remove_instance_variable, :respond_to?, :send, :singleton_class, :singleton_method, :singleton_methods, :taint, :tainted?, :tap, :to_enum, :to_s, :trust, :untaint, :untrust, :untrusted?]
```

Here comes the confusing part. In Ruby, all classes are objects.

```ruby
>> Class.superclass
Module
>> Class.superclass.superclass
Object
>> Class.superclass.superclass.superclass
BasicObject
>> Class.superclass.superclass.superclass.superclass
nil
```

Constructor goes by the name `initialize`.

```ruby
def MyClass
  EXAMPLE_CONSTANT = 90001

  def initialize(foo)
    @insance_variable = foo
  end

  def public_instance_method
    # This method is visible by everyone.
  end

  def self.public_class_method
    # This method is only visible on the class level (not the instance level).
    @@class_variable = 'something'
  end

  protected

  def protected_instance_method
    # This method is not visible outside the class but is visible to child classes.
  end

  private

  def private_instance_method
    # This method is only visible within this class.
  end

  def self.private_class_method
    # This method is only private because of the `private_class_method` method below.
  end
  private_class_method :private_class_method
end
```

There are other ways to create classes and methods in Ruby, but the above is the most common.

### Mixins

Mixins are Ruby's answer to multi-inheritance.

Multi-inheritance was avoided because experience shows that it's complicated and problematic.

When different classes need some shared behaviour but they already inherit from
something (besides, using inheritance for sharing code is an anti-pattern),
and you don't want to use composite objects, then the shared behaviour can
live inside a `module`.

A module is similar to a `class` in Ruby, except you cannot instantiate it.
It's a collection of functions and constants. When you `include` a module as
part of a class, those functions and constants become part of the class.

```ruby
require 'yaml'

module Serializable
  def to_file
    File.open(filename, 'w') do |f|
      f.write(serialize)
    end
  end

  private

  def filename
    "object_#{self.object_id}.txt"
  end

  def serialize
    YAML.dump(self)
  end
end

class Foo
  def initialize(a, b)
    @a, @b = a, b
  end
end

f = Foo.new(1, 2)
f.to_file
```

Ruby also comes with its own predefined modules. Some of the most important ones are `enumerable` and
`comparable`. These two modules provide the mixin class with a bunch of useful behaviour, given that the class
defined `each` for iterating through a collection, and `<=>` for comparing two objects.

For example, they provide behaviour such as

```ruby
>> [1, 3, 2].sort
[1, 2, 3]
>> [1, 5, 8].any? { |i| i > 6 }
true
>> [1, 2, 3, 4].select { |i| i % 2 == 0 }
[2, 4]
>> [1, 2, 3].max
5
>> [1, 2, 3].inject(:+)
6
>> [3, 2, 1].reverse
[1, 2, 3]
```
