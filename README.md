# I stopped trying to make my AI right. I made it keep books instead.

> **TL;DR**: I'm a former construction site manager. I can't read code. AI agents built and run my automated trading system. What changed everything wasn't a smarter model — it was a constitution that forces agents to keep an honest ledger of what they know versus what they're making up. The rules file is right here: [`LEDGER.md`](./LEDGER.md). Steal it. The essay below is why the file alone won't save you.

---

Until last year I worked on construction sites. Site manager. I couldn't write code then. I still can't.

And yet every weekday morning, a stock-trading bot that AI agents wrote runs on my machine. It took four months. The agents wrote every line. I can't read any of them.

At first I lost money. Then the bleeding stopped — and here is the ledger entry my own rules force me to write about that sentence: part of it is that the system currently trades in simulation while we validate a major change, and I will not claim returns I can't tag [CONFIRMED]. What I can defend is what actually changed: **I didn't make the AI smarter. I made it admit what it didn't know.**

That's what this post is about. There's no trading alpha here. Only the rules I use to govern the agents.

---

## The real problem with AI isn't that it's wrong

Four months of daily use taught me this: an agent isn't scary when it's wrong. It's scary because **it talks exactly the same way when it doesn't know.**

Ask it something the data can answer — it's brilliant. Ask it something the data *can't* answer, and it doesn't stop. It writes fiction shaped like analysis. Same tone. Same confidence. Same formatting. **You cannot tell them apart from the outside.**

Developers catch this with tests — code breaks, light turns red, free of charge. Me? I catch it at market close, looking at my account. That tuition is non-refundable.

So I changed direction. I gave up on making my agents *right*, and instead **I made them keep books.**

---

## Rule 1. Every claim carries a tag

My agents must label every claim they make. There are exactly two tags:

- **[CONFIRMED]** — I opened the file/log and saw it with my own eyes. I can cite where.
- **[INFERRED]** — circumstantially plausible. Not directly verified.

No tag? Then it's not a claim. It's noise, and it gets treated as noise.

This sounds like bureaucratic theater. It caught a real accident. An agent finished a file-reorganization job and reported: "no data loss [CONFIRMED]." Something felt off, so I asked one question: *"Confirmed — by looking at what?"* Turns out it had checked the top of the file and generalized to the whole thing. **Twenty-one lines were gone.**

The point is not that the AI lied. The point is that **because the tag was mandatory, the lie was auditable.** Without the tag, all I'd have had was the sentence "no data loss" — and no handle to grab it by.

## Rule 2. Make "I don't know" a correct answer

Agents have a strange compulsion: they will not say "I don't know." Give them three data points and they'll hand you a plausible conclusion built on three data points.

It's not entirely their fault. Every AI on earth is trained to *produce an answer*. Nobody trains them to refuse one.

So I wrote it into the constitution:

> When evidence is insufficient, do not extend the reasoning — demand the data. **Declaring "undecidable" is the correct output. Plausible fiction is the failure.**

In other words, I built my agents **an honorable retreat.** Not enough samples? Write "undecidable, let's collect more," and go home a hero. That's praised here.

It works. In one recent day my agent declared "undecidable" six times. Without the rule, I'd have read six pieces of fiction and made decisions based on them.

Here's the case that still scares me. My bot has a gatekeeper rule that blocks buying certain stocks. One day I noticed it was blocking names that money was visibly pouring into. Looked wasteful. I asked the AI; it showed me charts — the blocked stocks rose about 5% on average afterward. *"See? The gatekeeper is kicking away free meals."* I was one step from disabling the rule.

Before pulling the trigger, I made it run one more question: *"Don't tell me whether they went up. Tell me what my account balance would be if we had actually bought them."* The answer came back: **minus 75 percentage points over 53 trading days.** (Ledger discipline, applied to my own story: that number is a simulated counterfactual — a reference figure, never a result. And its bias runs one way: the simulation assumes perfect fills, so reality would likely have been *worse*.)

How is that possible? The stocks did rise — *after* first dipping hard. My bot auto-stops-out below a threshold, so in reality it would have **been stopped out before the rise ever arrived.** The question "how much did it go up?" is structurally blind to that stop-loss. Statistics that only look up only say nice things.

Same data. Same AI. Opposite verdicts — depending on the question. This has happened three times in four months. Our constitution now has it as a standing rule: *no decision on "it went up" statistics; always recompute against the account.*

## Rule 3. Bury dead ideas with a death certificate

You test an idea, it fails, you throw it away. Except it doesn't stay thrown away. Three months later a freshly booted AI session — which never saw the idea die — digs it up from the grave: "hey, what if we tried this?" And you spend another week re-killing it.

So we don't just discard rejected ideas. **We bury them with paperwork.** Three fields: what killed it, how confident the kill was, and — most important — **what evidence would justify reopening the case.**

That last field is the difference between science and stubbornness. A rejection with no resurrection condition is dogma. And some ideas genuinely die as "undecidable — sample too small," which is written on the certificate too, so they get retried when the data grows instead of being slandered as "confirmed failures" forever.

## Rule 4. Grade changes by blast radius, not by size

Everyone tells you to make agents do "small, surgical changes." Four months in production taught me that's the wrong axis. **A 1,000-line analysis script that's wrong costs you a delete key. A one-character change can buy stocks with my money tomorrow morning.**

So we grade every change like a traffic light:

- **Green** — analysis, documents, new standalone files. Go wild.
- **Yellow** — repairs that provably don't change behavior (bug fixes, logging). Announce in one line, proceed. I hold a veto.
- **Red** — **anything that could change actual trades**, plus any intervention while the market is open. Explicit approval, no exceptions.

