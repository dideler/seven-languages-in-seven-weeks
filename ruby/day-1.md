Ruby is a pure object-oriented language. Almost everything in Ruby is an object,
and everything returns a value.

```ruby
>> 4
4
>> 4.class
Fixnum
>> 4.object_id
9
>> 4.methods
["inspect", "%", "<<", "singleton_method", ... ]
```

Everything but `nil` and `false` evaluates to `true`.

```ruby
>> puts 'Careful there old schooler, 0 is truthy!' if 0
Careful there old schooler, 0 is truthy!
nil
```

When an object doesn't respond to a message, you can open it up and change it.
<sup>1, 2</sup>

```ruby
>> 30.fizzbuzz?
NoMethodError: undefined method `fizzbuzz?' for 30:Fixnum
	from (irb):1
	from /Users/dideler/.rbenv/versions/2.3.0/bin/irb:11:in `<main>'
>> class Integer
>>   def fizzbuzz?
>>     self.modulo(15).zero?
>>   end
>> end
:fizzbuzz?
>> 30.fizzbuzz?
true
```

Classes do not have to inherit from the same parent to have the same behaviour,
thanks to Ruby's dynamic typing (type checking happens at runtime execution).
If it acts like a duck, let it be a duck, don't discriminate.

```ruby
>> [100, '100', 100.0].each do |value|
>>   puts "#{value.class} #{value.inspect} responds to message `to_i` with #{value.to_i}"
>> end
Fixnum 100 responds to message `to_i` with 100
String "100" responds to message `to_i` with 100
Float 100.0 responds to message `to_i` with 100
```

Duck typing is very important for clean object-oriented design.
A well known design philosophy is to code to interfaces rather than
implementations. This means different objects can have different
implementations, but when using those objects, you interact with them
the same way through their common interface rather than handling each
object in a special manner.

---

1. Monkey patching is usually frowned upon in practice as it leads to
   surprising behaviour. If you must do it, consider namespacing the patch
   by placing it in a [module] then including the module in the desired class.
2. In the example the `Integer` class is opened up instead of the `Fixnum`
   class. The `Fixnum` class inherits from `Integer`, so does the `Bignum`
   class. It's generally better to define methods in the `Integer` class.

[module]: http://ruby-doc.org/core/Module.html
