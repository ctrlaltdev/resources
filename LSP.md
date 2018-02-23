# Liskov Substitution Principle - LSP

Substitutability is a principle in object-oriented programming stating that, in a computer program, if S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e. an object of type T may be substituted with any object of a subtype S) without altering any of the desirable properties of T (correctness, task performed, etc.). More formally, the Liskov substitution principle (LSP) is a particular definition of a subtyping relation, called (strong) behavioral subtyping, that was initially introduced by Barbara Liskov in a 1987 conference keynote address titled Data abstraction and hierarchy. It is a semantic rather than merely syntactic relation because it intends to guarantee semantic interoperability of types in a hierarchy, object types in particular. Barbara Liskov and Jeannette Wing formulated the principle succinctly in a 1994 paper as follows:

> Subtype Requirement: Let ϕ ( x ) be a property provable about objects x of type T. Then ϕ ( y ) should be true for objects y of type S where S is a subtype of T.

In the same paper, Liskov and Wing detailed their notion of behavioral subtyping in an extension of Hoare logic, which bears a certain resemblance to Bertrand Meyer's design by contract in that it considers the interaction of subtyping with preconditions, postconditions and invariants.

## Principle

Liskov's notion of a behavioral subtype defines a notion of substitutability for objects; that is, if S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program (e.g. correctness).

Behavioral subtyping is a stronger notion than typical subtyping of functions defined in type theory, which relies only on the contravariance of argument types and covariance of the return type. Behavioral subtyping is provably undecidable in general: if q is the property "method for x always terminates", then it is impossible for a program (e.g. a compiler) to verify that it holds true for some subtype S of T, even if q does hold for T. Nonetheless, the principle is useful in reasoning about the design of class hierarchies.

Liskov's principle imposes some standard requirements on signatures that have been adopted in newer object-oriented programming languages (usually at the level of classes rather than types; see nominal vs. structural subtyping for the distinction):

* Contravariance of method arguments in the subtype.
* Covariance of return types in the subtype.
* No new exceptions should be thrown by methods of the subtype, except where those exceptions are themselves subtypes of exceptions thrown by the methods of the supertype.

In addition to the signature requirements, the subtype must meet a number of behavioral conditions. These are detailed in a terminology resembling that of design by contract methodology, leading to some restrictions on how contracts can interact with inheritance:

* Preconditions cannot be strengthened in a subtype.
* Postconditions cannot be weakened in a subtype.
* Invariants of the supertype must be preserved in a subtype.
* History constraint (the "history rule"). Objects are regarded as being modifiable only through their methods (encapsulation). Because subtypes may introduce methods that are not present in the supertype, the introduction of these methods may allow state changes in the subtype that are not permissible in the supertype. The history constraint prohibits this. It was the novel element introduced by Liskov and Wing. A violation of this constraint can be exemplified by defining a mutable point as a subtype of an immutable point. This is a violation of the history constraint, because in the history of the immutable point, the state is always the same after creation, so it cannot include the history of a mutable point in general. Fields added to the subtype may however be safely modified because they are not observable through the supertype methods. Thus, one can derive a circle with fixed center but mutable radius from immutable point without violating LSP.


[The Liskov Substitution Principle](https://github.com/ctrlaltdev/resources/blob/master/pdf/lsp.pdf)