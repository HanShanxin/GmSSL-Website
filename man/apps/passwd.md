# NAME

passwd - compute password hashes

# SYNOPSIS

**gmssl passwd**
\[**-help**\]
\[**-crypt**\]
\[**-1**\]
\[**-apr1**\]
\[**-salt** _string_\]
\[**-in** _file_\]
\[**-stdin**\]
\[**-noverify**\]
\[**-quiet**\]
\[**-table**\]
{_password_}

# DESCRIPTION

The **passwd** command computes the hash of a password typed at
run-time or the hash of each password in a list.  The password list is
taken from the named file for option **-in file**, from stdin for
option **-stdin**, or from the command line, or from the terminal otherwise.
The Unix standard algorithm **crypt** and the MD5-based BSD password
algorithm **1** and its Apache variant **apr1** are available.

# OPTIONS

- **-help**

    Print out a usage message.

- **-crypt**

    Use the **crypt** algorithm (default).

- **-1**

    Use the MD5 based BSD password algorithm **1**.

- **-apr1**

    Use the **apr1** algorithm (Apache variant of the BSD algorithm).

- **-salt** _string_

    Use the specified salt.
    When reading a password from the terminal, this implies **-noverify**.

- **-in** _file_

    Read passwords from _file_.

- **-stdin**

    Read passwords from **stdin**.

- **-noverify**

    Don't verify when reading a password from the terminal.

- **-quiet**

    Don't output warnings when passwords given at the command line are truncated.

- **-table**

    In the output list, prepend the cleartext password and a TAB character
    to each password hash.

# EXAMPLES

**gmssl passwd -crypt -salt xx password** prints **xxj31ZMTZzkVA**.

**gmssl passwd -1 -salt xxxxxxxx password** prints **$1$xxxxxxxx$UYCIxa628.9qXjpQCjM4a.**.

**gmssl passwd -apr1 -salt xxxxxxxx password** prints **$apr1$xxxxxxxx$dxHfLAsjHkDRmG83UXe8K0**.

# COPYRIGHT

Copyright 2000-2016 The OpenSSL Project Authors. All Rights Reserved.

Licensed under the GmSSL license (the "License").  You may not use
this file except in compliance with the License.  You can obtain a copy
in the file LICENSE in the source distribution or at
[https://www.openssl.org/source/license.html](https://www.openssl.org/source/license.html).
