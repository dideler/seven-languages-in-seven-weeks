Print the string "Hello, world."
```ruby
print 'Hello, world.'
```

---

For the string "Hello, Ruby", find the index of the workd "Ruby"
```ruby
'Hello, Ruby'.index('Ruby')
```

---

Print your name ten times
```ruby
10.times do
  puts 'Dennis'
end
```

---

Print a string "This is sentence 1" where the number 1 changes from 1 to 10
```ruby
1.upto(10) do |i|
  puts "This is sentence #{i}"
end
```

---

Run a Ruby program from a file
```ruby
$ ruby filename.rb
```

---

Write a basic "guess the number" game
```ruby
answer = rand(101)

loop do
  print 'Guess a number: '
  guess = gets.chomp.to_i

  if guess < answer
    puts 'Too low'
  elsif guess > answer
    puts 'Too high'
  else
    puts 'Got it'
    break
  end
end
```
