---
title: "DNS over HTTP resolver announcement Using DHCP or Router Advertisements"
abbrev: "DoH resolver announcement using DHCP or Router Advertisements"
docname: draft-peterson-doh-dhcp
date: 2019
author:
    -
      ins: T. Peterson
      name: Thomas Peterson
      email: nosretep.samoht@gmail.com

ipr: trust200902
area: General
workgroup:
keyword: Internet-Draft
stand_alone: yes
pi: [toc, sortrefs, symrefs]

normative:
  RFC2119:

--- abstract

This specification describes a DHCP option and Router Advertisement (RA)
extension to inform clients of the presents of a DNS over HTTP (DoH) service to
be used for DNS queries.

--- middle

# Introduction

This document.

# Conventions and Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in BCP 14 {{RFC2119}} {{!RFC8174}}
when, and only when, they appear in all capitals, as shown here.

## Relationship with existing

DHCP already provides {{!RFC3132}} .

# The DoH Option

The DoH DHCP/RA option informs the client that a DoH service is available for
use for .

In order to support multiple "classes" of clients, the network operator can provide
the URI template {{!RFC6570}} which describes how a client can construct the URL
to use for resolution.


The maximum length of the URI template that can be carried in IPv4 DHCP is 255
bytes, so URI templates longer than 255 bytes SHOULD NOT be used in IPv6 DHCP or
IPv6 RA.

## IPv4 DHCP Option

The format of the IPv4 DoH DHCP option is shown below.

{#fig-bit-string-layout}
~~~

~~~

* Code: The DoH DHCPv4 option (one octet).
* Len: The length, in octets of the URI template.
* URI Template: The DoH resolver available for use

## IPv6 DHCP Option

~~~

~~~

## The DoH IPv6 RA Option

The format of the DoH Router Advertisement option is shown below.

~~~

~~~

* Type: TODO
* Length: 8-bit unsigned integer representing the entire length of all fields,
in units of 8 bytes.
* URI Template: The DoH resolver available for use

# Security Considerations

This document currently has no security considerations.

# IANA Considerations

This document makes no request of IANA.

--- back

# Acknowledgments
{:numbered="false"}

TODO
