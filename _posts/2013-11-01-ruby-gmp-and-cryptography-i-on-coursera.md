---
layout: default
title: Ruby, GMP and Cryptography I on Coursera
comments: true
tags:
  - ruby
  - cryptography
---

# Ruby, GMP and Cryptography I on Coursera

I've recently taken an [online course on cryptography][1], which is taught on Coursera by Dan Boneh, Professor of CS and EE at Stanford University. I can't praise the course enough for its thoroughness and reasoning about pretty much everything you'd want to know about cryptography and I strongly advise anyone interested to give it a try.

Programming assignments are one of the particular features of the course. Even though they are not required to obtain a certificate, they still are fun and challenging exercises, strengthening your grasp of cryptography theory. The choice of how exactly you will complete assignments is up to you, any programming language or style is fine. This post is for those who prefer using Ruby for just about anything.

As part of your implementation, you are required to manipulate very large numbers in some peculiar ways, and instead of seeking help from Ruby native citizens like `Bignum` or `BigDecimal`, my suggestion is to use the blazing fast C library [GMP][2] and [GMP RubyGem][3] which provides Ruby bindings to GMP.

## Preparations

1. Make sure you have Ruby, RubyGems and GMP library installed and working.

2. Install the gem:

  ```bash
  $ gem install gmp
  ```

3. Include `GMP` into the namespace:

  ```ruby
  require 'gmp'
  include GMP
  ```

4. Use your \\(\mathbb{Z}\\) superpowers wisely.

## What are these superpowers?

Start by creating a GMP-flavored integer:

```ruby
a = Z(93)                   # => 93
a.class                     # => GMP::Z
```

\\(x = \lfloor\sqrt{a}\rfloor\\)

```ruby
x = a.sqrt
```

\\(x = a^c\\)

```ruby
x = a**c
```

\\(x = \gcd(a, b)\\)

```ruby
x = a.gcd(b)
```

Extended Euclidean algorithm: \\(x = \gcd(a, b)\\) and \\((m, n)\\) are [Bézout coefficients][4] for \\((a, b)\\) such that \\(a m + b n = \gcd(a, b)\\)

```ruby
x, m, n = a.gcdext(b)
```

\\(x \equiv a^{-1}\pmod{p}\\) such that \\(a x \equiv a a^{-1} \equiv 1\pmod{p}\\)

```ruby
x = a.invert(p)
```

\\(x \equiv a^c\pmod{p}\\)

```ruby
x = a.powmod(c, p)
```

## A brief example

```ruby
require 'gmp'
include GMP

Z(10).sqrt                  # => 3
Z(7).invert(17)             # => 5
Z(5).powmod(5, 7)           # => 3
((Z(93)**94)**95)**96       # => really large number computed very fast
```

## Actual answers to the course assignments

You will not find them here.

[1]: https://www.coursera.org/course/crypto "Cryptography I on Coursera"
[2]: http://gmplib.org "GMP"
[3]: https://rubygems.org/gems/gmp "GMP RubyGem"
[4]: http://en.wikipedia.org/wiki/B%C3%A9zout%27s_identity "wiki: Bézout's identity"
