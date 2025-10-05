https://youtu.be/WNohIcMOnEw

# What is internet? 

It's when we send the information and receiver or
receive the information. Be it when we
request a web page from Google's web
server in order to see Google search
results, be it anything else. It's an
exchange of information. And in order
for this exchange to be successful, we
need our information to reach the next
hop. And if the hook that we're aiming
to reach is too far, our information
need to make a few hopes, a few jumps in
order to reach that information. And we
needed an administrative control in
order to form those hopes through which
our information can
pass. 

# What Is an Autonomous System (AS)?

These hops were called autonomous
system. Autonomous system is one or more
routers that represent a single hop.
It's an administrative control over a
single network, right? We don't care
whether they have more routers work or
switches working privately, right? But
on the outside, it's one public
administrative entity. Apologies, it may
not necessarily be public, but it's one
administrative entity.


# ASN: Autonomous System Number

- Initially it was a 16-bit (2 byte) number: 1 to 65535.

- After 2007, IANA (Internet Assigned Numbers Authority) introducted 32-bit (4-Byte) number: 65536 to 4294967295 (4.2 billion).

- ASN are provided by RIRs (Regional Internet Registeries)

# Types of AS:

1. Stub AS: One ISP upstream, no transit

2. Multihomed AS: Multiple ISP, no transit

3. Transit AS: Internet transit, paid (on basis of traffic volume)

- Stub AS and Multihomed AS are used by iBGP to route the traffic internally, while Transit AS is used by EBGP in order to provide public connectivity.