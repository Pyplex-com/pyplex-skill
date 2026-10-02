# A video template for other Pyplex users

Creators can turn an edit into a template: another user adds their own photo, every AI shot is remade for them, and the creator earns a fee each time (see [creators](../creators.md)).

## How video templates work

- In the Pyplex editor, every clip on the timeline that came from a Pyplex AI generation becomes a **step**. When someone uses the template, each step is generated again for them; everything else — music, text, transitions, the creator's own files — stays exactly as the creator made it.
- For each step's input (photo, video or audio), the creator chooses: the user gives their own, or the creator's file is used (kept private).
- Each step works from its own input — one step's result can't yet feed into the next step. Design steps that each take the user's photo directly.
- The creator sets a fee for each step, from $0 to $2.00; users pay the AI price plus that fee. Settings are locked — users can only pick a higher resolution.
- **Publish template** sits next to Export in the editor. Publishing charges a test fee equal to one full run, and the template is reviewed before it goes public.

## Plan a template that works for everyone

1. **One input from the user** — usually one clear photo of themselves (or their pet, product or room).
2. Two to five AI steps, each a striking change of that one photo.
3. Prompts that work for any face, age and skin tone. Try the steps with two or three different photos before publishing.
4. Music, text and transitions finish it: a hook line, cuts on the beat, one strong transition into the best step.

Ideas that suit the one-photo rule:

- **Me through the decades** — five image-edit steps: the same person in the 1950s, 70s, 90s, 2000s and today; a beat-cut slideshow edit.
- **Movie poster me** — three image-edit steps: an action poster, a romance poster, a horror poster.
- **Cinematic portrait** — three image-to-video steps from the same photo with different camera moves (slow push-in, orbit, a turn toward the camera), cut to music.
- **Product glamour** for sellers — four image-edit steps placing the product on marble, in water, on a mountain and in a studio, plus one slow-orbit video step.

## Build it with the AI

1. Make each step with the creator's own sample photo: `request_upload_link` → an edit or image-to-video model → quote → yes → start.
2. `create_video_edit` with those generations ("generation:<id>"), the music and the text.
3. Give the creator the Open in Editor link and tell them: watch it, then press **Publish template** next to Export, name each step, choose for each input whether the user gives it, and set the fee.
