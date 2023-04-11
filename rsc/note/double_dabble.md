# double dabble

convert BINARY to BCD

1. What is a BCD ?
   - BCD stands for Binary Coded Decimal, like in Decimals we have units,
     BCD seperate those
2. How it works ?
   - Look at the [Wikipedia page](https://en.wikipedia.org/wiki/Double_dabble), they offer a complete explanation about the process.

# LOOK UP TABLE OPTIMISATION

from `Erikbot#6368` of the "Logic World" Discord Server, at:
- [#1 thread](https://discord.com/channels/401255675264761866/901195561980543007/938075954629185597)
- [#2 thread](https://discord.com/channels/401255675264761866/901195561980543007/938089065738289252)

basically:
`|` = OR
`&` = AND
`~` = NOT

## MODULE 4bit

```bash
variable: a
	(a | b) &
	(a | c | d)

variable: b
	~c &
	(b | d) &
	(a | ~d)

variable: c
	(a | c) &
	(c | ~d) &
	(d | ~b)

variable: d
	(a | b | d) &
	(a | c | d) &
	(~a | ~d) &
	(~b | ~d)
```

## MODULE 5bit

```bash
variable: a
	(a | b) &
	(a | c | d)

variable: b
	(a | b | c) &
	(a | c | ~d) &
	(d | e | ~c) &
	(d | ~b | ~c) &
	(e | ~b | ~d)

variable: c
	(c | e) &
	(b | d | ~e) &
	(b | e | ~d) &
	(a | ~d | ~e) &
	(d | ~b | ~c)

variable: d
	(a | b | d) &
	(b | d | e) &
	(~b | ~d) &
	(b | e | ~c) &
	(a | c | d | ~e) &
	(~a | ~d | ~e)

variable: e
	(~a | ~e) &
	(b | d | ~c) &
	(a | b | c | e) &
	(e | ~b | ~c) &
	(e | ~b | ~d) &
	(~c | ~d | ~e) &
	(c | d | ~b | ~e)
```

## MODULE 8bit

```bash
variable: a
	(a | b) &
	(a | c | d)

variable: b
	(a | b | c) &
	(a | c | ~d) &
	(d | e | ~c) &
	(d | ~b | ~c) &
	(e | ~b | ~d)

variable: c
	(d | f | ~a) &
	(b | c | d | e) &
	(c | ~b | ~d) &
	(a | b | d | ~e) &
	(a | b | c | e | f) &
	(~b | ~d | ~e) &
	(b | e | ~c | ~d) &
	(b | f | ~c | ~e) &
	(d | e | f | ~b | ~c)

variable: d
	(c | e | f | ~b) &
	(c | e | g | ~b) &
	(e | f | g | ~a) &
	(a | b | c | d | e) &
	(b | d | ~c | ~e) &
	(d | g | ~c | ~e) &
	(e | f | ~a | ~d) &
	(e | g | ~a | ~d) &
	(a | b | c | d | f | g) &
	(d | ~a | ~e | ~f) &
	(f | ~b | ~c | ~e) &
	(a | c | e | ~d | ~f) &
	(c | f | g | ~b | ~d) &
	(~c | ~d | ~e | ~f) &
	(d | e | ~b | ~c | ~f) &
	(a | b | c | f | ~d | ~e) &
	(a | b | c | g | ~d | ~f) &
	(b | e | f | g | ~c | ~d)

variable: e
	(f | ~a | ~d) &
	(g | ~a | ~e) &
	(b | c | d | ~f) &
	(b | d | f | ~c) &
	(c | d | e | ~g) &
	(d | f | g | ~b) &
	(a | b | c | e | g) &
	(b | g | ~c | ~f) &
	(c | e | ~b | ~d) &
	(f | ~b | ~e | ~g) &
	(g | ~b | ~c | ~d) &
	(a | b | c | ~e | ~g) &
	(b | f | g | ~d | ~e) &
	(~c | ~e | ~f | ~g) &
	(a | c | ~d | ~f | ~g) &
	(b | e | ~d | ~f | ~g) &
	(c | g | ~b | ~e | ~f) &
	(d | e | ~b | ~c | ~f) &
	(e | f | ~c | ~d | ~g)

variable: f
	(b | c | d | e | f) &
	(c | f | ~b | ~d) &
	(d | e | ~b | ~f) &
	(e | g | ~a | ~f) &
	(a | b | d | f | ~e) &
	(b | e | f | g | ~c) &
	(d | ~a | ~e | ~g) &
	(d | ~b | ~c | ~f) &
	(d | ~b | ~f | ~g) &
	(f | ~b | ~d | ~e) &
	(a | b | g | ~d | ~f) &
	(e | f | g | ~c | ~d) &
	(a | c | d | f | g | ~e) &
	(b | c | ~d | ~f | ~g) &
	(d | e | ~b | ~c | ~g) &
	(d | e | ~c | ~f | ~g) &
	(f | g | ~a | ~d | ~e) &
	(a | b | e | f | ~d | ~g) &
	(b | c | d | g | ~e | ~f) &
	(b | ~c | ~d | ~e | ~g) &
	(e | ~b | ~c | ~f | ~g) &
	(a | c | g | ~d | ~e | ~f)

variable: g
	(c | e | g | ~b) &
	(d | e | f | ~a) &
	(a | c | d | e | g) &
	(b | e | ~c | ~g) &
	(d | g | ~c | ~e) &
	(e | f | ~c | ~g) &
	(e | g | ~a | ~d) &
	(c | ~b | ~e | ~g) &
	(e | ~a | ~f | ~g) &
	(e | ~c | ~d | ~g) &
	(f | ~a | ~e | ~g) &
	(g | ~c | ~e | ~f) &
	(a | c | d | ~e | ~g) &
	(b | e | f | ~c | ~d) &
	(c | d | e | ~b | ~f) &
	(d | e | g | ~b | ~f) &
	(a | b | c | f | g | ~e) &
	(b | f | ~c | ~d | ~g) &
	(d | g | ~a | ~e | ~f) &
	(f | g | ~b | ~d | ~e) &
	(a | b | c | g | ~d | ~f) &
	(a | b | e | f | ~d | ~g) &
	(c | ~d | ~e | ~f | ~g) &
	(d | ~b | ~e | ~f | ~g)
```
