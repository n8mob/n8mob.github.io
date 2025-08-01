---
title: Highlighting Differences
date: 2025-08-01
layout: post
---

I was reviewing changes before I committed them. This particular file had a line marked as changed, but I couldn’t see what had changed. Usually that means a whitespace change. I counted my indents... four spaces on both.
I changed the diff-window's setting from 'Ignore whitespace' to 'Do not ignore'. Still nothing.

I usually like word-level diffs. I'm detail-capable, but not detail-oriented, so I usually set my diff to highlight at the word-level instead of the line level. But for this I pulled out the big, highly-detailed, gun: character-level differences.

Still nothing!

I ended up stepping through the line, character by character. It worked: I found I had added a `?` for chaining together some optional properties.

I had changed:

```tsx
puzzle.encoding.encodeText(...)
```

to:

```tsx
puzzle?.encoding?.encodeText(...)
```

---

### It was an "insertion" not a "change"

I was using a JetBrains IDE (WebStorm in this case), where the settings are found in:

> **Preferences → Editor → Color Scheme → Diff & Merge**

Each change type (Inserted, Changed, Deleted) has an **Important** color and an **Error Strip Mark** (for the scroll bar). The real gotcha ("got me") was that the Important Insertion was showing up against the Change background color, not the default background color (or the Inserted background color, for that matter). So the color difference was just too subtle.

I made the **Inserted:Important** color brighter. I still have to look closely to see the single-character change in question, but, at least now I can see it if I look for it! Before I couldn't even see it when looking closely!

Also: I usually do side-by-side diffs. I'm visual like that. But my AI coding assistant mentioned that I could try the **Unified Diff view**. I tried it afterward and it did help, because it made it easy to see where the characters on the two lines didn't match up.

### 

---

### The Takeaway
_*I*_ happened to make this particular change, but we're all using AI tools more and more. In reviewing changes, literally "highlighting differences" is more important than ever.
