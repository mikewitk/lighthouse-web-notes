# RUBY

## Classes

```ruby
# good_dog.rb

class GoodDog
end

sparky = GoodDog.new
```

## Modules

 A module is a **collection of behaviors** that is useable in other classes via mixins. 
 A module allows us to **group reusable code into one place**. 

```ruby
module Speak
  def speak(sound)
    puts sound
  end
end

class GoodDog
  include Speak
end

class HumanBeing
  include Speak
end

sparky = GoodDog.new
sparky.speak("Arf!")        # => Arf!
bob = HumanBeing.new
bob.speak("Hello!")         # => Hello!
```

## Classes ad Objects - Part I

### States and Behaviours

**Constructor**

```ruby
# good_dog.rb

class GoodDog
  def initialize
    puts "This object was initialized!"
  end
end

sparky = GoodDog.new        # => "This object was initialized!"
```
In the above example, instantiating a new GoodDog object triggered the initialize method and resulted in the string being outputted. **We refer to the initialize method as a constructor**, because it gets triggered whenever we create a new object.

**Instance Variables**
```ruby
# good_dog.rb

class GoodDog
  def initialize(name)
    @name = name
  end
end
```

**Instance Methods**
```ruby
# good_dog.rb

class GoodDog
  def initialize(name)
    @name = name
  end

  def speak
  "#{@name} says arf!"
end
end

sparky = GoodDog.new("Sparky")
puts sparky.speak
```
**Acessor Methods**
Finally, as a convention, Rubyists typically want to name those **getter and setter methods using the same name as the instance variable they are exposing and setting**. We'll make the change to our code as well:
```ruby
class GoodDog
  def initialize(name)
    @name = name
  end

  def name                  # This was renamed from "get_name"
    @name
  end

  def name=(n)              # This was renamed from "set_name="
    @name = n
  end

  def speak
    "#{@name} says arf!"
  end
end

sparky = GoodDog.new("Sparky")
puts sparky.speak
puts sparky.name            
# => "Sparky"
sparky.name = "Spartacus"
puts sparky.name            
# => "Spartacus"
```

Because these methods are so commonplace, **Ruby has a built-in way to automatically create these getter and setter methods for us, using the attr_accessor method**. Check out this refactoring of the code from above.
```ruby
# good_dog.rb

class GoodDog
  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def speak
    "#{@name} says arf!"
  end
end

sparky = GoodDog.new("Sparky")
puts sparky.speak
puts sparky.name            # => "Sparky"
sparky.name = "Spartacus"
puts sparky.name            # => "Spartacus"
```
The **attr_accessor method takes a symbol as an argument**, which it uses to create the method name for the getter and setter methods. 
> **attr_acessor** create **getter** and **setter** methods
> **attr_reader** create **getter** method
> **attr_writer** create **setter** method

ex: attr_accessor :name, :height, :weight

Refactoring mehtod *speak* so change from calling the instance variable to the **instance method**
```ruby
def speak
  "#{name} says arf!"
  end
end
```

**SELF**

# good_dog.rb
```ruby
class GoodDog
  attr_accessor :name, :height, :weight

  def initialize(n, h, w)
    @name = n
    @height = h
    @weight = w
  end

  def speak
    "#{name} says arf!"
  end

  def change_info(n, h, w)
    self.name = n
    self.height = h
    self.weight = w
  end

  def info
    "#{self.name} weighs #{self.weight} and is #{self.height} tall."
  end
end
```

## Class Methods





