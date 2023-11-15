---
layout: post
title: "Combinations, Variations, Permutations"
categories: [EmailMarketing]
---
A short cheet sheet useful for a tech marketer. For example, a **combination** can help to find a number of possible scenarios to test entry source criteria. A **variation** explains why a system requires stronger passwords than a 4-digits bicycle lock&hellip;

## Combinations - Order Does Not Matter
If the ACME fintech company offers five different products (n-number of uniquely identified product codes), how many scenarios does a QA person need to test the possible product combinations, if a Client purchased a k-number of unique products? It could be useful to test different versions of a copy to display depending on the product combination.

```html
Cn,k = n! / k!(n - k)!

Let k = 3, n = 5
Cn,k = 5! / 3!(5-3)! = 120 / 6(2)! = 120 / 12 = 10
```
There are **10 possible scenarios** to test all the product combinations.

## Varations - Order Matters
A longer password makes guessing it more difficult due to a larger number of possibilities. For example to calculate a number of arrangements for a bicycle lock, that has four plates (k) with 0-9 digits (n-elements), and the digits may repeat on each of the plate, for example 1-1-1-1, use the formula for variations with repetition allowed:

```text
Vn,k = n^k
Vn,k = 10^4 = 10000
```

With passwords it is more complicated due to so called **entropy** which measures password strenght using more sophisticated math. Nevertheless, in simple terms a one letter long passwrod that uses lower-case and upper-case letters has 52 (52^1) variations while a two letter long password creates 2704 (52^2) possible combinations.

## Permutations - Order Matters
To depict permutations without repetition, take n number of people standing in a queue. The P number of possible arrangements of those people can be expressed by:
```html
Pn = n!
P7 = 7! = 5040
```

## Resources
*  [Password Entropy](https://www.omnicalculator.com/other/password-entropy)