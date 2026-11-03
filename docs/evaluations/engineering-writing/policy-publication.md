# Privacy and terms publication

Published the Engineering writing privacy policy and terms of service, added their public URLs to version 0.1.2, and rebuilt the submission ZIP. Both pages are readable on GitHub without authentication.

## Confirmed practices and scope

Daniel Medeiros confirmed that the plugin is an instructions-and-assets package with no developer-operated backend, analytics, telemetry, or conversation access. Information reaches the maintainer through GitHub Issues only. The maintainer uses public support information to answer questions and maintain the plugin; users may request removal of content he controls, while GitHub and others may retain copies outside his control.

The terms preserve the existing Apache-2.0 license and describe the free plugin, AI-provider terms, review of generated writing, and support without a service guarantee. An independent reviewer checked the pages against the package, confirmed practices, and license and found no actionable issues. This was a factual and consistency review, not a certification of legal compliance.

## Published URLs

- [Privacy policy](https://github.com/dpmedeiros/llm-harness-md-files/blob/codex/engineering-writing-plugin/plugins/engineering-writing/PRIVACY.md)
- [Terms of service](https://github.com/dpmedeiros/llm-harness-md-files/blob/codex/engineering-writing-plugin/plugins/engineering-writing/TERMS.md)

Fetched the HTML and raw Markdown without authentication after pushing the pages. Both HTML pages identified the correct policy and publisher; the raw published files matched the local source bytes. The manifest uses these verified URLs. Keep this branch available while the listing points to it, or publish replacement pages and update the manifest before removing the branch.

## Version 0.1.2 archive

Archive: `/tmp/engineering-writing-0.1.2-submission.zip`.

SHA-256: `192010edd1ff9e453ebad0699494c2a57e705b27723403c20726ddfb57cd0d8a`.

The archive contains eleven files, including both policy pages, the Apache-2.0 license, and the icon. Validated the source manifest against Agent Plugins 1.0, checked all four listing URLs and text limits, inspected the ZIP inventory and byte equality with the source, then repeated package and reference checks after extraction. Skill Creator's validator passed on the extracted skill.

`WRITING.md` and all skill instructions are unchanged from `ce768df`. No OpenAI Platform draft was uploaded, replaced, submitted, or published during this work. The new ZIP can replace the earlier package when the user is ready to update their draft.
