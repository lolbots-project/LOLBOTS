# Contributing

Thank you for contributing!

When submitting new LOLBots, please submit a `yml` source file (`entries/`), as these are used to generate everything else. Next, review `README.md` and ensure that your LOLBot meets the criteria: a legitimate, intended bot capability with interesting or unexpected abuse potential that would be useful to an attacker.

There's nothing special about the format. Just base your entry off an existing one and modify as required. Please ensure that you do not add or remove any of the fields; all are required except `maturity_notes`, which is optional. The meaning of each field is described in `NOTICE.md`.

There is a template that can be used, located in `templates/`, if you do not want to copy one of the existing LOLBots.

It is also important to use the abuse categories and maturity levels listed in `NOTICE.md`, since they relate to how entries are indexed and it is crucial to get them right for everything to work.

Please keep entries at the technique level: no payloads, weaponized prompts, or instructions aimed at a specific target. If your entry describes a flaw in a specific product, please report it to the vendor first.

Looking forward to your contributions!
