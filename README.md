# WDM Optical Networks - Complete Simplified Guide

---

## Part 1: Network Basics

### Generic Network Architectures

Think of a communication network like a postal system with multiple layers:

1. **Access Networks**
   - Where users connect (home, office, local)
   - Like local post offices
   - Example: Your home internet connection to your ISP

2. **Metro Network**
   - Connects cities/regions
   - Like regional sorting facilities
   - Handles local carrier traffic

3. **Long Haul Network (Core/Backbone)**
   - Connects continents
   - Like international mail distribution centers
   - Carries massive amounts of data between major cities
   - **Long Haul Nodes**: Switching centers where multiple routes intersect
     - Switch and groom traffic (route it properly)
     - Add protection and restoration (backup routes)

---

## Part 2: Network Generations

| Generation | Name | Medium | Technology | Processing | Status |
|---|---|---|---|---|---|
| **G1** | Electronic Network | Copper cables | Electronic | Electronic | Old (still used) |
| **G2** | Optical Network | Fiber | Single wavelength | Electronic | Legacy systems |
| **G3** | Optical Network | Fiber | WDM | Electronic + Hybrid | **Currently deployed** |
| **G4** | All-Optical | Fiber | WDM | Optical | Research phase |

### Key Differences:

**G1 (Copper)**: Slow, like sending one letter at a time through one tube
**G2 (Single-wavelength Fiber)**: Faster, but still one "color" of light per fiber
**G3 (WDM)**: Multiple "colors" of light in one fiber - **this is what we focus on**
**G4 (All-Optical)**: Processing happens with light (very advanced)

---

## Part 3: Why WDM? The Problem

### The Fiber/Processor Bottleneck

**The Crisis:**
- Fiber capacity grows MUCH faster than switching capacity
- Microprocessors dissipate increasing power (heat)
- Electronic switches can't keep up with fiber speed

**Real Example:**
To handle a petabit (1 million gigabits) interconnect:
- Would need **100,000 ports** at 10 Gb/s each
- Would need **800,000 fiber connections**
- Physically impossible with current electronics!

### Solution: Use multiple wavelengths (colors) in one fiber

Instead of one conversation per fiber, pack many conversations (different light colors) into one fiber.

---

## Part 4: WDM Network Evolution

### Timeline:
- **1995**: Point-to-Point systems (2.5 Gb/s, 8 channels)
- **2000**: OADM introduction (10 Gb/s, 16-32 channels)
- **2005**: Flexible networks (40 Gb/s, 64 channels)
- **2010+**: Meshed networks (100-400 Gb/s, 128+ channels)

### What Changed:
1. **Line Bit Rate**: Data speed per wavelength increased
2. **Number of Channels**: More colors of light
3. **Transparent Distance**: How far light travels before needing conversion
4. **Network Architecture**: Fixed → Flexible → Fully Meshed
5. **Components**: Simple → Complex optical switches

---

## Part 5: Three Generations of WDM Networks

### Generation 1: Point-to-Point WDM System

**What it is:** Simple direct connection between two locations

**How it works:**
```
Location A ──[Multiple wavelengths in fiber]──> Location B
   λ₁ → Transmitter 1
   λ₂ → Transmitter 2
   λ₃ → Transmitter 3
   λ₄ → Transmitter 4
```

**Components:**
- **TE (Terminal Equipment)**: Your device (router, etc.)
- **TX (Transmitter)**: Converts electrical to optical signal
- **Wavelength Multiplexer**: Combines all λ's into one fiber
- **Optical Amplifier**: Boosts signal strength
- **Wavelength Demultiplexer**: Splits λ's back at destination

**Key Facts:**
- Commercially available since 1990s
- 64 channels common, 160 max at that time
- Cost-effective upgrade for existing point-to-point links

**Example:** A university connecting its main campus to a remote research facility 100km away, using 4 different wavelengths to send 4 different data streams simultaneously.

---

### Generation 2: Wavelength Add/Drop Multiplexers (WADM/OADM)

**The Problem with Point-to-Point:** 
If you want to pick up or drop off data at an intermediate location, you have to convert the light to electricity, process it, then convert back—inefficient!

**The Solution:**
Add the ability to pick up and drop off specific wavelengths at intermediate nodes.

