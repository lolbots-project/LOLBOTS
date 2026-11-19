# LOLBots

**Living Off The Land Bots: a community catalog of legitimate AI agent capabilities that attackers can borrow.**

LOLBAS taught defenders to ask what a "trusted" binary can be talked into doing. LOLBots asks the same question of the bots running in your environment.

> **Status:** Early draft. The schema, entries, and mappings are all subject to change. See [Roadmap](#roadmap).

For the project's goal, definitions, license, disclaimer, and the meaning of every entry field, read [NOTICE.md](NOTICE.md) first. This README covers what belongs in the catalog, how it's organized, and how to get involved.

---

## What counts as a LOLBot?

A capability qualifies for an entry when it meets all of these criteria:

- **It is legitimate and intended.** The bot is supposed to have it. Bugs and vendor-specific flaws belong in vulnerability disclosure, not here, unless the underlying capability is a design property worth documenting.
- **Abuse needs no malware.** The attacker supplies instructions, content, or influence. The bot supplies the tooling and the access.
- **It passes the confused-deputy test.** The capability meets all three of these conditions:
  1. **Input trust:** Untrusted content can reach the bot while the capability is available.
  2. **Authority:** The capability acts with more privilege than whoever supplied that content.
  3. **Visibility:** The resulting action would look normal to existing monitoring and approval flows.
- **It would help an attacker.** Examples include code execution, data exfiltration, persistence, privilege escalation, lateral movement, and evading detection.
- **It can be described defensively.** If you can't write a useful detection or mitigation, the entry isn't ready.

Combinations count. Two capabilities that are each harmless alone (one that reads private data, another that writes outward) can be an entry together.

### What's out of scope

- Model-level attacks with no connection to deployment capabilities, such as training-data extraction or jailbreak recipes.
- Ready-to-run payloads, weaponized prompts, or attack instructions aimed at a specific named target.
- Vendor bug reports. Please disclose those to the vendor first.

---

## Repository layout

```
.
├── README.md          You are here
├── NOTICE.md          Goal, definitions, license, field reference
├── LICENSE            Project license
├── CONTRIBUTING.md    How to submit entries
├── entries/           One YAML file per entry
│   └── LOLBOT-001-coding-agent-shell-tool.yml
└── templates/         Blank entry template and schema
```

Files in `entries/` are named `LOLBOT-NNN-short-name.yml`. Each is self-contained and machine-readable, so it can be indexed, searched, or turned into detection content without scraping prose.

---

## Using the catalog

- **Detection engineers:** Start with the `detection` field and treat each entry as a hypothesis to test against your own agent telemetry. Entries are meant to be translated into your SIEM's query language, not copied verbatim.
- **Red and purple teams:** Use entries as a checklist of agent behaviors to evaluate in your own authorized, non-production environments.
- **Platform and security architects:** Use the `trust_assumption` and `mitigation` fields during design reviews of agent deployments. Look for the combinations, not just individual tools.
- **Researchers:** Cross-reference `maturity` to see which techniques are well established and which still need reproduction. Replications and corrections are welcome.

Everything here is a starting point. Agent behavior depends on model version, permission mode, and configuration, so verify against your own environment.

---

## Finding new entries

If you want to propose an entry, this process tends to work well:

1. **Inventory the agent's capabilities:** tools, identities and credentials, readable data, outbound channels, anything that persists between sessions, and everyone or everything that can influence its input.
2. **Apply the three confused-deputy questions** to each capability.
3. **Check the pairs and triples.** Build a capability-by-capability matrix and look hard at the cells where private data, untrusted input, and an outbound channel meet.
4. **Form a hypothesis** and test it in an isolated lab with dummy data, throwaway credentials, and harmless canary strings.
5. **Record the context:** product, version, configuration, and permission settings.
6. **Rate the maturity honestly.** A well-labeled `theoretical` entry is more useful than an overstated `demonstrated` one.

Public research, conference talks, incident reports, and advisories are also good sources. When you cite one, ask what legitimate feature made the incident possible, and write the entry about that feature.

---

## Contributing

Contributions of every size are welcome: new entries, improvements to detection and mitigation guidance, corrected mappings, replications, and typo fixes.

1. Read [NOTICE.md](NOTICE.md) and [CONTRIBUTING.md](CONTRIBUTING.md).
2. Copy the template from `templates/`.
3. Keep it at the technique level.
4. Open a pull request.

If your finding affects a specific product, report it to the vendor and allow reasonable time for a response before submitting.

---

## Roadmap

- [X] Finalize entry schema and publish JSON Schema validation in CI
- [X] Publish `CONTRIBUTING.md` and the entry template
- [ ] Add a pattern taxonomy above individual entries, grouping them by root cause
- [ ] Expand coverage: email and calendar assistants, RPA, chat and ticketing bots, and agent memory stores
- [ ] Verify all ATT&CK and ATLAS mappings
- [ ] Searchable website
- [ ] Sigma-style detection content for high-confidence entries

---

## Naming

"LOLBots" is a nod to LOLBins and LOLBAS and to the broader "living off the land" tradition in security. It is not affiliated with those projects.

---

## Acknowledgements

This project builds on ideas and conventions from the community:

- The **LOLBAS Project**, which established the model of cataloging legitimate tools by their abuse potential.
- **GTFOBins**, for the same approach applied to Unix binaries.
- **MITRE ATT&CK** and **MITRE ATLAS**, for shared vocabularies for adversary behavior against enterprises and AI systems.
- The researchers who publish agent security findings. Entries credit their sources.

### Maintainers

- `[Ethan Houk / N0ctu4ry]`

### Contact

- `lolbots-project@proton.me`
