# Intro to TDD, RSpec, and Learn

## Intro to TDD, RSpec, and Learn

### Video

### Objectives

1. Define the purpose of a code test.
2. Read the RSpec tests.
3. Run tests via the `learn` command.
4. Understand test output.
5. Write code to make test pass.

### What's a Test?

A lot of labs on Learn include tests that verify that the code you write behaves and produces the desired result. It's a sort of an abstract concept at first, but it's worth starting to understand, not only so you can be more productive on Learn, but also because Test-Driven-Development, TDD, is considered the most reliable methodology for delivering quality code. TDD is practiced by the best developers in the world and ignored at the peril of the rest. We'll introduce it to you slowly and you'll quickly get the heart of it.

Often when programming we know what we want our program to do but we aren't sure how to make that happen. Sometimes, we're not even 100% sure that the code we wrote will always behave as we expect.

Imagine needing to write a method, `current_age_for_birth_year`, the purpose is to figure out how old a person currently is based on the year the person was born. A method like this is probably used on the majority of social networks. I tell Facebook that I was born in 1984, the year is currently 2015, Facebook knows that I am currently 31 years old. Next year, without updating Facebook at all, because of this working method, Facebook will know that I'll be 32.

Thinking about the example above, we could define the following requirement of our code.

If the year is currently 2015 and I was born in 1984, when I call the method `current_age_for_birth_year` and provide it my birth year, 1984, by passing that year as an argument, `current_age_for_birth_year(1984)`, I expect it to return 31. 

Expressing that narrative in code is called a test. In an ideal world, I could code this requirement with something like:

```
I expect the method current_age_for_birth_year(1984) to return 31
```

The [RSpec Testing Framework](http://rspec.info/) is a ruby library designed to allow programmers to describe the behavior and outcomes of their programs in a very natural language similar to the above example. Lots of Ruby and Ruby on Rails labs on Learn include RSpec tests. Let's learn a bit about RSpec.

### Reading the Test in `spec/current_age_for_birth_year_spec.rb`

At this point all we want you to be able to do is understand testing at a high level. The idea is that labs come with expectations for how your code should behave and you write the code to make those tests work.

All of our tests are located within the `spec` directory. The code within the `spec` directory is only designed to test that our actual code works. We rarely need to change any code within the `spec` directory.

Our actual code, our programs, our solutions to the challenges in the lab, the stuff that makes our tests pass, are are coded outside of the `spec` directory, generally in the root of the lab directory or in files in directories like `lib` or `app` and more.

In this lab, our tests are in `spec/current_age_for_birth_year_spec.rb` and our actual program and solution will be in a file `current_age_for_birth_year.rb`.

When we run our test program, `spec/current_age_for_birth_year_spec.rb`, that code will load the code in `current_age_for_birth_year.rb` and try to execute `current_age_for_birth_year(1984)` with the expectation that it returns 31. If so, the test will pass. Anything else will make it fail.

The code for our test within `spec/current_age_for_birth_year_spec.rb` is:

```ruby
require_relative '../current_age_for_birth_year.rb'

describe "current_age_for_birth_year method" do
  it "returns the age of a person based on the year of birth" do
    age_of_person = current_age_for_birth_year(1984)
    expect(age_of_person).to eq(31)
  end
end
```

Let's break this code down. The first line of the test, `require_relative '../current_age_for_birth_year.rb`, loads the code from our actual program file so that we can use all the code in that file in our test. That line connects our test to our actual program. 

The next line: `describe "current_age_for_birth_year method" do` is the RSpec language and can basically be ignored for now beyond the actual semantics and meaning. We are simply saying, via valid ruby, that this test describes the `current_age_for_birth_year` method. The only things that are required in this line of code are the `describe` RSpec method and the ruby `do` keyword, the rest of this line is entirely arbitrary and of our own design. After all `"current_age_for_birth_year method"`, is a String of data and could not possibly matter to Ruby because it is not interpreted, it's just data. When we write tests we use the `describe` RSpec method and strings to describe what we are testing. This code is entirely for you, the programmer, and has very little meaning to RSpec or Ruby.

After describing the subject of our test, what we're testing, the method `current_age_for_birth_year`, we use the RSpec method `it` to state an expectation or behavior of that method. `it "returns the age of a person based on their year of birth" do` is very similar to the first line, `it` is an RSpec method, `do` is a ruby keyword, and `"returns the age of a person based on the year of birth"` is a Ruby string that has no meaning to the code and is only there to provide you, the programmer, with a description of what behavior we're currently testing.

The next two lines are our actual test code and the most important part of the `spec/current_age_for_birth_year_spec.rb` file. It is within this block of code, until the proceeding `end` keyword which closes the block of code begun by the `it` RSpec method, that we actually test our code.

To actually test our code, we need to use the method that this test relies on, that this test is designed to exercise. So the first real line of code in our test is: `age_of_person = current_age_for_birth_year(1984)`. What we're doing here is calling a method, `current_age_for_birth_year(1984)`, the very method we're suppose to define and implement, passing it a known argument, `1984`, and assigning the return value of the method to a variable called `age_of_person`. What do you think the value of `age_of_person` should be if the method `current_age_for_birth_year` is called with `1984` as the argument?

The next line of code proposes that exact question with an expected outcome. Using lots of `RSpec` methods and syntax, we say, quite colloquially: `expect(age_of_person).to eq(31)`. What this line of code means is that the we `expect` the value of the variable `age_of_person` `to` `eq` (equal) `31`. That is to say, given that `age_of_person` is the return value of the method `current_age_for_birth_year(1984)`, we can expect that the variable equals 31, the age of the person born in 1984. That's a test.

Our test loads our code, uses our code in the manner desired, and compares the result of our code with a known outcome so that we know our code behaves as we expected.

We could imagine another specification of the `current_age_for_birth_year` method as another `it` block within the opening `describe` block:

```ruby
it "should return the current year for a person born in year 0" do
  twenty_fifteen = current_age_for_birth_year(0)
  expect(twenty_fifteen).to eq(2015)
end
```

There are many kind of tests and Test Driven Development and RSpec are very complex topics, however, just focus on the semantics and meaning of the spec files and you'll be fine and get the hang of it quickly. It's a tremendously valuable skill to be introduced to this early.

A test is always going to be about setting up a state with a known result and comparing that known result or expectation to the behavior of your program, ensuring that your program behaves as you expected.

### Running Our Tests

Now that we can read our test code in our spec file, let's actually run the tests. We're going to execute our test program, which is going to load our real program, try to use it in a certain manner we defined in our tests, and report on the results. To do all this, simply run the `learn` command in your terminal, assuming you've installed the `learn-co` gem with `gem install learn-co`.

The `learn` command loads RSpec to run the tests. RSpec will automatically look in a directory called `spec` and try to execute all files ending in `_spec.rb`. So you type in `learn`, RSpec is loaded, RSpec finds the file `spec/current_age_for_birth_year_spec.rb`, and it executes that code.  RSpec is just ruby, so everything in our test file `spec/current_age_for_birth_year_spec.rb` must be valid Ruby.

So to run your tests, just type `learn` in this lab's directory.

### Understanding Test Output

When you run the tests with the `learn` command you're going to get the results of the test. RSpec will report on what is working and what is broken and why. When you run this lab's test suite with `learn`, before writing any solution code in `current_age_for_birth_year.rb`, you'll see output similar to:

```
current_age_for_birth_year method
  returns the age of a person based on the year of birth (FAILED - 1)

Failures:

  1) current_age_for_birth_year method returns the age of a person based on the year of birth
     Failure/Error: age_of_person = current_age_for_birth_year(1984)
     NoMethodError:
       undefined method `current_age_for_birth_year' for #<RSpec::ExampleGroups::CurrentAgeForBirthYearMethod:0x007fbb8b0607b8>
     # ./spec/current_age_for_birth_year_spec.rb:5:in `block (2 levels) in <top (required)>'

Finished in 0.00063 seconds (files took 0.1535 seconds to load)
1 example, 1 failure

Failed examples:

rspec ./spec/current_age_for_birth_year_spec.rb:4 # current_age_for_birth_year method returns the age of a person based on the year of birth
```

Let's break this down.

```
current_age_for_birth_year method
  returns the age of a person based on the year of birth (FAILED - 1)
```

Those lines are summaries of what we are testing and what failed. They correspond directly to the Strings provided to `describe` and `it` and are simply there to provide context.

```
  1) current_age_for_birth_year method returns the age of a person based on the year of birth
     Failure/Error: age_of_person = current_age_for_birth_year(1984)
     NoMethodError:
       undefined method `current_age_for_birth_year' for #<RSpec::ExampleGroups::CurrentAgeForBirthYearMethod:0x007fbb8b0607b8>
     # ./spec/current_age_for_birth_year_spec.rb:5:in `block (2 levels) in <top (required)>'
```

This actually describes why our test failed. 

```
  1) current_age_for_birth_year method returns the age of a person based on the year of birth
```

That line just joins the Strings passed to `describe` and `it` to create a description of what broke..

```
     Failure/Error: age_of_person = current_age_for_birth_year(1984)
```

That line raises the line of code in our test suite that created the failure and error. The rest of the output describes the error:

```
     NoMethodError:
       undefined method `current_age_for_birth_year' for #<RSpec::ExampleGroups::CurrentAgeForBirthYearMethod:0x007fbb8b0607b8>
     # ./spec/current_age_for_birth_year_spec.rb:5:in `block (2 levels) in <top (required)>'
```

Before writing any code, our test suite is failing because a line of code within it, namely the line `age_of_person = current_age_for_birth_year(1984)`, tried calling a method, `current_age_for_birth_year`, which we expected to have been defined, but has yet to be defined, thus resulting in a `NoMethodError`.

We can run our test suite as many times as we want, it's totally free. In fact, we suggest that every time you make a change to your code and think it might solve something in the test, run the test suite again, it's free. Run the test suite a lot, and read the errors, they are clues. It's totally cool to have errors, a big part of programming is simply getting past the current error your test suite raises and getting to a new error. Progressing through errors until your tests pass is a very normal development cycle.

### Making Our Tests Pass

So, we conceptually understand what we're trying to build, a method called `current_age_for_birth_year`, that when given an argument of a year of birth, `current_age_for_birth_year(1984)`, returns the age of a person, `31`. Our test suite actually executes this code and compares the result of it to the desired outcome, failing until the expectation and the outcome are equal.

The first error thrown by the test suite is that our code, defined in `current_age_for_birth_year.rb`, was expected to define a method called `current_age_for_birth_year`, but did not, resulting in our `NoMethodError`.

Let's fix this error by defining a method in `current_age_for_birth_year.rb` called `current_age_for_birth_year`.

Add the following to the file: `current_age_for_birth_year.rb`

```ruby
def current_age_for_birth_year
end
```

Save the file and go back to your terminal and run the `learn` command. You'll see output including:

```
  1) current_age_for_birth_year method returns the age of a person based on the year of birth
     Failure/Error: age_of_person = current_age_for_birth_year(1984)
     ArgumentError:
       wrong number of arguments (1 for 0)
     # ./current_age_for_birth_year.rb:1:in `current_age_for_birth_year'
     # ./spec/current_age_for_birth_year_spec.rb:5:in `block (2 levels) in <top (required)>'
```

Our tests are still failing, but for a new reason. Previously we lacked the method definition, now we have the method defined, however, our tests are complaining that the line of code `age_of_person = current_age_for_birth_year(1984)` evoked the method `current_age_for_birth_year` incorrectly as it called that method with an argument but the method we defined does not accept an argument.

Let's fix that.

Update the code in `current_age_for_birth_year.rb` to entirely read:

```ruby
def current_age_for_birth_year(birth_year)
end
```

There we define the method `current_age_for_birth_year` to accept an argument and name that argument `birth_year`. The method does nothing else.

Run `learn` again and your failures should resemble:

```
  1) current_age_for_birth_year method returns the age of a person based on the year of birth
     Failure/Error: expect(age_of_person).to eq(31)
       
       expected: 31
            got: nil
       
       (compared using ==)
     # ./spec/current_age_for_birth_year_spec.rb:6:in `block (2 levels) in <top (required)>'
```

This failure isn't a syntax error related to undefined methods or arguments, but rather, this error is telling us that we expected the return value of the method `current_age_for_birth_year(1984)`, stored in the variable `age_of_person` to equal 31, but in actuality, the method returned the value `nil`.

That's perfect. We now need to add actual logic to that method to solve the problem.

How do we calculate the difference between the year currently and the year provided to the method as an argument `birth_year`? You might simply subtract the current year from the birth year.

```ruby
def current_age_for_birth_year(birth_year)
  2015 - birth_year
end
```

Run `learn` again and you should see the test suite passing. Great job!

At this point you should stage your solution with `git add .` and commit it with `git commit -am "Done"` and push it with `git push` and open a pull request and make this lab pass. But there's more to think about.

### Weird Things About Testing and Code

 If we stop and think about what we've done two weird things might occur to you.

#### What's our program actually do?

First, while our tests pass, if we were to run just our program file alone, `ruby current_age_for_birth_year.rb`, it seemingly does nothing. You run that command in your shell and you get no output. What sort of program is this file `current_age_for_birth_year.rb` if it does nothing when you run it? What value does it provide?

Actually files and programs like the code in `current_age_for_birth_year.rb` are common and valuable. That file isn't meant to be useful alone. Rather, that file is considered a library. It's a unit of code that just defines a functionality or method that are meant to be loaded and used in more complex programs.

For example, an application that displays a profile of a person might require or load this simple program and use the defined method to display the person's age.

It isn't that the file `current_age_for_birth_year.rb` doesn't do anything. It does something very significant, it defines a method, it creates a unit of work that any other ruby program that loads or requires this file can use. We do this all the time with programs, to make complex programs simple, we break up the functionalities into separate pieces and files that are smaller and easier to manage, edit, and understand.

If you want to see this technique in practice, try this for fun.

Make a new file called `how_old_are_you.rb`. In that file, put the following code and save it:

```ruby
require_relative './current_age_for_birth_year.rb'

puts "What year were you born?"
birth_year = gets.to_i

users_age = current_age_for_birth_year(birth_year)

puts "You are: " + users_age.to_s + " years old."
```

Run this program with `ruby how_old_are_you.rb`. There shouldn't be any errors if you copied all the code from the tutorial but if they are, just read them and try to debug them or ask for help on Learn.

What this program does is load the code in our original program `current_age_for_birth_year.rb`. It then prints the string "What year were you born?". It prompts the user for input via the `gets` method and converts the input to an integer with `to_i`.

The program then evokes / calls the method `current_age_for_birth_year`. The cool part is that this method is not defined within this file, rather, it was defined in a singular, simple file, and just loaded and used in this more complex program.

This is the architecture of real applications.

#### Our Tests Are Only Temporarily Correct

The second weird thing about the current implementation is the test suite and our solution are brittle and can produce a false positive. In a year, our code will break but our tests will still pass. As long as we are relying on hard coded notions of the current year, our code and tests aren't honest. Imagine the following test, making use of Ruby's `Time` class and methods.

File: `spec/current_age_for_birth_year_spec.rb`
```
require_relative '../current_age_for_birth_year.rb'

describe "current_age_for_birth_year method" do
  it "returns the age of a person based on the year of birth" do
    current_year = Time.now.year
    birth_year = 1984
    answer = current_year-birth_year
    age_of_person = current_age_for_birth_year(birth_year)
    expect(age_of_person).to eq(answer)
  end
end
```

That test would use the year at the moment the test was executed to compute the accurate result and compare it to the result of the method.

To make that pass you would have to implement your solution in `current_age_for_birth_year.rb` as:

```ruby
def current_age_for_birth_year(birth_year)
  Time.now.year - birth_year
end
```
