# Milestone 3

The deliverable for this milestone is the output of the command `openssl s_client -connect $INGRESS:443 -servername marketplace.boutiquestore.com -CAfile root.crt` which verifies that the ingress gateway is configured with the correct TLS certificate and the openssl client can verify the certificate root of trust and successfully complete a TLS handshake.

```shell
⎈ |minikube:default py-3.8.6 malston-a01 in ~/workspace/istio-liveproject
± ma |master ?:16 ✗| → openssl s_client -connect $INGRESS:443 -servername marketplace.boutiquestore.com -CAfile root.crt
CONNECTED(00000003)
depth=1 O = boutiquestore Inc., CN = boutiquestore.com
verify return:1
depth=0 CN = marketplace.boutiquestore.com, O = boutique store
verify return:1
---
Certificate chain
 0 s:/CN=marketplace.boutiquestore.com/O=boutique store
   i:/O=boutiquestore Inc./CN=boutiquestore.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIC7jCCAdYCAQAwDQYJKoZIhvcNAQEFBQAwOTEbMBkGA1UECgwSYm91dGlxdWVz
dG9yZSBJbmMuMRowGAYDVQQDDBFib3V0aXF1ZXN0b3JlLmNvbTAeFw0yMTA2Mjcy
MDQwNTRaFw0yMjA2MjcyMDQwNTRaMEExJjAkBgNVBAMMHW1hcmtldHBsYWNlLmJv
dXRpcXVlc3RvcmUuY29tMRcwFQYDVQQKDA5ib3V0aXF1ZSBzdG9yZTCCASIwDQYJ
KoZIhvcNAQEBBQADggEPADCCAQoCggEBAJqir4DaOKgWvmubUTamx0t1mNsu+GJz
C/vNNUuMTN3l+zD6b/A1IaY9P3DUTRQjpBiA09KTYu1FlqitnLlo6gtYzi14CJVF
pwYHRyGMpAYv890je1LQ8PMpMGxySGjO1xrMaAJDxoPo6ahv0YX44PthYDAwI1pW
6wIGx+HI8VESe/6XtbQ0uRdwbhnM4biIIzR+Ek7gd/haae+hMocXQ8yehWK67189
PdW5zRAJ3CLNx77SOsgqqG9fnccRsk0M7De1Pikxns+sUWxCDggiabYGBbeLmzkw
Zi5NXWtIVdWxS/jkl0hc5ITFOb8oDStnUPqvOUfx0jjvxu4ix/RAwBcCAwEAATAN
BgkqhkiG9w0BAQUFAAOCAQEABlXQns8U//ypNZGozlALDfn4KUWASLXOBJ2umR5o
V3wdCCJGzlio4m1Lfi1QMcpzuntF1ez6k5vkIK3PvGLKQE62rv56KfQdHT+f2nij
zipoPHWtDUorOy2cpFaBGscCe05rEyua113+jR/2rxF77W0RYJSlSwc2Vz697W3W
HU+l1wVMWiQnaUJQDhnNaPl9RGcBSUwffdsxGX7wlGhMZW/R2j7Alseeq3N/vOk3
AbJS8qhgHAgY1vA5MDuS4adT0sIjCMw9q/wRxNe+Y6PHviKvUjWd4L6UBfX4hfQt
Lej3QFPND65Ow9d8JafOsWO8RhpHHIQeMGRd3mIAYBvTKA==
-----END CERTIFICATE-----
subject=/CN=marketplace.boutiquestore.com/O=boutique store
issuer=/O=boutiquestore Inc./CN=boutiquestore.com
---
No client certificate CA names sent
Server Temp Key: ECDH, X25519, 253 bits
---
SSL handshake has read 1397 bytes and written 319 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-CHACHA20-POLY1305
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-CHACHA20-POLY1305
    Session-ID: 093D2C7F93F92724F1BF76392C1E4414944512B37AFB041C3D5A26F0219F4B4F
    Session-ID-ctx:
    Master-Key: 2BD3E69F386184EFAAC42AFF271F58110E1DFA6E93974F945DAFF106622822F28A3FC7FFBE5277F63B2BCCE9E5C4257C
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - d1 2e ff 5d 61 9c 97 06-13 9e 86 d5 63 f0 e9 2d   ...]a.......c..-
    0010 - 23 8d 76 d9 7d fc b4 c4-ae df 19 78 ab 85 27 d2   #.v.}......x..'.
    0020 - d7 c3 cb 03 2a b1 ca 66-fb 16 1c 77 12 ef 19 da   ....*..f...w....
    0030 - e5 5f 47 54 2b 1f 43 66-74 8e 64 55 c5 29 cc 5d   ._GT+.Cft.dU.).]
    0040 - 2b 4e b9 88 18 8b 69 1f-ef 4e bf e7 e7 66 35 d3   +N....i..N...f5.
    0050 - 06 ac db 08 7e 88 fb d1-9e f1 1b 40 b6 c2 2b 9b   ....~......@..+.
    0060 - a5 7d 94 4b 6b cd 7e 61-7e d9 b9 4b b9 54 33 95   .}.Kk.~a~..K.T3.
    0070 - cc e7 93 3f a8 26 06 ed-e6 cd 3e c4 2e de c9 18   ...?.&....>.....
    0080 - fc 5d 6d 09 d7 b3 fa e4-69 54 82 1e 65 e2 56 fb   .]m.....iT..e.V.
    0090 - 01 94 ad bc f7 3f 69 53-50 1d 71 bc a9 7d e4 1f   .....?iSP.q..}..
    00a0 - db e7 f1 7a 37 a7 26 e9-0a a6 b8 e3 2e 49 46 fd   ...z7.&......IF.
    00b0 - 70 35 b1 d9 32 a8 4a c1-28 94 83 b3 bb 6e 36 26   p5..2.J.(....n6&

    Start Time: 1624827887
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
---
```