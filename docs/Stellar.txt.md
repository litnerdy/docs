Stellar.txt
===========
## Introduction

The Stellar.txt file is used to provide the internet information about your domain’s Stellar integration. Any web site can publish Stellar network information. This is useful to announce your validation key, your federation server, peers you are running, other validators in your UNL, if you are a gateway etc.

### Publishing stellar.txt

Given the domain "DOMAIN", the stellar.txt will be searched for in this order:

- https:/<span></span>/stellar.DOMAIN/stellar.txt
- https:/<span></span>/DOMAIN/stellar.txt
- https:/<span></span>/www.DOMAIN/stellar.txt

### Enabling cross-origin resource sharing (CORS)
You must enable CORS on the stellar.txt so people can access this file from other sites, the following HTTP header MUST be set for all requests to stellar.txt and its dependent files.

 Access-Control-Allow-Origin: *

**Important:** You should only enable CORS for stellar.txt (or any files it references), so for example in Apache you would set something like:

```xml
<Location "/stellar.txt">
    Header set Access-Control-Allow-Origin "*"
</Location>
```

Or in nginx:

```json
location /stellar.txt {
 add_header 'Access-Control-Allow-Origin' '*';
}
```

For other webservers, see: http://enable-cors.org/server.html

### Testing CORS

1. Run a curl command in your terminal similar to this (replace stellar.stellar.org with where your stellar.txt file is hosted):

  ```bash
  curl --head https://stellar.stellar.org/stellar.txt
  ```

2. Verify the `Access-Control-Allow-Origin` header is present as shown below.

  ```bash
  curl --head https://stellar.stellar.org/stellar.txt
  HTTP/1.1 200 OK
  Accept-Ranges: bytes
  Access-Control-Allow-Origin: *
  Content-length: 482
  ...
  ```

3. Also run the command on a page that should not have it and verify `Access-Control-Allow-Origin` the header is missing.

## Stellar.txt example

```ini
Sample stellar.txt

This file is UTF-8 with Dos, UNIX, or Mac style end of lines.
Blank lines and lines beginning with '#' are ignored.
Undefined sections are reserved.
No escapes are currently defined.


#   A list of accounts that are controlled by this domain.
[accounts]
gBAde4mkDijZatAdNhBzCsuC7GP4MzhA3B

#   A validation public key that is declared
#   to be used by this domain for validating ledgers and that it is the
#   authorized signature for the domain.
[validation_public_key]
n3gVwaSDBtVi4Xd2XBh7rvcwis4uBabu5aNn7WKtEqazJbLHR9n

#   List of ips of known stellards.
#   One ipv4 or ipv6 address per line.
#   A port may optionally be specified after adding a space to the address.
#   By convention, if known, IPs are listed in from most to least trusted.
[ips]
192.168.0.1
192.168.0.1 3939
2001:0db8:0100:f101:0210:a4ff:fee3:9566


#   List of Stellar validators on this node's UNL.
#
#   For domains, stellard will probe for https web servers at the specified
#   domain in the following order: stellar.DOMAIN, www.DOMAIN, DOMAIN
[validators]
reddit.com
n3gVwaSDBtVi4Xd2XBh7rvcwis4uBabu5aNn7WKtEqazJbLHR9n
n3gVwaSDBtVi4Xd2XBh7rvcwis4uBabu5aNn7WKtEqazJbLHR9n John Doe

#   The endpoint which clients should query to resolve stellar addresses
#   for users on your domain.
[federation_url]
https://api.stellar.org/federation

#   This section allows a gateway to declare currencies it currently issues.
#   [currency] [issuing address]
[currencies]
USD gBAde4mkDijZatAdNhBzCsuC7GP4MzhA3B
BTC gBAde4mkDijZatAdNhBzCsuC7GP4MzhA3B
LTC gM4Fpv2QuHY4knJsQyYGKEHFGw3eMBwc1U
```
