---
layout: post 
title: Calling subs from separate script (Perl)
---

To better organise your code or to allow code to be referred to by
multiple scripts it can be best to call the code, which is a sub in this
example, from a separate perl script.

-   You must refer to the separate script by adding the following line
    near to the top of the perl script you are calling it from:

<!-- -->

    require "script.pl";

-   Your new script must return \'true\' when it is compiled, place the
    following at the end of your script

<!-- -->

    1;

#### Example

main.pl:

    #!/usr/local/bin/perl

    require "script.pl";

    #Variables in main.pl are parsed if referenced in showresult:
    my $location = "England";

    my $output = &showresult("Hello",3);
    print $output;

script.pl:

    #!/usr/local/bin/perl

    sub showresult {

    my $message = $_[0];
    my $number = $_[1];

    return "You are located in $location, the message is $message and your lucky number is $number.\
    ";
    1;

Output:

    You are located in England, the message is Hello and your lucky number is 3.

[Category:Perl](Category:Perl "wikilink")
