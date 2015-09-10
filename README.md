# semi-iso
pawel-n's weakened partial isomorphisms that work with lenses, with `tuple-morph` hastily torn out so I could build
under GHC 7.10.2.

## Forked?

`tuple-morph` doesn't build under GHC 7.10.2 (not sure about 7.10.1); seems something's funny with type inference
in GADT case analysis, but I didn't look into it closely.

```haskell
-- | Appends two HLists.
(++@) :: HList a -> HList b -> HList (a ++ b)
HNil         ++@ ys = ys
(HCons x xs) ++@ ys = HCons x (xs ++@ ys)
```

```
/home/eric/haskell/tuple-morph/Data/Tuple/Morph/Append.hs:44:2:
    Couldn't match type ‘a’ with ‘x0 : a0’
      ‘a’ is a rigid type variable bound by
          the type signature for
            (++@) :: HList a -> HList b -> HList (a ++ b)
          at Data/Tuple/Morph/Append.hs:42:10
    Expected type: HList a
      Actual type: HList (x0 : a0)
    Relevant bindings include
      (++@) :: HList a -> HList b -> HList (a ++ b)
        (bound at Data/Tuple/Morph/Append.hs:43:1)
    In the pattern: HCons x xs
    In an equation for ‘++@’: (HCons x xs) ++@ ys = HCons x (xs ++@ ys)
```

For now, I just forked `semi-iso` to tear out `tuple-morph`.

## Stack

Put in your `stack.yaml`:

```
 location:
    git: git@github.com:ericbaer/semi-iso
    commit: f37fa1f257025f967adf7ca75b1c21fa0b9b5ac2
```

## Cabal

```
$ git clone https://github.com/ericbaer/semi-iso
$ cd myproject
$ cabal sandbox init
$ cabal sandbox add-source ../semi-iso
```
