# Candidate Frameworks

## F1: Law of Standards Risk Test

Source support:

- `computer/standard.htm`: proactive official standards frequently lead to adoption of simpler de facto standards.
- `computer/index.htm`: Sowa applies the law to Linux/POSIX-like compatibility versus Windows API.
- `computer/memo125.htm`: FS/GRAD risked losing customers because urgent needs and competitors would not wait.

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

- `computer/memo125.htm`: primary architecture is a closed list of fundamental interfaces; secondary architecture is open ended.
- `computer/memo125.htm`: COLBY had secondary components but lacked primary architecture.
- `computer/index.htm`: HLS/AFS ambiguity around hardware/software tradeoffs and migration.

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

- `computer/memo125.htm`: smooth migration must have top priority; interim products should be upward compatible.
- `computer/index.htm`: System/370-compatible and RISC-compatible paths were possible.
- `computer/afs/index.htm`: AFS objects and descriptors could integrate heterogeneous systems.

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

- `computer/memo125.htm`: implement ops in basic instruction set, debug, then microcode frequent routines.
- `computer/afs/index.htm`: Cocke's view that hardware should not implement what compilers can process as fast or faster.
- `computer/index.htm`: one bit for descriptors and conventional hardware could have supported FS legacy.

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

- `computer/index.htm`: management would not listen; career-killing questions.
- `computer/tftim.htm`: frequent reorganizations and ad hoc task forces were signs of trouble.
- `computer/memo125.htm`: security prevented whole-system understanding; large groups designed before architecture was stable.

Executable form:

1. Identify whether technical dissent is answerable with evidence.
2. Count reorganizations and task forces used as substitutes for architecture.
3. Check whether builders can understand the whole primary system.

Triple verification:

- V1: Supported by index, Task-Force Tim, and Memo 125.
- V2: Predicts hidden architecture risk in modern programs.
- V3: Distinct because it maps organization symptoms to system-design failure.

Status: accepted.
