# Burp Suite Cheat Sheet

## Overview

Burp Suite is a web vulnerability testing platform used for intercepting, analyzing, and modifying HTTP/S traffic.

## Basic Workflow

1. Configure browser proxy to 127.0.0.1:8080
2. Import Burp CA certificate to handle HTTPS
3. Define scope in *Target → Scope*
4. Intercept requests, analyze, and send to tools (Repeater, Intruder, etc.)

## Common Usage

* **Proxy Tab**: Intercept/modify requests
* **Repeater**: Replay and modify requests for testing
* **Intruder**: Automated attacks with payloads
* **Decoder**: Encode/decode data (Base64, URL, etc.)
* **Comparer**: Diff responses

## Useful Shortcuts

* Right-click request → *Send to Repeater*
* Ctrl+Shift+R → Quick send to Repeater
* Ctrl+Shift+I → Send to Intruder

## Setup

* Intercept proxy at 127.0.0.1:8080 and install Burp CA certificate in your browser.
* Use *Target → Scope* to limit noise to the lab/host.

## Core Tabs

* **Proxy**: Intercept \& modify requests
* **Repeater**: Resend and tweak requests to test hypotheses
* **Intruder**: Automate payloads (use Pitchfork/Clusterbomb strategically)
* **Decoder/Comparer**: Quick encode/decode and diff responses

## Quick Wins

* Look for verbose errors, version headers, hidden endpoints.
* Send interesting requests to **Repeater** and try auth bypass patterns.
* Use **Logger++** extension to track requests if volume is high.
* Use Intruder strategically (don’t brute-force everything)
