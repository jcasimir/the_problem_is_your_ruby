# The Problem is Your Ruby

## (Intro)

### Stop Trying

Stop trying to be an expert at Rails.

### Is Rails Difficult?

There has been debate recently as to whether Rails is getting harder to learn. "There's so much to it," people will tell you. Back in the 2005 stone age the API was way smaller, you could quickly master everything you needed to know.

And the API has grown. ActiveSupport now has about a bazillion tools to make your life easier. There are six ways to solve every problem.

Is it hard to become a "Rails Expert" today? Yes. Harder than it used to be? Yes. But it still doesn't matter.

### Rails "Expertise"

There's almost no point in becoming a Rails expert. Unless you're going to be Yehuda Katz or Aaron Patterson, spending your days refactoring the framework, true expertise in Rails is unnecessary.

You probably don't want to be an expert in the framework, you want to be expert in *building applications*. And that challenge hasn't changed.

## Real Skills

Instead, focus on Ruby. Focus on Object-Oriented Programming. Focus on design.

In the end, it really doesn't matter whether you write `article.comments.count == 0` or `article.comments.any?`. Much of what the Rails API gives you is to beautify the last 10% of your codebase. So focus your thinking and learning on the other 90%.

Let's talk about a few areas for exploration.

### Object Oriented Design

Mastering object oriented design is the holy grail of Ruby. I could stand here and tell you to read "Patterns of Enterprise Application Architecture" or "Design Patterns: Elements of Reusable Object-Oriented Software" and then you'll know all that there is to know about OOD.

But, the truth is, I've never read those. I might someday, but that day hasn't come yet.

### How I Got Here

I have a degree in Computer Systems Engineering. I know that's not cool in the Ruby world, but what's really uncool is that I left college knowing jack shit about OO.

