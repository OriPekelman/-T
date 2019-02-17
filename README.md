# Introducing #!T2017

`#!T2017` is the latest revision of the #!T language specification.


## #!T is a shorthand notation for TPL

 #!T is a modern, more efficient, distributed and highly scalable version of [IRP](http://esolangs.org/wiki/IRP) it can leverage modern ReSTful APIs with clients in most programming languages. But it also has an online interpreter with many  supported consoles. The language itself is fully unicode compliant, though some clients my not support all characters sets. 
 
## Syntax

 #!T has a simple extensible syntax allowing for a wide range of DSLs :

 * The language shebang, preceded optionally by a call stack referential operator (RT: @{identifier}) 
 * followed by  any NL, or PL expression that may contain out of band referential coroutines
 * optionally terminated by an indirection function (via @{identifier}) or callback (fyi @{identifier}).
 * #!T programs are immutable, every program must have a unique identifier a publishing timestamp, an author identifier (@{identifier}). Code may not be modified after publication.
 * #!T programs may be embedded in other execution environments (such as in browser HTML).
 
Every #!T program MUST be decomposed to functions (or sub-programs) that may only contain a maximum of 280 unicode glyphs. For #!T to be backward compatible with programs written in versions prior to #!T2017 they MUST container no more than 140 unicode glyphs.

* Programs longer than 280 unicode glyphs may be implemented using threads, but idiomatic #!T requires that each sub-program be self-sufficient.
* Programs may reference external binary resources, which themselves may be encoded #!T programs. In which case the Client is expected to interpret the external program inline, passing any external context to the internal closure.
* #!T programs may implement reactive (functional or non-functional patterns) by `replying` both to top-level programs and threaded sub-programs. It is the runtime's responsibility to restitute a global execution ordering.

## Runtime

The  #!T runtime consists of a cloud execution environment with two modes of operation (public and private). 

* A #!T  program is either executed through the ReSTful API or through an interpreter console both require a "Genesis node" account. 
* The program is automatically received by "Worker nodes" (AKA followers) which MUST receive it, MAY display the program and MAY execute any of its instructions. 
* A "Worker node" can either be a human operator or an automatic #!T Worker (also known as a bot) that may  decide to :
    * Execute the inline routine
    * Repeat the message as is
    * Modify and repeat the message 
    * Add a referential operator or an indirection function or callback(RT, VIA, FYI)
    * Subscribe as a "Worker node"" to the "Genesis node" or to any "Drone node" that was in the execution chain of  the program
    * Terminate by following an out of band referential coroutine
    * Terminate by disregarding the message

## Error handling

* #!T explicitly does not contain any error handling. Worker nodes may `unfollow`, `mute` or `report` #!T programs containing errors. #!T delegates error handling to the runtime.
* Workers _MAY_ implement non-fatal panic in lieu of exception handling.
* Runtimes _MUST_ implement _deplatforming_ for #!T programs that contain exceptions to common decency protocols.

### Scalability and execution order
The infrastructure running #!T is highly scalable though, it has been known to suffer downtimes. Message delivery time is not guaranteed. Also the level of distribution of each function is dependent on the initial number of "Drone nodes" the "Genesis node" and on the quality of the inline function.

### Double shebang operation
"Drone" nodes should infer if a function is written in NL (Natural language) or PL (Programming language) and should infer the specific implementation.

A specific set of ""Drone nodes"" may assume for any given "Genesis node" a default language. In case strict detection is required a double shebang may be introduced (see examples).

### Shebang-less operation
The language shebang may be dropped if there are many "Worker nodes" that are #!T aware.

### Referential Coroutines ("Links")
Referential coroutines are often indirect calls that have external dependencies and may require additional processing (for example through t.co or goo.gl services)

### Referential operator
Referential operator (RT:) MAY in order to maximize scalability and distribution include legacy IRP syntax (such as using the "Please" keyword) but those can be abbreviated to the more modern "plz" or altogether dropped. 

# #!T Examples:

Simplest iterative brainfuck function with inferred PL runtime :

    #!T ++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>+++++. --. >++++++++++++++.

Referential iterative brainfuck function inferred PL runtime :
    
    #!T --[------->++<]>-.--.>-[--->+<]>-.[--->+<]>++++.[->++<]>.[++++>---<]>-.+++.---------.+++++++.-----------.++++++.------.+++++++.+.------------.+++++++++++++.-[->+++++<]>-.[->+++<]>+.+.+++++++++++++.++++++.-.[---->+<]>+++.+++.--.>-[--->+<]>-.


Example of an iterative referential Ruby function with an internal out of band referential coroutine using a double shebang  :
    
    #!T #!/usr/bin/ruby \nputs "#!T https://github.com/OriPekelman/T/ via @OriPekelman"

Simplest referential coroutine:

    #!T https://github.com/OriPekelman/T/

Indirect referential coroutine:

    #!T @OriPekelman writes about #!T https://github.com/OriPekelman/T/
    
A more scalable referential coroutine:

    #!T 3 things that will blow your mind about #!T by @OriPekelman https://github.com/OriPekelman/T/ #DistributedComputing #blockchain

Referential operator with an indirect referential coroutine:

     RT: @damz #!T check out this cool repo by @OriPekelman https://github.com/OriPekelman/T/

Referential operator with an indirect referential coroutine with legacy IRP syntax:
    
    RT Please: #!T upgrade your IRP prorgrams to TPL by @OriPekelman https://github.com/OriPekelman/T/
    
Referential operator with an indirect referential coroutine and  modernized IRP syntax:
    
    RT plz: #!T migrating IRP to TPL @OriPekelman https://github.com/OriPekelman/T/

Embedded #!T with referential operator with an indirect referential coroutine and modernized IRP syntax provoking panic in an inlined IPL binary:

> Warning: Note that Embedded #!T may require Javascript to render inlined binaries.

# License

The language itself is licensed under CC, but most runtimes are proprietary. There are open source implementations that are both API and binary compatible like [https://joinmastodon.org/](Mastodon) and others that require only moderate adaptation [http://tent.io](http://tent.io) 
