# Hiding data structures

Part of writing code that can be changed is to ensure that nothing in a Class, not even the class itself, is dependent on how that class organizes its data.

If, for example, a class's `initialize` method gets changed such that its instance variables have a new structure, any of that class's methods that call those variables will get borked when that change happens.

Two things you should do. One, use Ruby's `attr` methods(`attr_accessor`, `attr_reader`) to expose the instance variables in methods:

```ruby
class Hello
  attr_reader :foo, :bar
  def initialize(foo, bar)
    @foo = foo
    @bar = bar
  end
  
  def foo
    @foo * 100 # this is the value we actually want, not @foo
  end
  
  def reads_foo
    puts @foo     # this is simplistic, but if you wanted @foo * 100, this is wrong
    puts foo      # this can't get borked, even if you update foo elsewhere
  end
end
```

The other thing is if you're assuming structure of data coming in, that could change... I'm just going to use Metz's examples here.

```ruby
# BAD

class ObscuringReferences
  attr_reader :data
  
  def initialize( data )
    @data = data # this is a 2d array of different tire size info pairs
  end
  
  def diameter
    # [0] is rim, [1] is tire
    # what happens if the API from which you get that data in the first place changes? You're relying on magic numbers.
    data.collect |cell|
      # some computation around cell[0] and cell[1]
    end
  end
end
```

```ruby
# GOOD

class RevealingReferences
  attr_reader :wheels
  
  def initialize( data )
    @wheels = wheelify( data )
  end
  
  def diameters
    wheels.collect |wheel|
      wheel.rim + ( wheel.tire * 3.14159 )
    end
  end
  
  Wheel = Struct.new( :rim, :tire )
  def wheelify
    # now you only have to update this in one place, even if your vendor's API changes
    data.collect |cell|
      Wheel.new( cell[0], cell[1] )
    end
  end

end
```