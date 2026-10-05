# Lab 1: HTTP/TCP and DNS/UDP in Wireshark

[Repository overview](../README.md) · [Comparison report (PDF)](report/comparing_TCP_UDP.pdf)

Open the linked captures in Wireshark and type each filter into the display-filter bar.

## HTTP over TCP

Capture: [`neverssl_start.pcapng`](neverssl_start.pcapng)

Display filter:

```text
tcp.stream == 16
```

The three-way handshake, using Wireshark's relative sequence numbers:

| Packet | Direction | Flags | Sequence | Acknowledgment | TCP payload length |
| --- | --- | --- | --- | --- | --- |
| 2978 | Client → server | SYN | 0 | 0 | 0 |
| 3015 | Server → client | SYN, ACK | 0 | 1 | 0 |
| 3016 | Client → server | ACK | 1 | 1 | 0 |

Packet 3017 is the `GET /online/` request. The `200 OK` response (gzip-compressed HTML) arrives in two segments, packets 3026 and 3027; Wireshark shows the reassembled response on packet 3027. Later, the server sends `FIN, ACK` in packet 3087 and the client acknowledges it in packet 3088. That pair is the server's side of the close; the capture doesn't show every step of a full two-way shutdown.

| What it shows | Screenshot |
| --- | --- |
| HTTP request and `200 OK` response | [HTTP 200 OK](screenshots/part1_HTTP_OK.png) |
| Client SYN | [Handshake step 1](screenshots/part2_handshake_1_syn.png) |
| Server SYN, ACK | [Handshake step 2](screenshots/part2_handshake_2_syn.png) |
| Client ACK | [Handshake step 3](screenshots/part2_handshake_3_syn.png) |

The third screenshot's filename ends in `_syn`, but it shows the final ACK.

## DNS over UDP

Capture: [`udp_dns.pcapng`](udp_dns.pcapng)

Display filter:

```text
dns.id == 0x2b02
```

Packet 24 is an A-record query for `neverssl.com`, sent from client port `52938` to DNS port `53`. Packet 25 is the matching response, which returned `34.223.124.45` at the time of the capture. The domain's address may have changed since.

- [DNS query and UDP header](screenshots/part3_udp_query.png)
- [DNS response and returned address](screenshots/part3_udp_response.png)

## The comparison report

The [report](report/comparing_TCP_UDP.pdf) compares TCP and UDP on connection setup, reliability, ordering, typical uses and overhead. It is the version I submitted.

One correction to its checksum statement: an all-zero UDP checksum means "no checksum" only over IPv4. Over IPv6 the UDP checksum is required, apart from a few narrow exceptions. Either way, UDP does not guarantee delivery or ordering. The report's performance comparison is qualitative; the lab did not measure latency or throughput. See [RFC 768](https://www.rfc-editor.org/rfc/rfc768.html) and [RFC 8200, section 8.1](https://www.rfc-editor.org/rfc/rfc8200.html#section-8.1).
