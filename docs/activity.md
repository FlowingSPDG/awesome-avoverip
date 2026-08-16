# Protocol Activity & Adoption Metrics

Point-in-time snapshot for comparing how active and widely adopted each AV over IP protocol is.  
**Last updated:** August 2026

> See also: [`research.md`](research.md) for technical deep-dives (especially [NDI transport & RUDP](research.md#3-ndi)).

---

## How to Read This Document

| Column | Meaning |
|--------|---------|
| **Adoption** | Market penetration, product count, real-world deployment scale |
| **Dev Activity** | Recent releases, spec updates, SDK churn |
| **OSS Activity** | Open-source repo commits, releases, community size |

### Data Sources

- GitHub API (`pushed_at`, releases, stars) — August 2026
- Official alliance / vendor publications (AIMS, SRT Alliance, RIST Forum, NDI, Vizrt)
- crates.io / npm where applicable
- SMPTE / AMWA / IETF standards revision dates

---

## Summary Dashboard

| Protocol | Category | Adoption | Dev Activity | OSS Activity |
|----------|----------|----------|--------------|--------------|
| [NDI](#ndi) | LAN video | High | High | Medium |
| [OMT](#omt) | LAN video | Low | High | Medium |
| [ST 2110](#st-2110) | Broadcast IP | High | High | Medium |
| [IPMX](#ipmx) | Pro AV (open) | Low | High | Low |
| [SRT](#srt) | WAN contribution | High | High | High |
| [RIST](#rist) | WAN contribution | High | Medium | High |
| [WebRTC/WHIP/WHEP](#webrtc) | Browser / cloud | High | High | High |
| [Dante](#dante) | Audio AoIP | High | High | Low |
| [SDVoE](#sdvoe) | LAN HDMI | High | Medium | None |

---

## NDI

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **First released** | 2015 (10th anniversary 2025) | [IBC 2025](https://www.ibc.org/ibc-show/news/ndi-open-standard-turns-ten-with-renewed-ambition/22439) |
| **Latest core tech** | NDI 6.3 (Jan 2026); 6.3.1 follow-up | [NDI 6.3 press](https://ndi.video/stories/press/ndi-6-3-core-tech-update-brings-advanced-control-and-visibility/) |
| **Certified products** | 2,000+ products, 600+ manufacturers (2024) | [Vizrt / Motilde](https://motilde.com/en/ndi-potential-realities-in-monitoring-market/) |
| **NDI Tools downloads** | ~9,000/week (Mac + Windows) | [IBC 2025, Roberto Musso](https://www.ibc.org/ibc-show/news/ndi-open-standard-turns-ten-with-renewed-ambition/22439) |
| **SDK docs updated** | Continuous (GitBook); references NDI 6.3 | [docs.ndi.video](https://docs.ndi.video/) |
| **Corporate status** | Standalone open standard (spun from Vizrt, 2025) | [IBC 2025](https://www.ibc.org/ibc-show/news/ndi-open-standard-turns-ten-with-renewed-ambition/22439) |

### Open Source Ecosystem

| Repo | Stars | Last Push | Latest Release | Notes |
|------|-------|-----------|----------------|-------|
| [DistroAV/DistroAV](https://github.com/DistroAV/DistroAV) | 4,508 | 2026-06-29 | Active | OBS NDI plugin; 65 open issues |
| [GrantSparks/grafton-ndi](https://github.com/GrantSparks/grafton-ndi) | 33 | 2026-06-15 | v1.0.0 (2026-06) | Rust NDI 6 SDK bindings; ~53k crates.io downloads |
| [obsproject/obs-studio](https://github.com/obsproject/obs-studio) | 75,046 | 2026-08-15 | — | NDI via DistroAV plugin |

**OSS notes:** NDI protocol is closed, but the **integration layer** is active (DistroAV, grafton-ndi). grafton-ndi is the most actively maintained third-party SDK wrapper (Rust, NDI 6).

---

## OMT

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **First released** | May 2025 | [openmediatransport.org](https://openmediatransport.org/) |
| **Latest SDK release** | libomtnet v1.0.0.16 (2026-06) | [GitHub releases](https://github.com/openmediatransport/libomtnet/releases) |
| **Shipped in products** | vMix 29+ (Oct 2025), OBS plugin, Sienna tools | [vMix KB](https://www.vmix.com/knowledgebase/article.aspx/380/video-quality-settings-for-omt) |
| **GitHub org** | 12 public repos, 269 followers | [openmediatransport](https://github.com/openmediatransport) |
| **Adopters list** | Small, growing (vMix, Sienna, Central Control) | Official site |

### Open Source Ecosystem

| Repo | Stars | Last Push | Latest Release | Notes |
|------|-------|-----------|----------------|-------|
| [openmediatransport/omtplugin](https://github.com/openmediatransport/omtplugin) | 66 | 2026-06-03 | v1.0.0.16 | OBS plugin |
| [openmediatransport/libomtnet](https://github.com/openmediatransport/libomtnet) | 26 | 2026-07-23 | v1.0.0.16 | Official .NET stack |
| [openmediatransport/libvmx](https://github.com/openmediatransport/libvmx) | 24 | 2026-08-14 | — | VMX1 codec |
| [openmediatransport/omtcapture](https://github.com/openmediatransport/omtcapture) | 20 | 2026-04-29 | — | Pi 5 encoder; slower cadence |
| [MikanseiLaboratory/openmediatransport-rs](https://github.com/MikanseiLaboratory/openmediatransport-rs) | 1 | 2026-08-12 | — | Community Rust stack |
| [MikanseiLaboratory/vmx-rs](https://github.com/MikanseiLaboratory/vmx-rs) | 1 | 2026-08-12 | — | Community Rust codec |
| [MikanseiLaboratory/omt-tools](https://github.com/MikanseiLaboratory/omt-tools) | 4 | 2026-08-12 | — | Tauri tooling |

**OSS notes:** Very young but **high commit velocity** on official repos (multiple pushes/week in mid-2026). Ecosystem size is tiny vs NDI.

---

## ST 2110

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **First published** | 2017–2019 (core parts) | [SMPTE ST 2110](https://www.smpte.org/standards/st2110) |
| **Latest revisions** | ST 2110-30:2025, ST 2110-41:2024 | [SMPTE recently updated](https://www.smpte.org/standards/recently-updated-documents) |
| **Industry award** | 2025 Emmy® Award | [SMPTE FAQ](https://www.smpte.org/smpte-st-2110-faq) |
| **Certified products** | 100+ AIMS member solutions | [AIMS Solutions](https://solutions.aimsalliance.org/) |
| **Deployment** | Dominant in broadcast IP facilities; IBC/NAB plugfests ongoing | Industry consensus |

### Open Source Ecosystem

| Repo | Stars | Last Push | Notes |
|------|-------|-----------|-------|
| [OpenVisualCloud/Media-Transport-Library](https://github.com/OpenVisualCloud/Media-Transport-Library) | 241 | 2026-08-13 | Software ST 2110 stack; active DPDK/AF_XDP development |
| [OpenVisualCloud/Media-Communications-Mesh](https://github.com/OpenVisualCloud/Media-Communications-Mesh) | 23 | 2025-07 | Distributed mesh on MTL |
| [sony/nmos-cpp](https://github.com/sony/nmos-cpp) | 188 | 2026-08-13 | NMOS registry/node; IS-04/05 |
| [AMWA-TV/nmos-testing](https://github.com/AMWA-TV/nmos-testing) | 66 | 2026-08-07 | Official conformance tool |

**OSS notes:** Standards body activity is high (annual revisions). OSS focuses on **infrastructure plumbing** (MTL, NMOS), not end-user apps.

---

## IPMX

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **Based on** | ST 2110 + AES67 + NMOS + VSF TR-10 | [ipmx.io](https://ipmx.io/) |
| **Product certification** | Started 2026 (Geneva event) | [PlexusAV certification](https://www.avnetwork.com/products/plexusav-achieves-official-ipmx-certification-for-av-over-ip-products) |
| **Certified vendors** | PlexusAV, Barco, Lawo, Matrox (early) | AIMS / AMWA / VSF / EBU program |
| **Shipped products** | Early adopter stage | Growing at ISE/NAB 2026 |

**Notes:** Spec activity high; product count still low. Early adopter stage for certified products.

---

## SRT

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **Open sourced** | 2017 | Haivision |
| **Alliance members** | 650+ | [SRT Alliance](https://www.srtalliance.org/) |
| **Industry award** | 2020 Emmy® | Haivision |
| **Latest libsrt** | v1.5.6 (2026-07-20) | [GitHub releases](https://github.com/Haivision/srt/releases) |
| **Integrated in** | FFmpeg, OBS, VLC, GStreamer, cloud CDNs | Ubiquitous |

### Open Source Ecosystem

| Repo | Stars | Last Push | Open Issues |
|------|-------|-----------|-------------|
| [Haivision/srt](https://github.com/Haivision/srt) | 3,581 | 2026-08-06 | 371 |
| [Haivision/srt-live-transmit](https://github.com/Haivision/srt-live-transmit) | — | — | CLI relay tool |

**Release cadence:** 3 releases in 2026 (v1.5.4 → v1.5.6), steady maintenance.

**OSS notes:** Mature, heavily used, actively maintained reference implementation.

---

## RIST

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **VSF TR-06-1** | 2018 | First profile |
| **RIST Forum** | 150+ members | [VSF RIST AG](https://www.vsf.tv/RIST.shtml) |
| **Certified products** | 20+ vendors | [rist.tv/certified-products](https://www.rist.tv/certified-products) |
| **Integrated in** | FFmpeg, VLC, OBS, GStreamer, Wireshark | Via librist |
| **TR-06-3** | 2022 — tunneling (ST 2110, MPEG-TS) | Advanced profile |

### Open Source Ecosystem

| Repo | Location | Notes |
|------|----------|-------|
| [librist](https://code.videolan.org/rist/librist) | VideoLAN GitLab | Canonical; BSD-2-Clause |
| [nanake/librist](https://github.com/nanake/librist) | GitHub mirror | Sync mirror |

**OSS notes:** Active integration into major media tools. Spec evolution slower than SRT but strong broadcast vendor backing.

---

## WebRTC

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **WHIP standardized** | RFC 9725 (2025) | [IETF](https://datatracker.ietf.org/doc/rfc9725/) |
| **WHEP** | IETF draft (near RFC) | [draft-ietf-wish-whep](https://www.ietf.org/archive/id/draft-ietf-wish-whep-18.html) |
| **OBS WHIP** | Shipped in OBS 30+ | Native output |
| **Cloud adoption** | Cloudflare, Red5, Dolby, AWS | WHIP/WHEP ingest/egress |

### Open Source Ecosystem

| Repo | Stars | Last Push | Notes |
|------|-------|-----------|-------|
| [bluenviron/mediamtx](https://github.com/bluenviron/mediamtx) | 19,819 | 2026-08-15 | v1.20.0 (2026-08); very active |
| [pion/webrtc](https://github.com/pion/webrtc) | 16,718 | 2026-08-15 | Pure Go stack |
| [meetecho/janus-gateway](https://github.com/meetecho/janus-gateway) | 9,151 | 2026-07-27 | General WebRTC gateway |
| [obsproject/obs-studio](https://github.com/obsproject/obs-studio) | 75,046 | 2026-08-15 | WHIP output |
| [FFmpeg/FFmpeg](https://github.com/FFmpeg/FFmpeg) | 63,332 | 2026-08-15 | WHIP/WHEP in progress |

**OSS notes:** High OSS velocity. WHIP/WHEP standardization drove interoperable tooling in 2024–2026.

---

## Dante

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **Manufacturers** | 400+ | Audinate |
| **Pro AV audio share** | ~90% | Industry estimates |
| **Dante AV (video)** | Limited (AJA-centric) | Niche vs NDI/SDVoE |
| **AES67 mode** | Available on most devices | Interop bridge |

**Notes:** Dominant in audio; almost no open protocol implementation (proprietary). Activity is vendor-driven.

---

## SDVoE

| Metric | Value | Source / Notes |
|--------|-------|----------------|
| **Founded** | 2016 | [sdvoe.org](https://sdvoe.org/) |
| **Alliance members** | 50+ technology partners | SDVoE Alliance |
| **Differentiator** | <100 μs latency, lossless 4K60, 10GbE | Semtech BlueRiver |
| **OSS** | None (closed API/SDK) | Alliance-licensed |

**Notes:** Stable Pro AV niche. No public spec or OSS.

---

## Cross-Protocol OSS Comparison

| Repo | Protocol | Stars | Last Push | Release (2026) |
|------|----------|-------|-----------|------------------|
| mediamtx | WebRTC/WHIP/WHEP/SRT/RTSP | 19,819 | Aug 2026 | v1.20.0 (Aug) |
| obs-studio | SRT, WHIP, plugins | 75,046 | Aug 2026 | Frequent |
| FFmpeg | SRT, RIST, WHIP* | 63,332 | Aug 2026 | Continuous |
| srt | SRT | 3,581 | Aug 2026 | v1.5.6 (Jul) |
| DistroAV | NDI | 4,508 | Jun 2026 | Active |
| grafton-ndi | NDI (Rust) | 33 | Jun 2026 | v1.0.0 (Jun) |
| Media-Transport-Library | ST 2110 | 241 | Aug 2026 | Active |
| nmos-cpp | NMOS | 188 | Aug 2026 | Active |
| omtplugin | OMT | 66 | Jun 2026 | v1.0.0.16 (Jun) |
| openmediatransport-rs | OMT | 1 | Aug 2026 | Pre-1.0 |

\* WHIP/WHEP support in FFmpeg is evolving.

---

## Methodology Notes

1. **GitHub `pushed_at`** reflects any branch activity, not just releases.
2. **Stars** indicate awareness, not production usage.
3. **Product counts** come from vendor self-reporting (NDI, AIMS) — treat as order-of-magnitude.
4. Metrics are updated manually; automate via CI if this repo grows.

Contributions welcome — see [CONTRIBUTING.md](../CONTRIBUTING.md).
