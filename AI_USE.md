# AI Use Disclosure — PA1

_Generative AI is allowed on PA1 as a tutor, reviewer, debugging partner and
helper with tooling. It is not allowed to be the author of your work. See the PA1
brief, "AI, Authorship and You". Fill in every section. "None" is an acceptable
answer only if it is true._

## 1. Did you use generative AI on this assignment?

- [ ] No. I did not use any generative AI tool for any part of PA1.
- [x] Yes, as described below.

## 2. Statement (the syllabus form)

> The authors acknowledge the utilization of Gemini, a language model
> developed by Google, in the preparation of this assignment. Gemini
> was employed in the following manner(s) within this assignment: troubleshooting a tshark file write 
> permission error, troubleshooting a VS Code Remote SSH error, 

## 3. Log

| # | What I asked (summary) | What I used from the answer | What I changed or rejected | How I checked it was right |
|---|---|---|---|---|
| 1 | I got a permission denied error when using tshark to write to the evidence folder. | The solution was to capture the file to tmp with sudo, and move it to the evidence directory with sudo mv. | Nothing | I made sure the file was in the evidence folder and could be opened with my user. |
| 2 | VS code is stuck in a downloading server loop. | I used the command "rm -rf ~/.vscode-server" to clear the cache. | I ignored a step about checking the VM's disk space. | I ran the command in the vm terminal and was able to SSH with VS Code again. |
| 3 |  |  |  |  |  |
## 4. Where AI-produced material remains

_List each file and function (or document section) that still contains code or
text an AI tool generated, even after you edited it. If none, say none._

## 5. One thing the AI got wrong — or how you checked it

_Describe one answer, suggestion or piece of code that was wrong, misleading or
did not fit the specification, and how you caught it. If you found nothing wrong,
say so and describe how you checked (a test you ran, the part of the
specification you compared it with). If you did not use AI, describe one thing
you got wrong yourself and how you caught it._
