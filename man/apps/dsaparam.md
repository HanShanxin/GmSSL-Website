# NAME

dsaparam - DSA parameter manipulation and generation

# SYNOPSIS

**gmssl dsaparam**
\[**-help**\]
\[**-inform DER|PEM**\]
\[**-outform DER|PEM**\]
\[**-in filename**\]
\[**-out filename**\]
\[**-noout**\]
\[**-text**\]
\[**-C**\]
\[**-rand file(s)**\]
\[**-genkey**\]
\[**-engine id**\]
\[**numbits**\]

# DESCRIPTION

This command is used to manipulate or generate DSA parameter files.

# OPTIONS

- **-help**

    Print out a usage message.

- **-inform DER|PEM**

    This specifies the input format. The **DER** option uses an ASN1 DER encoded
    form compatible with RFC2459 (PKIX) DSS-Parms that is a SEQUENCE consisting
    of p, q and g respectively. The PEM form is the default format: it consists
    of the **DER** format base64 encoded with additional header and footer lines.

- **-outform DER|PEM**

    This specifies the output format, the options have the same meaning as the
    **-inform** option.

- **-in filename**

    This specifies the input filename to read parameters from or standard input if
    this option is not specified. If the **numbits** parameter is included then
    this option will be ignored.

- **-out filename**

    This specifies the output filename parameters to. Standard output is used
    if this option is not present. The output filename should **not** be the same
    as the input filename.

- **-noout**

    this option inhibits the output of the encoded version of the parameters.

- **-text**

    this option prints out the DSA parameters in human readable form.

- **-C**

    this option converts the parameters into C code. The parameters can then
    be loaded by calling the get\_dsaXXX() function.

- **-genkey**

    this option will generate a DSA either using the specified or generated
    parameters.

- **-rand file(s)**

    a file or files containing random data used to seed the random number
    generator, or an EGD socket (see [RAND\_egd(3)](http://man.he.net/man3/RAND_egd)).
    Multiple files can be specified separated by an OS-dependent character.
    The separator is **;** for MS-Windows, **,** for OpenVMS, and **:** for
    all others.

- **numbits**

    this option specifies that a parameter set should be generated of size
    **numbits**. It must be the last option. If this option is included then
    the input file (if any) is ignored.

- **-engine id**

    specifying an engine (by its unique **id** string) will cause **dsaparam**
    to attempt to obtain a functional reference to the specified engine,
    thus initialising it if needed. The engine will then be set as the default
    for all available algorithms.

# NOTES

PEM format DSA parameters use the header and footer lines:

    -----BEGIN DSA PARAMETERS-----
    -----END DSA PARAMETERS-----

DSA parameter generation is a slow process and as a result the same set of
DSA parameters is often used to generate several distinct keys.

# SEE ALSO

[gendsa(1)](http://man.he.net/man1/gendsa), [dsa(1)](http://man.he.net/man1/dsa), [genrsa(1)](http://man.he.net/man1/genrsa),
[rsa(1)](http://man.he.net/man1/rsa)

# COPYRIGHT

Copyright 2000-2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
