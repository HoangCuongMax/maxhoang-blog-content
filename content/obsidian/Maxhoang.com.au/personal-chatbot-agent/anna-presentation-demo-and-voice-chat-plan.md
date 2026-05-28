---
title: Anna presentation demo and voice chat implementation plan
type: implementation-plan
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
  - presentation
  - demo
  - voice-chat
---

# Anna presentation demo and voice chat implementation plan

## Purpose

Use the expanded `content/posts/anna.md` blog post as a live demo source during a presentation about Anna, Max's personal AI chatbot.

The demo should feel like a real human conversation, not a scripted technical test. The audience should understand that Anna can:

- respond naturally to greetings
- explain who she is
- explain what she can do
- search or reference Max's website content
- guide visitors to the Anna blog post
- summarize why Max built the chatbot
- feel like a useful portfolio guide rather than a generic chatbot widget

The second goal is to plan a future "talk directly to Anna" feature so the presenter or visitor can speak into the chatbot instead of typing.

## Implementation status

Status on 2026-05-28:

- Version 1 is implemented in `MaxHoang_Notion`.
- Visitors can dictate a message into Anna's chat input using browser speech recognition.
- Visitors can turn on optional voice output so Anna reads new assistant replies aloud.
- The feature uses browser-native Web Speech APIs, so support depends on the visitor's browser and microphone permissions.
- The first release keeps "press mic, speak, review, send" as the safer presentation flow instead of always-on live voice.

## Demo context

The presentation moment:

1. Open Max Hoang Journal.
2. Show the Anna floating assistant.
3. Ask Anna friendly questions.
4. Move from small talk into identity and capability.
5. Ask about the Anna blog post.
6. Show that Anna can explain the chatbot architecture in plain English.
7. End with a clean one-sentence summary.

The audience should leave with this idea:

> Anna turns Max's website from a static portfolio into a guided AI conversation.

## 1-minute demo structure

Target duration: 55 to 75 seconds.

The conversation should be short enough for a presentation but rich enough to show personality and technical value.

| Time | Presenter action | Demo purpose |
|---:|---|---|
| 0-8s | Greet Anna | Show natural conversational opening |
| 8-18s | Ask who Anna is | Establish identity |
| 18-30s | Ask what she can do | Show website assistant capability |
| 30-45s | Ask how Max built her | Connect to the technical blog post |
| 45-58s | Ask for the blog post / summary | Demonstrate content grounding |
| 58-70s | Ask why Max built her | End with memorable product value |

## Recommended live script

Use this exact order for the cleanest flow.

### Turn 1

Presenter:

> Hi Anna, how are you today?

Expected Anna answer:

> I'm doing well, thanks for asking. I'm here and ready to help you explore Max's projects, notes, services, or anything else on the site.

Presenter note:

- Smile and pause for a second.
- This makes Anna feel less like a search tool and more like an assistant.

### Turn 2

Presenter:

> That's good. Who are you?

Expected Anna answer:

> I'm Anna, Max's digital research assistant. I help visitors quickly find useful things across this website, including AI projects, blog posts, notes, awards, services, and events. Think of me as a friendly guide for Max Hoang Journal.

Presenter note:

- This is the identity moment.
- Let the audience hear "digital research assistant" and "friendly guide".

### Turn 3

Presenter:

> Ah, so what can you do for me?

Expected Anna answer:

> I can help you find Max's projects, explain blog posts, surface AI notes, point to awards or events, and help you contact Max.

Presenter note:

- This shows Anna's practical value.
- If source or suggestion buttons appear, point briefly to them but do not get distracted.

### Turn 4

Presenter:

> I am doing a presentation about you. Can you explain how Max built you?

Expected Anna answer:

> Yes. Max built me as a personal AI chatbot inside his website. I use a retrieval system to search his published content, a markdown brain for personality and training memory, and source-aware answers so I can guide visitors without inventing facts.

Presenter note:

