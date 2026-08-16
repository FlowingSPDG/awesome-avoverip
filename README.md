# Awesome AV over IP [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of standards, protocols, tools, products, and open-source projects for Audio/Video over IP (AVoIP).

Professional video and audio transport over IP networks spans many use cases — LAN live production, broadcast facilities, and internet contribution — each with different optimal protocols. This repository collects research notes, product pointers, and **open-source implementations**.

## Contents

- [Standards Map](#standards-map)
- [Protocol Activity](#protocol-activity)
- [SMPTE Family (ST 2001 / ST 2101 / ST 2110)](#smpte-family)
- [NDI (Network Device Interface)](#ndi-network-device-interface)
- [OMT (Open Media Transport)](#omt-open-media-transport)
- [SRT (Secure Reliable Transport)](#srt-secure-reliable-transport)
- [WebRTC / WHIP / WHEP](#webrtc--whip--whep)
- [Other Major Standards](#other-major-standards)
- [Open Source Projects](#open-source-projects)
- [Selection Guide](#selection-guide)
- [Related Resources](#related-resources)
- [Contributing](#contributing)
- [License](#license)

---

## Standards Map

| Standard | Type | Primary Use Case | Typical Network | Latency | Open | Bandwidth (1080p60 ref.) |
|----------|------|------------------|-----------------|--------|------|--------------------------|
| [NDI](#ndi-network-device-interface) | Protocol (SDK) | LAN live production, PTZ, switchers | 1GbE+ | Sub-frame to few frames | Free SDK, closed spec | HX ~8 Mbps, High BW ~200 Mbps |
| [OMT](#omt-open-media-transport) | Protocol | LAN live production (open alternative) | 1GbE | Sub-frame | MIT, fully open | Low / Med / High presets |
| [ST 2110](#smpte-family) | Standard suite | Broadcast, OB, IP facilities | 10/25/100GbE | Very low (uncompressed) | SMPTE standard | ~2.1 Gbps uncompressed |
| [IPMX](#ipmx) | Suite (ST 2110 extension) | Pro AV with HDCP/KVM | 1GbE+ (JPEG XS) | Low | Open | Compression-dependent |
| [SRT](#srt-secure-reliable-transport) | Protocol | Internet contribution & distribution | Public internet / WAN | Configurable | Open source | H.264/HEVC compressed |
| [RIST](#rist) | Protocol | Internet contribution (multi-vendor) | Public internet / WAN | Low–medium | Open spec | Profile-dependent |
| [WebRTC](#webrtc--whip--whep) | Protocol family | Browser delivery, sub-second viewing | Internet | 50–250 ms | IETF standards | Adaptive bitrate |
| [AES67](#aes67) / [Dante](#dante) | Audio AoIP | Sound, conferencing, broadcast audio | 1GbE | 0.25–few ms | AES67 open / Dante proprietary | Uncompressed PCM |
| [RAVENNA](#ravenna) | AoIP technology | Broadcast audio, ST 2110 integration | 1GbE+ | Very low | Open | Uncompressed PCM |
| [SDVoE](#sdvoe) | Protocol | Meeting rooms, digital signage | 10GbE | <100 μs | Closed spec | Uncompressed 4K60 |

> Detailed research: [`docs/research.md`](docs/research.md) · Activity metrics: [`docs/activity.md`](docs/activity.md)

---

## Protocol Activity

| Protocol | Score | Momentum | Latest Release | Products / Scale |
|----------|-------|----------|----------------|------------------|
| NDI | 5/5 | ↑ | NDI 6.3 (Jan 2026) | 2,000+ products, 600+ vendors |
| SRT | 5/5 | → | libsrt v1.5.6 (Jul 2026) | 650+ alliance members |
| WebRTC/WHIP/WHEP | 5/5 | ↑ | RFC 9725 WHIP (2025) | Cloud + OBS native |
| ST 2110 | 4/5 | ↑ | ST 2110-30:2025 | 100+ AIMS solutions |
| RIST | 4/5 | ↑ | TR-06-3 (2022) | 150+ forum members |
| Dante | 4/5 | → | Continuous | 400+ manufacturers |
| OMT | 3/5 | ↑↑ | libomtnet v1.0.0.16 (Jun 2026) | vMix 29+, early adopters |
| IPMX | 3/5 | ↑↑ | Certification began 2026 | Early certified products |
| SDVoE | 3/5 | → | Stable since 2016 | 50+ alliance partners |

Full metrics, OSS repo activity, and methodology: [`docs/activity.md`](docs/activity.md)

---

## SMPTE Family

### Terminology (important)

Among **ST 2001 / ST 2010 / ST 2101 / ST 2110**, their roles in AV over IP differ:

| Standard | Official Name | Role in AV over IP |
|----------|---------------|-------------------|
| **ST 2110** | Professional Media Over Managed IP Networks | **Core suite** — separate RTP essence streams over IP |
| **ST 2110-10** | System Timing and Definitions | Foundation (PTP, RTP, SDP) |
| **ST 2110-20** | Uncompressed Active Video | Uncompressed video payload |
| **ST 2110-21** | Traffic Shaping | Packet pacing |
| **ST 2110-30** | PCM Digital Audio | Uncompressed audio (AES67-aligned) |
| **ST 2110-40** | Ancillary Data | ANC / metadata |
| **ST 2059** | PTP clock profiles | Synchronization foundation for ST 2110 |
| **ST 2022** | MPEG-2 TS over IP | Legacy IP transport (ST 2022-6 wraps SDI) |
| **ST 2001-1** | Reg-XML | **Not an IP transport standard** — SMPTE metadata XML mapping |
| **ST 2101** | AC-4 in AES3 | **Not an IP transport standard** — AC-4 packing in AES3 |
| **ST 2010** | — | **No widely recognized SMPTE number** (likely ST 2110-10, ST 2022, or ST 2059) |

### ST 2110

[SMPTE ST 2110](https://www.smpte.org/standards/st2110) carries separate elementary essence streams (video, audio, ancillary data) over managed IP networks. Built on VSF TR-03; [2025 Emmy Award](https://www.smpte.org/smpte-st-2110-faq) winner. The de facto standard for SDI-to-IP migration.

**Key traits:** Independent stream routing, PTP sync (ST 2059), NMOS for discovery/connection, uncompressed (-20) through JPEG XS (-22).

**Resources:**
- [AIMS Alliance](https://aimsalliance.org/)
- [AIMS Member Solutions](https://solutions.aimsalliance.org/) — certified product catalog
- [AMWA NMOS](https://specs.amwa.tv/nmos/)
- [RAVENNA ST 2110 introduction](https://www.ravenna-network.com/introduction-to-smpte-st-2110/)

### ST 2110 Products (selected)

| Category | Vendors | Examples |
|----------|---------|----------|
| Encoders / Decoders | Evertz, Haivision, Grass Valley, AJA | Makito X4, AMPP, BRIDGE LIVE |
| NIC / FPGA IP | Matrox, NVIDIA/Mellanox | DSX LE5, X.mio5 ST 2110 NIC |
| Routing / Processing | Lawo, Ross Video, Cobalt Digital | V__matrix, Ultrix Carbonite, 9900 series |
| Monitoring | Telestream, Bridge Technologies, Leader | PRISM, VB440, LV5600 |
| Switches | Arista, Cisco | Broadcast IP switches |
| PTP Grandmaster | Meinberg, Net Insight | LANTIME, Nimbra Sync |
| Audio I/O | Calrec, SSL, Focusrite | ImPulse, System T, RedNet |

> Full catalog: [AIMS Member Solutions](https://solutions.aimsalliance.org/)

---

## NDI (Network Device Interface)

[NDI](https://ndi.video/) is a LAN-oriented AV over IP protocol from Vizrt NDI. One of the most widely adopted Pro AV solutions. Now operates as a standalone open standard (spun from Vizrt, 2025).

| Item | Detail |
|------|--------|
| License | Free SDK (non-commercial); **Advanced SDK** is commercial |
| Latest | **NDI 6.3** (Jan 2026); 6.3.1 follow-up |
| Adoption | 2,000+ products, 600+ manufacturers; ~9k NDI Tools downloads/week |
| Discovery | mDNS (default); NDI Discovery Server for large/cloud deployments |
| Default transport (v5+) | **RUDP** (Reliable UDP) — see [research doc](docs/research.md#32-transport-protocols-by-ndi-version) |
| Codec profiles | High Bandwidth (SHQ), HX / HX2 (H.264), HX3 (H.265) |
| Strengths | Largest IP video ecosystem, sub-frame latency, vMix/OBS/TriCaster |
| Weaknesses | Closed wire protocol; mDNS doesn't cross subnets without Discovery Server |

### SDK Tiers

| Feature | Standard SDK | Advanced SDK |
|---------|-------------|--------------|
| License | Free (non-commercial) | Commercial ([sales@ndi.video](mailto:sales@ndi.video)) |
| LAN send/receive | ✓ | ✓ |
| HDR encode/decode | Limited | ✓ (10-bit+) |
| HX3 passthrough/decode | — | ✓ |
| KVM | — | ✓ |
| Genlock / AV sync | — | ✓ |
| Per-instance JSON config | — | ✓ (transport, codec, NIC binding) |
| FPGA / embedded IP | — | ✓ (Agilex 7, etc.) |
| CLI recording | — | ✓ |
| Transport toggles (RUDP/TCP/UDP/multicast) | Basic | Full per-instance control |

→ [SDK vs Advanced SDK FAQ](https://docs.ndi.video/all/faq/sdk/what-are-the-differences-between-the-ndi-sdk-and-the-ndi-advanced-sdk)

### Transport Protocols (by NDI version)

| Version | Transport | Role |
|---------|-----------|------|
| NDI 1 | Single TCP | Baseline fallback; universal compatibility |
| NDI 3 | UDP + FEC | Low-latency; error correction on lossy links |
| NDI 4 | Multi-TCP (MPTCP) | Multi-NIC; hardware TCP offload |
| NDI 5+ | **RUDP** (default) | Reliable UDP + multi-stream congestion control |
| All | Multicast UDP+FEC | Optional fan-out; **disabled by default** (IGMP risk) |
| All | TCP | Automatic fallback when peer lacks negotiated mode |

### RUDP vs QUIC (investigation summary)

NDI's RUDP is **not IETF QUIC** (RFC 9000). It is a **proprietary Reliable UDP** designed for LAN live production. Some third-party articles incorrectly equate RUDP with QUIC; official NDI documentation describes a custom protocol.

| Aspect | NDI RUDP | IETF QUIC |
|--------|----------|-----------|
| Wire format | Proprietary (closed) | Standardized (RFC 9000) |
| Runs on | UDP | UDP |
| Reliability | Selective retransmit (sequence numbers) | Streams + loss recovery |
| Congestion control | Multi-stream aggregate CC per source | Per-connection CC (BBR/Cubic) |
| Multiplexing | All streams from one source → single connection | Multiple streams per connection |
| Encryption | Not TLS-based | TLS 1.3 integrated |
| HTTP/3 | No | Yes (native mapping) |
| Design goal | LAN video at scale | General internet transport |

**Conceptual similarity to QUIC:** Both solve "TCP is too slow for real-time media over UDP" by adding reliability, flow control, and congestion control on top of UDP. NDI RUDP's **aggregate multi-stream congestion control** (all NDI streams from one source share one CC context) is architecturally similar to QUIC's stream multiplexing — but the algorithms, handshake, and wire format are entirely different.

Key RUDP behaviors ([official docs](https://docs.ndi.video/all/developing-with-ndi/sdk/performance-and-implementation)):
- Non-blocking streams: packet loss on one stream doesn't block others
- Packet coalescing + async send batching (reduces kernel overhead)
- USO (UDP Segmentation Offload) on Windows; GSO/UDP_SEGMENT on Linux 4.18+
- Receiver-side scaling for interrupt handling

**Official resources:**
- [NDI Product Finder](https://ndi.video/product-finder/)
- [NDI Protocols white paper](https://docs.ndi.video/all/getting-started/white-paper/ndi-protocols)
- [Performance & Implementation](https://docs.ndi.video/all/developing-with-ndi/sdk/performance-and-implementation)
- [Advanced SDK docs](https://docs.ndi.video/all/developing-with-ndi/advanced-sdk)
- [NDI 6 overview](https://ndi.video/tech/ndi6/)

### Products (selected)

**Cameras / PTZ:** BirdDog (first full NDI 6.3 hardware line), PTZOptics, Panasonic, Sony, Lumens, Marshall, JVC  
**Encoders / Converters:** Magewell, Kiloview, AJA, Epiphan  
**Production:** Vizrt TriCaster, vMix, OBS (via DistroAV), mimoLive, Ross Carbonite  
**Network:** NETGEAR AV Line, Yamaha SWX/SWR switches

### Open Source (NDI ecosystem)

NDI wire protocol is closed. OSS tools wrap the NDI SDK:

| Project | Language | NDI SDK | Last Active | Notes |
|---------|----------|---------|-------------|-------|
| [DistroAV/DistroAV](https://github.com/DistroAV/DistroAV) | C++ | Runtime 6.3+ | Jun 2026 | OBS plugin (GPL-2.0); 4.5k★ |
| [GrantSparks/grafton-ndi](https://github.com/GrantSparks/grafton-ndi) | Rust | NDI 6 SDK | Jun 2026 | Idiomatic bindings; Tokio/async; PTZ; ~53k crates.io downloads |
| [obsproject/obs-studio](https://github.com/obsproject/obs-studio) | C | Via DistroAV | Aug 2026 | Production host |

**grafton-ndi** highlights:
- Safe Rust FFI over NDI 6 SDK (discovery, send, receive, FrameSync, tally, PTZ)
- Optional Tokio / async-std wrappers
- Self-hosted docs (NDI license prevents docs.rs hosting)
- Companion: [grafton-birddog](https://github.com/GrantSparks/grafton-birddog) for BirdDog camera API

---

## OMT (Open Media Transport)

[OMT](https://openmediatransport.org/) is a royalty-free, MIT-licensed LAN protocol (2025). Community-driven, positioned as an open alternative to proprietary LAN transports.

| Item | Detail |
|------|--------|
| Transport | TCP unicast |
| Discovery | DNS-SD + optional Discovery Server (port 6399) |
| Codecs | VMX1 (video), FPA1 (32-bit float planar audio) |
| Quality | Low / Medium / High / Preview |
| Formats | 4:2:2 default; 4:4:4+alpha up to 16-bit |
| Strengths | Fully open spec, sub-frame latency, per-frame XML metadata |
| Weaknesses | TCP unicast scales bandwidth with receivers; smaller ecosystem than NDI |

**Official resources:**
- [openmediatransport.org](https://openmediatransport.org/)
- [GitHub Organization](https://github.com/openmediatransport)
- [Protocol spec (PROTOCOL.md)](https://github.com/openmediatransport/libomtnet/blob/main/PROTOCOL.md)

### Products / Tools

| Vendor | Products |
|--------|----------|
| [vMix](https://www.vmix.com/) 29+ | OMT I/O, Desktop Capture, Viewer, Matrix Router |
| [Sienna](https://www.sienna-tv.com/omt/) | Signal Generator, Monitor, Router, OBS Plugin |
| [OBS Studio](https://obsproject.com/) | Via [omtplugin](https://github.com/openmediatransport/omtplugin) |
| [Central Control](https://centralcontrol.io/) | OMT Signal Generator |
| Raspberry Pi 5 | [omtcapture](https://github.com/openmediatransport/omtcapture) / [omtplayer](https://github.com/openmediatransport/omtplayer) |

### Open Source

**Official ([openmediatransport](https://github.com/openmediatransport)):**
- [libomtnet](https://github.com/openmediatransport/libomtnet) — .NET reference implementation
- [libomt](https://github.com/openmediatransport/libomt) — C wrapper
- [libvmx](https://github.com/openmediatransport/libvmx) — VMX1 codec
- [omtplugin](https://github.com/openmediatransport/omtplugin) — OBS plugin (Windows/macOS)
- [omtcapture](https://github.com/openmediatransport/omtcapture) — Raspberry Pi 5 encoder
- [omtplayer](https://github.com/openmediatransport/omtplayer) — Raspberry Pi 5 decoder
- [.github](https://github.com/openmediatransport/.github) — Org docs and download links

**Community:**
- [MikanseiLaboratory/openmediatransport-rs](https://github.com/MikanseiLaboratory/openmediatransport-rs) — Pure Rust OMT stack
- [MikanseiLaboratory/vmx-rs](https://github.com/MikanseiLaboratory/vmx-rs) — Pure Rust VMX1 codec
- [MikanseiLaboratory/omt-tools](https://github.com/MikanseiLaboratory/omt-tools) — OMT tooling (Tauri launcher)

---

## SRT (Secure Reliable Transport)

[SRT](https://www.srtalliance.org/) is an open-source protocol by Haivision (2017) for low-latency live video over unreliable networks. [2020 Emmy Award](https://www.haivision.com/products/srt-secure-reliable-transport/) winner.

| Item | Detail |
|------|--------|
| License | MPL 2.0 |
| Security | AES-128/256 |
| Strengths | Internet-grade reliability, firewall traversal, wide adoption |
| Weaknesses | Not suited for LAN multicast fan-out |

**Resources:** [SRT Alliance](https://www.srtalliance.org/) · [Haivision SRT](https://www.haivision.com/products/srt-secure-reliable-transport/) · [libsrt docs](https://github.com/Haivision/srt/blob/master/docs/README.md)

### Products (selected)

Haivision (Makito X4, SRT Gateway), Teradek, Magewell, Kiloview, AJA, Vizrt TriCaster, vMix, OBS, FFmpeg, AWS Elemental MediaConnect

### Open Source

- [Haivision/srt](https://github.com/Haivision/srt) — Reference library (libsrt)
- [Haivision/srt-live-transmit](https://github.com/Haivision/srt-live-transmit) — CLI stream relay tool
- [FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg) — Native SRT mux/demux via libsrt
- [obsproject/obs-studio](https://github.com/obsproject/obs-studio) — Built-in SRT output
- [GStreamer](https://gitlab.freedesktop.org/gstreamer/gst-plugins-bad) — `srtsrc` / `srtsink` elements

---

## WebRTC / WHIP / WHEP

[WebRTC](https://webrtc.org/) enables real-time browser communication. [WHIP](https://datatracker.ietf.org/doc/rfc9725/) (ingest) and [WHEP](https://www.ietf.org/archive/id/draft-ietf-wish-whep-18.html) (egress) standardize HTTP-based signaling for live streaming.

| Item | Detail |
|------|--------|
| Latency | 50–250 ms |
| Codecs | H.264, VP8/VP9, AV1, Opus |
| Strengths | Browser-native, simple HTTP handshake |
| Weaknesses | Not for uncompressed LAN production; needs SFU/MCU design |

### Products (selected)

Nimble Streamer, MediaMTX, Janus, Cloudflare Stream, Red5 Pro, Dolby OptiView, OBS (WHIP), Larix Broadcaster, Sebiu Labs WHEP Gateway

### Open Source

- [bluenviron/mediamtx](https://github.com/bluenviron/mediamtx) — Media server (RTSP/RTMP/SRT/WebRTC/WHIP/WHEP)
- [janus-gateway/janus](https://github.com/meetecho/janus-gateway) — WebRTC server/gateway
- [pion/webrtc](https://github.com/pion/webrtc) — Pure Go WebRTC stack
- [aiortc/aiortc](https://github.com/aiortc/aiortc) — Python WebRTC
- [Eyevinn/webrtc-player](https://github.com/Eyevinn/webrtc-player) — WHEP browser player
- [Eyevinn/whip-whep-js](https://github.com/Eyevinn/whip-whep-js) — WHIP/WHEP client library
- [obsproject/obs-studio](https://github.com/obsproject/obs-studio) — Native WHIP output
- [FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg) — WHIP/WHEP support (in progress)

---

## Other Major Standards

### AES67
Open AES interoperability standard (RTP + PTP + SDP). Bridge between Dante, RAVENNA, Livewire, etc.  
→ [AIMS AES67 FAQ](https://aimsalliance.org/aes67-faq/)

### Dante
[Audinate Dante](https://www.getdante.com/) — dominant Pro AV audio AoIP (~400+ manufacturers). Video extension: [Dante AV](https://www.getdante.com/products/dante-av/).

### RAVENNA
[RAVENNA](https://www.ravenna-network.com/) — open AoIP for broadcast; native ST 2110/AES67 integration.  
→ [Standards Comparison](https://www.ravenna-network.com/overview/standards-comparison/)

### RIST
[RIST](https://www.rist.tv/) — VSF standard for interoperable internet live transport.  
→ [RIST Tested Products](https://www.rist.tv/certified-products) — Cobalt Digital, Evertz, Grass Valley, Zixi, Net Insight Nimbra

### SDVoE
[SDVoE](https://sdvoe.org/) — zero-latency uncompressed HDMI over 10GbE (Semtech).  
→ [Specifications](https://sdvoe.org/technology/specifications/)

### IPMX
[IPMX](https://ipmx.io/) — ST 2110 + AES67 + NMOS for Pro AV (HDCP, KVM, discovery).  
Certified products from PlexusAV, Barco, Lawo, Matrox (2026+).

### NMOS
[NMOS](https://specs.amwa.tv/nmos/) — discovery and connection management for ST 2110 (IS-04, IS-05, IS-08).

### ST 2022 (legacy)
MPEG-2 TS over IP. ST 2022-6 wraps uncompressed SDI (~30% more bandwidth than ST 2110 for 1080p).

---

## Open Source Projects

A consolidated index of open-source AV over IP implementations, grouped by protocol.

### Cross-Protocol / General Purpose

| Project | Description |
|---------|-------------|
| [FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg) | SRT, RIST, WebRTC/WHIP; universal media toolkit |
| [GStreamer](https://gitlab.freedesktop.org/gstreamer/gstreamer) | Plugin pipeline for SRT, RTP, WebRTC |
| [obsproject/obs-studio](https://github.com/obsproject/obs-studio) | Live production; SRT, WHIP; NDI/OMT via plugins |
| [VLC](https://code.videolan.org/videolan/vlc) | Playback; librist and libsrt support |

### SMPTE ST 2110 & NMOS

| Project | Description |
|---------|-------------|
| [OpenVisualCloud/Media-Transport-Library](https://github.com/OpenVisualCloud/Media-Transport-Library) | Software ST 2110 stack (DPDK/AF_XDP); -10/-20/-21/-30/-40, ST 2022-7 |
| [OpenVisualCloud/Media-Communications-Mesh](https://github.com/OpenVisualCloud/Media-Communications-Mesh) | Distributed ST 2110 media mesh built on MTL |
| [sony/nmos-cpp](https://github.com/sony/nmos-cpp) | NMOS Registry, Node, Connection API (IS-04, IS-05) in C++ |
| [AMWA-TV/nmos-testing](https://github.com/AMWA-TV/nmos-testing) | Official NMOS API conformance testing tool |
| [rhastie/easy-nmos](https://github.com/rhastie/easy-nmos) | Docker Compose NMOS lab (registry + node + testing) |
| [sony/nmos-js](https://github.com/sony/nmos-js) | NMOS client UI/library in JavaScript (IS-04, IS-05) |
| [bbc/nmos-web-router](https://github.com/bbc/nmos-web-router) | Web-based NMOS routing controller |

### NDI

| Project | Description | Activity |
|---------|-------------|----------|
| [DistroAV/DistroAV](https://github.com/DistroAV/DistroAV) | OBS plugin for NDI (GPL-2.0); requires NDI Runtime 6.3+ | ★★★★☆ (4.5k★, Jun 2026) |
| [GrantSparks/grafton-ndi](https://github.com/GrantSparks/grafton-ndi) | Idiomatic Rust bindings for NDI 6 SDK; async, PTZ, FrameSync | ★★★☆☆ (33★, v1.0.0 Jun 2026) |
| [GrantSparks/grafton-birddog](https://github.com/GrantSparks/grafton-birddog) | Rust bindings for BirdDog camera API | Companion to grafton-ndi |

### OMT

| Project | Description |
|---------|-------------|
| [openmediatransport/libomtnet](https://github.com/openmediatransport/libomtnet) | Official .NET OMT implementation |
| [openmediatransport/libvmx](https://github.com/openmediatransport/libvmx) | VMX1 codec |
| [openmediatransport/omtplugin](https://github.com/openmediatransport/omtplugin) | OBS plugin |
| [MikanseiLaboratory/openmediatransport-rs](https://github.com/MikanseiLaboratory/openmediatransport-rs) | Community Rust OMT stack |
| [MikanseiLaboratory/vmx-rs](https://github.com/MikanseiLaboratory/vmx-rs) | Community Rust VMX1 codec |

### SRT

| Project | Description |
|---------|-------------|
| [Haivision/srt](https://github.com/Haivision/srt) | libsrt reference implementation |
| [Haivision/srt-live-transmit](https://github.com/Haivision/srt-live-transmit) | CLI relay and testing tool |

### RIST

| Project | Description |
|---------|-------------|
| [librist](https://code.videolan.org/rist/librist) | Reference RIST library (VSF TR-06-1/2) |
| [nanake/librist](https://github.com/nanake/librist) | GitHub mirror of librist |

### WebRTC / WHIP / WHEP

| Project | Description |
|---------|-------------|
| [bluenviron/mediamtx](https://github.com/bluenviron/mediamtx) | Ready-to-use media server with WHIP/WHEP |
| [janus-gateway/janus](https://github.com/meetecho/janus-gateway) | General-purpose WebRTC gateway |
| [pion/webrtc](https://github.com/pion/webrtc) | Go WebRTC implementation |
| [aiortc/aiortc](https://github.com/aiortc/aiortc) | Python WebRTC |
| [Eyevinn/webrtc-player](https://github.com/Eyevinn/webrtc-player) | WHEP player component |
| [Eyevinn/whip-whep-js](https://github.com/Eyevinn/whip-whep-js) | WHIP/WHEP JS client |

### Audio over IP

| Project | Description |
|---------|-------------|
| [linuxaudio/jacktrip](https://github.com/jacktrip/jacktrip) | Low-latency networked audio (not AES67, but relevant) |
| [bondagit/aes67-linux-daemon](https://github.com/bondagit/aes67-linux-daemon) | Experimental AES67 daemon for Linux |

---

## Selection Guide

```
LAN live production (low cost, easy setup)
  → NDI / OMT (choose OMT for open spec)

LAN live production (highest quality, 10GbE available)
  → SDVoE / ST 2110 / IPMX

Broadcast facility / OB truck / IP plant
  → ST 2110 + NMOS + PTP

Audio only (conferencing, sound)
  → Dante (ecosystem) / AES67 (interop)

Internet contribution & distribution
  → SRT / RIST

Browser viewing, sub-second latency
  → WebRTC + WHIP/WHEP
```

---

## Related Resources

### Industry Alliances
- [AIMS Alliance](https://aimsalliance.org/) · [SRT Alliance](https://www.srtalliance.org/) · [RIST Forum](https://www.rist.tv/)
- [SDVoE Alliance](https://sdvoe.org/) · [VSF](https://www.vsf.tv/) · [AMWA](https://www.amwa.tv/) · [AVIXA](https://www.avixa.org/)

### Learning
- [SMPTE ST 2110 FAQ](https://www.smpte.org/smpte-st-2110-faq)
- [AVIXA — AV over IP Standards Overview](https://xchange.avixa.org/posts/av-over-ip-standards-overview-different-standards-for-different-tasks)
- [RAVENNA Standards Comparison](https://www.ravenna-network.com/overview/standards-comparison/)

---

## Contributing

Pull requests welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released under [CC0 1.0 Universal](LICENSE).
