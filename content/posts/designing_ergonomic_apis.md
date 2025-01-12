+++
title = "Designing Ergonomic APIs in Rust"
date = "2025-01-11"
draft = true

[taxonomies]
tags=["Rust", "API Design", "Engineering"]
+++
# Designing Ergonomic APIs in Rust

[Rust](https://rustlang.org) is a [great programming language](https://survey.stackoverflow.co/2024/technology#admired-and-desired).
It has a strong type system, memory safety, concurrency as a first class feature, a powerful macro system,
and a focus on developer productivity, in addition to being one of the fastest languages out there.
All of those attributes have been covered by too many blogs, articles, and talks to count.
The ecosystem of crates is growing rapidly,
but many of the foundational crates are of a quality that is hard to find in other languages.
Crates like [Chrono](https://github.com/chronotope/chrono), [Tokio](https://tokio.rs), and [Hyper](https://hyper.rs) are well-designed,
well-documented, and well-maintained.
This isn't to suggest that other languages don't have great ecosystems,
but the quality of core crates in the Rust ecosystem is just on another level.
They're not just good, they're great.
They have a level of correctness, robustness, and attention to detail that is hard to find in any other language.
Moreover, there are a *lot* of examples of really incredible open source projects written in Rust.
I've been blown away by the quality of the crates I've used in Rust since I started working in the language.
The code is so good in fact, that it's honestly pretty intimidating.

I've spent the last several months building libraries in Rust,
and I've come to appreciate the sum of the language's strengths for a reason I haven't seen discussed much:
obvious correctness drives ergonomics.
Because the language is so strict, it's easy to identify where you've taken shortcuts to get things working.
Like probably everyone who's ever written code, I have taken shortcuts I regretted to make deliveries on time.
I've also been fortunate enough to have the opportunity to go back and fix much of that technical debt.
The results have been rather remarkable.

By simply fixing the things that were obviously wrong, I've been able to make my code more correct, robust, and simple.
I've arrived at a place where I have some pretty great ergonomics in some of the APIs I've built
just by fixing the things that were obviously wrong or more onerous than they needed to be.

## What are Ergonomics?

The ergonomics of a programming language are the features that make it easy to write code.
Languages like Go, Python, and Ruby are known for their ergonomics.
They have a simple syntax, powerful standard libraries, and a focus on developer productivity.
Unfortunately their ergonomics come at the cost of making it easy to introduce runtime errors
and structural issues that can be difficult to debug.
It's easy to quickly develop functionality in those languages,
but there tends to be a long tail of bugs and performance issues.
It's easy to get things *mostly right*,
but it's near impossible to get things *exactly right*.

Rust, on the other hand, has a reputation for being difficult to learn and use,
seemingly at odds with the admiration and praise heaped on the language.
It has a steep learning curve, a complex type system,
and a focus on memory safety and performance that forces developers to worry about things they might not even consider in other languages.
Frustratingly, you have to do all of those things before your code even compiles.

The ergonomics of libraries are a little different.
An ergonomic library is one that is easy to use, easy to understand, and hard to misuse.
It's easy to get started with, and it's pleasant to use as intended.
It should be hard to use wrong, handle errors gracefully, and provide helpful feedback when things go awry.

## Ergonomics in Rust

Using the really great crates in the Rust ecosystem is like a masterclass in API design.
Need to serialize a complex data structure?

[Serde](https://serde.rs) makes it easy.
```rust
#[derive(Serialize)]
Struct MyComplexType{...
```

**Boom**, done.

Need to make a complicated  SQL query?
[Diesel](https://diesel.rs") has you covered.
```rust
let results =
      orders::table
      .inner_join(users::table.on(orders::user_id.eq(users::id)))
      .inner_join(order_items::table.on(order_items::order_id.eq(orders::id)))
      .filter(order_items::product_id.eq(product_id))
      .select((users::username,
          diesel::sql_function::sum(order_items::price).as(total_spent)))
      .group_by(users::username)
      .order_by(diesel::sql_function::sum(order_items::price).desc())
      .limit(10)
      .load::<(String, i32)>(conn)?;
```
**Whoa**, that's a big, complex expression that just does exactly what I want.

There are so many incredible examples of great API design in the Rust ecosystem.
Rust's standard library is the only standard library that I've ever used that I would describe as both
"great" and easily readable.

The Rustacean's that really drive the ecosystem write an unbelievable ammount of code.
Not only do they write a lot of code, but they write a lot of really good code.
I've never understood quite how they do it.
Having the opportunity to spend the time to really polish code myself has given me some insight though.
The key is to just keep fixing the things that are obviously wrong.

## What's Wrong?

The Rust language is very specific.
Very little is implicit.
If you want to copy something, you have to call `.clone()`.
If you get an error, you have to explicitly handle it (or call `.unwrap()` 🤮).
If you've coded yourself into a corner with the borrow checker,
you have to refactor your code to fix your access patterns.

Fortunately, it's pretty easy to make sweeping changes in Rust for the same reasons that writing it in the first place is difficult.
The compiler catches cases where you've made a mistake, or missed something that needs to be updated.
The result is that once a major refactor compiles again, the code probably still works as expected.
The compiler very particular, but it has your back, and it's a great feeling.


  It also tends to prickle at that sense of perfectionism that many developers have:
- "I shouldn't need to clone that here, I should be able to pass a reference".
- "I shouldn't need to unwrap that here, I should be able to handle the error".
- "I should be able to prevent that mistake from happening in the first place".
- "I shouldn't need to write that boilerplate, I should be able to use a macro".

This results in a lot of revisiting code that works, but isn't quite right.
Many of the examples above are so subtle in many languages that even experienced developers might not notice them.
In Rust, they're glaringly obvious.

This is very much a double edged sword.
- It's easy to get lost in the weeds of perfectionism
- It's also Rust's superpower

## Fixing the Obvious

The API examples above weren't this good in their first release, or their second, or their tenth.
Their authors made them work, and then they made them better.
They are great examples of what can be accomplished with a lot of time, effort, and dedication.
The crates that are incredible works of engineering today have stood the test of time.
They have fixed the papercuts reported by thousands of users.
They have been polished to a mirror sheen and are a joy to use because so many of the things that are obviously wrong have been addressed.
Someone already found the rough edges you were going to run into,
and either fixed the issue themselves, or reported the issue to the authors who did.
Sometimes fixing the issue was easy, and sometimes it was hard.
Sometimes it required a major refactor, and sometimes it required a new feature.
Sometimes it required working with the language team itself to introduce new language features or fix bugs.

The result is that the really great crates in the Rust ecosystem are a joy to use.
It's not just because the authors are genius programmers(many of them are).
It's because they've spent the time to fix the things that were obviously wrong,
over and over again.
