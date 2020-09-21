# unison-expect

`unison-expect` lets you create test expectations that result in expressive failure messages.
It is currently in an early-development state.

## Installation

```
.> pull https://github.com/fboeller/unison-expect:.trunk .external.expect.v0
```

## Usage

Create a function and test watches.

```
brokenFib : Nat -> Nat
brokenFib n = 
    if n == 0 then 0 
    else if n == 1 then 1 
    else brokenFib (drop n 1) + brokenFib (drop n 2)

test> brokenFib.tests.t1 = [expectNat (brokenFib 0) (ToEqual 1)]
test> brokenFib.tests.t2 = [expectNat (brokenFib 1) (ToEqual 1)]
test> brokenFib.tests.t3 = [expectNat (brokenFib 3) (ToEqual 3)]
```

Unison evaluates the test watches and prints an expressive failure message indicating the actual value and expected value.

```
Now evaluating any watch expressions (lines starting with `>`)... Ctrl+C cancels.

    7 | test> brokenFib.tests.t1 = [expectNat (brokenFib 0) (ToEqual 1)]
    
    🚫 FAILED Expected 0 to equal 1 (cached)
  
    8 | test> brokenFib.tests.t2 = [expectNat (brokenFib 1) (ToEqual 1)]
    
    ✅ Passed  (cached)
  
    9 | test> brokenFib.tests.t3 = [expectNat (brokenFib 3) (ToEqual 3)]
    
    🚫 FAILED Expected 2 to equal 3 (cached)
```