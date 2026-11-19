# ATM CA certificate bundle

`rootcert.pem` contains ten public CA certificates: six roots and the four Amazon RSA 2048 intermediates M01, M02, M03, and M04 discussed for ATM connectivity. This is a selected compatibility bundle, not the full catalog of Amazon intermediate authorities.

| Certificate | Expires (UTC) |
|---|---|
| Amazon Root CA 1 | January 17, 2038 |
| Amazon Root CA 2 | May 26, 2040 |
| Amazon Root CA 3 | May 26, 2040 |
| Amazon Root CA 4 | May 26, 2040 |
| Go Daddy Root Certificate Authority - G2 | December 31, 2037 |
| GoDaddy TLS Root CA - R1 | August 24, 2040 |
| Amazon RSA 2048 M01 | August 23, 2030 |
| Amazon RSA 2048 M02 | August 23, 2030 |
| Amazon RSA 2048 M03 | August 23, 2030 |
| Amazon RSA 2048 M04 | August 23, 2030 |

This file contains public certificates only. No private keys or server certificates are included. Servers normally supply their intermediate certificates during TLS. M01–M04 are also included locally for compatibility testing with ATM software; their presence does not prove they are required by every ATM. Amazon can use other issuing authorities in future.

The six-root-only version is retained as `roots-only.pem`. Amazon recommends root-based trust for general-purpose clients; do not assume adding every intermediate is needed or prevents future compatibility problems.

## Sources and integrity

The Amazon roots and GoDaddy G2 came from the CDS-distributed `CDS Rootcert.pem` bundle. GoDaddy R1 was obtained from GoDaddy's official repository. M01–M04 were downloaded from the official Amazon Trust Services repository; their published fingerprints, CA constraints, validity periods, and signatures against Amazon Root CA 1 were verified. Certificate SHA-256 fingerprints and exact expiration times are recorded in `manifest.json`. The file SHA-256 is recorded in `SHA256SUMS`.

- [CDS source bundle](https://ncratleos.quickbase.com/up/bwhk6p3be/g/r3/eg/vb)
- [Amazon Trust Services repository](https://www.amazontrust.com/repository/)
- [Amazon intermediate certificates](https://www.amazontrust.com/repository/cross-signed-and-externally-operated-subordinate-cas-certificates)
- [GoDaddy certificate repository](https://certs.godaddy.com/repository/)

## Import and validation

Download `rootcert.pem` as a file and copy it to the root of the USB drive. A private GitHub raw URL requires authentication; download while signed in instead of copying the web page contents.

- Genmega: use the supported certificate import under Customer Setup > Change Processor > SSL > Load Cert from USB.
- Hyosung SE: use Customer Setup > Select Processor > TCP/IP Type > Download Cert. From USB.

Menu names and support vary by software version. Importing may replace the existing trust file; preserve a supported prior copy before testing. Test the target server with certificate verification enabled and record the result. This bundle is not a firmware update or manufacturer-signed load file. ATM import and compatibility have not been verified on every board/software combination.

A root's expiration date is not a guarantee of connectivity until that date: server chains, algorithms, revocation state, and software requirements can change.

## Validation of this revision

Host-side OpenSSL TLS 1.2 checks passed for na.termgw.com at 3.142.137.129, 52.14.105.239, 54.69.111.60, and 52.35.64.170, and atm.columbusdata.net at 198.28.31.98, both with and without SNI on November 19, 2026. These results do not establish successful import or validation on an actual ATM. The intermediate certificates were individually verified against the root-only file, avoiding circular verification against themselves.
