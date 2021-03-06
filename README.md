# Validation

![NICTA](http://i.imgur.com/Ns5hntl.jpg)

Several data-types like Either but with differing properties and type-class
instances.

Library support is provided for those different representations, include
`lens`-related functions for converting between each and abstracting over their
similarities.

Download from [hackage](http://hackage.haskell.org/package/validation).

* `AccValidation`

  The `AccValidation` data type is isomorphic to `Either`, but has an instance
  of `Applicative` that accumulates on the error side. That is to say, if two
  (or more) errors are encountered, they are appended using a `Semigroup`
  operation.

  As a consequence of this `Applicative` instance, there is no corresponding
  `Bind` or `Monad` instance. `AccValidation` is an example of, "An applicative
  functor that is not a monad."

* `Validation`

  The `Validation` data type is isomorphic to `Either` and has a `Monad`
  instance that does the same as `Either`. The only difference to `Either` is
  the constructor names and surrounding library support.

* `ValidationT`

  The `ValidationT` data type is the monad transformer for `Validation`. An
  instance of `MonadTrans` is provided for `(ValidationT err)`. Due to the
  arrangement of the `ValidationT` type constructor, which permits a `MonadTrans`
  instance, there is no possible `Bifunctor` instance. Consequently, the
  `ValidationB` data type provides a `Bifunctor` instance (but not a
  `MonadTrans` instance). Library support is provided to exploit the isomorphism
  to `ValidationB`.

  Note that since `AccValidation` is not a monad, there is also no corresponding
  monad transformer for this data type.

* `ValidationB`

  The `ValidationB` data type is similar to the monad transformer for
  `Validation` (`ValidationT`), however, due to the arrangement of the
  `ValidationB` type constructor, which permits a `Bifunctor` instance, there is
  no possible `MonadTrans` instance. Consequently, the `ValidationT` data type
  provides a `MonadTrans` instance (but not a `Bifunctor` instance). Library
  support is provided to exploit the isomorphism to `ValidationT`.

* `Validation'`

  The `Validation' err a` type-alias is equivalent to 
  `ValidationT err Identity a` and so is isomorphic to `Either` and others.
  Libraries are supplied accordingly.
