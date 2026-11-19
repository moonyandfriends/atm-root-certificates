# ATM root certificate bundle

`rootcert.pem` contains six public CA certificates for manual import into compatible Genmega and Hyosung ATM software.

| Certificate | Expires (UTC) |
|---|---|
| Amazon Root CA 1 | January 17, 2038 |
| Amazon Root CA 2 | May 26, 2040 |
| Amazon Root CA 3 | May 26, 2040 |
| Amazon Root CA 4 | May 26, 2040 |
| Go Daddy Root Certificate Authority - G2 | December 31, 2037 |
| GoDaddy TLS Root CA - R1 | August 24, 2040 |

This file contains public certificates only. No private keys, server certificates, or Amazon M01-M04 intermediate certificates are included. The server supplies its intermediate certificates during a TLS connection.

## Sources and integrity

The Amazon roots and GoDaddy G2 came from the CDS-distributed `CDS Rootcert.pem` bundle. GoDaddy R1 was obtained from GoDaddy's official repository. Certificate SHA-256 fingerprints and exact expiration times are recorded in `manifest.json`. The file SHA-256 is recorded in `SHA256SUMS`.

- [CDS source bundle](https://ncratleos.quickbase.com/up/bwhk6p3be/g/r3/eg/vb)
- [Amazon Trust Services repository](https://www.amazontrust.com/repository/)
- [GoDaddy certificate repository](https://certs.godaddy.com/repository/)

## Import and validation

Download `rootcert.pem` as a file and copy it to the root of the USB drive. A private GitHub raw URL requires authentication; download while signed in instead of copying the web page contents.

- Genmega: use the supported certificate import under Customer Setup > Change Processor > SSL > Load Cert from USB.
- Hyosung SE: use Customer Setup > Select Processor > TCP/IP Type > Download Cert. From USB.

Menu names and support vary by software version. Importing may replace the existing trust file; preserve a supported prior copy before testing. Test the target server with certificate verification enabled and record the result. This bundle is not a firmware update or manufacturer-signed load file. ATM import and compatibility have not been verified on every board/software combination.

A root's expiration date is not a guarantee of connectivity until that date: server chains, algorithms, revocation state, and software requirements can change.
