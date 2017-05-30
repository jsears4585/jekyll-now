## What Is It?

```ruby
class Duck
  def speak
    "Quack!\n"
  end

  def swim
    "I'm a great swimmer.\n"
  end
end
```



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



```ruby
mallard = Duck.new
donald = Imposter.new
```



```ruby
def ducks_go_quack duck
  puts duck.class.name + " Class says: " + duck.speak + " (via " + __method__.to_s + " method)\n\n"
end

def ducks_can_swim duck
  puts duck.class.name + " Class says: " + duck.swim + " (via " + __method__.to_s + " method)\n\n"
end
```



```
ducks_go_quack mallard
ducks_go_quack donald

ducks_can_swim mallard
ducks_can_swim donald
```



```
Duck Class says: Quack!
 (via ducks_go_quack method)

Imposter Class says: Believe me, I'm the best quacker in the world!
 (via ducks_go_quack method)

Duck Class says: I'm a great swimmer.
 (via ducks_can_swim method)

Imposter Class says: I pay people to swim for me...
 (via ducks_can_swim method)
```
