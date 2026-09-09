# Lab 1: HTTP/TCP and DNS/UDP in Wireshark

[Repository overview](../README.md) · [Original comparison report (PDF)](report/comparing_TCP_UDP.pdf)

These notes describe the saved coursework captures. Open the linked files in Wireshark and enter each filter in the display-filter bar.

## HTTP over TCP

Capture: [`neverssl_start.pcapng`](neverssl_start.pcapng)

Display filter:

```text
tcp.stream == 16
```

The recorded three-way handshake uses Wireshark's relative sequence numbers:

| Packet | Direction | Flags | Sequence | Acknowledgment | TCP payload length |
| --- | --- | --- | --- | --- | --- |
| 2978 | Client → server | SYN | 0 | 0 | 0 |
| 3015 | Server → client | SYN, ACK | 0 | 1 | 0 |
| 3016 | Client → server | ACK | 1 | 1 | 0 |

Packet 3017 requests `GET /online/`. Packet 3027 returns `200 OK` with HTML content; the original notes record a gzipped response. The capture also records a server `FIN, ACK` at packet 3087 and the client's acknowledgment at packet 3088. That pair describes the recorded server-side close exchange, not every step of a complete two-sided shutdown.

| Evidence | Screenshot |
| --- | --- |
| HTTP request and successful response | [HTTP 200 OK](screenshots/part1_HTTP_OK.png) |
| Client SYN | [Handshake step 1](screenshots/part2_handshake_1_syn.png) |
| Server SYN, ACK | [Handshake step 2](screenshots/part2_handshake_2_syn.png) |
| Client ACK | [Handshake step 3](screenshots/part2_handshake_3_syn.png) |

The third screenshot retains its original filename ending in `_syn`; its role in the handshake is the final ACK.

## DNS over UDP

Capture: [`udp_dns.pcapng`](udp_dns.pcapng)

Display filter:

```text
dns.id == 0x2b02
```

Packet 24 is an A-record query for `neverssl.com`, sent from client port `52938` to DNS port `53`. Packet 25 is the matching standard response, returning `34.223.124.45`. This is the address observed in the saved capture, not a claim about the domain's current address.

- [DNS query and UDP header](screenshots/part3_udp_query.png)
- [DNS response and returned address](screenshots/part3_udp_response.png)

## Reading the comparison report

The [submitted PDF](report/comparing_TCP_UDP.pdf) compares connection establishment, reliability, ordering, use cases, and overhead. It remains unchanged as coursework evidence.

One clarification to its checksum statement: an all-zero UDP checksum indicates omission for IPv4; IPv6 normally requires a UDP checksum, with narrowly defined exceptions. UDP itself does not provide reliable or ordered delivery. The report's performance comparison is qualitative; this lab does not establish a latency or throughput benchmark. See [RFC 768](https://www.rfc-editor.org/rfc/rfc768.html) and [RFC 8200, section 8.1](https://www.rfc-editor.org/rfc/rfc8200.html#section-8.1).

The captures contain surrounding traffic and network metadata. Documentation and file references were reviewed during cleanup; no new packets were captured and no lab application was rerun.
