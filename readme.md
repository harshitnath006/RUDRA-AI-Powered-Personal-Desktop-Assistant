# &lt;Rudra ai &gt;

Rudra is a cross-platform personal AI assistant with real-time voice conversation, desktop automation, visual awareness, persistent memory, and an optional phone dashboard. It runs locally on Windows, macOS, and Linux and uses Gemini Live for AI audio sessions.

**Maintainer:** Harshit Nath

## Capabilities

- Low-latency, multilingual voice conversation.
- Desktop and browser automation through modular actions.
- Requested screen and camera analysis.
- Persistent preferences, notes, projects, session summaries, and monitored topics.
- Weather, search, reminders, system telemetry, media, and file workflows.
- A trusted-phone dashboard for encrypted commands, live phone audio, and file transfer.

## Quick start

### Prerequisites

- Python 3.11 or 3.12
- A microphone
- A Gemini API key
- Node.js 20+ only for the optional web command center

### Install dependencies

```powershell
py -3.11 -m pip install -r requirements.txt
```

On macOS/Linux, use your Python 3.11/3.12 interpreter:

```bash
python3 -m pip install -r requirements.txt
```

For first-run setup that also installs Playwright browsers:

```powershell
py -3.11 setup.py
```

### Configure

Copy `config/api_keys.example.json` to `config/api_keys.json`, then add your local Gemini API key.

```json
{
  "gemini_api_key": "your-gemini-api-key",
  "assistant_name": "Rudra",
  "user_name": "Your name",
  "os_system": "windows",
  "ui_color": "#a78bfa",
  "morning_brief_enabled": true
}
```

Do not commit a real API key. See [configuration](docs/CONFIGURATION.md) for all supported settings.

### Start the desktop assistant

```powershell
py -3.11 main.py
```

The PyQt interface opens first. Complete the initial key setup if prompted; Rudra then connects to Gemini Live and starts listening.

## Interfaces

### Phone dashboard

The desktop runtime starts a local phone dashboard when its server dependencies are available. Select **Remote Control** in the desktop UI to generate a one-time QR code or pairing key. Pair only on a trusted local network.

See the [remote dashboard guide](docs/REMOTE-DASHBOARD.md) for the pairing flow, API reference, and security notes.

### Web command center

`web-ui` is an independent Next.js visual command center with an animated Rudra orb, waveform, responsive layout, dark/light themes, and keyboard controls. It does not replace the desktop runtime or phone dashboard.

```powershell
cd web-ui
npm install
npm run dev
```

Open `http://localhost:3000`.

## Documentation

| Guide | Use it for |
| --- | --- |
| [Configuration](docs/CONFIGURATION.md) | API keys, settings, memory, certificates, and dependencies |
| [Architecture](docs/ARCHITECTURE.md) | Runtime flow, components, persistence, and extension points |
| [Remote dashboard](docs/REMOTE-DASHBOARD.md) | Pairing, endpoints, trusted-network boundaries, and troubleshooting |
| [Development](docs/DEVELOPMENT.md) | Local checks, contribution workflow, and documentation maintenance |

## Project structure

```text
R.U.D.R.A/
├── main.py              # Runtime orchestration and Gemini Live session
├── ui.py                # PyQt6 desktop UI, HUD, setup, and customization
├── actions/             # System, browser, search, media, reminder, and vision actions
├── core/                # Prompt, speech engines, local LLM client, installer
├── memory/              # Configuration helpers and persistent memory
├── dashboard/           # FastAPI phone dashboard and static client
├── web-ui/              # Optional Next.js command center
├── config/              # Local configuration and optional TLS certificates
└── requirements.txt     # Python dependencies
```

## Safety and privacy

- `config/api_keys.json` can contain your Gemini API key and personal settings; keep it local.
- The phone dashboard binds to the local network. Do not expose it directly to the public internet.
- Desktop automation, remote commands, and file transfers run on the computer hosting Rudra. Review commands before allowing them to run.

## Credits

This project is a modified version of **MARK L (50)** by **FatihMakes**, licensed under **[Creative Commons Attribution-NonCommercial 4.0 International](https://creativecommons.org/licenses/by-nc/4.0/)**.

## License

No root `LICENSE` file was included in this checkout. The upstream README identifies the project as **CC BY-NC 4.0**. You may share and adapt the material with appropriate attribution, a license link, and a clear indication of changes; commercial use is not permitted. Read the complete [CC BY-NC 4.0 legal terms](https://creativecommons.org/licenses/by-nc/4.0/) before redistribution.
