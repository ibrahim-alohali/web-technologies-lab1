# Web Technologies Lab 1: Wireshark

University coursework from September 2025. I used Wireshark to look at an HTTP exchange over TCP and a DNS exchange over UDP, then wrote a short report comparing the two protocols.

## Start here

- [Lab notes and packet walkthrough](lab1_wireshark/readme.md)
- [TCP and UDP comparison report (PDF)](lab1_wireshark/report/comparing_TCP_UDP.pdf)
- [HTTP/TCP capture](lab1_wireshark/neverssl_start.pcapng)
- [DNS/UDP capture](lab1_wireshark/udp_dns.pcapng)
- [Screenshots](lab1_wireshark/screenshots/)

The notes follow the TCP three-way handshake, an HTTP request and response, the server's connection close and a DNS query and response, with the packet numbers for each step.

## Viewing the captures

Open either `.pcapng` file in [Wireshark](https://www.wireshark.org/) and apply the display filters given in the lab notes. The PDF and screenshots open directly on GitHub.

Packet numbers, addresses and stream numbers belong to these saved captures and will differ in a new capture. The captures also contain unrelated background traffic and network details from the computer used for the lab.

## Note

The `django_app/` folder is an empty placeholder. The Django coursework is in a separate repository, [computer-web-labs](https://github.com/ibrahim-alohali/computer-web-labs).
