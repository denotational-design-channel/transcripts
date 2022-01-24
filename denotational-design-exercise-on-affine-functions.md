## Denotational Design on Affine Functions - Part 1/5 - Introduction

Today I want to take you through a small exercise in Denotational
Design, a way of designing software developed by Conal Elliott. A full treatment of it is outside the scope of this video and, frankly, my ability since I'm still learning its intricacies.

The core of the idea is to derive implementations from a _denotational_ specification, which is a specification expressed using well-understood mathematical structures.

Accordingly, in Denotational Design the first choice to make is that of the _denotation_: a mathematical structure with simple, precise and well-understood properties. The simplicity of the denotation is very important. Without simplicity we have little chance of understanding its suitability as a model of what we want to implement. A desire for simplicity is a recognition of our limitations as reasoning beings; even the best of us are not particularly rigorous, accept fuzziness and contradictions in our thinking, and have relatively little patience.

For us to say our implementation is _correct_ we must have something against which to measure that correctness. That "something" is the denotation. If it is not simple our derivations and proofs will be correspondingly not simple. Worse, it may be hard to discern whether a complex denotation is a suitable model for what we wish to implement.

Today we will look at a simple example of Denotational Design in
action. As our denotation we will consider the affine functions. You may recall from high school algebra that such functions have the form `f(x) = ax + b` for some constants `a` and `b`.  In this exercise our domain and co-domain are Rational Numbers. Reasoning with the Real Numbers is surprisingly difficult and not currently supported by the Agda Standard Library.

While the denotation is the affine functions themselves, we want to come up with a _representation_ of these functions as data. In this particular example we have chosen pairs of rationals as our
representation. Choosing a good representation is a key creative act in Denotational Design. In this example the choices are limited and happen to be obvious but this is not always the case.

Once we have chosen the representation we can _and should_ define a _meaning function_ that maps from the data type we have chosen to the denotation.

In our case the meaning function is define as follows

```
⟦_⟧ : ℚ × ℚ → (ℚ → ℚ)
⟦ (a , b) ⟧ = λ x → ax + b
```
]

The type of the meaning function is from pairs of rational numbers to functions from rationals to rationals. The definition says that given a pair of rationals `a` and `b` it maps to the function `f(x) = ax +b`. This function is expressed in Agda by the lambda expression `λ x → a * x + b`.

Another question is "what should the API on this representation look like?"  Should we just choose an interface using our taste and experience? While this is the most common choice, perhaps there is a better way.

Another key idea in Denotational Design is that the denotation can _and should_ inform our design of the representation's interface.  A good denotation should be a well-understood mathematical structure replete with elegant and useful mathematical properties. The structure will often have operations that can be performed upon its components, that can then be transferred to the representation with little or no  modification. Guidance from the denotation is far preferable to choosing an interface for the representation based merely on taste or experience, since many mathematical structures have had the benefit of decades (even centuries!) of study and refinement.

Affine functions are instances of a mathematical structure that has great versatility and applicability, known as the monoid. A monoid is a set combined with an binary associative operator. The set must contain a distinguished element that is both the right and left identity of the associative operator. A monoid is expressed, mathematically, as follows:

```
∀ f g h → (f ∙ g) ∙ h ≡ f ∙ (g ∙ h)
∀ f → f ∙ ε ≡ f
∀ f → ε ∙ f ≡ f
```

In fact, affine functions are monoids in at least two ways.

The first way that they are a monoid is under function addition and the constant function that returns zero. The addition of functions `f` and `g` is defined point-wise. That is, `f ⊹ g` is a new function which at  point `x` has value `f x + g x`.

The second way that they are an instance of a monoid is under under function composition and the identity function. Function composition is defined as `f ∘ g = λ x → f (g x)` while identity is just `λ x → x`.

Now we come to a key point that is much more powerful than it first appears.  For a given mathematical structure, _if_ we define analogous structures on the _representation_ and _also_ stipulate that there is a _homomorphism_ -- via the meaning function -- between the analogous structures and the denotation's stuctures then we get two things:

1. We can use the homomorphism properties to _derive_ the
   implementation of the analogous structures on the
   representation. That will be the main focus of this series of
   videos.

2. The laws that hold on the denotation are _transferred_ to the
   representation for free. There is no need to do any further proof.

In this video, I won't go into why the second point is true but it is a key tenet of Denotational Design and it allows us to treat the representation _as if it were the denotation_. The same mathematical properties hold, which allow us to use our understanding of the denotation whenever we use the representation. Doing so can be of immense utility when writing our programs.

Now let's summarise what we're going to do in this series of videos. The API that we will define for our representation -- pairs of rational numbers -- will precisely mirror the mathematical structures that are defined on the denotation -- functions from rational numbers to rational numbers. We will assume that the representation is a monoid and then proceed to derive the operations for the two monoid instances I spoke of earlier: one monoid under function addition and the constant zero function, the other monoid under function composition and the identity function.

One thing I'm really hoping to impart in this presentation is just how good Agda is as an aid to Denotational Design. Its dependent type system allows us to do things that are qualitatively different from what is possible in other languages.

I'll present a technique for deriving implementations from specifications that is not only intuitive and familiar to those who have done equational reasoning, but is machine-checked as well. After all, there is no higher standard than a machine-checked proof.

With that rather long introduction now out of the way, let's proceed to our first derivation. We will consider the fact that the denotation is a monoid under function addition and the constant zero function, and as our very first exercise derive the corresponding addition function on the representation -- pairs of rational numbers.

See you in the next video.
