## What Is It?

### tl;dr

Duck typing is (often) a feature of dynamically-typed languages. In short, duck typing is concerned with which methods an object will respond to, and not necessarily the class to which it belongs.

That is, if an object has *duck-like methods*, Ruby will treat it like a duck, even if it wasn't constructed inside of a "duck" class.

### An Example

First, we begin by creating a Duck class. Of course, ducks can speak (or quack) and are celebrated swimmers, so we should be sure to included these methods within the class.

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

For the sake of demonstrating the phenomenon of duck typing, we will create an Imposter class. Note how the Imposter Class shares similar methods to the Duck class we created above ("speak" and "swim").

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

Now we can create an instance of each class with an appropriate name...

```ruby
mallard = Duck.new
donald = Imposter.new
```

And then write a few methods that take in duck or *duck-like* objects as parameters and call the shared "speak" and "swim" methods (and also provide some additional information about which method and class were involved in each call with the ".class.name" and "__method__" methods).

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

And witness the results. Even though "Duck" and "Imposter" are different classes, we are able to successfully pass them as arguments to the "ducks_go_quack" and "ducks_can_swim" methods because both the "Duck" and "Imposter" classes have "speak" and "swim" methods.

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

For a discussion on how to leverage duck typing in a practical situation, I recommend that you check out Jarrod Rotolo's awesome article [Duck, Duck, Ruby: Duck Typing in Ruby](http://revelry.co/duck-typing-with-ruby/ "Duck, Duck, Ruby: Duck Typing in Ruby").

When in doubt, remember the saying that gave "duck typing" its name:

> If it looks like a duck, swims like a duck, and quacks like a duck, then it's probably a duck.

![Duck Running GIF](http://cdn.jsears.co/duck_running.gif)
