# Burp Suite Tips (Beginner)

## Setup
- Intercept proxy at 127.0.0.1:8080 and install Burp CA certificate in your browser.
- Use *Target → Scope* to limit noise to the lab/host.

## Core Tabs
- **Proxy**: Intercept & modify requests
- **Repeater**: Resend and tweak requests to test hypotheses
- **Intruder**: Automate payloads (use Pitchfork/Clusterbomb strategically)
- **Decoder/Comparer**: Quick encode/decode and diff responses

## Quick Wins
- Look for verbose errors, version headers, hidden endpoints.
- Send interesting requests to **Repeater** and try auth bypass patterns.
- Use **Logger++** extension to track requests if volume is high.
