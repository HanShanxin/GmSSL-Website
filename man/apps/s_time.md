# NAME

s\_time - SSL/TLS performance timing program

# SYNOPSIS

**gmssl** **s\_time**
\[**-help**\]
\[**-connect host:port**\]
\[**-www page**\]
\[**-cert filename**\]
\[**-key filename**\]
\[**-CApath directory**\]
\[**-CAfile filename**\]
\[**-no-CAfile**\]
\[**-no-CApath**\]
\[**-reuse**\]
\[**-new**\]
\[**-verify depth**\]
\[**-nbio**\]
\[**-time seconds**\]
\[**-ssl3**\]
\[**-bugs**\]
\[**-cipher cipherlist**\]

# DESCRIPTION

The **s\_time** command implements a generic SSL/TLS client which connects to a
remote host using SSL/TLS. It can request a page from the server and includes
the time to transfer the payload data in its timing measurements. It measures
the number of connections within a given timeframe, the amount of data
transferred (if any), and calculates the average time spent for one connection.

# OPTIONS

- **-help**

    Print out a usage message.

- **-connect host:port**

    This specifies the host and optional port to connect to.

- **-www page**

    This specifies the page to GET from the server. A value of '/' gets the
    index.htm\[l\] page. If this parameter is not specified, then **s\_time** will only
    perform the handshake to establish SSL connections but not transfer any
    payload data.

- **-cert certname**

    The certificate to use, if one is requested by the server. The default is
    not to use a certificate. The file is in PEM format.

- **-key keyfile**

    The private key to use. If not specified then the certificate file will
    be used. The file is in PEM format.

- **-verify depth**

    The verify depth to use. This specifies the maximum length of the
    server certificate chain and turns on server certificate verification.
    Currently the verify operation continues after errors so all the problems
    with a certificate chain can be seen. As a side effect the connection
    will never fail due to a server certificate verify failure.

- **-CApath directory**

    The directory to use for server certificate verification. This directory
    must be in "hash format", see **verify** for more information. These are
    also used when building the client certificate chain.

- **-CAfile file**

    A file containing trusted certificates to use during server authentication
    and to use when attempting to build the client certificate chain.

- **-no-CAfile**

    Do not load the trusted CA certificates from the default file location

- **-no-CApath**

    Do not load the trusted CA certificates from the default directory location

- **-new**

    performs the timing test using a new session ID for each connection.
    If neither **-new** nor **-reuse** are specified, they are both on by default
    and executed in sequence.

- **-reuse**

    performs the timing test using the same session ID; this can be used as a test
    that session caching is working. If neither **-new** nor **-reuse** are
    specified, they are both on by default and executed in sequence.

- **-nbio**

    turns on non-blocking I/O.

- **-ssl3**

    these options disable the use of certain SSL or TLS protocols. By default
    the initial handshake uses a method which should be compatible with all
    servers and permit them to use SSL v3 or TLS as appropriate.
    The timing program is not as rich in options to turn protocols on and off as
    the [s\_client(1)](http://man.he.net/man1/s_client) program and may not connect to all servers.

    Unfortunately there are a lot of ancient and broken servers in use which
    cannot handle this technique and will fail to connect. Some servers only
    work if TLS is turned off with the **-ssl3** option.

- **-bugs**

    there are several known bug in SSL and TLS implementations. Adding this
    option enables various workarounds.

- **-cipher cipherlist**

    this allows the cipher list sent by the client to be modified. Although
    the server determines which cipher suite is used it should take the first
    supported cipher in the list sent by the client.
    See the [ciphers(1)](http://man.he.net/man1/ciphers) command for more information.

- **-time length**

    specifies how long (in seconds) **s\_time** should establish connections and
    optionally transfer payload data from a server. Server and client performance
    and the link speed determine how many connections **s\_time** can establish.

# NOTES

**s\_time** can be used to measure the performance of an SSL connection.
To connect to an SSL HTTP server and get the default page the command

    gmssl s_time -connect servername:443 -www / -CApath yourdir -CAfile yourfile.pem -cipher commoncipher [-ssl3]

would typically be used (https uses port 443). 'commoncipher' is a cipher to
which both client and server can agree, see the [ciphers(1)](http://man.he.net/man1/ciphers) command
for details.

If the handshake fails then there are several possible causes, if it is
nothing obvious like no client certificate then the **-bugs** and
**-ssl3** options can be tried
in case it is a buggy server. In particular you should play with these
options **before** submitting a bug report to an GmSSL mailing list.

A frequent problem when attempting to get client certificates working
is that a web client complains it has no certificates or gives an empty
list to choose from. This is normally because the server is not sending
the clients certificate authority in its "acceptable CA list" when it
requests a certificate. By using [s\_client(1)](http://man.he.net/man1/s_client) the CA list can be
viewed and checked. However some servers only request client authentication
after a specific URL is requested. To obtain the list in this case it
is necessary to use the **-prexit** option of [s\_client(1)](http://man.he.net/man1/s_client) and
send an HTTP request for an appropriate page.

If a certificate is specified on the command line using the **-cert**
option it will not be used unless the server specifically requests
a client certificate. Therefor merely including a client certificate
on the command line is no guarantee that the certificate works.

# BUGS

Because this program does not have all the options of the
[s\_client(1)](http://man.he.net/man1/s_client) program to turn protocols on and off, you may not be
able to measure the performance of all protocols with all servers.

The **-verify** option should really exit if the server verification
fails.

# SEE ALSO

[s\_client(1)](http://man.he.net/man1/s_client), [s\_server(1)](http://man.he.net/man1/s_server), [ciphers(1)](http://man.he.net/man1/ciphers)

# COPYRIGHT

Copyright 2004-2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
