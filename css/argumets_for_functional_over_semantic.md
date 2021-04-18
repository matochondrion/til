REASONS WHY FUNCTIONAL CSS, OR MIXED, IS OFTEN THE BETTER CHOICE
================================================================================

Why use functional/atomic CSS instead of semantic, BEM, or other modles, and
when not to...

Let's Define Exactly What Atomic CSS Is
--------------------------------------------------------------------------------

https://css-tricks.com/lets-define-exactly-atomic-css/

"Atomic CSS", "Functinal CSS", "Utility Classes" are aliases for:
> Atomic CSS the approach to CSS that favors small, single-purpose classes with
> names based on visual function.

Why Can't We Use Functional CSS and Regular CSS at the Same Time?
--------------------------------------------------------------------------------

https://css-tricks.com/why-cant-we-use-functional-css-and-regular-css-at-the-same-time/

> ...when you need to balance readability, dependencies, and optical
> adjustments, writing regular CSS in a regular old-fashioned stylesheet is
> still my favorite thing in the world. But functional CSS still solves a ton
> of other problems very eloquently.

```html
<div class="margin-bottom-20px">
  <p>Item 1 description goes here</p>
  <button class="btn">Item 1 description goes here</button>
</div>
```

```css
.btn {
  padding: 10px 15px;
  margin: 0 15px 10px;
  // rest of the styles go here
}
```

> ...we use functional classes to make layout adjustments that might be
> specific to a particular feature that we’re working on. However!  That Button
> component is made up of a regular ol’ CSS file.
> 
> ... making brand new CSS files for custom components is way easier than
> trying to make these components out of a ton of classes like margin-*,
> padding-*, etc.
> 
>  ...we solve the following three issues with functional CSS by writing our
>  custom styles in a separate CSS file for this particular instance:
> 
> * Readability
> * Managing property dependencies
> * Avoiding the painful fact that visual design doesn’t like math (optical
>   adjustments)

> ...a lot of CSS property/value pairs are written in relation to one
> another. Say, for example, `position: relative` and `position: absolute`.
> I want to be able to see these dependencies and I believe it’s harder to do
> that with functional CSS. CSS often depends on other bits of CSS and it’s
> important to see those connections with comments or groupings of
> properties/values.
>
> ...what we’re trying to prevent with functional classes...is creating tons of
> stylesheets that do a ton of very specific or custom stuff. Going back to that
> earlier example with the margin beneath those two elements for a second:

```html
<div className='margin-bottom-20px'>
  <p>Item 1 description goes here</p>
  <Button>Checkout item</Button>
</div>
```

> In the past our teams might have written something like this instead:

```html
<div className='cool-feature-description-wrapper'>
  <p>Item 1 description goes here</p>
  <button>Checkout item</button>
</div>
```

> A new CSS file called cool_feature_description_wrapper.scss would need to be
> created in our application:

```css
.cool-feature-description-wrapper {
  margin-bottom: 20px;
}
```

> I would argue that styles like this make our code harder to understand,
> harder to read, and encourages diversions from our library of components. By
> replacing this with a class from our library of **functional classes**, it’s
> much easier to read, and change in the future. It also solves a
> custom solution for our particular needs without forking our library of
> styles.


Semantic CSS Rebuttal
--------------------------------------------------------------------------------

http://nicolasgallagher.com/about-html-semantics-front-end-architecture/

https://adamwathan.me/css-utility-classes-and-separation-of-concerns/

