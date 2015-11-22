# Ruby Tricks

### Random number generator

Generate random float between 0.0 and 1.0

    rand
    => 0.3162109656780836

Generate random int between 0 and 3

    rand(3)
    => 1

Generate random int between 100 and 102

    rand(100..102)
    => 102

Generate random int between 100 and 101

    rand(100...102)
    => 101

### Awesome Print

Gem info
https://github.com/michaeldv/awesome_print

Require gem

    require "awesome_print"

Print an array

```
ap [:q, :w, :e]
[
    [0] :q,
    [1] :w,
    [2] :e
]
```

Print nested data

```
data = [{first: "Bob", last: "Smith", details: %w{:a, :b}}, {first: "Jim", last: "Cook", details: %w{:c, :w}}]
ap data
[
    [0] {
          :first => "Bob",
           :last => "Smith",
        :details => [
            [0] ":a,",
            [1] ":b"
        ]
    },
    [1] {
          :first => "Jim",
           :last => "Cook",
        :details => [
            [0] ":c,",
            [1] ":w"
        ]
    }
]
```
