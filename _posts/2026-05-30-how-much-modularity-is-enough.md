---
title: "How Much Modularity is Enough?"
excerpt: >-
  How far should we pursue code modularity? A practical look at SOLID,
  single responsibility, when to modularize a feature versus shipping it,
  and how AI assistants fit into the workflow.
date: 2026-05-30
tags: ["programming", "opinion"]
header:
  teaser: /assets/images/posts/how-much-modularity-is-enough/cover.jpg
---

Sometimes I question myself: how far should I — or we — pursue code modularity?

The ideal answer is to make the entire codebase of a project modular. In reality, that can be difficult to achieve. In a company, we have different stakeholders with different needs and requests, and especially as deadlines approach, modularity is often the first thing abandoned as long as the product ships. On a personal project, you might not think much about modularity either — as long as it ships. But in commercial projects, you need to think about modularity, because it helps you maintain a large codebase across different people and teams and makes knowledge transfer easier.

By using modularity, you isolate the codebase into separate modules that interact with each other either directly via hard references or indirectly via base interfaces or delegates. Modularizing your code also lets you hide internal complexity and expose only what the user needs to know, while providing ways to extend the module's capabilities through component-based design, class inheritance, or interface extension.

---

### Principles and Patterns

To make your code modular, you can apply the **SOLID**, **DRY**, and **KISS** principles, as well as design patterns that help you organize and solve code problems. That said, simply knowing these principles won't make you proficient in using them — you need hands-on experience and exposure to best practices to truly understand when and how to apply them.

When I first learned about SOLID, I ended up adding interfaces to almost all of my code, and my mentor laughed about it. It was quite the fun learning experience.

In my humble opinion, the most important principle of all is **Single Responsibility** — I believe the rest stem from it. With single responsibility, you can implement DRY and KISS simultaneously, and from there, apply other SOLID principles and appropriate design patterns naturally.

#### Single Responsibility Principle

A class or function should do one thing and do it well. This principle also makes unit testing much easier, since you can confidently verify that a function "does it well."

#### Open/Closed Principle

Code should be open for extension but closed for modification. If your code already incorporates single responsibility, you can design functions or classes to be extendable. The challenge I personally run into is that we don't always know in advance what needs to be extensible. We can predict, but we might miss something — so sometimes modification is unavoidable.

#### Liskov Substitution Principle

A child class should be able to replace its parent class without breaking the program. This also ties back to single responsibility. For example, you might have an `Enemy` base class with `move()` and `attack()` methods — but then a game designer requests a static turret enemy, leaving `move()` empty. Instead, you could separate concerns into an `Enemy` base class and an `IMoveable` interface.

#### Interface Segregation Principle

Don't force code to depend on things it doesn't use. When building a game, it's tempting to create a broad `ICharacter` interface, but you'll likely end up with empty implementations since not all characters share the same behavior. A better approach is to split it into focused interfaces: `IMoveable`, `IDamageable`, `IDateable`, etc.

Some interfaces are obvious from the start — like `ITickable` or `IStartable` for systems outside the main game loop — but for gameplay code, you might not realize you need this principle until the codebase has grown.

#### Dependency Inversion Principle

Depend on abstractions (interfaces), not concrete implementations. For example, in a cross-platform game with a save system — Firebase on mobile, Steam Cloud on PC, and a proprietary API on console — you'll still end up with some platform-specific branching, but you can define an `ISaveData` interface and let each platform implement it. Gameplay code then only needs to call `save()` or `load()` without knowing the underlying implementation.

*As a side note: while writing this, I re-read about SOLID and realized I still have more to learn and much room to improve my understanding.*

---

### When to Modularize

In my opinion, code that must be strictly modularized is the **core** of a project — the foundational features that will always exist and can be reused across different projects. Features that are still in active development or prototyping, however, can afford looser modularity. When a feature is rapidly changing and iterating, adding layers of abstraction can slow things down.

As a coder's experience grows, even loosely written code becomes more manageable. Once a feature is considered complete, you can revisit and modularize it. There may be updates in the future, but we can't guard against every unknown change — it's better to update the module again when needed than to over-engineer for uncertainty.

---

### AI as a Coding Assistant

With the rise of AI coding tools, this workflow becomes even more practical. You can quickly prototype features with AI, and once a feature is accepted, ask AI to help modularize it. You can also ask AI to follow your project's coding standards during prototyping so it doesn't stray too far, helping you catch bugs early — whether caused by the AI or yourself.

AI is also very helpful during the modularization phase, offering suggestions and insights you might not have considered. However, you need to review its output critically rather than accepting it blindly, since the suggested solution may not suit your project, may be over-engineered, or may be unnecessarily complex. Keep the AI in check.

---

### A Real-World Example

Take *Monster Hunter* as an example. The core modules established early on — inventory, save system, weapon system, damage system — are relied upon by every monster and hunter, especially during combat. The concrete behavior of weapons may change (as with some weapon movesets in *Monster Hunter World* and *Wilds*), but the underlying module that handles it should remain relatively stable.

Monster AI behavior, on the other hand, is more iterative — programmers try different approaches, designers create and refine monster behaviors through feedback cycles, before eventually landing on something solid enough to be modularized and reused for other monsters. This is purely my assumption based on observing the series and my own experience.

---

### Closing Thoughts

Even with the rise of AI, we still have a duty to keep learning — so we can use AI to assist our work rather than blindly trust it.

Finally, with all this modularity, you end up with a bunch of loosely coupled modules — and some that are slightly more coupled. There's usually still one place in the project where things come together: your main function, player character, player controller, game state, or some central manager. That's the place where everything kicks off and orchestrates the whole project. That central hub is inevitable — and that's okay.

---

*Cover photo by [Ksenia Pixelesse](https://unsplash.com/@pixelesse?utm_source=noodle-eater&utm_medium=referral) on [Unsplash](https://unsplash.com/photos/a-pile-of-blue-puzzle-pieces-on-top-of-a-table-W0YSKWCKDS8?utm_source=noodle-eater&utm_medium=referral).*