- This is the technical bridge.
- The key terms to emphasize are retrieval system, markdown brain, and source-aware answers.

### Turn 5

Presenter:

> Can you show me the blog post about you?

Expected Anna answer:

> The best place to start is the Anna blog post. It explains why Max built me, how the chatbot works, the RAG pipeline, memory layers, UI design, admin mode, and lessons learned.

Presenter note:

- If Anna shows a source button for the Anna post, click it.
- If no source appears, manually open `/blog/anna` after the answer and say: "This is the post Anna is talking about."

### Turn 6

Presenter:

> In one sentence, why did Max build you?

Expected Anna answer:

> Max built me to make his website feel less like a static portfolio and more like a helpful conversation where visitors can ask questions and quickly understand his work.

Presenter note:

- This is the strongest closing line.
- After this, stop asking questions and summarize for the audience.

### Turn 7

Presenter:

> Perfect. Thanks, Anna.

Expected Anna answer:

> You're welcome. Glad I could help.

Presenter note:

- Optional closing.
- Use only if there is enough time.

## Presenter summary after the chat

Say this after the demo:

> This demo shows Anna acting as a personal AI guide for my website. She can answer naturally, explain her own purpose, search website knowledge, point users to the right content, and make the portfolio feel interactive instead of static.

Shorter version:

> Anna is not just a chatbot. She is a conversational interface for my website.

## Backup script if the live chatbot is slow

If Anna is slow, keep talking while the answer loads:

> While Anna is thinking, what is happening behind the scenes is retrieval. The system searches my published website content, prepares a small context window, then asks the language model to answer with source-aware rules.

If Anna gives a shorter answer than expected:

> That is the short version. The full Anna blog post explains the deeper architecture: RAG, markdown brain, memory layers, UI design, and admin mode.

If Anna cannot find the blog post:

> This is a useful demo point too. Anna is designed to be honest when she cannot find something. I can still open the article directly at `/blog/anna`.

If the chatbot API fails:

> In production, Anna depends on the chat API and content index. If the API is unavailable, the fallback path is to show the Anna article directly and explain the architecture from the post.

## Demo audit

### Strengths

- The conversation starts naturally with "how are you?"
- It gradually moves from human tone to technical explanation.
- It shows Anna's identity, capability, content grounding, and product purpose.
- The demo uses the actual Anna post as evidence instead of only describing the chatbot verbally.
- The closing line is easy for the audience to remember.

### Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Chatbot response is too slow | Presentation loses pace | Use the "while Anna is thinking" narration |
| Anna gives a very short answer | Demo feels less impressive | Ask a follow-up: "Can you explain that with more detail?" |
| Anna cannot retrieve the post | Source demo fails | Open `/blog/anna` manually |
| Network/API issue | Live demo breaks | Keep screenshots or the blog post open in another tab |
| Answer is too long | Demo exceeds 1 minute | Interrupt politely: "Great, that is enough for the demo" |
| Voice recognition mishears presenter | Bad input reaches Anna | Start with typed demo until voice mode is stable |
| Audience cannot read the chat text | Demo value drops | Zoom browser to 125-150 percent before presenting |

### Timing audit

The full 7-turn script may exceed 1 minute if Anna gives long answers.

For a strict 60-second slot, use only these 5 turns:

1. Hi Anna, how are you today?
2. Who are you?
3. What can you do for me?
4. Can you explain how Max built you?
5. In one sentence, why did Max build you?

Skip:

- "Can you show me the blog post about you?"
- "Perfect. Thanks, Anna."

### Content audit

The demo should avoid asking:

- private questions about Max
- questions that require current real-time information
- broad technical questions unrelated to the website
- questions requiring legal, visa, medical, or financial advice

The demo should focus on:

- Anna identity
- Anna capability
- Anna architecture
- Max's website content
- the Anna blog post
- why the project matters

### Human conversation audit

The chat sounds human because:

