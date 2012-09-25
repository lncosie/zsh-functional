[![Build Status][travis-status-png]][travis-status]

# ZSH higher order functions <sup>&alpha;</sup>

You can look at [yogsototh's blogpost] for the idea of higher order functions
in zsh.

# Warning -- still in alpha

I have some plans to change the behavior of `map` and rename all lambda methods
to be considered default and thus just be named `map`, `each` etc.

## Install

If you are lazy just paste the following lines in your terminal:

    cd /tmp && \
    curl -O https://raw.github.com/yogsototh/zsh_functional/master/install.sh && \
    chmod u+x install.sh && . ./install.sh && \rm -f ./install.sh

If you want to have more control,
clone this repo to `~/.zsh/functional` and add

    . ~/.zsh/functional/functional.plugin.zsh

to your `.zshrc`

### Antigen

If you use [antigen], you can simply add

    antigen-bundle Tarrasch/zsh-functional

Among your other `antigen-bundle` commands.

## Examples and usage

Here are some examples with named functions (`map`, `filter`, `fold`):

    $ insideXY(){print -- "X $1 Y"}
    $ map insideXY a b c d
    X a Y
    X b Y
    X c Y
    X d Y

    $ add(){print -- $(($1+$2))}
    $ fold add {1..5}
    15

Here are some examples of using anonymous functions (`*l` and `*a`):

    $ filterl 'echo $1|grep a >/dev/null' ab cd ef ada
    ab
    ada

    $ folda '$1+$2' {1..5}
    15

    $ folda '$1*$2' {1..20}
    2432902008176640000

    $ mapl 'echo X $1:t Y' ~/.zsh/functional/src/*
    X each Y
    X filter Y
    X fold Y
    X map Y

    $ mapa '$1*2' {1..3}
    2
    4
    6

    $ mapl 'echo result $1' $(mapa '$1+5' $(mapa '$1*2' {1..3}))
    result 7
    result 9
    result 11

Please also refer to the tests for the usage of the other functions. The
advantages with the [cram] tests are that they are readable and validated.

Furthermore, some of the commands will print out their `--help` if they are
provided no arguments.

## Naming conventions

Each of the method families, `map`, `each`, `filter` and `fold` are having a
"normal version" accompanied with lambda function version and a arithmetic
lambda version.

### Lambda functions

Use the versions ending with `l`, like `mapl`, `eachl`, `foldl`.

### Arithmetic lambda functions

Similarly, use the functions ending with `a`.

## Contributing

Good idea! Just add a test and implement the new functionality and send away
your pull request! :)

## Running the tests

We test like [antigen does testing][antigen-tests].

## Creds

Yann Esposito for the *HoF* idea and big thanks to [Sterling's blogpost] for
discovering and starting implementing the anonymous function features.

[yogsototh's blogpost]: http://yannesposito.com/Scratch/en/blog/Higher-order-function-in-zsh/
[Sterling's blogpost]:  http://nicholassterling.wordpress.com/2012/03/30/a-zsh-map-function/
[antigen]: https://github.com/zsh-users/antigen
[cram]: https://bitheap.org/cram/
[antigen-tests]: https://github.com/zsh-users/antigen#running-the-tests
[travis-status]: https://secure.travis-ci.org/Tarrasch/zsh-functional
[travis-status-png]: https://secure.travis-ci.org/Tarrasch/zsh-functional.png
