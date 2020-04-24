# Bit Twiddling Hacks
> This project provides code snippets of Sean Anderson's compilation of [bit manipulation tricks](https://graphics.stanford.edu/~seander/bithacks.html) in [Python](https://www.python.org/) to make it easy to follow for those who do not have experience in [C](https://en.wikipedia.org/wiki/C_(programming_language)).

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Acknowledgement](#acknowledgement)
- [License](#license)
- [Contents](#contents)
  - [About the operation counting methodology](#about-the-operation-counting-methodology)
  - [Compute the sign of an integer](#compute-the-sign-of-an-integer)
  - [Detect if two integers have opposite signs](#detect-if-two-integers-have-opposite-signs)
  - [Compute the integer absolute value (abs) without branching](#compute-the-integer-absolute-value-abs-without-branching)
  - [Compute the minimum (min) or maximum (max) of two integers without branching](#compute-the-minimum-min-or-maximum-max-of-two-integers-without-branching)
  - [Determining if an integer is a power of 2](#determining-if-an-integer-is-a-power-of-2)
  - [Sign extending](#sign-extending)
    - [Sign extending from a constant bit-width](#sign-extending-from-a-constant-bit-width)
    - [Sign extending from a variable bit-width](#sign-extending-from-a-variable-bit-width)
    - [Sign extending from a variable bit-width in 3 operations](#sign-extending-from-a-variable-bit-width-in-3-operations)
  - [Conditionally set or clear bits without branching](#conditionally-set-or-clear-bits-without-branching)
  - [Conditionally negate a value without branching](#conditionally-negate-a-value-without-branching)
  - [Merge bits from two values according to a mask](#merge-bits-from-two-values-according-to-a-mask)
  - [Counting bits set](#counting-bits-set)
    - [Counting bits set, naive way](#counting-bits-set-naive-way)
    - [Counting bits set by lookup table](#counting-bits-set-by-lookup-table)
    - [Counting bits set, Brian Kernighan's way](#counting-bits-set-brian-kernighans-way)
    - [Counting bits set in 14, 24, or 32-bit words using 64-bit instructions](#counting-bits-set-in-14-24-or-32-bit-words-using-64-bit-instructions)
    - [Counting bits set, in parallel](#counting-bits-set-in-parallel)
    - [Count bits set (rank) from the most-significant bit upto a given position](#count-bits-set-rank-from-the-most-significant-bit-upto-a-given-position)
    - [Select the bit position (from the most-significant bit) with the given count (rank)](#select-the-bit-position-from-the-most-significant-bit-with-the-given-count-rank)
  - [Computing parity (1 if an odd number of bits set, 0 otherwise)](#computing-parity-1-if-an-odd-number-of-bits-set-0-otherwise)
    - [Compute parity of a word the naive way](#compute-parity-of-a-word-the-naive-way)
    - [Compute parity by lookup table](#compute-parity-by-lookup-table)
    - [Compute parity of a byte using 64-bit multiply and modulus division](#compute-parity-of-a-byte-using-64-bit-multiply-and-modulus-division)
    - [Compute parity of word with a multiply](#compute-parity-of-word-with-a-multiply)
    - [Compute parity in parallel](#compute-parity-in-parallel)
  - [Swapping Values](#swapping-values)
    - [Swapping values with subtraction and addition](#swapping-values-with-subtraction-and-addition)
    - [Swapping values with XOR](#swapping-values-with-xor)
    - [Swapping individual bits with XOR](#swapping-individual-bits-with-xor)
  - [Reversing bit sequences](#reversing-bit-sequences)
    - [Reverse bits the obvious way](#reverse-bits-the-obvious-way)
    - [Reverse bits in word by lookup table](#reverse-bits-in-word-by-lookup-table)
    - [Reverse the bits in a byte with 3 operations (64-bit multiply and modulus division)](#reverse-the-bits-in-a-byte-with-3-operations-64-bit-multiply-and-modulus-division)
    - [Reverse the bits in a byte with 4 operations (64-bit multiply, no division)](#reverse-the-bits-in-a-byte-with-4-operations-64-bit-multiply-no-division)
    - [Reverse the bits in a byte with 7 operations (no 64-bit, only 32)](#reverse-the-bits-in-a-byte-with-7-operations-no-64-bit-only-32)
    - [Reverse an N-bit quantity in parallel with 5 * lg(N) operations](#reverse-an-n-bit-quantity-in-parallel-with-5--lgn-operations)
  - [Modulus division (aka computing remainders)](#modulus-division-aka-computing-remainders)
    - [Computing modulus division by 1 << s without a division operation (obvious)](#computing-modulus-division-by-1--s-without-a-division-operation-obvious)
    - [Computing modulus division by (1 << s) - 1 without a division operation](#computing-modulus-division-by-1--s---1-without-a-division-operation)
    - [Computing modulus division by (1 << s) - 1 in parallel without a division operation](#computing-modulus-division-by-1--s---1-in-parallel-without-a-division-operation)
  - [Finding integer log base 2 of an integer (aka the position of the highest bit set)](#finding-integer-log-base-2-of-an-integer-aka-the-position-of-the-highest-bit-set)
    - [Find the log base 2 of an integer with the MSB N set in O(N) operations (the obvious way)](#find-the-log-base-2-of-an-integer-with-the-msb-n-set-in-on-operations-the-obvious-way)
    - [Find the integer log base 2 of an integer with an 64-bit IEEE float](#find-the-integer-log-base-2-of-an-integer-with-an-64-bit-ieee-float)
    - [Find the log base 2 of an integer with a lookup table](#find-the-log-base-2-of-an-integer-with-a-lookup-table)
    - [Find the log base 2 of an N-bit integer in O(lg(N)) operations](#find-the-log-base-2-of-an-n-bit-integer-in-olgn-operations)
    - [Find the log base 2 of an N-bit integer in O(lg(N)) operations with multiply and lookup](#find-the-log-base-2-of-an-n-bit-integer-in-olgn-operations-with-multiply-and-lookup)
  - [Find integer log base 10 of an integer](#find-integer-log-base-10-of-an-integer)
  - [Find integer log base 10 of an integer the obvious way](#find-integer-log-base-10-of-an-integer-the-obvious-way)
  - [Find integer log base 2 of a 32-bit IEEE float](#find-integer-log-base-2-of-a-32-bit-ieee-float)
  - [Find integer log base 2 of the pow(2, r)-root of a 32-bit IEEE float (for unsigned integer r)](#find-integer-log-base-2-of-the-pow2-r-root-of-a-32-bit-ieee-float-for-unsigned-integer-r)
  - [Counting consecutive trailing zero bits (or finding bit indices)](#counting-consecutive-trailing-zero-bits-or-finding-bit-indices)
    - [Count the consecutive zero bits (trailing) on the right linearly](#count-the-consecutive-zero-bits-trailing-on-the-right-linearly)
    - [Count the consecutive zero bits (trailing) on the right in parallel](#count-the-consecutive-zero-bits-trailing-on-the-right-in-parallel)
    - [Count the consecutive zero bits (trailing) on the right by binary search](#count-the-consecutive-zero-bits-trailing-on-the-right-by-binary-search)
    - [Count the consecutive zero bits (trailing) on the right by casting to a float](#count-the-consecutive-zero-bits-trailing-on-the-right-by-casting-to-a-float)
    - [Count the consecutive zero bits (trailing) on the right with modulus division and lookup](#count-the-consecutive-zero-bits-trailing-on-the-right-with-modulus-division-and-lookup)
    - [Count the consecutive zero bits (trailing) on the right with multiply and lookup](#count-the-consecutive-zero-bits-trailing-on-the-right-with-multiply-and-lookup)
  - [Round up to the next highest power of 2 by float casting](#round-up-to-the-next-highest-power-of-2-by-float-casting)
  - [Round up to the next highest power of 2](#round-up-to-the-next-highest-power-of-2)
  - [Interleaving bits (aka computing Morton Numbers)](#interleaving-bits-aka-computing-morton-numbers)
    - [Interleave bits the obvious way](#interleave-bits-the-obvious-way)
    - [Interleave bits by table lookup](#interleave-bits-by-table-lookup)
    - [Interleave bits with 64-bit multiply](#interleave-bits-with-64-bit-multiply)
    - [Interleave bits by Binary Magic Numbers](#interleave-bits-by-binary-magic-numbers)
  - [Testing for ranges of bytes in a word (and counting occurances found)](#testing-for-ranges-of-bytes-in-a-word-and-counting-occurances-found)
    - [Determine if a word has a zero byte](#determine-if-a-word-has-a-zero-byte)
    - [Determine if a word has a byte equal to n](#determine-if-a-word-has-a-byte-equal-to-n)
    - [Determine if a word has byte less than n](#determine-if-a-word-has-byte-less-than-n)
    - [Determine if a word has a byte greater than n](#determine-if-a-word-has-a-byte-greater-than-n)
    - [Determine if a word has a byte between m and n](#determine-if-a-word-has-a-byte-between-m-and-n)
    - [Compute the lexicographically next bit permutation](#compute-the-lexicographically-next-bit-permutation)
- [Contributing](#contributing)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Acknowledgement
> Hats off to Sean Eron Anderson, seander@cs.stanford.edu, for creating https://graphics.stanford.edu/~seander/bithacks.html

I **DO NOT** own any of this. The following contents comes directly from the above link. I will be happy to transfer the ownership of this repository to the original author, Sean Eron Anderson.

 I will not alter the explanations provided by Sean because they provide a lot of context. Where necessary, I will add a *NOTE* section as a quote, see below notation, or just as comments within the Python code.

> *example quote*

# License
[License Information](LICENSE.md)


# Contents

## About the operation counting methodology
When totaling the number of operations for algorithms here, any Python operator is counted as one operation. Intermediate assignments, which need not be written to RAM, are not counted. Of course, this operation counting approach only serves as an approximation of the actual number of machine instructions and CPU time. All operations are assumed to take the same amount of time, which is not true in reality, but CPUs have been heading increasingly in this direction over time. There are many nuances that determine how fast a system will run a given sample of code, such as cache sizes, memory bandwidths, instruction sets, etc. In the end, benchmarking is the best way to determine whether one method is really faster than another, so consider the techniques below as possibilities to test on your target architecture.

## Compute the sign of an integer
## Detect if two integers have opposite signs

```python
def integers_opposite_signs(x, y):
    """
    Given two integers x and y returns True iff
    x and y have opposite signs
    """
    return (x ^ y) < 0
```

Manfred Weis suggested I add this entry on November 26, 2009.

## Compute the integer absolute value (abs) without branching

```python
import sys
CHAR_BIT = sys.int_info.bits_per_digit
SIZE_INT = sys.int_info.sizeof_digit

def abs_val(x):
    mask = x >> (SIZE_INT * (CHAR_BIT - 1))
    return (x + mask) ^ mask
```

Patented variation:
```python
import sys
CHAR_BIT = sys.int_info.bits_per_digit

def abs_val(x):
    mask = x >> (CHAR_BIT - 1)
    return (x ^ mask) - mask
```

Some CPUs don't have an integer absolute value instruction (or the compiler fails to use them). On machines where branching is expensive, the above expression can be faster than the obvious approach, `r = (v < 0) ? -(unsigned)v : v`, even though the number of operations is the same.

On March 7, 2003, Angus Duggan pointed out that the 1989 ANSI C specification leaves the result of signed right-shift implementation-defined, so on some systems this hack might not work. I've read that ANSI C does not require values to be represented as two's complement, so it may not work for that reason as well (on a diminishingly small number of old machines that still use one's complement).

On March 14, 2004, Keith H. Duggar sent me the patented variation above; it is superior to the one I initially came up with, `r=(+1|(v>>(sizeof(int)*CHAR_BIT-1)))*v`, because a multiply is not used. Unfortunately, this method has been patented in the USA on June 6, 2000 by Vladimir Yu Volkonsky and assigned to Sun Microsystems. On August 13, 2006, Yuriy Kaminskiy told me that the patent is likely invalid because the method was published well before the patent was even filed, such as in How to Optimize for the Pentium Processor by Agner Fog, dated November, 9, 1996. Yuriy also mentioned that this document was translated to Russian in 1997, which Vladimir could have read. Moreover, the Internet Archive also has an old link to it. On January 30, 2007, Peter Kankowski shared with me an abs version he discovered that was inspired by Microsoft's Visual C++ compiler output. It is featured here as the primary solution. On December 6, 2007, Hai Jin complained that the result was signed, so when computing the abs of the most negative value, it was still negative. On April 15, 2008 Andrew Shapira pointed out that the obvious approach could overflow, as it lacked an (unsigned) cast then; for maximum portability he suggested `(v < 0) ? (1 + ((unsigned)(-1-v))) : (unsigned)v`. But citing the ISO C99 spec on July 9, 2008, Vincent Lefèvre convinced me to remove it becasue even on non-2s-complement machines -(unsigned)v will do the right thing. The evaluation of -(unsigned)v first converts the negative value of v to an unsigned by adding `2**N`, yielding a 2s complement representation of v's value that I'll call U. Then, U is negated, giving the desired result, `-U = 0 - U = 2**N - U = 2**N - (v+2**N) = -v = abs(v)`.


## Compute the minimum (min) or maximum (max) of two integers without branching
```python
def min(x, y):
    """
    Given integers x and y find min of the two
    """
    return y ^ ((x ^ y) & -(x < y))
```
On some rare machines where branching is very expensive and no condition move instructions exist, the above expression might be faster than the obvious approach, `r = (x < y) ? x : y`, even though it involves two more instructions. (Typically, the obvious approach is best, though.) It works because if `x < y`, then `-(x < y)` will be all ones, so `r = y ^ (x ^ y) & ~0 = y ^ x ^ y = x`. Otherwise, if `x >= y`, then `-(x < y)` will be all zeros, so `r = y ^ ((x ^ y) & 0) = y`. On some machines, evaluating `(x < y)` as 0 or 1 requires a branch instruction, so there may be no advantage.

To find the maximum, use:
```python
def max(x, y):
    """
    Given integers x and y find max of the two
    """
    return x ^ ((x ^ y) & -(x < y))
```
**Quick and dirty versions**

If you know that `INT_MIN <= x - y <= INT_MAX`, then you can use the following, which are faster because (x - y) only needs to be evaluated once.

> *Please note that Integers in Python3 are unbounded i.e the maximum integer representable is a fraction of the available memory. The constant `sys.maxsize` can be used to find the word-size; specifically, it's the maximum value integer that can be stored in the word, e.g., `2**63 - 1` on a 64-bit machine*.

```python
import sys
CHAR_BIT = sys.int_info.bits_per_digit
SIZE_INT = sys.int_info.sizeof_digit

def min(x, y):
    return y + ((x - y) & ((x - y) >> (SIZE_INT * CHAR_BIT - 1)))

def max(x, y):
    return x - ((x - y) & ((x - y) >> (SIZE_INT * CHAR_BIT - 1)))
```

Note that the 1989 ANSI C specification doesn't specify the result of signed right-shift, so these aren't portable. If exceptions are thrown on overflows, then the values of x and y should be unsigned or cast to unsigned for the subtractions to avoid unnecessarily throwing an exception, however the right-shift needs a signed operand to produce all one bits when negative, so cast to signed there. On March 7, 2003, Angus Duggan pointed out the right-shift portability issue. On May 3, 2005, Randal E. Bryant alerted me to the need for the precondition, `INT_MIN <= x - y <= INT_MAX`, and suggested the non-quick and dirty version as a fix. Both of these issues concern only the quick and dirty version. Nigel Horspoon observed on July 6, 2005 that gcc produced the same code on a Pentium as the obvious solution because of how it evaluates `(x < y)`. On July 9, 2008 Vincent Lefèvre pointed out the potential for overflow exceptions with subtractions in `r = y + ((x - y) & -(x < y))`, which was the previous version. Timothy B. Terriberry suggested using xor rather than add and subract to avoid casting and the risk of overflows on June 2, 2009.

## Determining if an integer is a power of 2
## Sign extending
### Sign extending from a constant bit-width
### Sign extending from a variable bit-width
### Sign extending from a variable bit-width in 3 operations
## Conditionally set or clear bits without branching
## Conditionally negate a value without branching
## Merge bits from two values according to a mask
## Counting bits set
### Counting bits set, naive way
### Counting bits set by lookup table
### Counting bits set, Brian Kernighan's way
### Counting bits set in 14, 24, or 32-bit words using 64-bit instructions
### Counting bits set, in parallel
### Count bits set (rank) from the most-significant bit upto a given position
### Select the bit position (from the most-significant bit) with the given count (rank)
## Computing parity (1 if an odd number of bits set, 0 otherwise)
### Compute parity of a word the naive way
### Compute parity by lookup table
### Compute parity of a byte using 64-bit multiply and modulus division
### Compute parity of word with a multiply
### Compute parity in parallel
## Swapping Values
### Swapping values with subtraction and addition
### Swapping values with XOR
### Swapping individual bits with XOR
## Reversing bit sequences
### Reverse bits the obvious way
### Reverse bits in word by lookup table
### Reverse the bits in a byte with 3 operations (64-bit multiply and modulus division)
### Reverse the bits in a byte with 4 operations (64-bit multiply, no division)
### Reverse the bits in a byte with 7 operations (no 64-bit, only 32)
### Reverse an N-bit quantity in parallel with 5 * lg(N) operations
## Modulus division (aka computing remainders)
### Computing modulus division by 1 << s without a division operation (obvious)
### Computing modulus division by (1 << s) - 1 without a division operation
### Computing modulus division by (1 << s) - 1 in parallel without a division operation
## Finding integer log base 2 of an integer (aka the position of the highest bit set)
### Find the log base 2 of an integer with the MSB N set in O(N) operations (the obvious way)
### Find the integer log base 2 of an integer with an 64-bit IEEE float
### Find the log base 2 of an integer with a lookup table
### Find the log base 2 of an N-bit integer in O(lg(N)) operations
### Find the log base 2 of an N-bit integer in O(lg(N)) operations with multiply and lookup
## Find integer log base 10 of an integer
## Find integer log base 10 of an integer the obvious way
## Find integer log base 2 of a 32-bit IEEE float
## Find integer log base 2 of the pow(2, r)-root of a 32-bit IEEE float (for unsigned integer r)
## Counting consecutive trailing zero bits (or finding bit indices)
### Count the consecutive zero bits (trailing) on the right linearly
### Count the consecutive zero bits (trailing) on the right in parallel
### Count the consecutive zero bits (trailing) on the right by binary search
### Count the consecutive zero bits (trailing) on the right by casting to a float
### Count the consecutive zero bits (trailing) on the right with modulus division and lookup
### Count the consecutive zero bits (trailing) on the right with multiply and lookup
## Round up to the next highest power of 2 by float casting
## Round up to the next highest power of 2
## Interleaving bits (aka computing Morton Numbers)
### Interleave bits the obvious way
### Interleave bits by table lookup
### Interleave bits with 64-bit multiply
### Interleave bits by Binary Magic Numbers
## Testing for ranges of bytes in a word (and counting occurances found)
### Determine if a word has a zero byte
### Determine if a word has a byte equal to n
### Determine if a word has byte less than n
### Determine if a word has a byte greater than n
### Determine if a word has a byte between m and n
### Compute the lexicographically next bit permutation

# Contributing
Please take a minute to go over the [Contribution Guidelines](CONTRIBUTING.md).

Contributions are welcome!
* [Issue reports](https://github.com/ianbrayoni/bithacks/issues)
* [Pull Requests](https://github.com/ianbrayoni/bithacks/pulls)