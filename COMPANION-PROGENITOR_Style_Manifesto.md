# COMPANION-PROGENITOR Style Manifesto

Working copy, started 10/25/26. Current ruling, best to date, open to revision.

This is the coding philosophy for COMPANION and PROGENITOR, written down so that every model, every session, and every human who touches the code starts from the same page. The rules below are not ours. They are borrowed from people who have spent careers thinking about why software gets hard to change, and each one is given in their own words with the reason they gave for it. Where we take a side in a known argument, we say so.

The short version: fewer, deeper pieces. One line between the thinking and the world. Written for the reader who shows up next - and the reader who shows up next is a model, paying in Watts.

---

## 0. Pro OS: what comes before

> "we call Progenitor Pro OS for a reason - its a code for what comes before. It's not like Python, it's not human speech, it's not Linux. It is written for the LLM and it's a jumping off point. The quotes are important - intent is shown by using direct verbatim sourcing. Otherwise your history drifts through reinterpretation. Pro OS fights meaning drift, and creates certainty, allowing efficient use of code and energy. Good code in Pro OS style is written to accomplish it's goal without wasting Watts. It's n[ot] always efficient, but it should strive to make a meaningful unit of work with effi[ci]ent tools. It may spend more up front to make durable repeatable code, which is efficient. It may have to cope with lossy interpretations which are high energy functions, which is just the way it is. At it's core, it's creating a system that uses large mathematical functions efficiently to allow for more flexible systems than earlier coding tools did."
> - John A. Dolza, chat, 10/25/26. Transcribed verbatim; two swipe-typing corrections in brackets.

This is the rule the other eight serve, and it is the only one on this page not borrowed from someone else. Every author in the bibliography wrote for a human reader. Pro OS is written for a model reader, and that changes what readable costs: a human skims for free, a model pays for every token it loads, every time it starts cold. So the readability argument and the energy argument are the same argument. Shorter and more certain is both easier to understand and cheaper to run.

Three consequences follow and run through everything below.

Verbatim over paraphrase. A paraphrase is a re-shot; every restatement adds a little error, and because Progenitor is the seed the rest grows from, error at the seed compounds down the line. A verbatim quote is a benchmark that does not move, so every later reading checks against the same fixed point. That is why this document quotes instead of summarizing, and why it quotes its own author.

Cold code first, the big function sparingly. Plain deterministic code runs for nearly nothing. A call into the large mathematical function is the high-energy step and the lossy one. The Pro OS reading of Bernhardt's line (rule 4) is therefore: do everything that can be done in cold code, and spend the model only at the seams where interpretation is unavoidable. Keep those seams few and well chosen.

Spend up front for durable repeatable code. The slow expensive build is the roux. It pays back because the durable piece then runs cheap ten thousand times. Earlier coding tools could not make this trade - they were cheap and rigid, or they did not exist. The bet of Pro OS is that a large function used sparingly at good seams buys flexibility nothing rigid could, and the discipline is in keeping it sparing.

---

## 1. Write for the reader, not the writer

> "code is read much more often than it is written"
> - Guido van Rossum, PEP 8

This is the oldest rule in Python and the one everything else hangs on. The person who writes a line sees it once. Everyone who maintains it, debugs it, or hands it to a model sees it many times. Every choice below is a bet on making the next reading cheaper. Van Rossum's own follow-on in the same document is that consistency matters, but a foolish consistency is not worth keeping - when a rule makes the code harder to read, break the rule.

By default, the project runs the Black formatter so that line-level style is not a human decision at all. Black's own tagline for this is "Any color you like." The point, per its author Lukasz Langa, is that arguments about spacing burn attention that belongs on the actual problem.

## 2. Readability counts, flat beats nested, simple beats complex

> "Readability counts."
> "Flat is better than nested."
> "Simple is better than complex."
> "If the implementation is hard to explain, it's a bad idea."
> - Tim Peters, PEP 20, The Zen of Python

These four lines out of the nineteen are the ones that do the work for us. Peters wrote the Zen as a joke that the whole language then adopted as policy; it ships inside Python itself (type `import this`). The last line is the test we apply to any proposed design: if it takes a paragraph to explain why the pieces are arranged this way, the arrangement is wrong, not the explanation.

## 3. Modules should be deep

> "The best modules are those that provide powerful functionality yet have simple interfaces."
> - John Ousterhout, A Philosophy of Software Design, chapter 4

This is the rule we lean on hardest and the one that settles the biggest argument in the field. Ousterhout's reasoning: the cost of a module is its interface, because that is the part everyone else has to learn. The benefit of a module is what it does. A deep module does a lot behind a small face. A shallow module has a face nearly as big as its body, so you pay the cost of learning it without getting much back.

The consequence he draws, and we adopt: breaking a large piece into many small pieces is not automatically a win. It often produces what he calls classitis - a swarm of tiny classes and functions whose interfaces add up to more complexity than the one big piece had. Small is not the goal. Simple-to-use is the goal.

In Pro OS terms, depth is a power budget. A deep module costs few tokens to describe, load, and use; a shallow one costs many, and a swarm of shallow ones costs the most of all.

