# reversi

A pure-Go Reversi (Othello) rules engine — no protocol, no I/O, standard
library only.

`LegalSquares` lists playable squares, `Place` applies a move and flips all
closed lines, and `Advance` decides who moves next — computing passes and
game-over deterministically from the position, so a pass is never a separate
message (which would only be a desync surface in networked play).

```go
b := reversi.Start()
for _, sq := range reversi.LegalSquares(b, 1) { // +1 = Black, moves first
    nb, err := reversi.Place(b, 1, sq)
    if err == nil {
        next, passed, over := reversi.Advance(nb, 1)
        _ = next; _ = passed; _ = over
        b = nb
        break
    }
}
black, white := reversi.Counts(b)
_ = black; _ = white
```

## Install

```sh
go get github.com/richardwooding/reversi
```

Extracted from [kibitz](https://github.com/richardwooding/kibitz).

## License

MIT
