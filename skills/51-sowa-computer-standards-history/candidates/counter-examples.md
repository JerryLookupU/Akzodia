# Candidate Counter-Examples And Anti-Patterns

## A1: Declared Standard Before Implementation And Use

Source: `computer/standard.htm`.

Failure pattern: a proactive system is declared standard before anyone has implemented it, tested it, used it, and lived with it.

Accepted.

## A2: Future-System Replacement Without Migration

Source: `computer/afs/index.htm`, `computer/memo125.htm`.

Failure pattern: a new architecture promises future capability but cannot move the installed base smoothly.

Accepted.

## A3: Secondary Components Masquerading As Architecture

Source: `computer/memo125.htm`.

Failure pattern: editors, commands, displays, compilers, or query tools create a sense of progress while primary architecture remains undefined.

Accepted.

## A4: Slogan-Driven Design

Source: `computer/memo125.htm`.

Failure pattern: terms such as "transaction oriented" or "display oriented" become design substitutes instead of being translated into resource, runtime, linkage, recovery, or interface requirements.

Accepted.

## A5: Hardware-First Elegance

Source: `computer/memo125.htm`, `computer/afs/index.htm`.

Failure pattern: implementing language/data structures in hardware without clear goals, compiler comparison, or measured performance.

Accepted.

## A6: Late System Integration

Source: `computer/memo125.htm`.

Failure pattern: separately developed sophisticated components are integrated late, after interactions become unmanageable.

Accepted.

## A7: Task-Force Substitution

Source: `computer/tftim.htm`.

Failure pattern: every critical problem spawns a task force, but the architecture and plan do not change.

Accepted.

## A8: Secrecy Against Builders

Source: `computer/memo125.htm`.

Failure pattern: security procedures prevent implementers from understanding the whole primary system.

Accepted.
