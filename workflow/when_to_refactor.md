Refactor in a Separate Commit Than the Feature - Before the Feature if Possible
================================================================================

Where
--------------------------------------------------------------------------------

> In general, if the refactoring is really outside the scope of the branch I
> would recommend making it a separate branch.
> 
> 1. Review *complexity*. If a branch has more than one functional change commit
>    or more than one refactoring commit it becomes time-consuming to review the
>    result, since now each commit has to be reviewed separately.
> 2. *Risk*. Any refactoring, no matter how well the code is tested, has some
>    non-zero risk of breaking things. Making a separate branch with a
>    refactoring allows splitting that risk from the more obvious risk of the
>    functional change.
> 3. Relevance. Is the suggested refactoring a natural consequence of the
>    functional change? This may be for example breaking up a class hierarchy
>    because the inheritance is no longer natural. If so it might be appropriate
>    to do it in the same commit as the functional change, as per the
>    red-green-refactor TDD cycle.
>
> source: https://softwareengineering.stackexchange.com/questions/414466/in-code-review-should-i-ask-to-do-a-refactor-outside-of-the-scope-in-a-pull-req

> If you combine refactoring and making a change to your code into the same
> commit, you are going to have a bad time.
> 
> http://jakegoulding.com/blog/2012/11/04/refactor-and-make-changes-in-different-commits/


When
--------------------------------------------------------------------------------

> * The best time to consider refactoring is **before** adding any updates or
>   new features to existing code.
> * Cleaning current code before adding new will improve the quality of the
>   product itself, and make it easier for future developers to build on the
>   original code.
> 
> * Another time to think about refactoring is **right after** you’ve delivered
>   a product to market.
> * This is the perfect time to do a little housekeeping, as chances are
>   developers now have more availability to work on refactoring before moving
>   on to the next job.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

When Not to Refactor
--------------------------------------------------------------------------------

> * When an application needs to be completely revamped from the start. It would
>   be much more efficient to simply start from scratch.
> 
> * If you are trying to get a product to market within a set time frame.
>   - Refactoring can be like going down the proverbial rabbit hole: Once you
>     start, it can become quite time-consuming.
>   - Adding any additional coding or testing to an already tight timeline will
>     lead to frustration and additional cost for your client.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

Why
--------------------------------------------------------------------------------

> * The basic purpose of code refactoring is to make the code more efficient
>   and maintainable.
> * This is key in reducing technical cost since it’s much better to clean up
>   the code now than pay for costly errors later.
> * Improves readability, makes the QA and debugging process go much more
>   smoothly.
> * Can certainly help prevent them in the future.
> * Avoid "Code Rot"
>   - Code rot results from duplicate code, myriad patches, and bad
>     classifications
>   - Different developers writing in their own styles can also contribute...as
>     there is no cohesion to the overall coding script.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

How
--------------------------------------------------------------------------------

* Red-Green-Refactor
* Refactoring by Abstraction
* Composing Method
* Simplifying Methods
* Moving Features Between Objects
* Preparatory Refactoring
* Other Methods

### Red-Green-Refactor

> Break refactoring down into three distinct steps:
> 
> 1. Stop and consider what needs to be developed. [RED]
> 2. Get the development to pass basic testing. [GREEN]
> 3. Implement improvements. [REFACTOR]
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Refactoring by Abstraction

> Primarily when there is a large amount of refactoring to do. Abstraction
> involves **class inheritances**, **hierarchy**, and **extraction** to 
> reduce unnecessary duplications in software code.
> 
> One example of abstraction is the **Pull-Up/Push-Down** method. These are two
> opposite forms of refactoring involving classes.
> 
> * The **Pull-Up** method pulls code parts into a superclass in order to
>   eliminate code duplication.
> * **Push-Down** takes it from a superclass and moves it down into subclasses.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Composing Method

> Involves streamlining code in order to reduce duplications:
> 
> * **Extraction** involves breaking down the code into smaller chunks in order
>   to find and “extract” fragmentation.
>   - The fragmented code is then moved to a separate method and replaced with
>     a call to this new method.
>   - In addition to
>   - The **method**, extraction can involve **class**, **interface**, and
>     **local variables** as well.
> * **Inline refactoring** reduces unnecessary methods while simplifying the
>   code.
>   - By finding all calls to the method and replacing them with the content of
>     the method, the method can then be deleted.
>     [I haven't heard of this being promoted, it's usually the other away
>     around?]
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Simplifying Methods

> The older code gets, the more garbled and complicated it tends to be.
> Consolidate conditional fragments and expressions and replace conditionals
> with polymorphism.
> 
> * Tweaking the interaction between classes.
> * Adding, removing, and introducing new parameters along with replacing
>   parameters with explicit methods and method calls
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Moving Features Between Objects

> Creating new classes and moving functionality between old
> and new classes.
> 
> * When one class has too much going on, it’s time to move some of that code to
>   another class.
> * Or if a class isn’t really doing that much, you can move its features to
>   another class and delete it altogether.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Preparatory Refactoring

> In his book Refactoring: Improving the Design of Existing Code author Martin
> Fowler talks about the process of preparatory refactoring.
> 
> This is done when a developer notices the need for refactoring while adding a
> new feature, so it’s actually a part of a software update as opposed to a
> separate refactoring process.
> 
> By noticing that the code needs to be updated at that moment, the developer is
> doing his or her part to reduce future technical debt.
> 
> > “It’s like I want to go 100 miles east but instead of just traipsing through
> > the woods, I’m going to drive 20 miles north to the highway and then I’m
> > going to go 100 miles east at three times the speed I could have if I just
> > went straight there. **When people are pushing you to just go straight there,
> > sometimes you need to say, ‘Wait, I need to check the map and find the
> > quickest route.’** The preparatory refactoring does that for me.”
> > - Software developer Jessica Kerr
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

### Other Methods

> There are dozens of other methods for code refactoring that can be found at
> Martin Fowler’s website and at Refactoring.com.
> 
> Will depend on the size and scope of your solution, the time-frame you have
> to perform refactoring, and the number of people available to assist in the
> overall process.
> 
> source: https://www.altexsoft.com/blog/engineering/code-refactoring-best-practices-when-and-when-not-to-do-it/

