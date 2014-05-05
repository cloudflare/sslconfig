sslconfig
=========

CloudFlare's Internet facing SSL cipher configuration

This repository tracks the history of the SSL cipher configuration used for
CloudFlare's public-facing SSL web servers. The repository tracks an internal
CloudFlare repository, but dates may not exactly match when changes are made.

There is a single file called conf which contains the configuration used in
CloudFlare's NGINX servers. This is only a fragment of the configuration.

We currently use OpenSSL 1.0.2-stable (+ patches).
