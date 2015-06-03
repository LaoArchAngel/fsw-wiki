# Long Branch Guidance

Long-running branches present several problems when it comes to [Continuous
Integration]().  This document aims to help reducing the number of long-running
branches as well as provide guidance for when it can't be avoided.

## Problems

Long-running branches present numerous obstacles during development.
However, the three most important are the need for continuous merging,
obscuring changed from the trunk, and bugs.

### Continuous Merging

While working in a long-running branch, you have two options;
you can either merge the main branch continuously to your topic branch,
or you can wait until the very end and perform a single large merge.
The latter option is a bad idea for reasons that will be covered later.
So for now, let us assume that we are merging our main branch every so often.

There is a reason why a large merge at the end sounds appealing,
at least until you actually have to do it.
That reason is that, generally, developers do not like doing merges.
They usually take a while, they are easy to get wrong,
and merging certain files that were not modified by hand (read: project files)
can be confusing.
Like chores and homework, we have a way of coping with merges that humans
(and developers in particular) have practiced and mastered since the dawn of
time. We procrastinate.
There is a highly relevant quote from Michael McCarthy regarding procrastination
and "self-service", but I think I'll leave the telling between
[you and google](http://lmgtfy.com/?q=procrastination+michael+mccarthy&l=1).

More to the point, merging is not something we want to be doing over and over.
And not just because it's painful and annoying.
The truth is that merging can cost a lot.
It costs a lot in time, in interrupted work-flow, and in frustration.
What's worse, continuous merges do not guarantee simple merges.
The larger the difference between your branch and the main branch,
the more that each merge will compound in complexity.
You might think that each merge "resets" the difference between the two branches,
but that's not entirely accurate.
The growing difference between your branch and the main branch is
`SUM(your non-merge commits since last merge) + SUM(all merge conflict resolution commits since you branched)`.

While there are [tools to help alleviate that](www.semanticmerge.com),
the only real cure is to merge your branch into the main branch and be done with it.
And this is assuming that there's only a single long-running branch,
although we will cover the true extent of that pain in...

### Obscured Changes

Merging in often is all well and good, but that's really assuming that everyone
else is merging into the main branch often.
If not (and who are we to complain, right?  Hey kettle! Black much?)
then it doesn't matter how often you pull and merge,
at the end of the day one of you is going to end up with a mother-of-all merges.
(Between you and me, I want you to know, I'm rooting for you.
Never mind that the other guy just read the exact same sentence.
I'm rooting for __YOU__!)

Merge pains aside, another significant problem with obscuring changes is the
potential to block further development.
One of the problems that generally surfaces from long-running branches is when
another developer gets a task that depend on the changes in said branch.
This can lead to several scenarios, none of which are very appealing.
The most common scenario is that the other developer branches from you branch.
This sounds like a good idea at the time, until they finish first and your
branch isn't ready for prime-time.
Conceivably, they should be able to merge into the main branch with a portion of
your branch.  This isn't always the case, however.
While the code the other dev was working on may function, there could be commits
in their history that break other parts of the software because the work is
incomplete. So now we're blocking other people from completing their own work.

Of course, when you're obscuring code changes (especially lots of code changes),
you're generally also obscuring logical changes.  And when you obscure logical
changes to an already changing code base, you're also likely introducint lots
and lots of...

### Bugs

One of the more significant problems with obscured changes is testing.
The shorter the life of a branch, the more it will be tested by other
developers and QA in different branches during the process of testing their own
changes.  There's also a lot less to test, which means it's a lot less likely
to hold up a release, which in turn results in fewer panic attacks and longer
life span for our release manager.
But don't let that keep you from merging your topic into the main branch early.
We still have merge pains to think about.

In short, smaller merges are easier to test.
It is easier to verify that your changes (or others' changes) do not conflict.
In this case we're not even talking about code conflicts. Those are easy.
Our source control can find those.  What source control can't find are the
logical conflicts that crop up.  In these cases, feature testing is often not
enough, and regular run-of-the-mill retro testing won't catch it.
What's left are the painful, all-hands-on-deck retro testing we all dearly
cherish.  We are nothing if not masochists.

As with all massive retros, there is one thing we know for sure.
There will be bugs in production. The difference in confidence between a
short-lived branch and a long-running one is amazing.
No one feels comfortable releasing a long-running branch.
A short-lived branch, however, goes in without a second thought.

## Short-Lived branches

### Changing Our Thought Process

We write code to solve problems.  They may not be bad problems to have,
but regardless, software is the solution we provide.
When we receive projects, or "tasks" (trust me, it's in quotes for a reason),
we immediately think of the solution of the problem in a very linear matter.
That is to say, we think we're at point A, we need to get to point B,
what's the shortest route in between?
This is an excellent way of thinking if we are reading a map.
Unfortunately, we're not reading a map, we're designing the road layout.
As it turns out, you can't pave a street through someone's living room just
because it would be the shortest path.
I suppose the history of the US Railroad would contradict that, but, you know,
different times. And besides, we're not building railroads and this metaphor
is stupid.  Let's move on.

Instead of thinking about paving the shortest route, think about the system as
a whole. What do the changes mean about the direction the company is moving?
What changes are likely to follow? What's the long-term business goal?
How do we make these changes to facilitate growth of the business in the future?
How much wood would a woodchuck chuck if a woodchuck could chuck wood?
Asking the important questions.

The point of this thought process is not to complicate the issue,
but rather to break it down into separate, self-contained chunks.
The solution stops being linear and becomes granular.
These granular portions of the solution are what then make up a branch.

#### Optional Reading: Systems and Sub-systems

In my young budding days of learning to become a programmer,
I spoke with a man who used to teach at Stanford University.
One of the courses he taught was what amounts to a philosophy course for engineers.
In that class, he taught that everything in the universe is a system,
and every system is composed solely of sub-systems.
For example, take a human being.
Every human is an independent system capable of functioning on its own.
A human, in turn, is composed entirely of sub-systems.
Digestive, nervous, dermal, etc.
Again, each of these systems in complete and self-contained.
They all have independent functions.
The most common argument is that none of these systems can stand on its own.
You need a vascular system in order to provide oxygen to the muscular and nervous
systems.  You need a nervous system in order for the vascular and muscular systems
to do anything.  That's true, but it's also true of any other system.  Going back
to the human, a human needs to be part of a viable ecosystem.  As it turns out,
we don't do so well in a vacuum.

This is the thought pattern that helps separate problems into their individual
components. A problem or project is an overview of what we want a system to do,
and it is the job of the engineer to break down what changes belong to which of
the system's sub-systems, or each of the sub-systems' sub-systems, to do the work
quickly, correctly, and adaptively.

A popular question is how far down the rabbit hole do we go?  Getting the perfect
answer to that question takes a lot of practice, but there is a level of
practicality. For example, there is very little reason to ever touch the .NET
Framework.  This isn't a rule, of course, as we make use of our fair share of
extension methods.  We generally don't have to worry about the operating system,
the assembly code, the CPU architecture, or the complexities of the motherboard.
The finance team also doesn't have to worry about the display of information on
the front-end.  The partner solutions team should not have to deal with product
fulfillment. An Order service should not be adding a credit card to customer.
And, of course, just because the project is to remodel the whole kitchen, that
does not mean that replacing the counters is the same job as installing a new
sink.

### The Testable Portion

One way of separating a project into multiple, separately deployable branches is
to identify the independently testable portions.  For example, when writing unit
tests, each public method becomes a testable portion. However, This could lead to
an excessive amount of branches.  Even in the desert a typhoon will drown you.
Instead, we can measure a testable portion as a class.  Each object generally
has a single unit testing class associated with it.

In OOP, each object should be defined by its behavior. In other words, each
object should be independently testable. If an object does not have behavior
then it is anemic, and in some OO circles, not an object but a struct or DTO.
This makes it untestable, and all of changes to it should generally be deployed
independently of anything else.  If you are adding values, make the changes before
the rest of the code.  If you are removing values, do it after.

In Microservices there are [5 architectural constraints](http://nirmata.com/2015/02/microservices-five-architectural-constraints/)
similar to OOP's SOLID. The two we are concerned with here, however, are Minimal
and Complete. Each service should provide a single business function, but no less.
This means that each service should be independently testable, much like an object from OOP.  

One of the reasons for branching based on testable portions is that, even though
the project is incomplete, the branch can be merged and released with some level
of confidence. The more complete the test suite, the higher the confidence.
This way each deployment brings the project closer to completion.  It can even
be set aside for other priorities without fear of losing relevance of the existing
code.

### Small Commits

Commit early and often.  This is one of the [holy tenants of git](http://sethrobertson.github.io/GitBestPractices/).
How does this help us make smaller branches?  Well, it doesn't.  This allows us
to take what would have been a very long branch and gives us the opportunity to
prune it into a smaller one.  How? Through the beautiful process of rebasing.
It's like being told to go to the dentist, isn't it? Some people accuse me of
taking pleasure in my work.

So how does rebasing help us?  Well, an [interactive rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase-i)
allows us to re-order the commits in our branch.  If you commit early and often,
what we should have is the ability to organize those commits so that we can merge
and there are are times you should really avoid it. For example, it's considered
a portion of them. Of course, a lot of caution should be taken when rebasing,
taboo to rebase a branch that has been pushed to a remote repository; or a
branch other people have branched from or are otherwise working on. Doing so
generally leads to the type of popularity you associate to "that one kid who
always pees in the pool".

Rebasing is something we should avoid, but it's a powerful tool if you know how
and when to use it. When it comes to the flexibility of fixing your branches and
releases, git and rebasing are great allies.

### The Power of Planning

We consistently measure the work associated with the projects assigned to us.
One of the processes that can make us more accurate at determining that measure
is actually to appropriately split each project into small-branch-sized tasks.
We should adopt a state of mind that a task isn't dev-complete until a branch is
ready to merge into develop.

Obviously this by itself doesn't help us because all that means is that we can
have one long-running branch that just isn't dev complete.  What it does give us,
however, is visibility. A task and a project should not be the same thing. A
task that does not move from in-progress stands out, and conceals the progress
we are actually making on the project.

The difficulty with good planning is the dependency on a strong knowledge of the
code base. It also requires a familiarity with solving similar problems. That
means that newer developers will depend heavily on their team leaders for
planning.

## Conclusion

Long branch bad. Short branch good. Zug-zug.
