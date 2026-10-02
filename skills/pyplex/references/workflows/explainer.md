# Explainer, how-to, tips or list video

Teach one thing clearly: an idea, a process, "5 mistakes", a recipe. Often faceless — pictures, motion graphics and a voice.

Read first: [story](../craft/story.md), [text](../craft/text.md), [sound](../craft/sound.md), [motion graphics](../craft/motion-graphics.md).

## 1. One idea, one shape

- The takeaway in one sentence: what the viewer will understand or be able to do afterwards.
- The shape: **concept** (name it → how it works, one layer at a time → why it matters), **steps** (the goal → step 1 … step N on the same stage → the result), **list** (hook → items with the best one last → wrap-up), or **case** (a real example → the lesson).
- Don't follow the order of the user's notes or article. Teach in the order a person understands.

## 2. Script

- A hook in the first two seconds: a surprising fact, a question, a common mistake.
- The takeaway by the second line; everything after it is the proof.
- One idea per line, 6–20 words, plain language. Make abstract things concrete: an example with real numbers, a comparison, a before and after.
- Signposts: "First…", "The trick is…", "Last one…".
- 30–60 s for social media — about 75–150 spoken words.

## 3. A picture for every line

Each line gets one picture that shows what it says — never a generic background:

- AI images with a slow `zoom_in` — the cheapest, calmest option — all in one style ("clean flat illustration, soft pastel colours" or "real photos, bright natural light").
- AI clips for the steps that need motion: hands pouring, a machine working.
- Cards for numbers, steps and key words, made with `create_motion_design` ([motion graphics](../craft/motion-graphics.md)); they're exported separately and added in the editor.
- For steps, keep the same "stage" (the same desk, the same kitchen) so the viewer watches the change, not the setting.

## 4. Voice, captions, music

- A voice-over per section with `elevenlabs/eleven-v3` or `elevenlabs/multilingual-v2`; music very low (0.15–0.2).
- Time the edit from the voice: each picture starts when its line starts (about 2.5 words per second). Tell the user the timing is estimated and easy to nudge in the editor.
- A caption for every phrase, with the key term `large` or in the accent colour.

## 5. The ending

Recap in one line — the takeaway again, sharper — then one call to action: follow for part 2, save this, try it today.
