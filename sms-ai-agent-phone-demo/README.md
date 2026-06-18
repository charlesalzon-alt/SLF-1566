# SMS AI Agent phone demo - Autopilot Nurturing

A single-file phone mock (iMessage style) that drives the Autopilot Nurturing SMS agent.
It runs in two modes against the n8n flow:

- **Simulate** - the phone UI POSTs each message to the n8n inbound webhook
  (`/autopilot-nurturing-inbound`) and renders the agent's reply. Fully demo-able from a
  browser, no carrier SMS.
- **Live SMS** - the "Start conversation" button calls the init webhook
  (`/autopilot-nurturing-init`), which sends a real SMS through the Twilio sender number
  (+1 213 423 4847) to the phone number entered in settings. The phone UI is a visual
  mirror of that conversation.

## Files

- `index.html` - complete single-file demo page with embedded CSS and JavaScript.

## Configuration

Set values in the on-page settings panel, or pass query params:

```
index.html?webhook=https://pricehubble.app.n8n.cloud/webhook&lead=<LEAD_ID>&name=Jane&lo=Alex&phone=%2B15550101234
```

| Field | Meaning | Default |
|---|---|---|
| `webhook` | n8n webhook base URL (no trailing slash) | `https://pricehubble.app.n8n.cloud/webhook` |
| `lead` | PriceHubble lead id to log activity against | the demo test lead |
| `name` | Customer first name | `Jane` |
| `lo` | Loan officer name | `Alex` |
| `phone` | Destination phone for live mode | empty |

## How to use

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`. Pick a mode, fill the settings, and click
"Start conversation".

## Notes

- The n8n flow must be active and have Anthropic + Twilio credentials attached.
- The webhook path is `responseNode`, so the flow returns `{ "reply": "..." }` which the
  phone renders.
