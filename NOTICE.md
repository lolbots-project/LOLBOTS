# NOTICE

This notice is the primary document for the LOLBots Project's terms, disclaimers, definitions, entry structure, and license acknowledgements.

Please refer to `README.md` for the inclusion criteria and the definition of "Living Off The Land" as applied to bots.

---

## Contents

- [Goal](#goal)
- [Definitions](#definitions)
- [License](#license)
- [Disclaimer](#disclaimer)
- [Consuming and contributing](#consuming-and-contributing)
- [Entry field reference](#entry-field-reference)
- [Third-party licenses](#third-party-licenses)

---

## Goal

The goal of the LOLBots Project is to document the legitimate, intended capabilities of AI agents and bots that can be repurposed to carry out attacker objectives, without the attacker bringing any malware of their own.

Where LOLBAS catalogs pre-installed binaries that can be abused, LOLBots catalogs the agent equivalents: the tools, connectors, identities, and automations that a bot already has, and the trust that people and systems already place in them. The attacker supplies only instructions or influence. The bot supplies the access, the authority, and the plausible reason to act.

LOLBots focuses on the **deployment** rather than the **model**. An entry describes how an agent's legitimate permissions and integrations create risk (the confused-deputy problem), whatever the quality of the underlying model.

Entries are written for defenders first. Each one pairs a technique-level description with detection ideas and mitigations. The project does not publish payloads, working exploits, or step-by-step attack instructions.

---

## Definitions

- **LOLBots Project** and **LOLBots** are used interchangeably in this document and refer to the LOLBots Project.
- **Bot / agent:** Software that uses an AI model to decide on and carry out actions, including coding agents, browser or computer-use agents, assistants wired into email and files, chat and CI/CD bots, and agents using tool connectors such as MCP servers.
- **Living Off The Land (LOL), for bots:** Achieving an objective by using only a bot's existing, legitimate capabilities and permissions, rather than introducing new malicious tooling.
- **Capability:** A tool, permission, integration, identity, or behavior that a bot legitimately has, such as running shell commands, reading a mailbox, or posting to a channel.
- **Entry:** A single documented capability and its abuse potential, stored as one YAML file under `entries/`.
- **Untrusted content:** Any text, file, page, message, or data that the bot may read but that is not authored by the bot's authorized operator or user.
- **Ambient authority:** Permissions a bot holds by default (credentials, sessions, tokens, tool access) that apply regardless of who or what influenced its current action.
- **Confused deputy:** A trusted party (here, the bot) that is induced to misuse its legitimate authority on behalf of a party who lacks that authority.
- **Sanctioned egress:** An approved channel through which data can leave a boundary (email, chat, issue comments, web fetch) and which is therefore rarely inspected as an exfiltration path.
- **Submitter:** An individual, group, organization, or entity that contributes to the LOLBots Project through project maintenance, issue submission, pull request submission, and so on.

---

## License

- The LOLBots Project is licensed under **GNU GENERAL PUBLIC LICENSE v3.0**. For license information, please refer to the `LICENSE` file.
- By submitting a contribution, a Submitter agrees that their contribution may be distributed under the project license.
- Submitters must have the right to contribute what they submit and must not submit material they do not have the right to license.

---

## Disclaimer

The LOLBots Project is provided for defensive, educational, and research purposes, including detection engineering, threat modeling, red and purple team exercises, and security awareness.

- The project is provided "as is," without warranty of any kind. Entries may be incomplete, may become outdated as products change, and may not apply to every version, configuration, or deployment.
- Agent products and models change quickly. Behavior documented in an entry may differ across versions, permission modes, and settings. Each entry's maturity rating describes the evidence available when it was written.
- Submitters and users are responsible for acting lawfully. Test only against systems you own or are explicitly authorized to test, using non-production environments and dummy data.
- The LOLBots Project includes and references resources from open and public sources to improve content quality. The project does **not** endorse any particular entity, vendor, product, project, group, or individual. Naming a product in an entry describes a capability and is not a statement about the vendor's security.
- Linked sites and references are not under the control of the LOLBots Project, and the project is not responsible for the content of external or third-party resources.
- Where an entry concerns a vulnerability in a specific product, Submitters are expected to follow coordinated disclosure with the vendor before publication. Design-level properties may be documented at the technique level without vendor coordination.

---

## Consuming and contributing

- To **consume** content, use the entries under `/entries` in this repository, or `[project website URL]` once available.
- To **contribute**, please read this notice, `README.md`, and `CONTRIBUTING.md`.
- New entries must follow the structure described in the next section and in the entry template (`[TEMPLATE-FILE]`).
- Entries must remain at the technique level: no payloads, no weaponized prompts, no operational instructions for attacking a specific named target.

---

## Entry field reference

Each entry is a single YAML file named `LOLBOT-NNN-short-name.yml`. The following fields are used. All fields are required unless marked optional.

| Field | Description |
|---|---|
| `schema_version` | The version of the entry schema the file conforms to. |
| `id` | Unique identifier in the form `LOLBOT-NNN`. Identifiers are never reused. |
| `name` | Short, descriptive name of the capability or abuse pattern. |
| `legitimate_capability` | What the bot is supposed to do. Describes the intended, benign use of the capability, since the project documents unexpected abuse of intended functionality. |
| `abuse_categories` | One or more categories describing how the capability can be abused. See [Abuse categories](#abuse-categories). |
| `trust_assumption` | The property of the environment or the people and systems around it that makes the abuse work, expressed as the confused-deputy condition. This is the key field of an entry. |
| `prerequisites` | What must be true for the technique to apply, such as which tools are enabled, what content the bot can read, and which permissions it holds. |
| `detection` | Telemetry, behavioral signals, and analytic ideas that defenders can use to spot the technique. |
| `mitigation` | Preventive and corrective controls that reduce the risk. |
| `mappings` | References to external frameworks. Contains `attack` (MITRE ATT&CK technique IDs) and `atlas` (MITRE ATLAS techniques). Either may be empty. Mappings are best-effort, and loose analogies should be marked as such in a comment. |
| `maturity` | How well the technique is evidenced. See [Maturity levels](#maturity-levels). |
| `maturity_notes` | *Optional.* Context for the maturity rating, such as differences between adjacent and agent-specific cases. |

### Abuse categories

| Value | Meaning |
|---|---|
| `execution_via_proxy` | Causing the bot to run commands or code on the attacker's behalf. |
| `exfiltration` | Using the bot's read access and outbound channels to move data out of a boundary. |
| `persistence` | Maintaining influence over the bot's future behavior, for example through memory, rules files, or configuration. |
| `privilege_escalation` | Gaining access beyond that of the party supplying the input by acting through the bot's greater permissions. |
| `lateral_movement` | Using the bot's reach (sessions, connectors, tokens) to move into other systems or accounts. |
| `defense_evasion` | Having malicious activity blend in with, or be attributed to, normal bot behavior so it avoids detection or approval. |
| `supply_chain` | Compromising the bot's inputs, dependencies, or automation pipelines in order to affect downstream users or systems. |

### Maturity levels

| Value | Meaning |
|---|---|
| `theoretical` | Reasoned from the capability analysis but not yet reproduced. |
| `demonstrated` | Reproduced in a controlled lab or publicly shown by credible research, with the conditions recorded. |
| `observed` | Seen in real-world incidents or reported attacks, in this form or a closely related one. |

---

## Third-party licenses

The LOLBots Project references external frameworks to help defenders connect entries to common vocabularies.

- **MITRE ATT&CK®:** ATT&CK is a registered trademark of The MITRE Corporation. The `attack` mappings reference ATT&CK technique identifiers. Use of ATT&CK is subject to MITRE's terms of use, which require reproducing MITRE's copyright designation and license in copies. `The MITRE Corporation (MITRE) hereby grants you a non-exclusive, royalty-free license to use ATT&CK® for research, development, and commercial purposes. Any copy you make for such purposes is authorized provided that you reproduce MITRE's copyright designation and this license in any such copy.

"© 2026 The MITRE Corporation. This work is reproduced and distributed with the permission of The MITRE Corporation."`
- **MITRE ATLAS™:** The `atlas` mappings reference techniques from MITRE ATLAS (Adversarial Threat Landscape for AI Systems). `Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0.

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

This project makes use of MITRE ATT&CK®.`

Since these frameworks are widely adopted, LOLBots attempts to map each entry to an appropriate technique where one applies. Mappings are informational, are not endorsed by MITRE, and may be revised as the frameworks evolve.
