# Ruby

An interpreted, dynamically typed, object-oriented (OO) language known for its
ease of use and readability.

Like the author, Ruby is my favourite programming language and the one I use
professionally.<sup>1</sup>

Matz, Ruby's creator, designed the language for programmer productivity
and fun. He believes that systems design needs to emphasize human, rather than
computer, needs. This strongly aligns with my own interests, as I often optimize
for happiness or [least regret][jeff-bezos].

A lot of its flexibility comes from having its code evaluated at runtime,
as opposed to at compile time. For example, this allows for a
[read–eval–print loop][REPL] (REPL), which facilitates exploratory programming,
debugging, and rapid iteration. The REPL includes the programmer more frequently
than the classic edit-compile-run-debug cycle. It also allows programmers to
easily perform "monkey patching", that is, modifying code at runtime.

Such flexibility and design choices come with a cost, mainly speed and execution
safety.<sup>2</sup>
But to most Rubyists that's a small price to pay for the efficiency gains and
the enjoyability they get from using the language. If you haven't found any joy
in programming lately, give Ruby a try, it may just make programming fun again.

---

1. At the time of writing. I'm sure it will change many times throughout my
   life.
2. Matz has admitted if he could change one feature of the language by going
   back in time, he would replace threads with actors or some other more
   advanced concurrency features.

[jeff-bezos]: https://www.youtube.com/watch?v=jwG_qR6XmDQ
[REPL]: https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop
