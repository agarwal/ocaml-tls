ocaml-tls
==========

TLS 1.0 and TLS 1.1 support in pure (O)Caml.

status
======

Client and server are working (mirage-server and mirage-client applications).

The mirage-server uses a mirage socket_stackv4 and listens on port 4433. Run the server ``./mir-mirage-tls-server``, and use ``openssl s_client -msg -connect 127.0.0.1:4433`` (use ``-tls1`` / ``-tls1_1`` to force a specific version) to start a secure conversation.

The mirage-client uses a mirage socket_stackv4 and connects to 127.0.0.1 port 4433. Run ``openssl s_server -key server.key -cert server.pem -msg`` before running ``./mir-mirage-tls-client``.

You can pass ``openssl s_server`` a ``-cipher`` argument (following values work at the moment: ``EDH-RSA-DES-CBC3-SHA DES-CBC3-SHA RC4-SHA RC4-MD5``.

implemented

- RFC 2246 - TLS Protocol version 1.0
- RFC 4346 - TLS Protocol version 1.1
- RFC 4366 - TLS extensions
- RFC 5746 - TLS Renegotiation Indication Extension

work in progress

- RFC 6520 - TLS Heartbeat extension
- RFC 3268 - AES Ciphersuites for TLS
- RFC 4492 - Elliptic Curve Cryptography Ciphersuites for TLS

trusted code base
=================

- this library
- cstruct https://github.com/avsm/ocaml-cstruct
- crypto from https://github.com/mirleft/ocaml-nocrypto (using C implementations of symmetric ciphers and hashes)
- uses zarith package (which interfaces libgmp)
- asn.1 parser combinator https://github.com/pqwy/ocaml-asn1-combinators
- OCaml runtime

plus obviously OCaml compiler, operating system, hardware

ciphersuites
============

currently we use the primitives from cryptokit (but are in the process of switching to ocaml-nocrypto).

key exchange
- DHE_RSA
- RSA

encryption
- 3DES-CBC
- RC4_128 (currently broken)

mac
- SHA1
- MD5

TODO (before any deployment)
============================

- address all [security concerns](https://github.com/mirleft/ocaml-tls/issues?labels=security+concern&page=1&state=open) in a convincing way
- fix config (currently Flow.default_config and Server.default_server_config)
- bits and pieces from useful extensions (heartbeat)
