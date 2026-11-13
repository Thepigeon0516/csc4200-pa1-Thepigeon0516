# AI Use Disclosure — PA1

_Generative AI is allowed on PA1 as a tutor, reviewer, debugging partner and
helper with tooling. It is not allowed to be the author of your work. See the PA1
brief, "AI, Authorship and You". Fill in every section. "None" is an acceptable
answer only if it is true._

## 1. Did you use generative AI on this assignment?

- [ ] No. I did not use any generative AI tool for any part of PA1.
- [X] Yes, as described below.

## 2. Statement (the syllabus form)

> The author (Daniel Geer) acknowledges the utilization of Claude, a language model
> developed by Anthropic, in the preparation of this assignment. codex
> was employed in the following manner(s) within this assignment: Guidance in tasks, code review, Debugging,
> Explaining necessary imports and functions need, Explanation.

## 3. Log

_One row per substantive interaction. Summaries are fine; you do not need to paste
whole conversations, but keep them in case you are asked._

| # | What I asked (summary) | What I used from the answer | What I changed or rejected | How I checked it was right |
|---|---|---|---|---|
| 1 |Asked for an explantion of the stuff need to be done to complete server.py and client.py |I used the funtions structures and what they need to do as well as the imports it recommened |I changed around the names of these functions and removed some of the imports that weren't necessary |I checked it with it with the full code and it said it was good |
| 2 |I asked if my etp.py matches the specifications in the documents given | I took the recomend changes in line of codes and looked into them | I changed them from raising an error to returning an empty payload |I looked at the specifications closely to see if what I did match what it says |

## 4. Where AI-produced material remains

_List each file and function (or document section) that still contains code or
text an AI tool generated, even after you edited it. If none, say none._
server.py
    do_get()
    do_put()
    
client.py
    exchange()
    write_local()
## 5. One thing the AI got wrong — or how you checked it

_Describe one answer, suggestion or piece of code that was wrong, misleading or
did not fit the specification, and how you caught it. If you found nothing wrong,
say so and describe how you checked (a test you ran, the part of the
specification you compared it with). If you did not use AI, describe one thing
you got wrong yourself and how you caught it._
An error in the code was in etp.py read_message() where after asking what I should put if the checks succeded it said to use
raise ValueError("BAD_VERSION"). The way I caught it was telling the AI the specifications for that partucallry section (8.1)

