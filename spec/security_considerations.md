## Security Considerations

Perfect protection from eavesdropping is not possible with HTTPS, for various
reasons. However, [[ref: DDURLs]] SHOULD be hosted in a way that embodies accepted
cybersecurity best practice. This is not strictly necessary to guarantee the
authenticity of the data. However, it safeguards privacy, discourages denial of
service, accords with a defense-in-depth mindset, aids regulatory compliance,
and makes it easier to troubleshoot. How a [[ref: DDURL]] is hosted should let clients
fetch a DID doc and a KEL with roughly the same confidence that's associated
with properly implemented online banking).

The common name in the SSL/TLS certificate from the server MUST correspond to
the way the server is referenced in the URL. This means that if the URL includes
`www.example.com`, the common name in the SSL/TLS certificate must be
`www.example.com` as well. Unlike `did:web`, the URL MAY use an IP address
instead. If it does, then the common name in the certificate must be the IP
address as well. Essentially, the URL and the certificate MUST NOT identify the
server in contradictory ways; subject to that constraint, how the server is
identified is flexible.

The server certificate MAY be self-issued, or it MAY chain back to an unknown
certificate authority. However, to ensure reasonable security hygiene, it MUST
be valid. This has two meanings, both of which are required:

*   The certificate MUST satisfy whatever requirements are active in the client,
    such that the client does accept the certificate and use it to build and
    communicate over the encrypted HTTPS session where a DID doc and KEL are
    fetched.
*   The certificate MUST pass some common-sense validity tests, even if the
    client is very permissive: It MUST have a valid signature, it MUST NOT be
    expired or revoked or deny-listed, and it MUST NOT have any broken links in
    its chain of trust.

If a [[ref: DDURL]] results in a redirect, each URL MUST satisfy the same security
requirements. A [[ref: DDURL]] MAY come from a URL shortener.