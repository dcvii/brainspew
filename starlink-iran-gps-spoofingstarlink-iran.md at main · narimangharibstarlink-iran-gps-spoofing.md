---
title: starlink-iran-gps-spoofing/starlink-iran.md at main · narimangharib/starlink-iran-gps-spoofing
source: https://github.com/narimangharib/starlink-iran-gps-spoofing/blob/main/starlink-iran.md
author:
  - "[[narimangharib]]"
published:
created: 2026-01-14
description: Technical analysis of Starlink terminal telemetry showing GPS spoofing detection during Iran's January 2026 internet shutdown - starlink-iran-gps-spoofing/starlink-iran.md at main · narimangharib/starlink-iran-gps-spoofing
tags:
  - clippings
  - secpar
---
**Date of Capture:** January 2026 **Location:** Iran (confirmed via terminal telemetry) **Context:** Iranian government internet shutdown with reported GPS interference targeting satellite communications

---

## Executive Summary

This report analyzes debug telemetry from a Starlink terminal operating in Iran during an extended government-imposed internet blackout. The data provides **direct technical evidence** of:

1. **GPS spoofing/jamming detection** - The terminal identified anomalous GPS signals and activated countermeasures (`inhibitGps: true`)
2. **Severe performance degradation** - ~20% sustained packet loss; connection never stabilized in 24 minutes of operation
3. **Degraded beam tracking accuracy** - Pointing error (~1°) exceeds attitude uncertainty (0.32°), indicating the terminal struggles to maintain optimal satellite tracking
4. **Resilient but impaired connectivity** - The link survived but bandwidth was restricted and connection remained unstable

This documents state-level electronic warfare against consumer satellite internet infrastructure, revealing both the attack's effectiveness at degrading service and Starlink's resilience in maintaining basic connectivity.

---

### Primary Indicators

```
"gpsStats": {
    "gpsValid": true,
    "gpsSats": 18,
    "noSatsAfterTtff": false,
    "inhibitGps": true
}
```

| Field | Value | Interpretation |
| --- | --- | --- |
| `gpsValid` | `true` | GPS receiver hardware is functional and locked |
| `gpsSats` | `18` | 18 GPS satellites are being tracked (healthy count) |
| `noSatsAfterTtff` | `false` | Satellites remain visible after initial fix |
| `inhibitGps` | **`true`** | Terminal detected untrustworthy GPS signals and disabled GPS-based positioning |

The combination of evidence suggests **GPS spoofing** (injection of fake signals) rather than simple jamming (signal blocking):

| Jamming Signature | Spoofing Signature | This Terminal |
| --- | --- | --- |
| Low satellite count | Normal satellite count | **18 satellites** (normal) |
| GPS invalid | GPS valid | **GPS valid** |
| Signal loss | Anomalous signal characteristics | **Inhibited** (detected anomaly) |

If the GPS was simply being jammed (signals blocked), we would expect:

- `gpsValid: false` or
- Very low `gpsSats` count (0-5)

Instead, we see 18 satellites with valid lock but **inhibited positioning** - the terminal's anti-spoofing algorithms detected that the GPS signals, while present and strong, cannot be trusted. This is consistent with the Iranian government broadcasting fake GPS signals to confuse satellite terminals.

---

### Connection Stability

| Metric | Value | Significance |
| --- | --- | --- |
| Terminal Uptime | 1,413 seconds (~24 min) | Sufficient time to stabilize |
| Stable Connection Time | **0 seconds** | Never achieved stability |
| EKF Convergence | 198 seconds | Extended (fallback positioning) |

**Critical finding**: After 24 minutes of operation, the terminal recorded **zero seconds of stable connection**. The Extended Kalman Filter (sensor fusion for positioning) took 198 seconds to converge - significantly longer than typical - indicating the terminal was struggling to establish reliable position without GPS.

### Packet Loss

| Metric | Instantaneous | 5-Minute Average |
| --- | --- | --- |
| POP Ping Drop Rate | 50% | **22%** |
| General Ping Drop | 0% | **20%** |

