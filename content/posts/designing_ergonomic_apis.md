+++
title = "Designing Ergonomic APIs in Rust"
date = "2025-01-11"
updated = "2025-01-11"
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
What's more, there are a *Lot* of examples of really incredible open source projects.
I've been blown away by the quality of the crates I've used in Rust since I started working in the language.
The code is so good in fact, that it's honestly pretty intimidating.

I've spent the last several months building a bunch of foundational (for other work) libraries in Rust,
and I've come to appreciate the sum of the language's strengths for a reason I haven't seen discussed as much:
obviously correct ergonomics.
Because the language is so strict, it's easy to identify where you've taken shortcuts to get things working.
Like everyone else, I've had deadlines and deliveries to make, and I've taken shortcuts that I've regretted.
I've also been fortunate enough to have the opportunity to go back and fix those shortcuts.
The results to have been rather remarkable.
By simply fixing the things that were obviously wrong, I've been able to make my code more correct, robust, and simple.
I've arrived at a place where I have some pretty great ergonomics in the APIs I've built
just by fixing the things that were obviously wrong or more onerous than they needed to be.

## What are Ergonomics?

The ergonomics of a programming language are the features that make it easy to write code.
Languages like Go, Python, and Ruby are known for their ergonomics.
They have a simple syntax, powerful standard libraries, and a focus on developer productivity.
Unfortunately their ergonomics come at the cost of making it easy to introduce runtime errors
and structural issues that can be difficult to debug.
It's easy to quickly develop functionality in those languages,
but there tends to be a long tail of bugs and performance issues.

Rust, on the other hand, has a reputation for being difficult to learn and use,
seemingly at odds with the admiration and praise heaped on the language.
It has a steep learning curve, a complex type system,
and a focus on memory safety and performance that forces developers to worry about things they might not even consider in other languages.
Frustratingly, you have to do all of those things before your code even compiles.

The payoff for that up-front effort is that Rust code tends to be more correct, robust, and simple.
The language's strictness forces you to think about the structure of your code,
and prevents you from making mistakes that would be easy to make in other languages.
Refactoring rust code is much easier than in many other languages,
for the same reasons that writing it in the first place is more difficult.
The compiler catches cases where you've made a mistake, or missed something that needs to be updated.
The result is that once a major refactor is compiles again, the code probably still works as expected.

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
**Whoa**, that's a big expression that just says exactly what I want.

There are so many incredible examples of great API design in the Rust ecosystem.
