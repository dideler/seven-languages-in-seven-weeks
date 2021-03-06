# Ruby

An interpreted, dynamically typed, object-oriented (OO) language known for its
ease of use and readability.

Ruby is popular when it comes to scripting or web development<sup>1</sup>.

Like the author, Ruby is my favourite programming language and the one I use
professionally.<sup>2</sup>

Matz, Ruby's creator, designed the language for programmer productivity
and fun. He believes that systems design needs to emphasize human, rather than
computer, needs. This strongly aligns with my own interests, as I often optimize
for happiness or [least regret][jeff-bezos].

A lot of its flexibility comes from having its code evaluated at runtime,
as opposed to at compile time. For example, this allows for a
[read–eval–print loop][REPL] (REPL), which facilitates exploratory programming,
debugging, and rapid iteration. The REPL includes the programmer more frequently
than the classic edit-compile-run-debug cycle. Ruby's runtime evaluation also
allows for "monkey patching" (modifying code at runtime) and dynamic typing
(types are evaluated at runtime).

Such flexibility and design choices come with a cost, mainly speed and execution
safety.<sup>3</sup> It's no wonder that the Ruby community takes testing very
seriously. But to most Rubyists these inconveniences are a small price to pay
for the efficiency gains and the enjoyability they get from using the language.
If you haven't found any joy in programming lately, give Ruby a try,
it may just make programming fun again.<sup>4</sup>

---

1. Ruby became popular as a web development language thanks to [Ruby on Rails][rails], a web framework.
2. At the time of writing. I'm sure it will change many times throughout my
   life.
3. Matz has admitted if he could change one feature of the language by going
   back in time, he would replace threads with actors or some other more
   advanced concurrency features.
4. In addition to the enjoyability of the language, the Ruby community can be
   a pleasure to work with. They are diverse, welcoming, and supportive while
   not taking themselves too seriously. You'll fit right in.

[rails]: http://rubyonrails.org/
[jeff-bezos]: https://www.youtube.com/watch?v=jwG_qR6XmDQ
[REPL]: https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop
