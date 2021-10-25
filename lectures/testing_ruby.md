## Testing Ruby code

Testing is a fundamental part of the working process. In production systems, you literally can't survive without writing tests.
We'll use [RSpec](https://rspec.info "RSpec") throughout the course.

---
#### Why testing is important?

Not only it makes you sleep better at night, but also a good-written tests act like a **documentation** for the code you write! 
In any new app, tests folder is a nice entry point to start the acknowledgment with a project.

---

#### Testing levels

In different articles, you can find a different explanations for testing levels. Usually it's called a "testing pyramid".
You can divide the tests types into 3 parts: unit, integration, system. 

- Unit tests are intended to test the smalles pieces of your codebase in isolation. (e.g. a method of a class).
- Integration tests are intended to test how components work together (e.g. interaction between 2 classes).
- System tests are intended to tests the system as a whole, usually using such instruments as Selenium or Cypress.

On this step, try to focus on unit tests only.
Here's the example of Factorial calculator and a unit test for it.

```ruby
class Factorial
  def factorial_of(n)
    (1..n).inject(:*)
  end
end
```

```ruby
describe Factorial do
  subject(:calculator) { Factorial.new }
  it "finds the factorial of 5" do  
    expect(subject.factorial_of(5)).to eq(120)
  end
end
```

✏️ On your own, try to implement a Fibonacci calculator and a corresponding spec file for it.

---

Please, take your time to carefully read the following materials and do not forget to write your own tests!

#### Links

- 🔗 [2 hour lecture on testing with RSpec from Alexander (RUS)](https://www.youtube.com/watch?v=eVSaLSpHHpY "2 hour lecture on testing with RSpec from Alexander (RUS)") -- the video lecture covers pretty much all the basics you need to get the idea of testing using RSpec [RUS].
- 🔗 [How to make RSpec your friend (RUS)](https://docs.google.com/presentation/d/1o5jBPePt9AHF9oWTQLXGt1Q1iGuZHI7B8kSV87fmHYc/edit#slide=id.p "How to make RSpec your friend (RUS)") -- A short presentation about RSpec testing best practices.
- 🔗 [ Better specs](https://www.betterspecs.org/ " Better specs") -- A web site collecting common styleguide agreements when writing tests in RSpec (note: sometimes the rules are violated so do not blindly follow them).
- 🔗 [Practical test pyramid](https://martinfowler.com/articles/practical-test-pyramid.html "Practical test pyramid") -- An advanced article about testing a real-world application. The examples are in Java but the overal theory is equal to all programming languages. (note: this is Okay if you won't understand anything).
- 🔗 [A book about testing practices](https://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627 "A book about testing practices") -- A nice book showing how to write an application in TDD manner step-by-step. Even thou this is not in Ruby, the overal examples are great and can be applied to Ruby applications as well.
