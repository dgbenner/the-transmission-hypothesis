# The Transmission Hypothesis

Experimental 20-seat streaming theater intercepting cultural transmissions. Cut-up methodology applied to archival video curation.

**We intercept. You interpret.**

## Overview

A pirate frequency theater that monitors and rebroadcasts signals from corporate training apparatus, state educational systems, underground media channels, and unidentified origins. Public domain archival content presented through scheduled protocols with live seat limiting.

Built using public domain sources (Internet Archive, Prelinger Collection, British Pathé) combined with original micro-transmissions and vintage commercial interstitials.

## Core Concept

- **20 concurrent receivers maximum** - Hard seat limit enforced
- **Scheduled protocols** - Themed 90-minute programming blocks
- **Live broadcast** - Synchronized viewing, no pause/rewind
- **Auto-disconnect** - Sessions end when protocol completes
- **Freeform mode** - Weekend randomized programming with 90-min limits

## Architecture

### Components

1. **Content Library** - Organized film archive (public domain sources)
2. **Schedule Database** - SQLite defining protocols and sequences  
3. **Playlist Generator** - Python script assembling streams
4. **Stream Server** - HLS delivery for synchronized viewing
5. **Web Frontend** - Terminal-aesthetic theater interface
6. **Session Management** - WebSocket for live seat counts

### Technology Stack

**Backend:**
- Python 3.x (Flask/FastAPI)
- SQLite database
- ffmpeg (HLS stream generation)
- WebSocket (real-time updates)

**Frontend:**
- HTML/CSS/JavaScript
- HLS.js (video playback)
- WebSocket client
- Monospace/terminal aesthetic

**Hosting Requirements:**
- VPS with 100GB+ storage
- 100+ Mbps bandwidth
- Ubuntu/Linux environment

## Content Sources

All content is public domain or legally accessible:

- **Internet Archive** - Prelinger Archives, feature films, educational content
- **British Pathé** - Historical newsreels (1896-1976)
- **Library of Congress** - National Film Registry, historical footage
- **Vintage Commercials** - Pre-1964 advertising (public domain)
- **Original Micro-Transmissions** - 1-2 minute created segments

## Installation

*Coming soon - project in active development*

### Prerequisites

```bash
# Required system packages
sudo apt install python3 python3-pip ffmpeg sqlite3

# Python dependencies
pip install flask sqlalchemy websockets
```

### Setup

```bash
# Clone repository
git clone [repo-url]
cd transmission-hypothesis

# Set up virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Initialize database
python init_db.py

# Download sample content
python download_content.py

# Start server
python server.py
```

## Usage

### Running the Theater

```bash
# Start streaming server
python stream_server.py

# Start web interface (separate terminal)
python web_server.py

# Access at http://localhost:5000
```

### Programming a Protocol

```python
# Example: Create new protocol
from models import Protocol, ProgramContent

protocol = Protocol(
    name="Theta-7",
    day_of_week=1,  # Monday
    start_time="20:00",
    duration_minutes=90
)

# Add content sequence
content = ProgramContent(
    protocol_id=protocol.id,
    sequence_order=1,
    content_type="film",
    content_path="/films/atomic_age/duck_and_cover.mp4"
)
```

## Project Status

**Current Phase:** Early development

- [x] Concept documentation
- [ ] Content library organization
- [ ] Database schema implementation
- [ ] Playlist generator
- [ ] HLS streaming setup
- [ ] Web interface design
- [ ] Session management
- [ ] First protocol programming

## Philosophy

This is an art project exploring consciousness alteration through media juxtaposition. It applies Gysin/Burroughs cut-up methodology to video curation, revealing patterns in how control systems operate across time and culture.

For complete conceptual framework, see [CONCEPT.md](CONCEPT.md).

## Contributing

This is a personal art project. Not currently accepting contributions, but feel free to fork and create your own transmission protocols.

## License

Code: MIT License

Content: Public domain sources only. See SOURCES.md for attribution.

## Acknowledgments

Influenced by: William S. Burroughs, Brion Gysin, Genesis P-Orridge, Night Flight, Z Channel, late-night Discovery Channel programming (1990s-2000s), numbers stations, pirate radio.

---

**Signal Status:** Under construction  
**Next Transmission:** TBD  
**Receivers:** 0/20

*"These broadcasts have never stopped. You are not discovering them. They are discovering you."*