> I had "separated my concerns", but there was still a very obvious coupling
> between my CSS and my HTML. Most of the time my CSS was like a mirror for my
> markup; perfectly reflecting my HTML structure with nested CSS selectors.
>
> My markup wasn't concerned with styling decisions, but my CSS was very
> concerned with my markup structure.
>
> Maybe my concerns weren't so separated after all.
>
> ### "Separation of concerns" is a straw man
>
> When you think about the relationship between HTML and CSS in terms of
> "separation of concerns", it's very black and white.
>
> You either have separation of concerns (good!), or you don't (bad!).
>
> This is not the right way to think about HTML and CSS.
>
> Instead, think about dependency direction.
>
> There are two ways you can write HTML and CSS:
>
> ~~"Separation of Concerns"~~
> CSS that depends on HTML.
>
> Naming your classes based on your content (like .author-bio) treats your HTML
> as a dependency of your CSS.
>
> The HTML is independent; it doesn't care how you make it look, it just
> exposes hooks like .author-bio that the HTML controls.
>
> Your CSS on the other hand is not independent; it needs to know what classes
> your HTML has decided to expose, and it needs to target those classes to
> style the HTML.
>
> In this model, your HTML is restyleable, but your CSS is not reusable.
>
> ~~"Mixing Concerns"~~
> HTML that depends on CSS.
>
> Naming your classes in a content-agnostic way after the repeating patterns in
> your UI (like .media-card) treats your CSS as a dependency of your HTML.
>
> The CSS is independent; it doesn't care what content it's being applied to,
> it just exposes a set of building blocks that you can apply to your markup.
>
> Your HTML is not independent; it's making use of classes that have been
> provided by the CSS, and it needs to know what classes exist so that it
> combine them however it needs to to achieve the desired design.
>
> In this model, your CSS is reusable, but your HTML is not restyleable.
>
> Neither is inherently "wrong"; it's just a decision made based on what's more
> important to you in a specific context.
>
> ~~Choosing reusability~~
>
> The turning point for me came when I read Nicolas Gallagher's About HTML
> semantics and front-end architecture.
> http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
>
> I came away from that blog post fully convinced that optimizing for reusable
> CSS was going to be the right choice for the sorts of projects I work on.
>
> The more a component does, or the more specific a component is, the harder it
> is to reuse.
>
> ### [re: BEM]
> Trying to come up with these component names all of the time is exhausting.
>
> When you make modifiers like `.actions-list--left`, you're creating a whole
> new component modifier just to assign a single CSS property. It's already got
> left in the name, so you're not going to fool anyone that it's "semantic" in
> any way either.
>
> What if we had another component that needed left-align and right-align
> modifiers, would we create new component modifiers for that as well?
>
> ~~We prefer composition to duplication.~~
> So if we had two actions lists, one that needed to be left aligned and
> another that needed to be right aligned, how could we solve that problem with
> composition?
>
> ~~Alignment utilities~~
> To solve this problem with composition, we need to be able to add a new
> reusable class to our component that gives us the desired effect.
>
> We were already going to call our modifers .actions-list--left and
> .actions-list--right, so there's no reason not to call these new classes
> something like .align-left and .align-right:
>
> ```css
> .align-left {
>   text-align: left;
> }
> .align-right {
>   text-align: right;
> }
> ```
>
> The number of classes used here might make you balk at first, but say we did
> want to make this [product card] a real CSS component instead of composing it
> out of utilities. What would we call it?
>
> We don't want to use content-specific names because then our component could
> only be used in one context.
>
> Maybe something like this?
>
> ```css
> .image-card-with-a-full-width-section-and-a-split-section { ... }
> ```
>
> Of course not, that's ridiculous. Instead we'd probably want to compose it
> out of smaller components, like we've talked about before.
>
> Well maybe it's housed in a card. Not all cards have a shadow though so we
> could have a `.card--shadowed` modifier, or we could create a `.shadow
> `utility that could be applied to any element. That sounds more reusable, so
> let's do that.
>
> It turns out some of the cards on our site don't have rounded corners, but
> this one does. We could make it `.card--rounded`, but we have other elements
> on the site that are sometimes rounded the same amount too, and those aren't
> cards. A rounded utility would be more reusable.
>
> ...you can see where I'm going with this.
>
> If you follow that trail far enough with a focus on reusability, building
> this component out of reusable utilities is the natural destination.
>
> ### Enforced consistency
>
> One of the biggest benefits of using small, composable utilities is that
> every developer on your team is always choosing values from a fixed set of
> options.
>
> You could try and enforce consistency through variables or mixins, but every
> line of new CSS is still an opportunity for new complexity; adding more CSS
> will never make your CSS simpler.
>
> If instead, the solution to styling something is to apply existing classes,
> all of a sudden that blank canvas problem goes away.
>
> Want to mute some dark text a little? Add the `.text-dark-soft` class.
>
> Need to make the font size a little smaller? Use the `.text-sm` class.
>
> When everyone on a project is choosing their styles from a curated set of
> limited options, your CSS stops growing linearly with your project size, and
> you get consistency for free.
>
> ### You should still create components
>
> If you need multiple buttons that have this same combination of classes, the
> recommended approach with Tachyons is to create an abstraction through
> templating rather than through CSS.
>
> This is a great approach for a lot of projects, but I still think there are a
> lot of use cases where it's more practical to create a CSS component than it
> is to create a template-based component.
>
> For the sort of projects I work on, it's usually simpler to create a new
> `.btn-purple` class that bundles up those 7 utilities than it is to commit to
> templatizing every tiny widget on the site.
>
> ~~...but build them using utilities first~~
> The reason I call the approach I take to CSS utility-first is because I try
> to build everything I can out of utilities, and only extract repeating
> patterns as they emerge.
>
> If you build things with utilities first and only extract components when you
> see worrisome duplication, you probably never need to extract a navbar
> component.
>
> Instead, your navbar might look something like this:
>
> ```html
> <nav class="bg-brand py-4 flex-spaced">
>   <div><!-- Logo goes here --></div>
>   <div>
>     <!-- Menu items go here -->
>   </div>
> </nav>
> ```
>
> There's just nothing there worth extracting.
>
> ### Isn't this just inline styles?
>
> It's easy to look at this approach and think it's just like throwing style tags
> on your HTML elements and adding whatever properties you need, but in my
> experience it's very different.
>
> With inline styles, there are no constraints on what values you choose.
>
> One tag could be font-size: 14px, another could be font-size: 13px, another
> could be font-size: .9em, and another could be font-size: .85rem.
>
> It's the same blank canvas problem you face when writing new CSS for every
> new component.
>
> Utilities force you to choose: You can't just pick any value want; you have
> to choose from a curated list.
>
> My experience is that building things utility-first leads to more consistent
> looking designs than working component-first, as unintuitive as it might
> sound at first.

Additional Good Information
--------------------------------------------------------------------------------

https://rangle.io/blog/styling-with-functional-css/
https://frontstuff.io/in-defense-of-utility-first-css

Frameworks
--------------------------------------------------------------------------------

https://tailwindcss.com
https://basscss.com
https://tachyons.io
https://css-tricks.com/need-css-utility-library/