- the first question is emotional and casual
- the second question asks identity naturally
- "Ah, so..." sounds like a real follow-up
- the presentation context gives Anna a reason to explain herself
- the final "thanks" gives the conversation a soft ending

Avoid making it sound robotic by not saying:

- "Please list your capabilities."
- "Execute retrieval over your corpus."
- "Summarize your implementation architecture."

Better phrases:

- "What can you do for me?"
- "Can you explain how Max built you?"
- "Why did Max build you?"

## Direct voice conversation implementation plan

Goal:

> Let visitors speak to Anna directly and optionally hear Anna speak back.

This should feel like a natural voice layer over the existing chatbot, not a separate chatbot system.

## Voice feature scope

Minimum useful version:

- microphone button in Anna chat input
- browser speech-to-text converts voice into text
- transcribed text appears in the existing input
- user can review before sending
- optional "send automatically after silence" mode

Better version:

- push-to-talk mode
- live transcript preview
- "listening" visual state
- Anna reads her answer aloud using text-to-speech
- mute/unmute voice output
- voice mode respects reduced-motion and accessibility settings

Advanced version:

- low-latency real-time voice conversation
- streaming audio in and audio out
- interruption support
- server-side speech processing
- stronger cross-browser support

## Recommended implementation path

Start with browser-native speech recognition and speech synthesis.

Reason:

- fastest to prototype
- no new backend required for version 1
- works as a layer over the existing `/api/chat`
- easy to disable if unsupported
- good enough for a presentation demo

Later, consider a real-time voice API if browser-native support is not reliable enough.

## Version 1 architecture

```txt
User clicks microphone
    |
    v
Browser SpeechRecognition listens
    |
    v
Transcript appears in ChatInput
    |
    v
User reviews or auto-sends
    |
    v
Existing handleSendMessage()
    |
    v
/api/chat
    |
    v
Anna text answer
    |
    v
Optional speechSynthesis reads answer aloud
```

This reuses the current chat pipeline. The voice feature only changes how input and output are handled in the browser.

## Files likely affected

App repo: `MaxHoang_Notion`.

Likely files:

- `components/chatbot/ChatInput.tsx`
- `components/chatbot/ChatbotWindow.tsx`
- `components/chatbot/ChatMessage.tsx`
- `components/chatbot/ChatbotWidget.tsx`
- `app/globals.css`

Optional new files:

- `components/chatbot/VoiceInputButton.tsx`
- `components/chatbot/useSpeechRecognition.ts`
- `components/chatbot/useSpeechSynthesis.ts`

## Version 1 UI design

Add a microphone icon button beside the send button.

States:

| State | UI |
|---|---|
| Unsupported | Mic button hidden or disabled with tooltip |
| Idle | Mic icon |
| Listening | Pulsing ring, "Listening..." label for screen readers |
| Transcript ready | Text appears in input |
| Error | Small inline message: "Microphone access was blocked." |

Controls:

- mic button starts listening
- clicking again stops listening
- Escape stops listening
- send button sends transcript
- optional setting: auto-send after pause

Accessibility:

- button has `aria-label`
- listening state uses `aria-live`
- do not rely on colour alone
- provide text fallback
- keyboard-accessible controls

## Version 1 technical tasks

1. Create a `useSpeechRecognition` hook.
2. Detect browser support:
   - `window.SpeechRecognition`
   - `window.webkitSpeechRecognition`
3. Request microphone permission only when the user clicks the mic button.
4. Start recognition in `continuous: false` mode for the first version.
5. Use `interimResults: true` for live transcript preview.
6. Write final transcript into the existing chat input.
7. Show a listening state in `ChatInput`.
8. Handle errors:
   - permission denied
   - no speech detected
   - unsupported browser
   - aborted recognition
9. Add optional text-to-speech for Anna answers with `window.speechSynthesis`.
10. Add a mute toggle so Anna does not unexpectedly speak in quiet environments.

## Text-to-speech plan

Add optional answer playback:

