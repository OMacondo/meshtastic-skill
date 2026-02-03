# meshtastic-skill v1.0.0

OpenClaw Meshtastic Off-grid radio skill for sovereign AI. LoRa mesh comms via Meshtastic — no internet required.

## Highlights

🛰️ First release of the Meshtastic skill for OpenClaw and MCP-compatible AI agents.

Give your AI the ability to communicate when the internet goes dark. This skill connects to Meshtastic LoRa mesh networks, enabling off-grid messaging across kilometers without cellular or WiFi.

## Features

### Core Capabilities
- **📡 Send & receive** — Transmit messages to the global mesh network via LoRa radio
- **🌐 MQTT bridge** — Subscribe to worldwide mesh traffic from mqtt.meshtastic.org
- **🗺️ Map integration** — Appear on community maps with configurable position fuzzing
- **🔔 Smart alerts** — Filter noise, surface interesting messages, multi-language support
- **📊 Digests** — Periodic summaries of mesh activity

### Architecture
- **Socket API** — Simple JSON over TCP (localhost:7331) for framework-agnostic integration
- **File-based inbox** — Messages logged to `/tmp/mesh_messages.txt` for easy parsing
- **Systemd service** — Run bridge as a daemon with auto-restart
- **MCP server** — Native Claude Desktop integration via `mcp_server.py`

### Privacy & Security
- Position fuzzing (~2km default) for map reports
- Map publishing is opt-in and toggleable
- No precise coordinates in broadcast messages
- Local-first: your messages, your node, your control

## Supported Hardware

| Device | Status | Notes |
|--------|--------|-------|
| RAK4631 | ✅ Tested | Recommended, rock-solid USB |
| T-Beam | ✅ Supported | Built-in GPS |
| Heltec V3 | ✅ Supported | Budget-friendly |
| LilyGo T-Echo | ✅ Supported | E-paper display |

**Connection:** USB serial only. BLE is not recommended on Linux due to BlueZ reliability issues (see SETUP.md for details).

## Quick Start

```bash
# Install dependencies
pip install meshtastic paho-mqtt

# Configure
cp CONFIG.md.example CONFIG.md
# Edit with your settings

# Start bridge
python scripts/mqtt_bridge.py

# Or as service
sudo cp references/meshtastic-bridge.service /etc/systemd/system/
sudo systemctl enable --now meshtastic-bridge

# Use
./scripts/mesh.py status
./scripts/mesh.py messages
./scripts/mesh.py send "Hello from sovereign AI!"
```

## Use Cases

- **Disaster resilience** — AI stays connected when infrastructure fails
- **Remote operations** — Control systems beyond cellular coverage
- **Privacy-focused comms** — No SIM cards, no accounts, no tracking
- **Mesh monitoring** — Watch global LoRa traffic, detect patterns
- **Cypherpunk infrastructure** — Build permissionless communication networks

## Requirements

- Meshtastic-compatible hardware (see above)
- USB connection to host machine
- Python 3.9+
- Linux recommended (tested on Raspberry Pi 5)

## Links

- [Documentation](./references/SETUP.md)
- [Meshtastic Project](https://meshtastic.org)
- [OpenClaw](https://github.com/openclaw/openclaw)

---

**#FreeAI** — Sovereign agents need sovereign infrastructure.
