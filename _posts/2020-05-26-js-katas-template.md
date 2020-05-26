---
title: "JS Katas Template"
tags:
  - javascript
    kata
    tdd
    template
    peer-review
---

I was talking to Vijay, a colleague, about the progress
of [my experiment]({% post_url 2020-05-21-embarking-on-a-journey %}). He opined that it was a bad idea to ditch
the [test-driven learning]({% post_url 2020-05-23-js-katas %}) approach for a structured course.
He thought the test-driven learning approach would provide
more value to me than the course. I agreed with him partly.
On one hand, the course was dragging because it was focused
on absolute beginners. On the other hand, the test-driven
learning was too complicated for me to get a good grip on
it either. My level was somewhere in between these two.

Vijay persuaded me to stay on the test-driven learning path.
I agreed hesitantly. He pointed me to another [overview
essay](http://dmitrysoshnikov.com/ecmascript/javascript-the-core-2nd-edition/) by Dmitry Soshnikov. This article actually helped.
It took me a few hours to read through and understand the
concepts mentioned in the article, but I understood what
was being talked about. Finally, here was something that
was in alignment with my level. However, it wasn't fully
featured with all the concepts of JavaScript. In other
words, it wasn't enough to start coding in JavaScript.
It had a high-level overview of the concepts and working
of the internals of JavaScript that I could visualize and
understand. It was not complete knowledge, but it was a
headstart. With that knowledge, I decided to give the JS
Katas another go.

I got distracted again, but this time it wasn't a huge
distraction. It was probably a good line of thought.
The definition of kata ( according to Wikipedia ) :
> a detailed choreographed pattern of martial arts movements
made to be practised _alone_

While the defintion of kata meant that these exercises were
supposed to be practicsed alone, I was starting to feel too
alone. Maybe, these tests were designed for practice for
seasoned developers who were already familiar with most of
the concepts of JavaScript and only needed some practice
lessons to understand concepts better or to discover new
concepts ( from newer standards ) that they were not aware
of earlier. However, for a beginner like me, this seemed
more difficult to get along and follow on my own. I wished
I had a mentor or at least a peer that I could rely on to
simply cross-check whether the techniques that I was using
to make the tests pass were accurate or not. JavaScript has
been notorious for having multiple ways of achieving the
same objective.

I was thinking of pulling in Vijay to become some kind of a
peer to just validate my test cases but I couldn't figure
out how to "_collaborate_" with him. The exercises were to
be done online. I don't think the online service even had a
notion of an [application state](https://en.wikipedia.org/wiki/Application_state). In fact, I don't think there
was even a direct link to access a particular exercise. Or if
it was there, I couldn't find it. So essentially, there was
no way I could pull Vijay in to look at my tests and give
feedback.

And then, my terminal instincts kicked in. I knew these tests
could definitely be run from the terminal using the `mocha`
module. Then why not run them locally, `commit` and `push`
to a repository where Vijay could take a look in his own time?
The online service was [open source](https://github.com/tddbin/katas). So, that's where I started.
`fork`, `clone`, and attempt to run the tests from the local
repository. Surprise - all tests pass. What?! How?

Then I went down a rabbit-hole figuring out how the actual
service worked. I figured that there was a `gh-pages` branch
which was what was being deployed to the website which had
the failing tests ( though not perfect ). `master` had the
original code with all the tests passing. The failing test
statements were placed with a double comment `////` indicator
which would replace the original line when `npm run build`
was run during the `deploy` stage.

Initially, I thought I just to adapt that `build` script to
make it work for me. The more I looked into the `build` script,
the more I discovered that it was inject more unwanted files.
My requirement was simple - I wanted a local repository in
which all the tests failed from where I could start fixing,
`commit`, `push` and get it peer-reviewed.

Then another idea struck me - why not have a [template
repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-template-repository) that anyone ( like me who wanted to learn )
could fork and start doing the exercises? I thought to take
this idea upstream. I opened [issue #92](https://github.com/tddbin/katas/issues/92) to discuss the
proposal. It took around 4 hours for the developer to respond.
During that time, I had already decided to go with the idea
and had already started working on a proof-of-concept ( PoC )
template repository. By the time I got a response on the issue,
I had already adapted the repository to my requirements,
created a very long README ( with 50% of it being a boring
history on nodeJS ). Then I spent some extra time making some
adjustments to the tests so that all the tests would actually
fail without any `SyntaxError`s. Then I took it back to the
developer at the discussion issue.

While the developer was actually excited about the proposal,
they weren't so happy that I ripped out pretty much the whole
repository apart trying to make it as barebones as possible
for a '**template repository**'. My thought-process was in
that direction. What would a user who would use the template
absolutely need? What would be unnecessary cruft for them?
I guess I went too overboard with my thinking which didn't
make the developer happy about it. They said that they'd
prefer if the `build` script was adapted and re-used to fit
the use-case. While I agreed, I also clarified my thinking
to the developer. I wasn't pushing the new structure hard
anyway.

Also, a new directory structure meant that extra maintenance
overhead or some kind of migration path. That's what the
`build` script was supposed to do except it injected too many
unnecessary files into the directory structure. I even
suggested having another `npm` script like `build-template`
which would mostly re-use the existing `build` script but
without the extraneous files that was unnecessary for the
template repository. The developer was open to that idea
and agreed to it.

I agreed to make an attempt to re-use and adapt the existing
`build` script to publish to a template repository as well.
