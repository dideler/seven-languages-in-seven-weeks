Access a file with and without code blocks

```ruby
file = File.open(filename)
# do stuff with file
file.close
```

```ruby
File.open(filename) do |file|
  # do stuff with file
end
```

The optional block ensures the File object will automatically be closed when the block terminates.

---

Translate a hash to an array

```ruby
>> { foo: 'bar' }.to_a
[ [:foo, 'bar'] ]
```

Translate an array to a hash

```ruby
>> [[1,2], [3,4]].to_h
{ 1 => 2, 3 => 4 }
```

---

Iterate through a hash

```ruby
>> { foo: 'bar' }.each { |e| puts e }
foo
bar
```

---

Print the contents of an array of sixteen numbers, four numbers at a time.

```ruby
>> array = 16.times.map.to_a
>> array.each_slice(4) { |element| p element }
[0, 1, 2, 3]
[4, 5, 6, 7]
[8, 9, 10, 11]
[12, 13, 14, 15]
```

---

Write a simple grep that prints the lines of a file having any occurrences of a phrase anywhere in the line.

```ruby
File.open(filename).grep(/pattern/)
```

Note the above is the simplest solution, [but has some drawbacks](http://stackoverflow.com/a/637391/72321).
