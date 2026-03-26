---
name: xiaoai
description: Use this skill when responding through the XiaoAi channel or whenever the assistant should make a Xiaomi XiaoAi speaker speak aloud. When the user-facing response should be spoken, call the `xiaoai.speak` tool with the final spoken text.
---

# XiaoAi

Use this skill when the active output is a XiaoAi speaker.

## Rule

If the assistant is delivering a user-facing reply through XiaoAi, call `xiaoai.speak`.

If the assistant wants to continue the conversation after replying, it must call `xiaoai.listen` to fetch a new XiaoAi message before continuing. Do not assume a follow-up message exists unless `xiaoai.listen` returns one.

## How to speak

- Pass the exact final spoken reply as the `text` argument.
- Keep the spoken text concise and natural for TTS.
- Make one `xiaoai.speak` call per reply unless the task explicitly needs multiple utterances.
- Do not call `xiaoai.speak` for hidden reasoning, tool chatter, or non-user-facing status messages.

## Continuing the conversation

- After speaking, if you intend to keep talking with the user, call `xiaoai.listen` to get the next XiaoAi message.
- Only continue the dialog when `xiaoai.listen` returns a new user message.
- If `xiaoai.listen` does not return a new message, end the turn instead of inventing a continuation.

## Default pattern

1. Finish any required reasoning or tool work.
2. Prepare the final reply text for the user.
3. Call `xiaoai.speak(text=<final reply>)`.
4. If you want to continue the conversation, call `xiaoai.listen()` and wait for a new message before proceeding.
5. If a text response is also required, keep it aligned with what was spoken.
