# NAME

dsa - DSA key processing

# SYNOPSIS

**gmssl** **dsa**
\[**-help**\]
\[**-inform PEM|DER**\]
\[**-outform PEM|DER**\]
\[**-in filename**\]
\[**-passin arg**\]
\[**-out filename**\]
\[**-passout arg**\]
\[**-aes128**\]
\[**-aes192**\]
\[**-aes256**\]
\[**-camellia128**\]
\[**-camellia192**\]
\[**-camellia256**\]
\[**-des**\]
\[**-des3**\]
\[**-idea**\]
\[**-text**\]
\[**-noout**\]
\[**-modulus**\]
\[**-pubin**\]
\[**-pubout**\]
\[**-engine id**\]

# DESCRIPTION

The **dsa** command processes DSA keys. They can be converted between various
forms and their components printed out. **Note** This command uses the
traditional SSLeay compatible format for private key encryption: newer
applications should use the more secure PKCS#8 format using the **pkcs8**

# OPTIONS

- **-help**

    Print out a usage message.

- **-inform DER|PEM**

    This specifies the input format. The **DER** option with a private key uses
    an ASN1 DER encoded form of an ASN.1 SEQUENCE consisting of the values of
    version (currently zero), p, q, g, the public and private key components
    respectively as ASN.1 INTEGERs. When used with a public key it uses a
    SubjectPublicKeyInfo structure: it is an error if the key is not DSA.

    The **PEM** form is the default format: it consists of the **DER** format base64
    encoded with additional header and footer lines. In the case of a private key
    PKCS#8 format is also accepted.

- **-outform DER|PEM**

    This specifies the output format, the options have the same meaning as the
    **-inform** option.

- **-in filename**

    This specifies the input filename to read a key from or standard input if this
    option is not specified. If the key is encrypted a pass phrase will be
    prompted for.

- **-passin arg**

    the input file password source. For more information about the format of **arg**
    see the **PASS PHRASE ARGUMENTS** section in [gmssl(1)](http://man.he.net/man1/gmssl).

- **-out filename**

    This specifies the output filename to write a key to or standard output by
    is not specified. If any encryption options are set then a pass phrase will be
    prompted for. The output filename should **not** be the same as the input
    filename.

- **-passout arg**

    the output file password source. For more information about the format of **arg**
    see the **PASS PHRASE ARGUMENTS** section in [gmssl(1)](http://man.he.net/man1/gmssl).

- **-aes128|-aes192|-aes256|-camellia128|-camellia192|-camellia256|-des|-des3|-idea**

    These options encrypt the private key with the specified
    cipher before outputting it. A pass phrase is prompted for.
    If none of these options is specified the key is written in plain text. This
    means that using the **dsa** utility to read in an encrypted key with no
    encryption option can be used to remove the pass phrase from a key, or by
    setting the encryption options it can be use to add or change the pass phrase.
    These options can only be used with PEM format output files.

- **-text**

    prints out the public, private key components and parameters.

- **-noout**

    this option prevents output of the encoded version of the key.

- **-modulus**

    this option prints out the value of the public key component of the key.

- **-pubin**

    by default a private key is read from the input file: with this option a
    public key is read instead.

- **-pubout**

    by default a private key is output. With this option a public
    key will be output instead. This option is automatically set if the input is
    a public key.

- **-engine id**

    specifying an engine (by its unique **id** string) will cause **dsa**
    to attempt to obtain a functional reference to the specified engine,
    thus initialising it if needed. The engine will then be set as the default
    for all available algorithms.

# NOTES

The PEM private key format uses the header and footer lines:

    -----BEGIN DSA PRIVATE KEY-----
    -----END DSA PRIVATE KEY-----

The PEM public key format uses the header and footer lines:

    -----BEGIN PUBLIC KEY-----
    -----END PUBLIC KEY-----

# EXAMPLES

To remove the pass phrase on a DSA private key:

    gmssl dsa -in key.pem -out keyout.pem

To encrypt a private key using triple DES:

    gmssl dsa -in key.pem -des3 -out keyout.pem

To convert a private key from PEM to DER format:

    gmssl dsa -in key.pem -outform DER -out keyout.der

To print out the components of a private key to standard output:

    gmssl dsa -in key.pem -text -noout

To just output the public part of a private key:

    gmssl dsa -in key.pem -pubout -out pubkey.pem

# SEE ALSO

[dsaparam(1)](http://man.he.net/man1/dsaparam), [gendsa(1)](http://man.he.net/man1/gendsa), [rsa(1)](http://man.he.net/man1/rsa),
[genrsa(1)](http://man.he.net/man1/genrsa)

# COPYRIGHT

Copyright 2000-2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
