---
name: human-design
description: Answer Human Design questions with the Tessera tools. Calculate a person's chart from date, time and place of birth (Type, Strategy, Authority, Profile, Definition, Incarnation Cross, centres, channels, gates), read the day's transits against it, compare two people's charts, and explain any type, authority, profile, line, centre, channel or gate, in English, Dutch or German. Use whenever the user asks for their Human Design chart or type, what an element of a chart means, how two people's designs fit together, or what today's transits activate.
---

# Human Design with Tessera

The `tessera` MCP server calculates Human Design charts from birth data with an ephemeris (the planets' real positions at birth and at the Design moment, 88 degrees of solar arc earlier) and historical time zones. Its texts are Tessera's own writing in English, Dutch and German. A chart cannot be worked out from memory: the gates depend on positions to a fraction of a degree, so always call a tool for a chart and never guess one.

## Pick the tool

- **A person's chart** ("what is my type?", "read my chart"): `get_chart` with `birth_date` (YYYY-MM-DD), `birth_time` (24-hour HH:MM, local clock time) and `birth_place` ("City, Country"). Ask for the birth time and place if the user has not given them. When the time is approximate ("around 3 pm"), pass `time_uncertainty_minutes`; when it is unknown, leave `birth_time` out.
- **Two people** ("how do my partner and I fit?", "our connection chart"): `compare_charts` with `person_a` and `person_b`, each holding the same birth fields plus an optional `name`.
- **Transits** ("what's in the air today?", "what does today activate for me?"): `get_transits`, with `person` for a personal reading and `date` for another day.
- **A term** ("what is a 5/1?", "what does the Sacral centre do?", "gate 34"): `explain` with the term as `topic`.
- **Language:** pass `language` `nl` or `de` when the user writes in Dutch or German, so titles and summaries come back in that language.

## Read the results correctly

- Each element has a `name` (the standard Human Design term, such as "Manifesting Generator" or "Emotional (Solar Plexus)") and a `title` (Tessera's plain-language name for it, such as "The Fast Responder"). Use the standard name first; the title and `summary` help explain it.
- **Place:** `person.place` is the town that was matched. If `other_places_with_this_name` is present and the user did not say which one, name the town used and ask if that is right. A wrong place can mean a wrong time zone.
- **Birth time:** `birth_time_sensitivity.may_change` lists the parts of the chart that differ within the stated uncertainty. When it is not empty, say plainly which parts are uncertain, and do not build a reading on them. With no birth time, Type and Authority often still hold, but Profile, the Moon and lines often do not.
- **Activations:** Personality (conscious, black in most charts) is the moment of birth; Design (unconscious, red) is about three months earlier. `gate_line` such as "34.2" is gate 34, line 2.
- **Channels** define the two centres they join. Defined centres are consistent energy; open centres take in and amplify what is around them.
- **Connections:** electromagnetic channels (each brings one gate) are attraction, companionship (both have it) is common ground, dominance (one has it, the other neither gate) means one person leads in that area, and compromise (one has it, the other one gate) tends to rub.
- **Transits:** `channels_completed_in_person_chart` are channels the day's planets complete with the person's own gates, the personal part of the day. `channels_formed_by_transits_alone` affect everyone.

## Keep it honest

Human Design is a system for self-reflection, not a science or a diagnosis. Present a chart as something to try on and test against experience, not as a verdict about the person. Each result carries links to the matching page in Tessera, free to open; pass on the relevant one when the user wants to read more.

## Good answers look like this

Placeholders in angle brackets stand for values from the tool results.

- "You are a <type.name>: <type.summary> Your strategy is to <type.strategy>, and your authority is <authority.name>, which means <authority.summary>"
- "Your profile is <profile.name>, <profile.title>: <profile.summary> Your birth time is only known to within <time_uncertainty_minutes> minutes, and within that window your <may_change> could differ, so treat those parts as provisional."
- "Together you form <n> electromagnetic channels, including <channel> (<title>): <name_a> brings gate <gate> and <name_b> brings gate <gate>."
