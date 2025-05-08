sslconfig
=========

Cloudflare's Internet facing SSL cipher configuration

Table of Contents
-----------------
1. [ChaCha20/Poly1305 patch](#chacha20poly1305-patch)
2. [Creating Certificates and Encrypting Emails on a Windows Machine](#creating-certificates-and-encrypting-emails-on-a-windows-machine)

This repository tracks the history of the SSL cipher configuration used for
Cloudflare's public-facing SSL web servers. The repository tracks an internal
Cloudflare repository, but dates may not exactly match when changes are made.

There is a single file called conf which contains the configuration used in
Cloudflare's NGINX servers. This is only a fragment of the configuration.

ChaCha20/Poly1305 patch
-----------------------

Cloudflare uses [a patch](patches/openssl__chacha20_poly1305_cf.patch) for
OpenSSL that enables the ChaCha20/Poly1305 cipher suites and implements
special logic to ensure it is only taken if it is the client's top cipher
choice.  Without this patch, the cipher suite choice in the configuration
will not work correctly.

Creating Certificates and Encrypting Emails on a Windows Machine
-----------------------------------------------------------------

To create certificates and encrypt emails on a Windows machine using OpenSSL, follow these steps:

1. Generate a private key and a certificate signing request (CSR) using OpenSSL:
   * Open a terminal or command prompt on your machine.
   * Run the following command to generate a private key:
     ```
     openssl genpkey -algorithm RSA -out private_key.pem
     ```
     This command generates a private key using the RSA algorithm and saves it to a file named `private_key.pem`.
   * You can also specify the key size by adding the `-pkeyopt` option. For example, to generate a 2048-bit RSA key, use the following command:
     ```
     openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
     ```
   * Run the following command to generate a certificate signing request (CSR):
     ```
     openssl req -new -key private_key.pem -out csr.pem
     ```
     This command generates a CSR using the private key and saves it to a file named `csr.pem`.

2. Submit the CSR to a Certificate Authority (CA) to obtain a signed certificate:
   * Follow the instructions provided by the CA to submit the CSR and obtain a signed certificate.
   * Save the signed certificate to a file named `certificate.pem`.

3. Configure your server to use the private key and the signed certificate for SSL/TLS encryption:
   * Edit the server configuration file to include the paths to the private key and the signed certificate.
   * For example, in an NGINX server configuration file, you can add the following lines:
     ```
     ssl_certificate /path/to/certificate.pem;
     ssl_certificate_key /path/to/private_key.pem;
     ```
   * Restart the server to apply the changes.

4. Apply the ChaCha20/Poly1305 patch for OpenSSL, as described in the `README.md` file.

For more details, you can refer to the `conf` file in this repository, which contains the SSL configuration used in Cloudflare's NGINX servers.
