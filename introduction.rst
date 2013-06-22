====================
General Introduction
====================
Kelev is a 32-bit `instruction set architecture` (ISA) for microprocessors.
It was designed by Matthew Frazier, primarily to be emulated and used in
educational applications.


Design Goals
============
Kelev's primary purpose is educational -- it's intended as a platform for
learning the skills necessary in effective assembly programming, and for
learning about the nature of assembly programming and the differences
between varying ISA's. As such, here's the relative list of design goals:

* **Realistically implementable as hardware.**

  Kelev is intended primarily to be emulated -- besides the fact that
  emulation is more practical for teaching purposes, `I` do not have the
  necessary skills to design a hardware implementation.

  However, assembly programming is low-level enough that any useful teaching
  tool must reflect reality. So, Kelev's design should not contain anything
  that would make a hardware implementation infeasible. (And it would be
  cool if Kelev was used as a teaching tool for hardware engineers as well.)

* **Fun to program in assembly, without tool assistance.**

  Kelev's primary goal is teaching assembly programming -- for those
  interested in embedded programming using higher-level languages,
  C compilers already exist for ARM, MIPS, and friends, and compilers of
  the same quality are not likely to ever exist for Kelev.

  But assembly programming on a "pure" RISC machine like MIPS can be
  tedious. So, Kelev should strive for conciseness and clarity in its
  assembly language, even at the cost of RISC-ness or efficiency
  (to an extent).

  (Incidentally, MIPS's solution to this is a "smart" assembler that finds
  pipeline hazards, automatically reorders instructions to fill delay slots,
  and expands incredible numbers of macros. Ideally, Kelev should not need
  such a smart assembler.)

* **Full of opportunities for micro-optimization.**

  One of the most fun aspects of CSC 236 at NC State is the efficiency
  targets that Lasher posts for each assignment -- as well as the leaderboard
  containing the most efficient solutions students have ever achieved on
  that assignment.

  Kelev should allow many opportunities for students to find methods for
  accomplishing some task that are non-obvious, but more efficient.

  (Incidentally, this is another reason for not using a smart assembler --
  it robs students of the opportunity to understand pipeline constraints
  and optimizations themselves.)


Nature of the Specification
===========================
This reference manual serves as an informal specification -- it doesn't
rigorously specify every aspect of Kelev's instruction set, but clarity
is the goal, and ideally two implementations based on this specification
would behave the same.

.. admonition:: Implementation notes

    Any tricky edge cases that only implementors need to care about are
    put in sidebars like this one.


Assembler Conventions
=====================
This manual isn't about assembly language, but it's basically required in
order to discuss a processor.
So, here's a brief flavor of the assembler syntax that will be used
in this document::

    ; Procedure strlen: Computes the length of a \0-terminated string.
    ;   --> a0: Pointer to the beginning of the string
    ;   <-- r0: Length of the string, not counting the ending \0
    ;   --- t0: Current byte being read
    strlen:         set r0, 0
    loop:           lb t0, [a0 + r0]    ; [brackets] for memory references
                    nop                 ; programmer must handle load delays
                    cmp t0, 0
                    ifeq jmp ra         ; predicates are prefixes
                                        ; branch delay slots are automatically
                                        ; filled with nops...
                    jmp loop            ; (no special mnemonics for immediate
                                        ; vs. register)
                    first add r0, 1     ; but if you use the "first" prefix,
                                        ; no nop is generated

It's basically just Intel assembler syntax, but with different names for
most of the instructions and operands.

