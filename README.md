<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Bit Twiddling Hacks](#bit-twiddling-hacks)
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
- [Contributions](#contributions)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Bit Twiddling Hacks
This project provides code snippets of Sean Anderson's compilation of [bit manipulation tricks](https://graphics.stanford.edu/~seander/bithacks.html) in [Python](https://www.python.org/) to make it easy to follow for those who do not have experience in [C](https://en.wikipedia.org/wiki/C_(programming_language)).

# Acknowledgement
> Hats off to Sean Eron Anderson, seander@cs.stanford.edu, for creating https://graphics.stanford.edu/~seander/bithacks.html

I **DO NOT** own any of this. The following contents comes directly from the above link. I would be happy to transfer the ownership of this repository to the original author, Sean Eron Anderson.

# License
[License Information](LICENSE.md)


# Contents

## About the operation counting methodology
## Compute the sign of an integer
## Detect if two integers have opposite signs
## Compute the integer absolute value (abs) without branching
## Compute the minimum (min) or maximum (max) of two integers without branching
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
Please take a minute to go over [Contributions Guidelines](CONTRIBUTING.md)

Contributions are welcome!
* [Issue reports](https://github.com/ianbrayoni/bithacks/issues)
* [Pull Requests](https://github.com/ianbrayoni/bithacks/pulls)