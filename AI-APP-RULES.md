# Rules for apps that call an AI model (draft v3)

Read only when building or changing code that talks to an AI model.

1. Mark the unchanging part of each request (instructions, tool list) for prompt caching.
2. Send only recent history (e.g. last 20 messages); summarise older parts.
3. Cap text from tools, emails and web pages (e.g. 3,000 characters).
4. Use a local or small model by default; the strongest only when needed.