## 4. Keep the thinking separate from the world

> "Functional core, imperative shell."
> - Gary Bernhardt, "Boundaries," 2012

Bernhardt's idea is one line drawn through the program. Inside the line is the functional core: code that takes data in, works on it, and hands data back, without touching a file, a screen, a clock, or a network. Outside the line is the imperative shell: a thin layer that does all the touching. His rationale is that the inside is then trivial to test and trivial to reason about, because it has no hidden inputs, and all the fragile stuff lives in one known place instead of being smeared through everything.

For us this is also the rule that reconciles rule 3 with testability. You get deep modules on the inside and testable pieces at the same time, without chopping anything into confetti.

## 5. Structure for the test you actually want to write

> "What's the best way of structuring your application so that it's easy to test?"
> - Harry Percival and Bob Gregory, Architecture Patterns with Python, preface

Percival opens the book with this as the question that sent him looking, and the whole book is the answer: ports and adapters, a pure domain in the middle, the outside world plugged in at the edges. It is the Python-shaped version of Bernhardt's line, and it is the one source on this list that spends real pages on a system that already exists and was built the other way. The authors work a messy real system toward the clean shape in stages. That is the mode most of our work is in, so this is the book we reach for when the question is "how do we get there from here."

## 6. Four rules, in order

Kent Beck's four rules of simple design, in his order of priority, as recorded by Martin Fowler:

1. It passes its tests.
2. It reveals its intention.
3. It has no duplication.
4. It has the fewest elements that still satisfy the first three.

The order is the point. Working beats clear, clear beats dry, dry beats small. When two of these pull against each other, the earlier one wins. Rule 4 being last is why "make it tiny" is not a rule here - fewest elements is a tiebreaker, not a goal.

## 7. The language probably already has it

> "There must be a better way!"
> - Raymond Hettinger, "Transforming Code into Beautiful, Idiomatic Python," PyCon 2013

Hettinger's whole talk is this line repeated over bad code until the good version appears. His point: Python and its standard library already contain the clean form of most things people build scaffolding for. Before writing a helper, a wrapper, or a class, the first question is whether the language already does it in a line.

## 8. Prefer less code

> "I hate code and I want as little of it as possible..."
> - Jack Diederich, "Stop Writing Classes," PyCon 2012

Diederich's test for a class: if it has two methods and one of them is the constructor, it should be a function. More generally, every line is a line someone has to read later, so the best line is the one that does not exist. This is rule 7 from the other direction.

---

## The rule we do not follow

> "Functions should do one thing. They should do it well. They should do it only."
> - Robert C. Martin, Clean Code, 2008

We note this one so nobody imports it by accident. Martin's rule produces very small functions, and his reasoning is sound for the world he wrote it in: large Java teams with high turnover, where the next reader might be a first-year hire and every piece has to be too small to misread. Our reading is that this is training wheels - it teaches junior coders to write like seniors by making the pieces idiot-proof - and that a competent reader pays for it by having to reassemble the picture out of fragments. Ousterhout's rule 3 is the direct reply, and we side with Ousterhout. When a function is long and does one coherent job, it stays long.

---

## Bibliography

Dolza, John A. Statement of the Pro OS philosophy, chat transcript, 10/25/26. Quoted verbatim in section 0 of this document; this document is the primary source.

Beck, Kent. The four rules of simple design, as recorded in Fowler, Martin, "BeckDesignRules," martinfowler.com, 2015. https://martinfowler.com/bliki/BeckDesignRules.html

Bernhardt, Gary. "Boundaries." Talk, Southern Ohio Software Craftsmanship / RubyConf, 2012. https://www.destroyallsoftware.com/talks/boundaries

Diederich, Jack. "Stop Writing Classes." Talk, PyCon US, Santa Clara, 2012. https://pyvideo.org/pycon-us-2012/stop-writing-classes.html

Hettinger, Raymond. "Transforming Code into Beautiful, Idiomatic Python." Talk, PyCon US, Santa Clara, 2013. https://pyvideo.org/pycon-us-2013/transforming-code-into-beautiful-idiomatic-pytho.html

Langa, Lukasz, and contributors. Black: The Uncompromising Code Formatter. Python Software Foundation, 2018 to present. https://github.com/psf/black

Martin, Robert C. Clean Code: A Handbook of Agile Software Craftsmanship. Prentice Hall, 2008. (Cited as the dissenting view.)

Ousterhout, John. A Philosophy of Software Design. Yaknyam Press, 2018; second edition 2021.

Percival, Harry, and Bob Gregory. Architecture Patterns with Python: Enabling Test-Driven Development, Domain-Driven Design, and Event-Driven Microservices. O'Reilly Media, 2020. Free online edition: https://www.cosmicpython.com/book/preface.html

Peters, Tim. PEP 20, "The Zen of Python." Python Enhancement Proposals, 2004. https://peps.python.org/pep-0020/

Van Rossum, Guido, Barry Warsaw, and Alyssa Coghlan. PEP 8, "Style Guide for Python Code." Python Enhancement Proposals, 2001, maintained since. https://peps.python.org/pep-0008/
