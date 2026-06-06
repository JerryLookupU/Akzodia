# Candidate Frameworks

## F1: Law of Standards Risk Test

Source support:

- `source-note section`: proactive official standards frequently lead to adoption of simpler de facto standards.
- `source-note section`: Sowa applies the law to Linux/POSIX-like compatibility versus Windows API.
- `source-note section`: FS/GRAD risked losing customers because urgent needs and competitors would not wait.

Executable form:

1. Name the official standard target X.
2. Name the simpler usable alternative.
3. Compare availability, migration cost, portability, explainability, implementation evidence, and ecosystem urgency.
4. Predict whether the official effort clarifies practice or accelerates a rival.

Triple verification:

- V1: Supported by standards essay, index discussion, and Memo 125.
- V2: Can assess modern APIs, agent protocols, and platform migrations.
- V3: More specific than "keep it simple" because it predicts adoption inversion.

Status: accepted.

## F2: Primary Versus Secondary Architecture Split

Source support:

- `source-note section`: primary architecture is a closed list of fundamental interfaces; secondary architecture is open ended.
- `source-note section`: COLBY had secondary components but lacked primary architecture.
- `source-note section`: HLS/AFS ambiguity around hardware/software tradeoffs and migration.

Executable form:

1. Separate fundamental system interfaces from feature facilities.
2. Stop secondary feature work if the primary base is undefined.
3. Define precise contracts that independent teams can implement against.

Triple verification:

- V1: Strong in Memo 125, indirectly supported by FS history and AFS/HLS.
- V2: Applies to platform APIs, operating systems, agent runtimes, and protocol stacks.
- V3: Distinct because it names a closed architecture set and open secondary set.

Status: accepted.

## F3: Evolutionary Migration Plan

Source support:

- `source-note section`: smooth migration must have top priority; interim products should be upward compatible.
- `source-note section`: System/370-compatible and RISC-compatible paths were possible.
- `source-note section`: AFS objects and descriptors could integrate heterogeneous systems.

Executable form:

1. Start with installed base and customer workloads.
2. Build interim products that add value now.
3. Keep transition protocols stable across old and new systems.
4. Let users move incrementally with rollback.

Triple verification:

- V1: Supported by Memo 125, index page, and AFS page.
- V2: Predicts failure of clean-break migrations and guides bridge design.
- V3: More specific than "be backward compatible" because it includes interim products and transition protocols.

Status: accepted.

## F4: Run Before Optimize

Source support:

- `source-note section`: implement ops in basic instruction set, debug, then microcode frequent routines.
- `source-note section`: Cocke's view that hardware should not implement what compilers can process as fast or faster.
- `source-note section`: one bit for descriptors and conventional hardware could have supported FS legacy.

Executable form:

1. Implement behavior in the most debuggable general layer first.
2. Measure frequency and bottlenecks.
3. Optimize only the small hot subset in hardware, native runtime, or special infrastructure.

Triple verification:

- V1: Supported by Memo 125, AFS, and index.
- V2: Applies to accelerators, native agent runtimes, kernel features, and protocol implementations.
- V3: Distinct because it ties optimization to architecture compatibility and definitive behavior.

Status: accepted.

## F5: Organizational Symptom Review

Source support:

- `source-note section`: management would not listen; career-killing questions.
- `source-note section`: frequent reorganizations and ad hoc task forces were signs of trouble.
- `source-note section`: security prevented whole-system understanding; large groups designed before architecture was stable.

Executable form:

1. Identify whether technical dissent is answerable with evidence.
2. Count reorganizations and task forces used as substitutes for architecture.
3. Check whether builders can understand the whole primary system.

Triple verification:

- V1: Supported by index, Task-Force Tim, and Memo 125.
- V2: Predicts hidden architecture risk in modern programs.
- V3: Distinct because it maps organization symptoms to system-design failure.

Status: accepted.
