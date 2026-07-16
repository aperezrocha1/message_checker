# Invitation message checker

A small tool built with Claude to catch a real mistake before it happens again.

## The problem

In a role that involved sending mission invitation messages to families using a shared template, changing only the location-specific details each time, I once forgot to update the mission dates before sending — a family thought they'd missed the mission entirely. I had to individually correct the message for everyone who'd already received it.

## What this tool does

Paste in a message template (with placeholders like `{{LOCATION}}` and `{{MISSION_DATES}}`) and the filled-in version you're about to send. The tool uses the Claude API to check for:

- Any placeholder that was never replaced with real content
- Whether the location, dates, and hospital name actually match a real mission on record — not just whether the fields look filled in, but whether they're *correct*
- Any other inconsistency in the message
- A plain-language summary of what the message tells the reader, as a final sanity check

It never sends anything. It's a review step that runs before a message goes out.

## Why it's built this way

- **No real patient data.** Every example in this tool uses invented names, dates, and hospitals. Real patient records are sensitive, and this project was intentionally scoped to never touch them.
- **The mission list is a plain editable text box**, not a database. It's simple, transparent, and doesn't add a dependency someone else would need to be trained on to maintain.
- **The API key is entered by the user at runtime**, not stored in the code. This keeps the tool safe to share publicly, but it's a tradeoff worth naming: a production version would keep the key server-side rather than asking someone to paste it into a browser page.

## How to use it

1. Get a free API key at [console.anthropic.com](https://console.anthropic.com)
2. Open the live tool (or download `invitation_checker.html` and open it in any browser)
3. Paste your API key, your template, and your filled-in message
4. Click "Check message"

## What I'd do differently next

The mission list has to be updated by hand each year. A future version could pull that list from a shared source of truth instead, so it doesn't quietly go stale.
