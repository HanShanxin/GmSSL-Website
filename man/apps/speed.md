# NAME

speed - test library performance

# SYNOPSIS

**gmssl speed**
\[**-help**\]
\[**-engine id**\]
\[**-elapsed**\]
\[**-evp algo**\]
\[**-decrypt**\]
\[**algorithm...**\]

# DESCRIPTION

This command is used to test the performance of cryptographic algorithms.
To see the list of supported algorithms, use the _list --digest-commands_
or _list --cipher-commands_ command.

# OPTIONS

- **-help**

    Print out a usage message.

- **-engine id**

    specifying an engine (by its unique **id** string) will cause **speed**
    to attempt to obtain a functional reference to the specified engine,
    thus initialising it if needed. The engine will then be set as the default
    for all available algorithms.

- **-elapsed**

    Measure time in real time instead of CPU time. It can be useful when testing
    speed of hardware engines.

- **-evp algo**

    Use the specified cipher or message digest algorithm via the EVP interface.

- **-decrypt**

    Time the decryption instead of encryption. Affects only the EVP testing.

- **\[zero or more test algorithms\]**

    If any options are given, **speed** tests those algorithms, otherwise all of
    the above are tested.

# COPYRIGHT

Copyright 2000-2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