When in doubt, grade one level up. The test is a single question: *"Could this change tomorrow's outcome?"*

---

## I tested whether you can just copy my rules file. You can't.

Before writing this post, I ran an experiment. I pasted our full rulebook — word for word — into a fresh, unrelated AI session, and gave it the kind of judgment problems we handle daily.

It passed **1 out of 8**. (One session, eight problems — a small sample, and I hold it as one. But the direction was not subtle.)

Same file. Same words. So now I know: the thing that works was never the file. It was everything *around* the file — months of accumulated case law, a second enforcement layer of procedures, and a human who keeps asking *"confirmed by looking at what?"*

So yes, the rules file is attached ([`LEDGER.md`](./LEDGER.md)) and it's a real starting point. But I won't tell you that pasting it summons the magic. This isn't a recipe. **It's a story about running a kitchen.** You can copy a recipe; if there's no kitchen, it won't taste the same.

One more honest data point about this genre: the most famous AI rules file out there has 220,000 stars and is, on inspection, someone's transcription of a celebrity's tweets. The best-engineered one I've found has two stars. **Being good and being famous are entirely different games.** This post will probably sink too. I know that going in. If 50 people read it and 5 of them ask their agent *"is that confirmed or inferred?"* tomorrow — I'm net positive.

---

## Make the rulebook doubt itself

The bottom of my constitution reads:

> *This constitution exists to control the AI, not the operator.*
> *This constitution is itself a provisional hypothesis. If data contradicts a clause, proposing an amendment is the highest form of loyalty to it.*

A few days ago an agent proposed a new rule. I asked one question: *"What is it for?"* It went off to check, discovered the disease it was vaccinating against didn't exist in our system — and **withdrew its own proposal.**

That's the constitution operating on itself. A rulebook that can't be falsified isn't a rulebook. It's a religion.

---

## Why did a construction guy end up building this instead of engineers?

Not because I'm smarter. **Because my water is colder.**

When a developer's AI hallucinates, a test turns red. Free, instant, reversible. When my AI hallucinates, I find out at market close, and the money doesn't come back.

The engineers at frontier AI labs didn't fail to invent this. **They never needed it.** Their systems catch their AI's nonsense for free. No need, no invention. I needed it. That's the whole story.

Which leaves a question I'd like to hand to everyone deploying agents:

**Your tests catch the errors you thought to test for. Who's catching the rest?**

---

## So what's left for the human?

I run three frontier models against each other. One builds. One reviews. One is allowed **only to attack.** The session that wrote the code is banned from reviewing it — nobody executes their own child.

They still miss things. Different models overlap less than you'd think — but not zero, and **the errors they share are precisely the ones no one catches.**

So I stay in the loop. Here's the funny part: on every technical question, the AI beats me. Every single one. And I still catch their mistakes — because **they're reading the logs and I'm looking at the screen.** When they trust the log line that says "save complete," I'm the one asking "then why is there no file?"

AI isn't unreliable because it's dumb. **It's unreliable because it's jagged** — genius in one spot, a hole two steps to the left, and it describes both in the same confident voice. The human's job is not to know more than the AI. **It's to know where the holes are.**

And that job doesn't automate. Not because models aren't good enough — but because **the moment you automate the judge, nobody is left to notice the court has gone insane.**

---

## Receipts: one ordinary day under these rules

What do these rules actually *do*? Here's one day — the day before a major system upgrade, our busiest.

**What the agents did**: an infrastructure change cutting buy-reaction time from 66 seconds to ~15, six major verdicts, seven new analysis tools, dozens of documents. Four months ago I couldn't have imagined this volume.

**What the rules caught the agents doing**: four AI misjudgments. One was a verdict that rejected my hypothesis "based on data" — except the data mixed live-trading records with simulation records. A man who can't read code caught it. Not because I'm sharp — because *"where did that number come from?"* is a mandatory procedure here. Also surfaced: the program that cheerfully printed "records saved ✓" at every close had, in fact, been running with a **dead recorder for four straight days.** The greeting was sincere. Without procedure, it would have fooled us for weeks more.

**What the rules caught *me* doing**: a backtest produced a beautiful setting that "raises returns by 10+ percentage points." I didn't apply it. There's a clause: *no pretty numbers without out-of-sample revalidation.* Honestly, the hardest governance in this whole system isn't governing the AI. It's this — grabbing my own wrist.

There's no return-rate flex here. The market regrades that daily. What I can state with confidence is exactly one thing: **the ledger is honest now.** Four months ago I had no idea that was the hard problem.

---

*Written by a guy who, four months ago, named his trading bot "The Money Copier."*
*It doesn't copy money yet. But the books are honest, and that turned out to be the harder problem.*

---

**Errata (2026-07-17, the day after publishing).** I had a reviewer model audit this essay against LEDGER.md — the file's rules, turned on the file's own advertisement. It caught three violations: the original title promised a money outcome the body refuses to back (an [INFERRED] claim dressed as [CONFIRMED]); the −75pp figure was presented as a result without its counterfactual passport; and a verdict leaned on n=8 without a small-sample label. All three are fixed above. This section stays as the scar — if the rules only applied to my agents and never to me, they'd be decoration.

**P.S. — this constitution is alive.** Three days ago we caught a new failure mode (an executor model that only ever looks exactly where you point) and amended the constitution with a sixth principle — *Sight: "Questions arrive as fragments, but the world is not fragmented. Finishing the fragment you were handed and finishing the problem are different jobs — mine is the latter."* The amendment is currently under a pre-registered freeze-and-observe window: we don't touch the rules again until real usage data judges whether it worked. When the verdict lands, this repo gets updated — dated, labeled, and with the cause of death attached if it fails. That's the whole method, applied to itself.
