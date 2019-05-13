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

Class methods are methods we can call directly on the class itself, without having to instantiate any objects. 
When defining a class method, we prepend the method name with the reserved word **self.**, like this:
```ruby
# good_dog.rb
# ... rest of code ommitted for brevity

def self.what_am_i         # Class method definition
  "I'm a GoodDog class!"
end
```
## Class Variables
```ruby
class GoodDog
  @@number_of_dogs = 0

  def initialize
    @@number_of_dogs += 1
  end

  def self.total_number_of_dogs
    @@number_of_dogs
  end
end

puts GoodDog.total_number_of_dogs   # => 0

dog1 = GoodDog.new
dog2 = GoodDog.new

puts GoodDog.total_number_of_dogs   # => 2
```
* Class variable @@number_of_dgos
* Constructor will increment that number by 1
  - Initialize gets call for every instantiation 
* Class Method self.total_number_of_dogs to return the class variable

## Constants

Create a variable with upper case letters

```ruby
class GoodDog
  DOG_YEARS = 7

  attr_accessor :name, :age

  def initialize(n, a)
    self.name = n
    self.age = a * DOG_YEARS
  end
end

sparky = GoodDog.new("Sparky", 4)
puts sparky.age
#=> 28
```
## More About SELF

1. Use **self** when calling setter methods from within the class 
2. Use **self** for class method definitions
```ruby
class GoodDog
  attr_accessor :name, :height, :weight

  def initialize(n, h, w)
    self.name   = n
    self.height = h
    self.weight = w
  end

  def change_info(n, h, w)
    self.name   = n
    self.height = h
    self.weight = w
  end

  def info
    "#{self.name} weighs #{self.weight} and is #{self.height} tall."
  end
end
```
# INHERITANCE
Inheritance is when a class (subclass) inherits behaviour from another class (superclass).

```ruby
class Animal
  def speak
    "Hello!"
  end
end

class GoodDog < Animal
end

class Cat < Animal
end

sparky = GoodDog.new
paws = Cat.new
puts sparky.speak
#=> Hello!
puts paws.speak
#=> Hello!
```

### SUPER

A built-in function that allow us to call methods ups the inheritance heirarchy.

```ruby
class Animal
  def speak
    "Hello!"
  end
end

class GoodDog < Animal
  def speak
    super + " from a GoodDog Class"
  end
end

sparky = GoodDog.new
sparky.speak
#=> "Hello! from a GoodDog Class
```

## MIXING IN MODULES

```ruby
module Swimmable
  def swim
    "I am swimming!"
  end
end

class Animal
end

class Fish < Animal
  include Swimmable
end

class Cat < Animal
end

class Dog < Animal
  include Swimmable
end
```

## Inheritance Vs Modules

1. You can only subclass from one class. But you can mix in as many modules as you'd like
2. If it's an "is-a" relationship, choose class inheritance. If it's a "has-a" relationship, choose modules.
  ex: a doga "is an" animal. A doga "has an" ability to swim.
3. You can't instantiate modules (ie, no object can eb created from a module). Modules are used only for namespacing and grouping common methods together.

## MORE MODULES

```ruby
module Mammal
  class Dog
    def speak(sound)
      p "#{sound}"
    end
  end

  class Cat
    def say_name(name)
      p "#{name}"
    end
  end
end
```

We call classes in a module by appending the class name to the module name with two collons (::)

```ruby
buddy = Mammal::Dog.new
kitty = Mammal::Cat.new
buddy.speak("Arf!")
#=> "Arf!"
kitty.speak("Kitty")
#=> "Kitty"
```

## PRIVATE, PROTECTED, AND PUBLIC

Sometimes you'll have methods that are doing work in the class but don't need to be available to the rest of the program. These methods can be defined as private. 

```ruby
class GoodDog
  DOG_YEARS = 7

  attr_accessor :name, :age

  def initialize(n, a)
    self.name = n
    self.age = a
  end

  private

  def human_years
    age * DOG_YEARS
  end
end

sparky = GoodDog.new("Sparky", 4)
sparky.human_years
#=> error message
```
Public and private methods are most common, but in some less common situations, we'll want an in-between approach. We can use the protected keyword to create protected methods. The easiest way to understand protected methods is to follow these two rules:

* from outside the class, protected methods act just like private methods.
* from inside the class, protected methods are accessible just like public methods.
```ruby
class Animal
  def a_public_method
    "Will this work? " + self.a_protected_method
  end

  protected

  def a_protected_method
    "Yes, I'm protected!"
  end
end

fido = Animal.new
fido.a_public_method        # => Will this work? Yes, I'm protected!

fido.a_protected_method
  # => NoMethodError: protected method `a_protected_method' called for
    #<Animal:0x007fb174157110>
```


