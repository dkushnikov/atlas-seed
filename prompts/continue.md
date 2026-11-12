# Continuation prompts

Two short prompts for the chats after the first one. Paste the one you need. If your rules already sit in custom instructions, a project's instructions, `AGENTS.md` or `CLAUDE.md`, skip the first block and start with the task.

## New chat with the rules pasted

Use this when the environment does not load your rules by itself (a plain ChatGPT chat without custom instructions, a Temporary chat, a chat in another tool).

```text
Here are my working rules for AI. Follow them in this chat. Confirm in one line which version you loaded ("rules vN loaded"), then wait for my task.

<paste the whole working-rules document here>
```

## Update after a correction

Use this when you have added a line to the source document and the short form must follow.

```text
Here is my working-rules document, version <N>. One rule changed since the last version: <say which>. Regenerate the short form from this document: plain text, under 1,500 characters, ending with "(rules v<N>)". Change nothing else.

<paste the whole working-rules document here>
```

Then paste the result into the field your environment reads ([environments.md](../environments.md)) and replace the old version there. If the field now shows "(rules v<N>)", the field and the document match. In a ChatGPT Project, also replace the uploaded document with the new version: the tail in the field does not cover the file.

## Re-running the full route

If you later run the full interview ([bootstrap-ritual.md](../bootstrap-ritual.md)), start it with your approved files in view:

```text
I already have approved working rules (document below, version <N>) and the identity files in <folder>. Read them first. Propose changes to these files; do not write a competing description of me. Where my answers today differ from the files, show both and ask which stands.
```