Sustained 20-22% packet loss over 5 minutes confirms this is not a momentary glitch but ongoing degradation. For comparison, healthy Starlink connections typically show <1% packet loss.

### Bandwidth Restriction

```
"dlBandwidthRestrictedReason": 1,
"ulBandwidthRestrictedReason": 1
```

Both uplink and downlink show bandwidth restriction (reason code 1). This indicates the terminal or network has imposed throughput limits, potentially as a protective measure when operating in degraded mode.

### Subsystem Readiness

```
"readyStates": {
    "cady": false,
    "scp": true,
    "l1L2": true,
    "xphy": true,
    "aap": true,
    "rf": true
}
```

All subsystems report ready **except `cady: false`**. While the exact function of CADY is not publicly documented, it being the sole subsystem not ready - while RF, physical layer, and other components are operational - suggests it may be related to positioning or coordination functions affected by GPS inhibition.

---

| Parameter | Actual | Desired | Difference |
| --- | --- | --- | --- |
| Azimuth | \-1.11° | \-0.05° | **1.06°** |
| Elevation | 69.97° | 68.76° | **1.21°** |
| Attitude Uncertainty | — | — | 0.32° |

**Key observation**: The dish is pointing approximately **1-1.2° away** from its desired direction, while the attitude uncertainty is only **0.32°**. This means:

- The terminal *thinks* it knows where it's pointing (low uncertainty)
- But it's actually pointing in a slightly wrong direction (actual ≠ desired)
- The error is 3-4x larger than the uncertainty

This is consistent with the terminal using fallback positioning methods that are less accurate than GPS. The phased array can still track satellites, but suboptimally, resulting in degraded signal quality and throughput.

### Attitude Estimation

| Parameter | Value |
| --- | --- |
| Attitude Estimation State | 2 (Converged) |
| Tilt Angle | 19.17° |
| Boresight Elevation | 69.97° |

The terminal did achieve attitude convergence (state 2), meaning it established *some* position estimate. However, the pointing errors suggest this estimate is degraded compared to GPS-based positioning.

---

## Terminal Configuration

### Operational State

| Parameter | Value | Notes |
| --- | --- | --- |
| Country Code | `IR` | Confirmed Iran |
| Roaming | **Active** | Operating outside registered region |
| Obstruction | 10.6% | Minor, not significant |
| Mobility Class | 2 | Configured for portable use |

### Hardware

| Component | Version |
| --- | --- |
| Dish Hardware | `rev4_panda_prod2` (Standard rectangular) |
| Dish Software | `2026.01.02.mr71031` |
| Router Hardware | `v3` |
| Router Software | `2025.12.30.mr67903` |

### Signal Quality

| Metric | Status |
| --- | --- |
| SNR Above Noise Floor | Yes |
| SNR Persistently Low | No |
| Ethernet Link | 1000 Mbps |

The signal-to-noise ratio is healthy and not persistently low. This confirms the **radio link itself is functional** - the terminal can communicate with satellites. The problems stem from positioning uncertainty affecting beam optimization, not from inability to reach satellites.

---

## Initialization Timeline

How long each startup phase took:

| Phase | Time | Notes |
| --- | --- | --- |
| GPS Valid | 23s | GPS receiver locked quickly (but later inhibited) |
| RF Ready | 27s | Radio hardware initialized |
| Burst Detected | 27s | Found satellite signal |
| Initial Network Entry | 82s | Joined Starlink network |
| First Control Plane | 134s | Established control channel |
| Network Schedule | 150s | Received beam schedule |
| First POP Ping | 157s | First ground station ping |
| Attitude Initialization | 153s | Initial attitude estimate |
| **EKF Converged** | **198s** | Extended - fallback positioning |
| **Stable Connection** | **Never** | Did not achieve in 24 minutes |

The 198-second EKF convergence is notably extended. More critically, the terminal **never achieved stable connection** despite completing all other initialization phases.

---

## System Alerts

### Active Alerts

| Alert | Status |
| --- | --- |
| Roaming | **Active** |

- No thermal throttling
- No motor problems
- No unexpected location warning
- No power supply issues
- No obstruction map reset
- No ethernet link problems

