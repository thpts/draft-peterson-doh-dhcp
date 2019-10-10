---
title: "DNS over HTTP resolver announcement Using DHCP or Router Advertisements"
abbrev: "DoH using DHCP or Router Advertisements"
docname: draft-peterson-doh-dhcp-00
date: {DATE}
author:
    -
      ins: T. Peterson
      name: Thomas Peterson
      email: nosretep.samoht@gmail.com

ipr: trust200902
category: std
area: General
workgroup:
keyword: Internet-Draft
stand_alone: yes
pi: [toc, sortrefs, symrefs]

normative:
    RFC2119:
    RFC3986:

informative:
    RFC2131:
    RFC3646:
    RFC8106:
    bootp-registry:
        title: "Dynamic Host Configuration Protocol (DHCP) and Bootstrap Protocol (BOOTP) Parameters"
        target: http://www.iana.org/assignments/bootp-dhcp-parameters
    dhcpv6-registry:
        title: "Dynamic Host Configuration Protocol for IPv6 (DHCPv6)"
        target: http://www.iana.org/assignments/dhcpv6-parameters
    icmpv6-registry:
        title: "Internet Control Message Protocol version 6 (ICMPv6) Parameters"
        target: http://www.iana.org/assignments/icmpv6-parameters

--- abstract

This specification describes a DHCP option and Router Advertisement (RA)
extension to inform clients of the presence of a DNS over HTTP (DoH) service to
be used for DNS queries.

--- middle

# Introduction

DHCPv4 {{RFC2131}}, DHCPv6 {{RFC3646}}, and IPv6 Router Announcements
{{RFC8106}} all provide means to inform clients of available resolvers using
the incumbent DNS protocol for querying, however there is no means of specifying
alternate protocols to perform DNS queries.

# Conventions and Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in BCP 14 {{RFC2119}} {{!RFC8174}}
when, and only when, they appear in all capitals, as shown here.

# The DoH Option

The DoH DHCP/RA option informs the client that a DoH service is available for
use for answering DNS queries. In order to support multiple "classes" of
clients, the network operator can provide the URI template {{!RFC6570}} which
describes how a client can construct the URL to use for resolution. Whilst DoH
servers may support multiple URI Templates, only one template MUST be
transmitted.

URI Templates that contain a host name SHOULD only be sent where a DHCP server
or Router provide name servers, as name resolution of any host name in the
template will require clients to use the non-DoH servers provided or manual
configuration.

The maximum length of the URI template that can be carried in IPv4 DHCP is 255
bytes, so URI templates longer than 255 bytes SHOULD NOT be used in IPv6 DHCP or
IPv6 RA.

## IPv4 DHCP Option

The format of the IPv4 DoH DHCP option is shown below.

~~~
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Code      |     Length    |      URI Template             .
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+                               .
.                                                               .
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
~~~

Code:
 : The DoH DHCPv4 option (one octet).

Length:
 : The length, in octets of the URI template.

URI Template:
 : The DoH server available, encoded following the rules of {{RFC3986}}.

## IPv6 DHCP Option

The format of the IPv6 DHCP option is shown below.

~~~
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          option-code          |           option-len          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
.                                                               .
.                          URI Template                         .
.                                                               .
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
~~~

option-code:
 : TODO (two octets)

option-len:
 : The length, in octects of the URI Template.

URI Template:
 : The DoH server

## The DoH IPv6 RA Option

The format of the DoH Router Advertisement option is shown below.

~~~
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Type      |     Length    |      URI Template             .
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+                               .
.                                                               .
.                                                               .
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
~~~

Type:
 : TODO (one octet)

Length:
 : 8-bit unsigned integer representing the entire length of all fields, in units
   of 8 bytes.

URI Template:
 : The DoH server available for use. This should be padded with NULL (0x0) to
   make the total option length (including the Type and Length fields) a
   multiple of 8 bytes.

# Security Considerations

An attacker with the ability to inject DHCP messages could include this option
and present a malicious resolver.

TODO: Further risk and threat assessments.

# IANA Considerations

TODO: This section must be updated after assignments have been issued.

This document requires the assignment of an option code assigned under the
"BOOTP Vendor Extensions and DHCP Options" {{bootp-registry}}, in
addition to an option code assigned under the "Option Codes" registry under
DHCPv6 parameters {{dhcpv6-registry}}.

Also, an assignment for an IPv6 RA Option Type from the "IPv6 Neighbor Discovery
Option Formats" registry under ICMPv6 paramters {{icmpv6-registry}}.

--- back

# Acknowledgments
{:numbered="false"}

TODO
