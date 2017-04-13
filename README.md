# crDFA

A Regex Syntax Parser, and Thompson NFA Transformer and Matcher based on [Russ Cox's Article "Regular Expression Matching Can Be Simple And Fast"](https://swtch.com/~rsc/regexp/regexp1.html) with Parse Tree Simplifications from [Guangming Xings Paper Minimized Thompson NFA - Chapter 3](http://people.wku.edu/guangming.xing/thompsonnfa.pdf) aiming at further creating a DFA tom improve performance.

Currently implemented Regex Syntax:

* Literals and concatenation `ab`
* Quantifiers `*`, `+`, `?` and Alternation `|`
* Groupings `a(ab)` (no capturing)
* Quantifiers `{2,4}`, `{2}`, `{4,}`
* Character Classes `[a-bK-Lxyß]` (negation missing)

Performance still lacks behind PCRE.

```
$ crystal run --release benchmark/compare.cr

building "(x+x+)+y" with Regex (PCRE)
  0.000000   0.000000   0.000000 (  0.000059)
building "(x+x+)+y" with RegExp (own impl
  0.000000   0.000000   0.000000 (  0.000036)

matching "xxxxxxxxxxxxxy" a first time with Regex (PCRE)
  0.000000   0.000000   0.000000 (  0.000016)
rx1.match(string) # => #<Regex::MatchData "xxxxxxxxxxxxxy" 1:"xxxxxxxxxxxxx">

matching "xxxxxxxxxxxxxy" a first time with RegExp (own impl
  0.000000   0.000000   0.000000 (  0.000012)
rx2.match(string) # => true

     Regex (PCRE) matching : xxxxxxxxxxxxxy   2.18M (457.98ns) (± 6.10%)       fastest
RegExp (own impl) matching : xxxxxxxxxxxxxy 628.93k (  1.59µs) (± 3.23%)  3.47× slower
```

## Installation

Add this to your application's `shard.yml`:

```yaml
dependencies:
  crDFA:
    github: ziprandom/crDFA
```

## Usage

```crystal
require "crDFA"
```

## Contributing

1. Fork it ( https://github.com/ziprandom/crDFA/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [ziprandom](https://github.com/ziprandom)  - creator, maintainer