The absence of `unexpectedLocation` alert is interesting - despite GPS being inhibited, the terminal determined its approximate location through alternative means (likely satellite ephemeris data and beam tracking).

---

## Technical Implications

1. **Anti-spoofing detection works** - Terminal correctly identified untrustworthy GPS and activated `inhibitGps`
2. **Fallback positioning is insufficient** - Connection never stabilized; pointing error 3-4x larger than uncertainty
3. **Bandwidth restriction engaged** - Both UL/DL restricted (reason 1) during GPS inhibition
4. **CADY subsystem affected** - Sole subsystem not ready, potentially positioning-related
5. **Opportunity for improvement** - Fallback algorithms need enhancement for contested RF environments

| Claim | Evidence Strength |
| --- | --- |
| GPS interference occurring | **Strong** - `inhibitGps: true` with 18 satellites |
| Spoofing vs jamming | **Strong** - High sat count + valid GPS + inhibited |
| Performance degradation | **Strong** - 20-22% sustained packet loss, 0s stable connection |
| Beam tracking affected | **Strong** - 1° pointing error vs 0.32° uncertainty |
| Causal link GPS→Performance | **Moderate** - Correlation clear, causation inferred |

1. **GPS spoofing documented** - Evidence of fake GPS signals, not just jamming
2. **Attack effectiveness** - Service severely degraded but not eliminated
3. **Resilience demonstrated** - Basic connectivity maintained under electronic warfare
4. **Mitigation limitations** - Current fallback positioning insufficient for normal performance

---

## Methodology

This analysis is based on debug telemetry exported from the official Starlink mobile application. The data represents a point-in-time snapshot of terminal status.

**Privacy protections applied:**

- Account identifiers removed
- Device serial numbers removed
- MAC addresses removed
- IP addresses removed
- Network configuration details removed
- Connected device information removed

---

## Conclusion

This telemetry provides documented technical evidence of:

1. **Active GPS spoofing** - Terminal detected fake GPS signals (18 satellites visible, GPS valid, but inhibited)
2. **Effective countermeasure activation** - Anti-spoofing triggered via `inhibitGps` flag
3. **Significant performance impact** - 20%+ packet loss, 0 seconds stable connection, bandwidth restricted
4. **Degraded beam tracking** - Pointing error 3-4x larger than attitude uncertainty
5. **Basic connectivity preserved** - Link survived despite electronic warfare

**The key finding**: While Starlink's anti-spoofing detection works, GPS interference effectively degrades service from broadband to barely-usable. The terminal stays online, but with:

- Sustained 20%+ packet loss
- Connection that never stabilizes
- Restricted bandwidth
- Suboptimal beam pointing

This demonstrates that GPS spoofing/jamming is an effective tactic to impair (though not eliminate) satellite internet service. SpaceX's fallback positioning algorithms maintain connectivity but cannot currently deliver normal performance under these conditions.

---

```
{
    "gpsStats": {
        "gpsValid": true,
        "gpsSats": 18,
        "noSatsAfterTtff": false,
        "inhibitGps": true
    }
}
```
```
{
    "initializationDurationSeconds": {
        "attitudeInitialization": 153,
        "burstDetected": 27,
        "ekfConverged": 198,
        "firstCplane": 134,
        "firstPopPing": 157,
        "gpsValid": 23,
        "initialNetworkEntry": 82,
        "networkSchedule": 150,
        "rfReady": 27,
        "stableConnection": 0
    }
}
```
```
{
    "alignmentStats": {
        "tiltAngleDeg": 19.167,
        "boresightAzimuthDeg": -1.107,
        "boresightElevationDeg": 69.966,
        "desiredBoresightAzimuthDeg": -0.047,
        "desiredBoresightElevationDeg": 68.763,
        "attitudeEstimationState": 2,
        "attitudeUncertaintyDeg": 0.325
    }
}
```
```
{
    "readyStates": {
        "cady": false,
        "scp": true,
        "l1L2": true,
        "xphy": true,
        "aap": true,
        "rf": true
    }
}
```

---

*This report was compiled from Starlink terminal debug telemetry. Original values preserved; privacy-sensitive information redacted. January 2026.*