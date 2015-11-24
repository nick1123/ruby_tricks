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

### String concating

Concat with '+' operator

    "hello " + "world"
    => "hello world"

Works the same without '+' operator

    "hello " "world"
    => "hello world"

### Substring search

Here's a handy shorcut

    s = "some string"
    
    s["some"]
    => "some"
    
    s["fail"]
    => nil

### String interpolation shortcut

String interpolation is easy to do in ruby:

    a = 1
    "string #{a}"
    => "string 1"

You can omit the {} if the variable has a leading sigil

    @a = 2
    $a = 3
    "string #@a"
    => "string 2"
    "string #$a"
    => "string 3"


### Syntax checker

The -c flag causes Ruby to check the syntax of the script and exit without executing. If there are no syntax errors, Ruby will print "Syntax OK" to the standard output.

```
ruby -c script.rb
```


### Ripper

Sometimes we get a result that we don't expect:

```
puts {}.class
=> NilClass
```

We can use Ripper to inspect what's going on in our call chain:

```
require 'awesome_print'
require 'ripper'

ap Ripper.sexp("puts {}.class")
[
    [0] :program,
    [1] [
        [0] [
            [0] :call,
            [1] [
                [0] :method_add_block,
                [1] [
                    [0] :method_add_arg,
                    [1] [
                        [0] :fcall,
                        [1] [
                            [0] :@ident,
                            [1] "puts",
                            [2] [
                                [0] 1,
                                [1] 0
                            ]
                        ]
                    ],
                    [2] []
                ],
                [2] [
                    [0] :brace_block,
                    [1] nil,
                    [2] [
                        [0] [
                            [0] :void_stmt
                        ]
                    ]
                ]
            ],
            [2] :".",
            [3] [
                [0] :@ident,
                [1] "class",
                [2] [
                    [0] 1,
                    [1] 8
                ]
            ]
        ]
    ]
]
```

.class is being called on the code block {}, which is nil.

Another example of using Ripper to build an abstract syntax tree:

```
ap Ripper.sexp("3 + (5 * 7)")
[
    [0] :program,
    [1] [
        [0] [
            [0] :binary,
            [1] [
                [0] :@int,
                [1] "3",
                [2] [
                    [0] 1,
                    [1] 0
                ]
            ],
            [2] :+,
            [3] [
                [0] :paren,
                [1] [
                    [0] [
                        [0] :binary,
                        [1] [
                            [0] :@int,
                            [1] "5",
                            [2] [
                                [0] 1,
                                [1] 5
                            ]
                        ],
                        [2] :*,
                        [3] [
                            [0] :@int,
                            [1] "7",
                            [2] [
                                [0] 1,
                                [1] 9
                            ]
                        ]
                    ]
                ]
            ]
        ]
    ]
]
```

### Array zipping

```
names = %w[bob joe tom]
ages = [19, 22, 24]

names.zip(ages)
=> [["bob", 19], ["joe", 22], ["tom", 24]]

Hash[names.zip(ages)]
=> {"bob"=>19, "joe"=>22, "tom"=>24}
```

### Explode range to array

```
[*37..43]
=> [37, 38, 39, 40, 41, 42, 43]
```

### JSON 

```
require 'json'
data = [{a: 1, b: 2}, {c:3, d:4}]
```

Convert data to json:

```
j data
=> [{"a":1,"b":2},{"c":3,"d":4}]
```

Pretty print json:

```
jj data
[
  {
    "a": 1,
    "b": 2
  },
  {
    "c": 3,
    "d": 4
  }
]
```


