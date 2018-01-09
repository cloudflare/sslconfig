sslconfig
=========

Cloudflare's Internet facing SSL cipher configuration

This repository tracks the history of the SSL cipher configuration used for
Cloudflare's public-facing SSL web servers. The repository tracks an internal
Cloudflare repository, but dates may not exactly match when changes are made.

There is a single file called conf which contains the configuration used in
Cloudflare's NGINX servers. This is only a fragment of the configuration.

ChaCha20/Poly1305 patch
-----------------------

Cloudflare uses [a patch](patches/openssl__1.1.0_chacha20_poly1305.patch) for
OpenSSL that enables the ChaCha20/Poly1305 cipher suites and implements
special logic to ensure it is only taken if it is the client's top cipher
choice.  Without this patch, the cipher suite choice in the configuration
will not work correctly.
