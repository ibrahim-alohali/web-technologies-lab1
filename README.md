# Web Technologies Lab 1: Wireshark

University coursework examining an HTTP exchange over TCP and a DNS exchange over UDP. The repository preserves the original packet captures, screenshots, and comparison report.

## Start here

- [Lab notes and packet walkthrough](lab1_wireshark/readme.md)
- [TCP and UDP comparison report (PDF)](lab1_wireshark/report/comparing_TCP_UDP.pdf)
- [HTTP/TCP capture](lab1_wireshark/neverssl_start.pcapng)
- [DNS/UDP capture](lab1_wireshark/udp_dns.pcapng)
- [Screenshot evidence](lab1_wireshark/screenshots/)

The lab follows TCP connection establishment, an HTTP request and response, a recorded connection-close exchange, and a DNS query/response pair. The notes map each observation to the files included here.

## Viewing the work

Open either `.pcapng` file in [Wireshark](https://www.wireshark.org/). Apply the display filters in the lab notes to locate the relevant packets. The PDF and screenshots can be viewed directly on GitHub; no application setup is required.

Packet numbers, addresses, and stream identifiers describe these saved captures. They will differ in a new capture. The files include surrounding network traffic and device/network metadata, so they should be treated as original coursework evidence rather than an anonymized dataset.

## Repository status

The [`django_app/`](django_app/) directory contains only a `.gitkeep` placeholder. There is no Django application in this repository. The separate [computer-web-labs](https://github.com/ibrahim-alohali/computer-web-labs) repository contains the later Django coursework.

The documentation has been checked against the stored files. No new network capture or historical lab rerun was performed during this cleanup. The submitted PDF is preserved; the lab notes include a clarification of its UDP checksum wording.
