sslconfig
=========

CloudFlare's Internet facing SSL cipher configuration

This repository tracks the history of the SSL cipher configuration used for
CloudFlare's public-facing SSL web servers. The repository tracks an internal
CloudFlare repository, but dates may not exactly match when changes are made.

There is a single file called conf which contains the configuration used in
CloudFlare's NGINX servers. This is only a fragment of the configuration.

We currently use OpenSSL 1.0.2-stable (+ patches).


RC4 patch
---------

CloudFlare uses [a patch](patches/openssl__disable_rc4.patch) that disables
use of RC4 in TLS v1.1+. Without this patch, effective cipher list for TLS v1.1+
will be different than the one we use in production.

ChaCha20/Poly1305 patch
-----------------------

CloudFlare uses [a patch](patches/openssl__chacha20_poly1305_cf.patch) for
OpenSSL that enables the ChaCha20/Poly1305 cipher suites and implements
special logic to ensure it is only taken if it is the client's top cipher
choice.  Without this patch, the cipher suite choice in the configuration
will not work correctly.
