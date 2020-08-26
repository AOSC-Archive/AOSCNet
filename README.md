# AOSCNet
A private network that connects buildbots and developers connected via Tinc

## Getting Started

Anyone can get connected into this network using tinc.

1. Install tinc.
1. Create your tinc config dir (In our example, `/etc/tinc/AOSCNet`).
1. Copy `tinc.conf` `tinc-up` `tinc-down` into your tinc config dir.
1. Modify `tinc.conf` in your tinc config dir so it contains your machine name. See Naming Convention.
1. Modify `tinc.conf` in your tinc config dir so it contains `ConnectTo=CLOSEST\_TRANSIT`. See Transit.
1. Modify `db.aosc` with the IP address you want to use and your machine name. See IP Assignment.
1. Copy either `tinc-world/hosts` or `tinc-cn/hosts` depending on your location to your tinc config dir.
1. Generate your pubkey with `tincd -n -K4096`.
1. Create a PR containing your pubkey with updated DNS.
1. Wait till your PR is merged.
1. Modify `tinc-up` in your tinc config dir to reflect the IP address assigned to you.
1. Start tinc, and enjoy AOSCNet.

## Naming Convention

In order to ensure we know which machine belongs to whom,
we kindly ask you to prefix your machine name with your nickname.

Also, when updating the DNS record, please add another entry with your arch/role.
See existing entries as a reference.

## Transit
All transits contain all hosts file within the region (cn or world).

Currently the following transits are in use

* staphus - PA, US, Verizon, IPv4 only
* staphnl - AMS, NL, Online.net, IPv4/v6

_Although staphcn is also acting as a transit, it does NOT have a clearnet IP address, and can only peer with machines with a clearnet IP address._

**Peering between CN and anywhere else has its own risk. AOSCNet is not responsible for any damage or legal issue caused by it.**

## IP Assignment

### IPv4
The IPv4 part of the AOSCNet has the address space of `10.127.7.0/24`.

IP addresses are assigned on a first-come-first-serve basis.

IP addresses in the range of `10.127.7.250-254` are reserved for transits.

As the IPv4 address is limited, IPv6-only machines are welcomed.

### IPv6
The IPv6 part of the AOSCNet has the address space of `fd10:127:7:2672::/64`.

Any machine on AOSCNet MUST has an IPv6 address.

The last 4 hex digits are assigned on a first-come-first-serve basis.

The penultimate 4 hex digits are assigned based on the role of the machine.

* `0000`: Reserved
* `0001`: Transit
* `0002`: x86\_64 buildbot
* `0003`: MIPS buildbot
* `0004`: ARM buildbot
* `0005`: PowerPC buildbot
* `0006`: RISC-V buildbot
* `000a`: Repo
* `0010`: Developers

## DNS

You may access any machine by `MACHINENAME.aoscnet.aureus.life`.

Set your DNS to `ns1.aoscnet.aureus.life` for a nice reverse-DNS lookup and `MACHINENAME.aoscnet.neo` domain.
