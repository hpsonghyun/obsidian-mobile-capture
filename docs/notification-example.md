# A notification becomes a Markdown record

This guided example follows **one fictional notification → one readable Markdown note**. It shows what information is kept and how the result could be used in Obsidian. The files are handwritten documentation fixtures, not output from a phone test or a bundled converter.

- [Input: notification.json](../examples/notification.json)
- [Expected result: notification-note.md](../examples/notification-note.md)
- [Workflow overview and diagrams](../README.md#how-the-workflows-are-implemented)

## What you can try now

Open the JSON in a text editor and the Markdown in a text editor or Obsidian. Compare the fields using the table below. You can copy the Markdown file into a vault and search its title or message text.

That file comparison is the complete public exercise today. It does not intercept a notification, configure a phone, run a collector, or generate a note automatically. The repository does not yet contain a Tasker profile, filtering JavaScript, queue worker, organizer, or installation package.

## 1. Inspect the fictional input

The example input uses a small documentation schema:

```json
{
  "example_only": true,
  "event_type": "notification",
  "received_at": "2026-01-15T14:30:00Z",
  "source_label": "Example notification app",
  "title": "Delivery update",
  "text": "Your sample order is ready for pickup."
}
```

These field names describe the example record. They are **not** an AutoNotification export schema or ready-made Tasker variables. A collector would need to map the fields exposed by its chosen notification source into its own record format.

The example includes no application package ID, device ID, account name, conversation name, telephone number, credentials, or local filesystem location. Every value is fictional.

## 2. Compare the expected note

The [expected Markdown file](../examples/notification-note.md) preserves the title and message, adds the received time and source label, and marks the file as an example. The short body looks like this:

```markdown
# Delivery update

Your sample order is ready for pickup.

Received: 2026-01-15 14:30 UTC
Source: Example notification app
```

The complete file also has frontmatter and an explicit fictional-example notice. Its timestamp is written as UTC for a consistent example; a real collector would need an explicit time-zone policy.

| Input field | Where it appears in the expected Markdown |
| --- | --- |
| `example_only: true` | `example: true` in frontmatter and the fictional-example notice. |
| `event_type: "notification"` | `type: notification-example` in frontmatter identifies this documentation fixture. |
| `received_at` | Preserved exactly in frontmatter; displayed as `2026-01-15 14:30 UTC` in the body. |
| `source_label` | `source` in frontmatter and the `Source:` line. |
| `title` | The Markdown heading. |
| `text` | The message paragraph. |

This fixture uses one event in a standalone note so the mapping is easy to inspect. In the reference workflow, the organizer merges captured entries into dated Markdown and maintains index and Daily Note links. Those larger outputs and their generation are not demonstrated by this fixture.

## 3. Understand the required apps

| What you want to do | What you need |
| --- | --- |
| Inspect the public input/output example | A text editor. Obsidian is optional for viewing and searching the Markdown. |
| Build the described notification capture flow on a phone | Android, Tasker and AutoNotification, notification and file access, Termux with Python for organization, and a writable vault folder. You must provide the automation components yourself. |

The notification flow does not require a connected PC or an AI response. Call transcription and photo interpretation have different requirements; see the unchanged [workflow prerequisites](../README.md#what-you-would-prepare).

## 4. Follow the setup order and its current boundary

The following is a setup outline for someone implementing the reference design. It is not a tested public installation guide.

1. **Inspect the fixtures first.** Decide which notification fields you need to retain and what a useful note should look like. This step is supported by the public files above.
2. **Prepare the destination.** Choose a writable vault folder and confirm that the phone tools you intend to use can access it. No machine-specific folder is prescribed here.
3. **Prepare the phone tools.** Install Tasker, AutoNotification, and Termux with Python, then configure the notification and file access required by your environment. Their official project links are listed in the [building blocks](../README.md#building-blocks).
4. **Supply the interception and filtering automation.** A Tasker profile needs to receive notification fields, map them, filter events, and apply your routing rules. **This repository does not provide that profile or its JavaScript.** The JSON fixture is an example record, not an importable phone configuration.
5. **Supply staging and organization.** The reference writes captured text before a separate worker merges dated notes and updates links. **The staging writer, queue worker, and organizer are not distributed here.** The expected Markdown file demonstrates a result, not a running implementation of those stages.
6. **Verify your implementation separately.** Use a controlled fictional notification and compare the saved fields with the expected record. Check repeated events and recovery in your own implementation before relying on unattended collection. No Android execution, device compatibility, or recovery result is claimed by this documentation exercise.

The public reproducibility boundary is therefore explicit: **you can inspect and copy the synthetic records; live collection and automatic organization require components that have not been released.**

## Feedback

[Suggest a missing field or explain a use case in Issues](https://github.com/hpsonghyun/obsidian-mobile-capture/issues). A fictional notification and the note you would want from it are enough to discuss an improvement; personal records are not needed.
