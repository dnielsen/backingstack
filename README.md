# backingstack

## Stack

### Phase 1

Nodeless Kubernetes env with below workload.

#### Frontend

`PHP Guestbook`

#### Backends 

`Redis` (1 master, 2 slaves)

### Phase 2

Frontend from Phase 1 with below backend options.

#### Backends

1. `Redis` (1 master, 2 slaves)
2. `Postgres`

### Phase 3

Frontend from Phase 2 with below backend options.

#### Backends

1. `Redis` (1 master, 2 slaves)
2. `Postgres`
3. One object store (`Scality`?)

### Phase 4

Frontend from Phase 3 with below backend options.

#### Backends

1. `Redis` (1 master, 2 slaves)
2. `Postgres`
3. One object store (`Scality`?)
4. One Email server (`Postfix`?)

## Timeline

[myechuri] 9/27/19 - Phase 1
[myechuri] 10/4/19 - Phase 2
[myechuri] 10/11/19 - Phase 3
[myechuri] 10/18/19 - Phase 4
[Lukas] ? - DevSpace add on

## Meetups / Workshops

Meetup 1: week of 11/11/19