**How it works:**
```
─→ DEMUX (split by color) ─→ SWITCHES (pick/drop) ─→ MUX (combine) ─→
   λ₁   ↓ [switch]↓   λ₁
   λ₂   ↓ [switch]↓   λ₂
   λ₃   ↓ [switch]↓   λ₃
   λ₄   ↓ [switch]↓   λ₄
        ↓ (can drop here)
```

**Example:** 
A fiber backbone from New York to Los Angeles:
- NY → Chicago → Denver → LA
- Wavelength 1 (λ₁) goes: NY → LA (full path)
- Wavelength 2 (λ₂) goes: NY → Chicago → (drops, doesn't continue)
- New data (λ₂) added: Chicago → Denver → LA

**Advantage:** Very flexible for linear networks (like a highway)
**Limitation:** Only works in a line, not a mesh network

---

### Generation 3: Fiber and Wavelength Cross-Connects

**The Need:** Build networks where data can go in many directions, not just a line.

**Three Types:**

#### A) Passive Star
```
Input Fiber 1 ─┐
Input Fiber 2 ─┼─→ [PASSIVE STAR] ─→ Output Fiber 1
Input Fiber 3 ─┼─→  (broadcasts)   ─→ Output Fiber 2
Input Fiber 4 ─┘                    ─→ Output Fiber 3
                                    ─→ Output Fiber 4
```

**How it works:**
- Takes a signal from input fiber, splits it equally to all outputs
- Like a radio broadcast station - everyone gets the same signal
- NO wavelength reuse (can't use λ₁ twice)
- **Problem**: Collisions! If two sources send λ₁ simultaneously, they crash

**Example:** 4 universities all transmitting λ₁ through a star → COLLISION!

---

#### B) Passive Router (Wavelength Router)
```
Input Fiber 1 ──┐        ┌─→ Output Fiber 1 (gets λ₁, λ₂, λ₃, λ₄)
Input Fiber 2 ──┼─ DEMUX─┤
Input Fiber 3 ──┼─[ROUTER]─┼─→ Output Fiber 2 (gets λ₁, λ₂, λ₃, λ₄)
Input Fiber 4 ──┘─ MUX ─┘
                └─→ Output Fiber 3 (gets λ₁, λ₂, λ₃, λ₄)
                └─→ Output Fiber 4 (gets λ₁, λ₂, λ₃, λ₄)
```

**How it works:**
- Routes each wavelength to a SPECIFIC output fiber
- λ₁ from Input 1 → Output 2
- λ₁ from Input 2 → Output 4
- λ₁ from Input 3 → Output 1
- **Allows wavelength reuse**: Multiple λ₁'s, but on different output paths

**Key advantage:** Fixed routing pattern (determined at manufacturing)

**Names in market:** WGR, AWG, Wavelength Router, Latin Router

**Example:** 
Building A wants to send data to Building D using λ₁
Building C also wants to send to a different location using λ₁ (on different output)
Both can happen simultaneously!

---

#### C) Active Switch (Wavelength Selective Cross-Connect)
```
Input 1 ──┐        λ₁ ┌─→ Output 1
Input 2 ──┼─ DEMUX─┤ 
Input 3 ──┼─[SWITCH]─┤ λ₂ ┌─→ Output 2
Input 4 ──┘── MUX──┤
                   λ₃ ┌─→ Output 3
                   λ₄ ┌─→ Output 4
```

**How it works:**
- Similar to passive router BUT **routing is reconfigurable**!
- Instead of fixed routing, you can change which wavelength goes where
- Each wavelength gets its own switch fabric
- Can be reconfigured on the fly

**Example:**
- Initially: Input 1, λ₁ → Output 2
- Later: Reconfigure → Input 1, λ₁ → Output 4
- **Like having programmable telephone switching**

**Limitation:** Can be "blocking"
- Problem: Can't send two signals with same λ from same input to same output
- Solution: Use **wavelength converters** to change the color of light

**Wavelength Converter Fix:**
If two calls need Input 1, λ₁ → Output 2:
- Call 1: Input 1, λ₁ → Output 2
- Call 2: Input 1, λ₁ (converted to λ₃) → Output 2
- Now both work!

---

## Part 6: Three Switching Technologies

### Technology 1: Wavelength-Routed Networks (OCS - Optical Circuit Switching)

**Core Concept:** Establish a permanent path (lightpath) before sending data

**How it works:**

1. **Setup Phase**: Request a connection
   ```
   Source → Network → Destination
   "I need a path from Node A to Node D"
   ```

2. **Lightpath Establishment**: Find route and wavelength
   ```
   A → B (λ₁) → C (λ₁) → D (λ₁)
   ```

3. **Data Transfer**: Stream data continuously
   ```
   Data flows constantly on this λ₁ path
   ```

4. **Teardown**: Release resources when done

**Like:** Telephone system
- Call setup (dial tone)
- Connection established
- Talk
- Hang up

**Key Challenge: The Wavelength Continuity Constraint**

Problem: Different nodes might use different wavelengths
```
Path needs λ₁ (Node A-B) but only λ₃ available (Node B-C)
                         ↓
              Need wavelength converter!
```

**The RWA Problem (Routing and Wavelength Assignment):**

Given:
1. A set of connection requests
2. Limited wavelengths per fiber

Find:
1. Best route for each connection
2. Which wavelength to assign

**Example:**
```
Request 1: Node 1 → Node 5 (needs a path)
Request 2: Node 2 → Node 6 (needs a path)
Request 3: Node 3 → Node 5 (needs a path)

Available: 4 wavelengths, some routes shared

Solution:
Req 1: Route 1→4→5 using λ₁
Req 2: Route 2→4→6 using λ₂
Req 3: Route 3→7→5 using λ₁ (different fiber, so OK)
```

**Routing Strategies:**

1. **Fixed Routing**: Always use shortest path (Dijkstra's algorithm)
   - Simple, fast
   - May block requests

2. **Fixed-Alternate Routing**: Try 3-4 different paths
   - Better blocking performance
   - More computational overhead

3. **Adaptive Routing**: Dynamically choose based on network state
   - Best performance
   - Most complex

**Wavelength Assignment Strategies:**

1. **Random**: Assign any available wavelength
   - Simple but inefficient

2. **First-Fit (FF)**: Take first available wavelength
   - Quick to compute
   - Good if wavelengths numbered logically

3. **Least-Used (LU)**: Assign wavelength used least across network
   - Better load balancing
   - Spreads usage evenly

4. **Most-Used (MU)**: Assign wavelength already in use on route
   - Fewer wavelength conversions needed
   - Cheaper (converters cost money!)

**Example of First-Fit:**
```
Path: Node 1→2→3→4

Wavelength usage:
λ₀ [USED] [USED] [FREE] [USED]
λ₁ [USED] [FREE] [USED] [FREE]
λ₂ [FREE] [USED] [USED] [USED]
λ₃ [USED] [USED] [USED] [FREE]

First-Fit looks at each link in order:
Link 1-2: λ₀ is used, try λ₁... λ₁ is used, try λ₂... λ₂ is FREE! ✓
Link 2-3: λ₂ is used, try λ₃... λ₃ is used, try λ₀... λ₀ is FREE! ✗
         Can't use λ₂ continuously!
         Need wavelength converter
```

---

### Technology 2: Optical Packet Switching (OPS)

**The Dream:** Process packets in the optical domain (no conversion to electronics)

**The Speed-Mismatch Problem:**

Why we need this:
- Fiber capacity doubles every 2-3 years (exponential)
- Electronic switching speeds double every 3-4 years
- **Gap is widening!**

**Real Numbers:**
To switch a petabit (10¹⁵ bits) interconnect:
- Need 100,000 ports at 10 Gb/s each
- 800,000 fiber connections
- **Physically impossible to build with electronics!**

**How OPS would work:**
```
Incoming IP packet (electronic) 
         ↓
Converted to optical (light)
         ↓
Processed entirely in optical domain
         ↓
Routed to output fiber (all optical!)
         ↓
No conversion back to electronics until destination
```

**Why it's hard:**

We lack:
1. **Optical Memory**: We have RAM (electronic). No optical equivalent!
   - Can't "store" light like we store bits in RAM
   
2. **Optical Computing**: 
   - Can't do header lookup in light
   - Can't modify packet address in optical domain
   - Optical logic circuits don't exist yet

**The Contention Problem:**

When two packets want same output simultaneously:
```
Packet A ──┐
           ├─→ Output Port 1, λ₁, same time
Packet B ──┘    COLLISION! What happens?
```

**In Electronics:** Use RAM buffer (store one, send later)
**In Optics:** No optical RAM! Two solutions:

**Solution 1: Fiber Delay Lines (FDL)**
```
Packet A ─────────────────────→ Output
                ↑ delayed
Packet B ──→ [Long fiber] ──→ (sent later)
```
Send one packet through long fiber to delay it, let other one go first

**Solution 2: Wavelength Converters**
```
Packet A ─→ Output, λ₁
Packet B ─→ Output, λ₁ (converted to λ₂)
Both on same fiber but different colors!
```

**Status:** OPS is still mostly research. Too hard to implement.

---

### Technology 3: Optical Burst Switching (OBS)

**The Compromise:** Between wavelength-routed (simple but inflexible) and OPS (ideal but impossible)

**Key Idea:**
- Group multiple IP packets into a "burst"
- Send the burst as one unit
- Control packet sent ahead to reserve resources
- Burst follows on the exact wavelength, with exact timing

**Like:** Pre-numbered parcels with manifest
- Control packet = manifest/address label
- Data burst = actual packages
- No conversion to electronics needed mid-network

**How it works:**

```
1. Ingress Node:
   - Multiple IP packets arrive
   - Assemble into a burst
   - Generate control packet (sent early)
   - Send burst after offset time

2. Core Network (Intermediate Nodes):
   - Control packet arrives first
   - Control plane processes in electronics
   - Sets up switching for data burst
   - Data burst passes through all-optically

3. Egress Node:
   - Receives burst
   - Disassembles back into IP packets
   - Delivers to destination
```

**Comparison: OPS vs OBS**

```
OPS:
- Individual packets processed
- Packet header examined at each hop
- Requires optical memory & computing
- More flexibility but much harder

OBS:
- Bursts of multiple packets
- Only control packet header examined
- Burst travels optically without processing
- Balanced approach, practical
```

---

## Part 7: Burst Assembly (How to Group Packets)

### Why Assemble Bursts?

Single packets → bursts because:
1. Better efficiency (fewer control messages)
2. More wavelength utilization
3. Lower overhead

### Three Assembly Methods:

#### 1) Timer-Based

**How it works:**
- Start timer
- Wait T milliseconds
- Send everything that arrived in that time

**Example:**
```
Time 0ms: Timer starts
Time 5ms: Packet 1 arrives
Time 8ms: Packet 2 arrives
Time 10ms: Timer expires → Send burst with Packets 1,2
```

**Tradeoff:**
- Timer too long → Packets wait (bad latency)
- Timer too short → Small bursts (lots of overhead)

**Best for:** Predictable traffic

---

#### 2) Threshold-Based

**How it works:**
- Keep collecting packets
- When X packets collected OR burst reaches Y bytes → Send burst

**Example:**
```
Threshold = 100 packets

Packet 1 arrives
Packet 2 arrives
...
Packet 100 arrives → Burst of exactly 100 packets sent
(even if just arrived!)
```

**Advantage:** Predictable burst size
**Disadvantage:** Variable delay (next packet might take 1ms or 100ms to arrive)

**Best for:** Bursty traffic (not smooth)

---

#### 3) Mixed Timer/Threshold

**How it works:**
- Either timer expires OR threshold reached
- Whichever comes first

**Example:**
```
Timer = 10ms
Threshold = 100 packets

Case A: 150 packets arrive in 5ms
  → Burst sent at 100 packets (threshold first)
  
Case B: Only 20 packets arrive in 10ms
  → Burst sent at 10ms (timer first)
```

**Best approach** but most complex to implement

---

## Part 8: Burst Scheduling

**The Job:** At ingress node, decide:
1. What offset time (delay between control packet and burst)?
2. Which wavelength/output link for this burst?
3. When to release resources?

### Two Scheduling Techniques:

#### 1) First-Fit (FF)

**Algorithm:**
```
For each burst:
  For each wavelength (in order):
    If wavelength is available:
      Assign burst to this wavelength
      Exit (don't check others)
```

**Advantage:** Fast (stop searching once found)
**Disadvantage:** May not find best wavelength

**Example:**
```
Available wavelengths: [λ₁, λ₂, λ₃, λ₄]
λ₁: Busy until 10.5ms
λ₂: Busy until 10.2ms ← First-Fit picks this!
λ₃: Busy until 10.1ms
λ₄: Busy until 10.3ms
```

---

#### 2) Latest Available Unused Channel (LAUC)

**Algorithm:**
```
For each burst:
  Find wavelength that becomes free LATEST
  Assign burst to that wavelength
```

**Advantage:** Better wavelength utilization (fills gaps)
**Disadvantage:** Slower computation

**Example:**
```
λ₁: Free at 10.5ms ← LAUC picks this (latest free time)
λ₂: Free at 10.2ms
λ₃: Free at 10.1ms
λ₄: Free at 10.3ms

Why? Longer wavelengths can be used by other bursts
```

---

## Part 9: OBS Signaling Protocols

**Goal:** How does control packet reserve bandwidth for data burst?

**Key Decision:** One-way or two-way?

### One-Way Reservation (Used in OBS)

**How it works:**
```
Source sends control packet → Network routes it → Destination

No acknowledgment sent back

Data burst follows on reserved wavelength
```

**Why OBS uses one-way?**
1. **Latency**: Two-way would double delay (send ack back)
2. **Flexibility**: Source doesn't wait for confirmation

**Three Signaling Protocols:**

#### 1) Just Enough Time (JET)

**Concept:**
- Control packet reserves bandwidth "just enough" for burst arrival
- Clever timing calculation

**How:**
```
Source calculates:
  "Burst will take 1ms to transmit"
  "Network delay is 5ms"
  
Source tells first node:
  "Reserve resources for 6ms starting at time T"
```

**Advantage:** Efficient (resources released soon after burst)
**Disadvantage:** Tight timing (no margin for error)

---

#### 2) Just In Time (JIT)

**Concept:**
- Control packet arrives, immediately followed by data burst
- Very tight synchronization

```
Time 0: Control packet arrives at Node 1
Time 0+ε: Data burst arrives at Node 1 (almost same time)
         Node 1 switches immediately
Time 0+2ε: Both travel to Node 2
```

**Best when:** Tight control possible (limited hops)

---

#### 3) Time Label (TL)

**Concept:**
- Control packet includes timestamp
- "Burst will arrive at time T"
- Nodes set up switch at that time

**Advantage:** More flexible (can handle variable delays)
**Disadvantage:** Requires accurate clocks everywhere

---

## Summary Table: Network Comparison

| Feature | OCS (Wavelength-Routed) | OPS | OBS |
|---|---|---|---|
| **Granularity** | Wavelength | Packet | Burst (100s packets) |
| **Switching** | Circuit-like | Packet-like | In-between |
| **Optical Processing** | None | Maximum | Minimal (control only) |
| **Implementation** | Deployed | Research | Testing |
| **Latency** | Low | Low | Medium |
| **Efficiency** | Good | Best | Very Good |
| **Complexity** | Medium | Very High | Medium-High |

---

## Key Takeaways

1. **WDM = Multiple colors of light in one fiber**
   - Solves electronic bottleneck problem

2. **Three Network Types:**
   - **OCS**: Fixed paths (like telephone)
   - **OPS**: Packet-level switching (like internet, but optical)
   - **OBS**: Hybrid approach (practical middle ground)

3. **The Challenge:**
   - Wavelength continuity (must use same color throughout path)
   - Limited wavelengths per fiber
   - Need to avoid collisions

4. **The Future:**
   - OCS deployed now (carrier backbones)
   - OBS in development (next generation)
   - OPS in research labs (long-term goal)

---

## Real-World Applications

**OCS Example:**
```
Netflix headquarters → Netflix data center (Los Angeles)
Dedicated λ₁ path established 24/7
All their streaming data flows on this wavelength
```

**OBS Example:**
```
Multiple companies sharing same fiber:
- Company A: Burst of 1000 packets on λ₁
- Company B: Burst of 500 packets on λ₂ 
- Control packets tell network "λ₁ coming in 50μs"
- Network sets up switch
- Both bursts travel through network optically
```

**Why not OPS now?**
```
Internet has billions of packets/second
Processing each at optical speeds = impossible with current technology
Would need optical memory & logic that doesn't exist yet
```
