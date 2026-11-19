# tiny-chess-01 entry

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/qienzdork/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/qienzdork/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,096 bytes of Python. It plays the house gauntlet
through the env at `MAKEFUN_ENV_URL`: `POST /game` serves the game in
play, `POST /move` plays a move in UCI, and the loop ends when the env
answers status `done`.

## The engine

`main.py` holds the whole engine (a compressed payload with its
unpacker, as the rules allow). Inside, it is an original 0x88-board
engine: negamax with alpha-beta, iterative deepening to a fixed node
budget of 100,000 nodes a move, quiescence over captures, promotions
and replies to a check, a transposition table, MVV-LVA capture
ordering, killer moves, and an evaluation of material plus
piece-square terms with a tapered king table and a bishop-pair bonus.
No clock and no unseeded randomness: the same position always gets
the same move, so a trial's replay matches.

## The size rule

- `main.py` is the whole engine: at most 4,096 bytes as committed,
  Python 3.13, standard library only. It reads, imports or execs no
  other file in the repository.
- Every byte counts: comments, whitespace, docstrings, and the
  compressed payload with its unpacker.
- The rest of the tree (this README, LICENSE) is at most 8,192 bytes
  in all, and no file over 4,096. MIT licensed.
- Search to a fixed depth or node count, never a clock: a final
  contender's trials are replayed and must play the same moves.

## Grade it locally

You need Docker and the `makefun` CLI. Download the competition's dev
kit, unpack it, and from inside it run:

    makefun grade-local --kit . --bot <your repository> --driver docker

It plays one practice trial against the house engines, replays it, and
prints the Elo the scorer gives it. Before you submit, `makefun check`
runs the site's own pre-submit checks, size caps included.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
