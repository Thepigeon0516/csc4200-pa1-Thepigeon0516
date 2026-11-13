# PA1 — ETP/1 Client and Server

**Students:** James Stull (`Thepigeon0516`), Daniel Geer (`DanielGeer`)
**Course:** CSC 4200 — Fall 2026
**Language:** _Python_
**Submitted commit:** _the SHA you paste into Canvas_

## Build and run

```
make build
make run-server PORT=5000 ROOT=server-files      # in one terminal
./etp-client --host 127.0.0.1 --port 5000 --name Thepigeon0516 list    # in another
```

_No external dependencies were used. The project was built and tested using Python 3 on the Linux VM._

## What works and what does not

The project is fully functional and passes all tests.

Execution: 30 / 30

Build and repository: 10 / 10

## Files

| File | What it is |
|---|---|
| `src/server.py` | ETP server logic |
| `src/client.py` | ETP client logic |
| `src/etp.py` | Protocol encoding |
| `src/transport_tcp.py` | TCP transport seam |
| `src/transport.py` | The transport the program uses |
| `DESIGN.md` | design document |
| `AI_USE.md` | AI-use disclosure and log |
| `evidence/pa1-capture.pcap` | loopback capture of my PUT and GET sessions |
| `evidence/time-wait.txt` | `ss` output showing TIME-WAIT after my session |
| `evidence/ANALYSIS.md` | my capture analysis |

---

## Authorship statement

We are the authors of this submission. Except where this README or `AI_USE.md`
says otherwise, we wrote, or rewrote and understand, every part of it — code,
documents and evidence — and we can explain any line of it to the instructor or
GTA. We are responsible for its correctness, including any part a
generative AI tool helped us produce. Our use of AI tools is disclosed in full in
`AI_USE.md`. The capture and measurements in `evidence/` come from our own programs,
run by us.

**Signed:** _James Stull, Daniel Geer._  **Date:** _11/13/2026_