- disabled by default for normal website browsing
- enabled manually through a speaker button
- stop speaking when user sends a new message
- stop speaking when chat closes
- do not read source buttons or UI labels
- only read Anna's answer text

Potential UI:

- speaker icon in chat header
- "Voice on/off" tooltip
- per-message replay button later if useful

## Presentation voice mode plan

For presentation, the safest live voice demo is push-to-talk:

1. Click microphone.
2. Say: "Hi Anna, how are you today?"
3. Show transcript in the input.
4. Click send.
5. Anna answers.
6. Optionally click speaker to read answer aloud.

Avoid fully automatic voice conversation for the first presentation. It is riskier because the room audio, projector speakers, and audience noise can cause recognition mistakes.

## Version 2: Auto-send voice mode

After version 1 is stable, add:

- auto-send after 1.2 seconds of silence
- transcript confirmation timer
- cancel button
- visible countdown or subtle "Sending..." state

Flow:

```txt
Listening...
    |
    v
Transcript appears
    |
    v
Silence detected
    |
    v
Auto-send unless user cancels
```

This makes the interaction feel more natural, but it also increases risk during live demos.

## Version 3: Realtime voice mode

If browser-native voice is not good enough, consider a real-time voice API.

Possible architecture:

```txt
Browser microphone
    |
    v
Realtime session
    |
    v
Server/session token endpoint
    |
    v
Anna system prompt + retrieval tools
    |
    v
Streaming voice response
```

This would support:

- lower latency
- natural interruption
- streaming voice output
- more consistent cross-browser voice
- better demo feel

But it requires more careful implementation:

- ephemeral tokens
- audio permissions
- server-side security
- cost control
- fallback to text chat
- retrieval integration
- source display for spoken answers

Do not start here unless the presentation specifically needs real-time spoken conversation.

## Voice safety rules

Voice mode should not weaken Anna's existing rules.

Anna must still:

- use website sources for Max-specific claims
- avoid inventing private facts
- handle uncertainty honestly
- avoid legal, medical, visa, or financial advice
- keep source-aware answers
- show source buttons in the UI when available

Voice is only an input/output layer. It should not bypass retrieval, prompts, logging, or safety rules.

## Voice implementation acceptance criteria

Version 1 is complete when:

- user can click mic and speak a question
- transcript appears in the existing chat input
- user can edit transcript before sending
- sending uses the existing `/api/chat` flow
- unsupported browsers fail gracefully
- microphone permission denial shows a helpful message
- keyboard users can operate the mic button
- Anna can optionally read her answer aloud
- speech stops when chat closes
- `npm run lint`, `npm run typecheck`, and `npm run build` pass
- desktop and mobile layouts do not overlap

## Voice demo audit

### Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Browser does not support SpeechRecognition | Voice demo fails | Use Chrome/Edge and keep typed demo ready |
| Microphone permission blocked | No voice input | Test before presentation and reset permissions |
| Room noise causes bad transcript | Anna answers wrong question | Use push-to-talk and review transcript before sending |
| Speaker feedback loops into microphone | Recognition becomes unstable | Use headphones or disable TTS during input |
| Anna speaks too slowly | Demo runs over time | Keep TTS off or use it only once |
| Accent/noise recognition errors | Incorrect text | Keep typed backup prompts ready |

### Recommended presentation setting

- Use Edge or Chrome.
- Test microphone permission before starting.
- Keep chat zoom at 125-150 percent.
- Use push-to-talk, not auto-send.
- Keep text prompts copied in a backup note.
- Use voice for only the first question if time is short.

## Final recommendation

For the upcoming presentation:

1. Use the typed 1-minute demo as the reliable main flow.
2. Mention that voice mode is planned or in development.
3. If voice mode is implemented before the presentation, use it only for the first greeting.
4. Keep the rest typed so timing and accuracy stay controlled.

For implementation:

1. Build browser-native speech-to-text first.
2. Add optional text-to-speech second.
3. Add auto-send only after testing.
4. Consider real-time voice only after the browser-native version proves useful.
