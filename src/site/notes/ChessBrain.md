---
{"dg-publish":true,"permalink":"/chess-brain/","dg-note-properties":{"date":"2026-04-24"}}
---


> ChessBrain is a project for developing some chess related programs. 

## ChessFront
This is the actual brainy parts of the system. It contains the foundational code to represent the game of chess, validate the rules and state and also search for moves. I had a series of blog posts explaining some of the techniques used to implement this in an efficient way which I will link and also add some more with time. 

### Features
- Bitboards and magic bitboards for move generation
- Zobrist hashing for transposition tables
- Pseudolegal move/capture only move generation
- Iterative deepening search
- Alpha/Beta search
- Quiescence selective search
- Late Move reductions
- MVV-LVA, Killer moves and history heuristic move ordering
- Time management
- Material and PST based tapered evaluation
- King safety/piece dynamism evaluation
- UCI support

### Posts
- [[PGN Parser\|PGN Parser]] - Ingesting a chess game
- [[Chess Bitboard\|Chess Bitboard]] - An efficient way to represent a game of chess in a computer
- [[Magic bitboard\|Magic bitboard]] - A fast attack generator implementation

## Apps
I also have an app to replay/edit a game PGN that also uses a UCI engine to evaluate a position. I use this app to mainly take notes on games that I played.

[![Screenshot-2026-04-24-at-1.52.12PM.md.png](https://img.dendiz.xyz/images/2026/04/24/Screenshot-2026-04-24-at-1.52.12PM.md.png)](https://img.dendiz.xyz/image/Er1a)

[![Screenshot-2026-04-24-at-1.53.20PM.md.png](https://img.dendiz.xyz/images/2026/04/24/Screenshot-2026-04-24-at-1.53.20PM.md.png)](https://img.dendiz.xyz/image/EHLX)