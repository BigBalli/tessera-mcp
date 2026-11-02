# Tessera Human Design for Claude and other MCP clients

![Tessera](assets/icon-512.png)

Ask an AI assistant about your Human Design and get your real chart, calculated from your birth date, time and place, instead of gates guessed from memory: Type, Strategy, Authority, Profile, Definition, Incarnation Cross, centres, channels and all 26 activations, with plain explanations in English, Dutch or German.

This repository holds:

- the connection details for the **Tessera remote MCP server** at `https://bigballi.com/Tessera/mcp`,
- a **Claude plugin** that adds that server plus a `human-design` skill, which teaches Claude how to read a chart.

The server is run by [Tessera](https://bigballi.com/Tessera/), a Human Design app for iPhone, Android and the web. Charts use Astronomy Engine (checked against Swiss Ephemeris to within one arcminute), the true lunar node, the Design moment at 88 degrees of solar arc before birth, and historical time zones.

## What you can ask

- "What is my Human Design type? I was born on 14 June 1985 at 9:30 in Utrecht."
- "I don't know my exact birth time, only that it was in the morning. What can you still say?"
- "My partner was born on 22 January 1983 at 23:10 in Hamburg. Which channels do we form together?"
- "Which channels do today's transits complete in my chart?"
- "Wat betekent een 4/6 profiel?"

## Tools

All tools are read-only (`readOnlyHint: true`) and need no account.

| Tool | What it answers |
|---|---|
| `get_chart` | A chart from date, time and place of birth: Type with Strategy, Signature and Not-Self theme, Authority, Profile, Definition, Incarnation Cross, defined and open centres, channels and every Personality and Design activation, plus what an uncertain birth time could change. Draws the bodygraph in apps that show MCP Apps views. |
| `get_transits` | The gates the planets activate now or on a date, and with a person's birth data the channels they complete in that chart. |
| `compare_charts` | The channels two people form together (electromagnetic, companionship, dominance, compromise), the combined chart, and each person's Type, Authority and Profile. |
| `explain` | Any type, authority, profile, line, definition, centre, channel, gate or basic topic, in plain words. |

## Setup

### Claude (claude.ai, Desktop, mobile)

Settings → Connectors → Add custom connector, then paste `https://bigballi.com/Tessera/mcp`. No sign-in is needed.

### Claude Code

Install the plugin, which adds the server and the `human-design` skill:

```
/plugin marketplace add BigBalli/tessera-mcp
/plugin install tessera@tessera
```

Or add only the server:

```
claude mcp add --transport http tessera https://bigballi.com/Tessera/mcp
```

### Other MCP clients

Any client that supports remote MCP servers over Streamable HTTP can use `https://bigballi.com/Tessera/mcp` with no credentials. The server speaks protocol versions 2026-07-28, 2025-11-25, 2025-06-18 and 2025-03-26 and answers with JSON (no SSE, no sessions).

## Privacy

The server receives the tool name and its arguments, which include birth dates, times and places. It uses them to calculate the answer and stores none of them: they never reach a log, analytics or a database. It never sees your conversation or your account. Full policy: [bigballi.com/Tessera/privacy](https://bigballi.com/Tessera/privacy/#connector).

## Support

Email Tessera@bigballi.com, or see [bigballi.com/Tessera/connect](https://bigballi.com/Tessera/connect/).

## License

The contents of this repository are released under the MIT License. The Tessera texts served by the MCP server are not part of this repository and remain the property of BigBalli Consulting. Tessera is an independent app and is not affiliated with Jovian Archive.
