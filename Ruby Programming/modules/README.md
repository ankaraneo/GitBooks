Modules

General Syntax:     A module is like a toolbox that contains a set of methods and constants. Modules are very much like classes, except they can’t create instances and can’t have subclasses. They’re just a way to store things that you might use later.  It doesn’t make much sense to store variables in a module, for by definition, variables change or vary. Constants however, should always stay the same, so including helpful constants inside a module is a good idea. Ruby constants are written in ALL_CAPS. So whenever you are creating a constant, it should be formatted accordingly.


Creating a Module:     Creating a module is almost identical to creating a class. Like class names, module names are written in CapitilizedCamelCase as well.

     It looks like this:

     module ModuleName
          # Insert methods and constants to use later
     end

Name-spacing & Scope Operators:     One of the main purposes of a module is to separate methods and constants into named spaces. This is called (conveniently), namespacing, and it’s how Ruby doesn’t confuse Math::PI and Circle::PI. The double colon in the previous example is called a scope resolution operator. It is just a way to tell ruby where you are looking for a specific piece of code. If you say Math::PI, then it tells Ruby to look inside the Math module and search for PI, and not any other PI such as in the module  Circle.


Importing External Modules:     Some modules, like MATH, are already present in the interpreter. However, sometimes you will need to be explicitly imported. We can do this using the require keyword. Like so: require ‘module’. We can do more than just require a module, we can also include it. Any class that include’s a certain module can use that module’s methods and constants. You use include like so: include Math. Notice how it doesn’t use the quotes to call on the module. Also, whenever you include a module inside a class, that class no longer has to use the scope resolution operator ( :: ) to define the module to look inside. Instead of writing Math::PI, you can just write PI.


Modules & Classes:     Whenever a module is used to mix in additional information and behavior into a class, it is called a mixin. Mixins allow us to customize a class without having to write additional code.

     Example:

     module Action
          def jump
               @distance = rand(4) + 2
               puts "I jumped forward #{@distance} feet!"
          end
     end

     class Rabbit
          include Action
          attr_reader :name
          def initialize(name)
               @name = name
          end
     end

     class Cricket
          include Action
          attr_reader :name
          def initialize(name)
               @name = name
          end
     end

     peter = Rabbit.new("Peter")
     jiminy = Cricket.new("Jiminy")

     peter.jump
     jiminy.jump

Notice how we define the jump method inside the Action module, the we include it into the Rabbit and Cricket class.


Extending Include:     The INCLUDE keyword only mixes that modules methods and information in at the instance level, to where only instances of that particular class can use the information. However, the EXTEND keyword mixes the modules methods into the class level. This means the class itself can use that module’s information, as opposed to just instances of that class.

     For example:

     module ThePresent
          def now
               puts "It's #{Time.new.hour > 12 ? Time.new.hour - 12 : Time.new.hour}:#{Time.new.min} #{Time.new.hour > 12 ? 'PM' : 'AM'} (GMT)."
          end
     end

     class TheHereAnd
          extend ThePresent
     end

     TheHereAnd.now

Notice how we extended the now method from ThePresent module into TheHereAnd class. This now allows the class to use the ThePresent module. Unlike before, where only instances of TheHereAnd class would have been able to use it.
