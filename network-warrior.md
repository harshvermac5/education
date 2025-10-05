Connection is an important concept. It’s what
distinguishes a sneaker net, in which
information is physically transferred from one
computer to another via removable media, from a
real network. When you slap a USB drive (does
anyone still use floppydisks?) into a computer,
there is no indication that the files came from
anothercomputer—there is no connection. A
connection involves some sort of addressing or
identification of the nodes on the network (even
if it’sjust master/slave or primary/secondary) .

Hubs may also be called repeaters for this
reason, but it is important to understand that
while a hub is a repeater,a repeater is not
necessarily a hub

10 Base 5 (Thick Net)
10 Base 2 (Thin Net)

“Propagation delay
skewshall not exceed 45 ns/100m.” It is quite another to
say, “The cablemust not exceed 100m.”

A collision domain is an areaof an
Ethernet network where collisions can occur. If
one station can prevent anotherfrom sending
because it is using the network, these stations
are in the same collisiondomain.

A collision domain is an areaof an
Ethernet network where collisions can occur. If
one station can prevent anotherfrom sending
because it is using the network, these stations
are in the same collisiondomain.

Internetwork operating System (IoS)

In Ethernet, switching is the act of
forwarding frames based on their destination
MAC addresses. In telecom, switching is the
act of making a connection betweentwo
parties. In routing, switching is the process
of forwarding packets from oneinterface to
another within a router.

Stacking is a way of connecting multipleswitches
together to form a single logical switch. This can
be useful when you needmore than the
maximum number of ports available on a single
fixed-configurationswitch (48) . The limitation of stacking is that the backplane of the stack is
limited to32 or 64 gigabits per second (Gbps) 

Autonegotiation is the feature that allows a port
on a switch, router, server, or otherdevice to
communicate with the device on the other end
of the link to determine theoptimal duplex mode
and speed for the connection. The driver then
dynamically configures the interface to the values
determined for the link.

Parallel detection works by
sending the signal being received to the local 10Base-T, 100Base-TX,and 100Base-T4 drivers. If
any one of these drivers detects the signal, the
interface isset to that speed.

Parallel detection determines only the link
speed, not the supported duplex modes.This is
an important consideration because the common
modes of Ethernet have differing levels of duplex support.

On 3750s, when the
switch is inVTP server mode, even when you configure
VLANs in CLI, they do notappear in the running
configuration.

NXOS and CatOS differences:

1. NXOS directly accepts multiple interfaces, and doesn't requires `interface range` command.

2. NXOS don't require `do` before running exec mode commands.

3. By default the ports are routed in NXOS switch, they require `switchport` and `no shut` before using as switch.

Ethernet standards are older than VLAN standard, hence there is no discussion of VLAN in Ethernet standard, despite they both cover Layer 2, datalink layer.

Cisco’s InterSwitch Link (ISL)

ISL differs from 802.1Qin a couple of ways. First,
ISL is a Cisco-proprietary protocol,whereas 802.1Q is an IEEE standard. Second, ISL encapsulates
Ethernet frames withinan ISL frame, while 802.1
Q alters existing frames to include VLAN tags.
Furthermore,ISLis capable of supporting only 1,000 VLANs,
while 802.1Q is capable of supporting 4,096 VLANs.

If an Ethernet frame has been created at the
maximum size of 1,518 bytes,ISL will add an extra 30
bytes,for a total frame size of 1,548 bytes. Theseframes
maybe counted as “giant” frame errors, though Cisco
equipmenthas no problem accepting them.

The checksum is added as trailer by ISL, is calculated based on frame incuding ISL header.

802.1Q takes a different approach to VLAN
tagging. Instead of adding more headersto a
frame, 802.1Q inserts data into existing headers.
An additional four-byte tag fieldis inserted
between the Source Address and Type/Length
fields. Because 802.1Q hasaltered the frame, the
FCS of the frame is altered to reflect the change.
Because only four bytes are added, the
maximum size for an 802.1Q frame is 1,522
bytes. This may result in “baby giant” frame
errors, though the frames will still be supported on cisco device

If you need to
connect a 3Com switch to your Cisco network,
you can do sowith an 802.1Q trunk even if
your Cisco network uses ISL trunks elsewhere.
Thetrunking protocol is local to each individual
trunk. If you connect to a 3Com switchusing
802.1Q, the VLANs on that switch will still be
accessible on switches connectedusing ISL
elsewhere.

a group of physical
Ethernet links bonded together is called an
EtherChannel in Cisco parlance, Unix admins
sometimes refer to the same configuration as a
trunk. Of course, in the Cisco world the term
“trunk” r
efers to somethingcompletely different:
a link that labels frames with VLAN information
so that multipleVLANs can traverse it. Some
modern Unixes sometimes create a bond interface
whenperforming link aggregation, and Windows
admins often use the term teaming when
combining links.

`show process cpu history` command is helpful when dealing with broadcast storm

Spanning tree works by selection of root bridge,
The root bridge is the bridge that all
other bridges need to reach via the shortest path
possible.
root bridge is seleceted on the basis of bridge ID, which is combination of brige mac address and bridge priority.

Bridge priority is a 2-Byte field and has default value of 32768 (0x8000).
Lowest bridge ID then lowest mac address is preferred.

Path costs are determined by adding each
bridge’s port priority to the initial pathcost
as BPDUs are forwarded from bridge to
bridge.

The root bridge does not have root ports; it only has
designated ports.

Flex Links on Cisco Nexus systems provide a Layer 2 link redundancy mechanism that serves as an alternative to the Spanning Tree Protocol (STP), allowing STP to be disabled while still maintaining basic link redundancy.
 This feature is configured on a pair of Layer 2 interfaces—either physical Ethernet ports or port channels—where one interface acts as the primary (active) link and the other as the backup (standby) link.
 Only one link in the pair forwards traffic at any given time, with the backup link ready to take over immediately if the primary link fails.
 The Spanning Tree Protocol is implicitly disabled on Flex Link interfaces to prevent loops, so it is essential to avoid configuring other redundant paths in the same topology.

UplinkFast allows a blocked uplink port to
bypass the listening and learning states when the designated port fails. This allows the
network to recover in five seconds orless. This
feature affects all VLANs on the switch. It also
sets the bridge priority to49,152 to ensure that
the switch will not become the root bridge.

BackboneFast adds functionality that detects
indirect link failures. It actively discoverspaths to
the root by sending out root link query PDUs after a link failure. When itdiscovers a path, it
sets the max age timer to 0 so the port can cycle
through the normallistening, learning, and
forwarding states without waiting an additional
20 seconds.

unidirectional link problems are handledby a
protocol called Unidirectional Link Detection
(UDLD) . UDLD is enabled bydefault and
should be left on.

The metric value is
determined by the routing protocol from which
the route was learned. Thus, the same link may have very different metrics depending on theprotocol
used. was learned. Thus, the same link may have very
different metrics depending on theprotocol
used.

The administrative distance is the value assigned to
each routing protocol to allowthe router to
prioritize routes learned from multiple sources.

Route Types:
1. Host route
2. Subnet
3. Summary (Group of subnet)
4. Major Network
5. Supernet (Group of major network)
6. Default route (route of last resort)
