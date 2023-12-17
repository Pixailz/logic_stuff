## Inventory

- 16 REG of 32 bit (A, B, C, D, ..., K)
- MAX DMUX: 256 (8bit)
- MAX COUNTER: MAX DMUX
- MAX MEMORY: MAX DMUX

> [!NOTE]
> Should improved how my DMUX work

## OPCODE

```
Unencoded payload:
LSB                             MSB
OOOOOOOO SSSSDDDD ELN00000 00000000
┌─────── ┌───┌─── ┌┌┌┌─────────────
│        │   │    │││└───────────── Reserved
│        │   │    ││└────────────── Not       │
│        │   │    │└─────────────── Less Than │ JMP FLAG
│        │   │    └──────────────── Equal     │
│        │   └───────────────────── Destination reg
│        └───────────────────────── Source reg
└────────────────────────────────── Operand
```

> [!NOTE]
> if **JMP FLAG** is satifisfied, JMP to whatever is set in the REG A
