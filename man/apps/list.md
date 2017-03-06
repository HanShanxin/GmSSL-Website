# NAME

list - list algorithms and features

# SYNOPSIS

**gmssl list**
\[**-help**\]
\[**-commands**\]
\[**-digest-commands**\]
\[**-digest-algorithms**\]
\[**-cipher-commands**\]
\[**-cipher-algorithms**\]
\[**-public-key-algorithms**\]
\[**-disabled**\]

# DESCRIPTION

This command is used to generate list of algorithms or disabled
features.

# OPTIONS

- **-help**

    Display out a usage message.

- **-commands**

    Display a list of standard commands.

- **-digest-commands**

    Display a list of message digest commands, which are typically used
    as input to the [dgst(1)](http://man.he.net/man1/dgst) or [speed(1)](http://man.he.net/man1/speed) commands.

- **-digest-algorithms**

    Display a list of message digest algorithms.
    If a line is of the form
      foo => bar
    then **foo** is an alias for the official algorithm name, **bar**.

- **-cipher-commands**

    Display a list of cipher commands, which are typically used as input
    to the [dgst(1)](http://man.he.net/man1/dgst) or [speed(1)](http://man.he.net/man1/speed) commands.

- **-cipher-algorithms**

    Display a list of cipher algorithms.
    If a line is of the form
      foo => bar
    then **foo** is an alias for the official algorithm name, **bar**.

- **-public-key-algorithms**

    Display a list of public key algorithms, with each algorithm as
    a block of multiple lines, all but the first are indented.

- **-disabled**

    Display a list of disabled features, those that were compiled out
    of the installation.

# COPYRIGHT

Copyright 2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