After school I got really interested in web applications. I understood the stuff that went into JSP and Servlets, (hint: it's mostly XML configuration), but this database thing was kind of a mystery to me. In my four years of CSE I had never worked with a Database. A friend pointed me towards...

### ( Database Design for Mere Mortals )

This book revolutionized how I think about data. It was the beginning of my understanding of OOP. All of a sudden, when I looked at a person, I didn't see a collection of data mashed together. Instead, I saw discreet child records: addresses, phone numbers, notable dates -- all in a flexible plurality.

### Programming is about Decomposition

That's when I started learning to break things down effectively. A good database design is a great foundation for an effective object design. True excellence at OO has to go beyond mapping database tables to objects, but a poor database design can severely limit your ability to build an effective OO system.

### Rails and ActiveRecord

For a few years I practiced and got really good at breaking down complex data into simple database schema. As I got started with Rails soon after, I now had a way to add capabilities to my data, objects that mixed data and function.

I loved it.

Then, around 2007, we started entering new territory. This idea of REST really entered our consciousness. The first and only book I read on the topic was excellent:

### ( RESTful Web Services )

It was so good that I never finished it. I couldn't wait to get going. It helped me evolve my idea of objects. I began to step away from database dependence.

The idea that first really changed my thinking was modeling "search" as a resource. And since it's a resource, by extension, I'll make it an object. "Search as an OBJECT?!? But it doesn't have a table?!?"

### Objects are Not Tables

Oh. It doesn't matter. There's a difference between data existing and data persisting. We can have data that's critical to our application, critical to our user, and it never hits the database. It's ephemeral, it's here, then it's gone.

Then I truly started seeing objects everywhere. I realized that objects aren't just about data, they're about functionality. How do we divide functions just like a database divides data -- increasing flexibility while decreasing duplication?

### ( Design Patterns in Ruby )

The third piece of the puzzle was, finally, a Ruby subject.

I had learned how to break down data, learned how to model objects with and without data stores, and finally here I learned how to coordinate objects.

Did I memorize the patterns? No. If you say "I implemented the strategy pattern," I would nod and not have any idea what you're talking about.

### What I know about OO

Everything I learned from studying these patterns boils down to this:

* You write programs because of collections
* Single Responsibility Principle / "Just One Idea"
* Preserve Encapsulation (Law of Demeter, "Tell, Don't Ask")
* Clarity over Magic

That's all I know about OO. Let's take a look at some ways to apply them to your Ruby and Rails code.

## Collections

I said "You write programs because of collections." If you just had one thing, one piece of data, you probably wouldn't need a program. You could just "do" whatever you're doing. When we write a program it's because we have hundreds, thousands, millions of things -- collections.

Collections are the gateway drug of good Ruby. Ruby handles collections as comfortably as any language I've used.

### ( Screenshot of Enumerable API )

If the internet could wear out like a book, this page should be tattered on your copy of the web. Humans don't think in `for` loops, we think in collections. Look at these methods and picture their application to real life.

### Partition 

Take `partition` for example. Imagine you want to sort a bowl of holiday M&Ms by color: red or green. How would you naturally do it?

Personally I'd grab two bowls for output, then go through each M&M and put it in the appropriate bowl. That's the same thing that `partition` does: it evaluates a condition and puts each element into one of two sets depending on the result. All the `true`s together, all the `false`s together.

How would an average programmer implement it? They'd probably write a for loop, iterate through the set, find the ones that satisfy the condition, remove them from the original set and put them into a new set. Then at the end, assign all the remainder to the other collection.

Mapping this to the physical world, it's like lining up all the M&Ms, scanning through them one by one, picking out the red ones, then sweeping the results into the green bowl. Does it work? Of course. 

But it's just not as natural. The joy of Ruby is when you write code that mimics your instincts, it follows the natural pathways of your brain. Your brain works with collections, and your Ruby code should too.

## Just One Idea

Where programs go wrong is when ideas get crossed over. If you keep one idea per "box" then you're much more likely to succeed. 

### (Boxes)

What's a "box"? It's

* application
* class
* module
* method
* line of code

You have five essential layers of abstraction. Big ideas go up top, and the little ones fit at the bottom. Novice and intermediate Ruby programmers conflate ideas at all levels, but they tend to completely skip the middle one.

### Modules

Modules are a great way to isolate an idea. They're a tool for wrapping up chunks of related code, giving a shared name.

As a programmer, you're probably kinda in love with organization. Is your work bag a sack with a zipper? No. It's got one pocket for pens, one area for papers, maybe a spot for your reader, a laptop pocket, a spot for the laptop charger, etc.

Modules allow us to create these spaces, the logical home for related code.

### Modules in Rails

When building Rails applications, modules complement your models.

For instance, let's say I'm building a contact manager application. 

### (People and Businesses) 

I'm going to have two types of contacts: people and businesses. In some ways they're similar, like both having phone numbers and physical addresses. But in some ways they're different: people have two or more names, companies just have one.

### Single Table Inheritance

You might be tempted to go down the road of Rails' Single Table Inheritance, like this:

(( STI example for Contact, Person, Company ))

But let me tell you: that's a dark and dangerous road. Personally, I've outlawed STI and never use it.

### Forego Inheritance?

Isn't inheritance the way of proper OO? Yes and no. The core idea there is about reusing shared code, and commonly that's modeled through inheritance.

But using modules is like inheritance taken to the next level. It's code reuse with total flexibility.

### Reuse via Module

In this contact manager, we can achieve the same simplifications using a common module. Like most of my Ruby, I'd write how I want to use the code first:

#### (( Person and Company using Module ))

Then implement the module to make that work:

#### (( Contact Module ))

Now there's no duplicated intelligence and the implementation clearly mimics the real concept.

### Utility Objects

Modules can also give a logical home to processor functionality. For instance, imagine we're writing a simple blog engine with articles and comments. We want to automatically handle URLs in text, turning them into HTML links.

We could implement a function like this:

#### (( Article class with linkify_text))

Then in the comment:

#### (( Comment class with linkify_text))

And obviously we could reduce that duplication by extracting a module and including it like we did before:

#### (( TextDecorator, Article, and Comment ))

But that feels a little weird to me. Including a module implies that this functionality is core to what this object does. In our previous scenario, a person was essentially an extension of `Contact`, so the include made sense.

Here, though, an Article is not, by nature, made up of a TextDecorator. The TextDecorator is a utility used by the Article. As such, I'd rather not `include` it and, instead, call a function on the module itself.

#### (( TextDecorator, Article, Comment ))

We have reduced code repetition and more clearly separated concerns.

## Clarity over Magic

We all know that Ruby has tremendous powers for magic. We can metaprogram indirections until we create a tangled web impossible to sort out.

Refactoring sometimes gets a bad rap because people see it as pointless -- it already worked, why change it? Refactoring is just about making code shorter, right?

And we can always make code shorter. We do have Perl roots, after all.

### Refactoring

But that's not what refactoring is about, it's not what expert Rubyists do. Yes, refactoring often results in shorter code, but that's only a side effect. We refactor to amplify clarity. To bring the implementation closer to the idea.

### Implementation and Ideas

Computers don't think, they don't have ideas. Our jobs are, essentially, to translate the complex ideas of the world into language these electronics can understand. Once the basic meaning, the basic functionality, is achieved, we must work, constantly, to bring the implementation closer to the concept.

As Rails developers, it's easy to fall in love with the new shiny. Let's look at a few ways we can amplify clarity by keeping it simple.

### Scopes

In Rails 2, scopes were amazing because we could compose multiple method calls together and, in the result, only fire one query:

#### (( Rails 2 Scopes ))

But, in Rails 3 and the AREL model, we can achieve that same gain by writing a class method:

#### (( Scope and class method side by side ))

The functionality is identical. Which is better? Which is more simple? Try adding a parameter:

#### (( Scope with Lambda, Class Method with Argument ))

Is there really any debate here? The class method is more clear. It follows our normal patterns. Is it more lines of code? Yes. But increasing clarity is always worth extra lines of code.

### ActiveSupport::Concern

A second example is `ActiveSupport::Concern`. Let's bring back our `Contact` module from before:

#### (( Original Contact Module ))

Then we can add `ActiveSupport::Concern` and reduce the implementation to this:

#### (( Contact with AS::C ))

Fewer lines of code? Yes. Is it more clear? I'm not sure. How does it work? To use it, do you have to know about the core Ruby language? About details of the AS::C library? Both. 

Really, it's a crutch. Some people are scared of this syntax:

#### (( Original Contact ))

Or say there's too much boiler plate. Well, don't be scared. There are only four ideas here:

* Extend will add class methods
* Include will add instance methods
* .send allows us to trigger these private methods from the outside
* Included is called when the module is included and passes the including class in as a parameter

If you can understand those four ideas, then there's nothing complex. The implementation is close to the idea. "Hey, including class, take these as class methods, take these as instance methods, and run this bit of code inside yourself."

`ActiveSupport::Concern` reduces code length but hurts clarity.

### Validations

I love teaching people about validations in Rails when they're first starting out. It's a great feature that you probably don't think much about. I teach people to write validations like this:

#### (( Several Validations using validates_x_of ))

Then, invariably, someone brings up this syntax:

#### (( One complex one using "validates" method ))

And tells me that it's better because it is fewer lines of code. We know that's a fallacy, but there's a more important argument. 

We don't like inline comments in Ruby because the code should be readable, like English, itself.

Close your eyes and let me read this to you. (( VALIDATES X presence true length 1..10 uniqueness true)). Can you parse it? Sure, because your brain has been bent by programming. But if I read that to a normal person off the street, what sense would they make of it? Not much.

#### (( Validates X of ))

What if I read them this? Will they get the idea? I bet they do. Will it take me twice as many words? Yes! Functionality and clarity are the only values, length doesn't matter.

#### Reducing Validation Repetition

( Use an each loop to validate multiple attributes )

### Clarity Always Wins

Always, always choose clarity in your code. Clarity is not cute and it's not magical. It just communicates, and that's your whole job.

## Conclusion

Give up the idea of being a Rails expert, because it doesn't matter. Instead, sharpen your expertise at breaking down complex systems, and your skills will never become antiquated.

## Additional Ideas

* Rails-isms that suck
  * "Base", instead "Nodes::Node", Plural::Singular
  * People don't know how to use super
  * Premature abstraction
