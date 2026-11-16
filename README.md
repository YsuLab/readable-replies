# readable-replies

A Claude skill that makes replies, files, and artifacts easier to read.

Claude knows a lot, but it often answers like a textbook. This skill makes it answer like a good teacher: the point first, a simple picture, then the details.

## Before and after

**Without the skill**

> It's worth noting that the issue you're experiencing is most likely caused by the DNS cache, which essentially stores outdated records, so you'll want to flush it and then restart the service.

**With the skill**

> **Your DNS cache is stale. Flush it.**
>
> 🧠 DNS is a phone book. Your computer keeps its own copy so it doesn't have to ask every time. Your copy still has the old number.
>
> 🔧 `sudo resolvectl flush-caches`, then restart the service.

Same facts. Shorter sentences, a picture you can hold in your head, and the command you need.

## What the skill does

It gives Claude 15 rules. They fall into four groups.

### 1. Get to the point

- The answer goes in the first two sentences.
- Long replies open with one bold verdict line.
- A length budget keeps replies tight: 1 to 3 sentences for a simple question, about 120 words for an explanation.
- No filler. No "Great question", no restating what you asked, no closing summary.

### 2. Explain it simply

- Every concept opens with an everyday picture. A reverse proxy is a receptionist. DNS is a phone book.
- The real technical terms come next, mapped onto the picture. You still learn the correct words.
- New things are compared to things you already know.
- Every explanation has one concrete example with real values.
- If the picture would mislead you, Claude says where it breaks.

### 3. Write clean sentences

These rules come from Strunk's *The Elements of Style*.

- One idea per sentence, mostly under 20 words.
- Active voice: "The script flushed the cache," not "The cache was flushed."
- Concrete claims: "latency dropped from 800 ms to 120 ms," not "performance improved."
- No needless words: "because," not "due to the fact that."
- No stock AI phrases such as "it's worth noting," "robust," or "seamless."

### 4. Break the wall of text

- Paragraphs stay at two or three sentences.
- After about five lines of prose, the shape changes: a list, a table, a code block, or a diagram.
- Numbers and comparisons become tables or charts.
- Emojis work as signposts, and each one has a single fixed meaning:

| Emoji | Meaning |
|---|---|
| 🧠 | The simple picture |
| 🆚 | A comparison |
| 🧪 | A concrete example |
| 🔧 | The fix or how-to |
| 📌 | The key point |
| ✅ ❌ ⚠️ | Works, broken, catch |

No other emojis are allowed. You can scan a reply by emoji alone.

## Reply shapes

The skill picks a shape based on what you asked.

| You ask | Claude answers with |
|---|---|
| "Why is X broken?" | Cause → Fix → Verify |
| "How does X work?" | Picture → How it works → Example → Catch |
| A simple question | One to three sentences |
| Anything long | The reply ends with one **Next:** action |

## Modes

Three phrases change how Claude replies.

- `caveman` turns on ultra-short replies. Fragments, no filler, commands stay exact.
- `normal mode` turns caveman off.
- `too dense` makes Claude rewrite its last answer more readably. It keeps every fact.

## Where it applies

- ✅ Chat replies
- ✅ Files: READMEs, docs, reports, commit messages
- ✅ Artifacts: docs, slides, pages, dashboards

In files and formal documents, Claude drops the chat voice and the emojis. The sentence rules stay.

## Install

### Claude app (web or desktop)

1. On this page, tap **Code → Download ZIP**.
2. In Claude, open your skills settings and upload the ZIP as a skill.
3. Start a new chat.

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/YsuLab/readable-replies ~/.claude/skills/readable-replies
```

## Test it

Paste this into a new chat:

```
How does DNS work, and why does my domain sometimes take time to update?
```

A good reply has:

- A one-line answer at the top.
- An everyday picture before any jargon.
- One example with real values.
- No paragraph longer than three sentences.

Then send `caveman` and ask anything.

## Make it yours

The whole skill is one file: `SKILL.md`. Open it and edit it. Most people tune these first:

- Rule 13, the length budget.
- Rule 14, the emoji set.
- Rule 15, how simple the explanations should be.

You can also ask Claude to change it for you: "Update my readable-replies skill so that..."

## How it was made

It started as one complaint: "Claude's answers are hard to read." We looked at four community skills, kept the best idea from each, and wrote our own rules around them.

| Skill | Idea we kept |
|---|---|
| writing-clearly-and-concisely (obra/the-elements-of-style) | Strunk's sentence rules |
| caveman (JuliusBrussee/caveman) | The on-request short mode |
| humanizer (blader/humanizer) | The ban list of stock AI phrases |
| plain-english-content (OpenHands/extensions) | Front-loading the answer |

The ideas came from those skills. The text is our own.
