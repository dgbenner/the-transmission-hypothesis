# State System & Frequency Fluctuation Concept

**Purpose:** Technical specification for the four broadcast states and frequency fluctuation behavior in The Transmission Hypothesis interface.

**For Implementation:** Reference this document when building the UI states and frequency monitoring display.

## State Hierarchy

### 1. SIGNAL LOST State
```
┌─────────────────────────────────┐
│                                 │
│     ◄ SIGNAL LOST ►             │
│                                 │
│     MONITORING: 540.7 MHz       │
│                                 │
│     [time] greenwich mean time  │
│                                 │
│     ░░░░░░░░░░░░░░░░░░░░       │
│                                 │
└─────────────────────────────────┘
```

### 2. STANDBY State
```
◄ STANDBY ►

MONITORING: 540.7 MHz
[current time] greenwich mean time

NEXT EVENT: PROTOCOL THETA-7
BEGINS: 19:00 greenwich mean time

0/20 SEATS AVAILABLE
```

### 3. COUNTDOWN State
```
◄ PROTOCOL THETA-7 ►

TRANSMISSION BEGINS IN:
00:14:37

MONITORING: 540.7 MHz
[time] greenwich mean time

3/20 SEATS OCCUPIED

████░░░░░░░░░░░░░░░░ 15%
```

### 4. ACTIVE TRANSMISSION State
```
◄ THETA-7 ► | 47M | 12/20

MONITORING: 540.7 MHz
[time] greenwich mean time
```

---

## Frequency Fluctuation Behavior

### Base Frequency
- Protocol home frequency: **540.7 MHz**
- Display as baseline most of the time

### Fluctuation Parameters
**Drift Range:** ±0.3 MHz (540.4 - 541.0 MHz)
- Small enough to feel like signal instability
- Large enough to be visually noticeable
- Stays within plausible tuning drift

**Timing Behavior:**
- Stable at 540.7 for 15-45 seconds (random interval)
- When drift occurs:
  - Individual digit "rolls" to new value
  - Takes 0.5-1.5 seconds to settle on new frequency
  - Holds new frequency for 3-8 seconds
  - Rolls back to 540.7 (or drifts to another value)

**Drift Patterns:**
- Single digit changes: 540.7 → 540.8 → 540.7
- Tenth place only: 540.7 → 540.9 → 540.6 → 540.7
- Occasional double drift: 540.7 → 540.5 → 541.0 → 540.7
- Very rare full instability: rapid rolling through multiple values

### Visual Effect Description

**Number Rolling Animation:**
```
5 4 0 . 7  →  5 4 0 . 8  →  5 4 0 . 9  →  5 4 0 . 7
              ↑ digit flips
              takes ~0.8 seconds
```

**Character Cycling (CRT-style):**
When digit changes, it doesn't smoothly transition - it **cycles through** intermediary values:
```
7 → 8 → 9 → 8 → 7
(each frame ~80-120ms, gives glitchy analog feel)
```

**Alternative: Slot Machine Roll:**
```
Digit position "spins" through numbers before landing:
7 → 2 → 5 → 9 → 3 → 8 (lands)
Quick roll effect, settles with slight "bounce"
```

### State-Specific Fluctuation Rules

**SIGNAL LOST:**
- More frequent fluctuations (every 10-20 seconds)
- Wider drift range (±0.5 MHz)
- Slower settling time (2-3 seconds)
- Reinforces instability

**STANDBY:**
- Normal fluctuation rate (every 20-40 seconds)
- Standard range (±0.3 MHz)
- Quick settling (~1 second)

**COUNTDOWN:**
- Reduced fluctuations (every 30-60 seconds)
- Tight range (±0.2 MHz)
- Signal stabilizing as transmission approaches

**ACTIVE TRANSMISSION:**
- Minimal fluctuations (every 60-90 seconds)
- Very tight range (±0.1 MHz)
- Signal locked but not perfect
- Rare sudden spike (±0.4 MHz) for drama

---

## Typography Specifications

**"greenwich mean time" display:**
- Font: IBM Plex Mono
- Size: 10-11px (very small, subtle)
- Color: #003300 (dimmed green, not primary text)
- Lowercase only
- Should feel like technical metadata, not prominent info

**Frequency Display:**
- Font: VT323 or IBM Plex Mono
- Size: 16-18px
- Color: #00FF00 (terminal green)
- Monospace critical for number rolling animation
- Each digit position must be fixed width

---

## Implementation Notes

### JavaScript Approach
```javascript
// Pseudocode for frequency fluctuation

const baseFrequency = 540.7;
const fluctuationRange = 0.3;

function startFrequencyFluctuation() {
  setInterval(() => {
    if (shouldFluctuate()) {
      const drift = getRandomDrift();
      animateFrequencyChange(baseFrequency, baseFrequency + drift);
      
      setTimeout(() => {
        animateFrequencyChange(baseFrequency + drift, baseFrequency);
      }, randomBetween(3000, 8000));
    }
  }, randomBetween(15000, 45000));
}

function animateFrequencyChange(from, to) {
  // Roll through intermediate values
  // Each digit position changes independently
  // Takes 500-1500ms total
}
```

### CSS Considerations
- Use `tabular-nums` font feature for fixed-width digits
- Consider `font-variant-numeric: tabular-nums;`
- Ensure consistent character width across all digits 0-9
- Position: fixed for frequency display so it doesn't shift layout

---

## Additional Atmospheric Effects

**Static/Interference (Optional):**
- During frequency drift, add subtle visual noise
- Slight text jitter (1-2px horizontal shift)
- Brief scan line effect
- Text flicker (very subtle, 5-10% opacity drop)

**Audio (Future Enhancement):**
- Subtle pitch change corresponding to frequency drift
- Static/interference sound during transitions
- Reinforces the "tuning" metaphor

---

## User Experience Impact

**What This Achieves:**
- Reinforces analog, unstable transmission aesthetic
- Creates subtle movement without being distracting
- Suggests you're monitoring a live, imperfect signal
- Adds life to static screens during STANDBY/SIGNAL LOST
- No explanation needed - viewers intuitively understand signal drift

**Timing Philosophy:**
- Long enough stable periods that it's not annoying
- Unpredictable enough that you notice when it happens
- Quick enough transitions that it feels responsive
- Rare enough that it stays interesting when spotted

The frequency becomes a "living" element - never perfect, always being monitored, occasionally drifting off signal. Very analog radio/shortwave feel.
