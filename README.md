Editor Nanny
============

**Note:** This project is in "sleeping" state and it might take a rather long time (0.5-1 years) until some work will
be done here. I opened the repository only for saving the idea of having such a tool as a helper for the future
Almost English system, and for realizing the whole thing independently of Almost English since I believe it will also
be useful outside of that programming language.

Introduction
------------

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
    library implementation, which is used in plugins for e.g. Gedit and others. When you have read the above-mentioned page,
    you probably will agree that this is a much smarter way of interpreting the ASCII Tab character than going to the
    next multiple of N columns — even mechanical typewriters were better than that.

    __Implemented in:__ Gedit (plugin)


 *  **Word-wrapping** of long lines, such that the continuation of a line starts at the same distance to the left as the
    first line was indented. The following example illustrates the wanted behavior:
    ```
    Next line is indented
         This is a rather long line of text: The quick brown fox jumps over the lazy dog
    ```
    is shown in most text editors as:
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

    __Implemented in:__ Geany

What if your favorite editor does not match those requirements? On the one hand, it looks as absurd to me as saying on the
arrival of a new webbrowser: "Will it run under DOS [with a CGA card]?". On the other hand, writing in Almost English with
`ed(1)` is better than doing the same in an old-fashioned unmaintainable language. So, **support for the "oldie" editors
must be implemented but in a way that does not hurt the the users that go without them** . This means that (1) the main
notation for Almost English programs shall not adhere to the legacy text model, and (2) that the presence of legacy model
support shall not lead to speed penalties, more memory consumption etc. in the compiler when it operates on non-legacy
source files. 


Implementation
--------------

Legacy text-model support is implemented by **a separate program, called the _Editor Nanny_** because its task is to look
after non-compliant editors, i.e. take their output and put it into a form usable by the Almost English compiler, and
translate standard Almost English notation (from IDE users) back to something that a legacy editor is familiar with.

The program will be written in C, because that's enough for simple non-interactive filter programs. Additionally, the
project is designed to be used outside of the Almost English context (wherever conversion from/to Elastic Tabstops is
required), so it should be as portable as possible.