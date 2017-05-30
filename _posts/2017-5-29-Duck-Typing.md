## What Is It?

### tl;dr

Duck typing is (often) a feature of dynamically-typed languages. In short, duck typing is concerned with which methods an object responds to and not to which class an object necessarily belongs.

If an object has *duck-like methods*, Ruby will treat it like a duck, even if it wasn't constructed inside a "duck" class.

### An Example

First, we begin by creating a Duck class. Of course, ducks can speak (or Quack!) and are celebrated swimmers, so we should be sure to included these methods within the class.

```ruby
class Duck
  def speak
    "Quack!\n"
  end

  def swim
    "I'm a great swimmer. Splash splash splash!\n"
  end
end
```

![Duck Pizza GIF](http://cdn.jsears.co/duck_pizza.gif)

Now, for the sake of demonstrating the phenomenon of duck typing, we will create an Imposter class. Note how the Imposter Class shares similar methods to the Duck class we created above ("speak" and "swim").

```ruby
class Imposter
  def speak
    "Believe me, I'm the best quacker in the world!\n"
  end

  def swim
    "I pay people to swim for me...\n"
  end
end
```

We can create an instance of each class with an appropriate name...

```ruby
mallard = Duck.new
donald = Imposter.new
```

And write a few methods that take in duck or *duck-like* objects as parameters and call the shared "speak" and "swim" methods (and provide some additional information about which method and class were involved in each call).

```ruby
def ducks_go_quack duck
  puts duck.class.name + " says: " + duck.speak + " (via " + __method__.to_s + " method)\n\n"
end

def ducks_can_swim duck
  puts duck.class.name + " says: " + duck.swim + " (via " + __method__.to_s + " method)\n\n"
end
```

Now, we can make calls to our new methods with either of our new *duck-like* objects...

```
ducks_go_quack mallard
ducks_go_quack donald

ducks_can_swim mallard
ducks_can_swim donald
```

And witness the results.

```
Duck says: Quack!
 (via ducks_go_quack method)

Imposter says: Believe me, I'm the best quacker in the world!
 (via ducks_go_quack method)

Duck says: I'm a great swimmer. Splash splash splash!
 (via ducks_can_swim method)

Imposter says: I pay people to swim for me...
 (via ducks_can_swim method)
```

For an discussion on how to leverage duck typing in a practical example, I recommend that you check out Jarrod Rotolo's awesome article [Duck, Duck, Ruby: Duck Typing in Ruby](http://revelry.co/duck-typing-with-ruby/ "Duck, Duck, Ruby: Duck Typing in Ruby").

When in doubt of what duck typing means in the future, remember the age-old saying from which the term "duck typing" originated:

> If it looks like a duck, swims like a duck, and quacks like a duck, then it's probably a duck.

![Duck Running GIF](http://cdn.jsears.co/duck_running.gif)
