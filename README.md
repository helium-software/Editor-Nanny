Editor Nanny
============

**Note:** This project is in "sleeping" state and it might take a rather long time (0.5-1 years) until some work will
be done here. I opened the repository only for saving the idea of having such a tool as a helper for the future
Almost English system, and for realizing the whole thing independently of Almost English since I believe it will also
be useful outside of that programming language.

What is it all about? — Well, Helium in general wants to do many things in an innovative and aesthetically pleasing way
_(don't read Web-technology hype, 'smart'phones, bloatware, patronizing skilled users, being proud of "shiny new stuff"
invented around 1990)_ while still being "small and simple" and fast even on "old" or small/power-saving computers. The
first part to strive for that ideals will be the creation of a new, more humane programming language that should ease doing
all the rest in a sane way. 

One piece of innovation I would like to realize is to abandon the idea that program source code has to be the sort of
old-fashioned ASCII telegrams that you can create with traditional text editors (vi, for example). Introducing a new fancy
binary (or XML-based) format with lots of extra markup does not seem the right way _(it violates "small and simple"),_ but
there are some particularities of traditional source code documents that I would like to avoid: (1) hard word-wrap by
insertion of Carriage-Return characters _inside_ a logical paragraph, and (2) the handling of indentation and tabulation
(i.e. text alignment) with a mixture of tabs and spaces. These issues are actually not related to the ASCII standard itself,
but rather caused by the text model used in standard plain-text editors. 

As I consider it dated to write programs with editors that don't really understand the language, Almost English will be
developed together with an IDE (programmer's editor and testbench), but fellow programmers have raised concern that some
people who generally favor the principles of the upcoming language will be repelled by the fact of having to use one
particular IDE. So, the design will be carried out such that any editing program will work that satisfies the following two
requirements:

 *  **Elastic tabstops**, as proposed by [Nick Gravgaard](http://nickgravgaard.com/elastictabstops/). There exists a shared
    library implementation, which is used in plugins for e.g. Gedit and Vim. When you have read the above-mentioned page,
    you probably will agree that this is a much smarter way of interpreting the ASCII Tab character than going to the
    next multiple of N columns — even mechanical typewriters were better than that.

 *  **Word-wrapping** of long lines, such that the continuation of a line starts at the same distance to the left as the
    first line was indented. While many GUI-based editors allow word-wrapping, I don't know of any editor that implements
    the second part of this requirement. So, the following example illustrates the wanted behavior:

    ```
    Next line is indented
         This is a rather long line of text: The quick brown fox jumps over the lazy dog
    ```
    is shown in current text editors as:
    ```
    Next line is indented
         This is a rather long line of text: The quick brown fox
    jumps over the lazy dog
    ```
    while it should look like:
    ```
    Next line is indented
         This is a rather long line of text: The quick brown fox
         jumps over the lazy dog
    ```
    Of course, the `jumps` could start even a bit more to the right, or preceded by an arrow etc.

What if your favorite editor does not match those requirements? arrival of a new browser "Will it run under DOS?"