========
Glossary
========

.. glossary::

    arithmetic logic unit
    ALU
        The part of the processor that performs simple integer calculations
        such as addition, subtraction, and bitwise logic.
        On some processors, this also multiplies and divides, but Kelev and
        `MIPS` both have separate multiply-divide units because of their
        `pipeline`\s.

        Math with non-integer values is handled by the `floating-point unit`.

    ARM
        A RISC instruction set architecture developed at Acorn Computers
        in Britain. It stands for "Acorn RISC Machine."
        It is slowly taking over the world due to its prevalence in mobile
        devices like smartphones, tablets, game consoles, and even small PC's.

        ARM is a 32-bit architecture like Kelev, and while `MIPS` was a
        stronger influence on Kelev's design, many architectural features
        (such as the 12-bit immediate format) were derived from ARM.

    CISC
        An acronym, standing for "Complex Instruction Set Computing."
        It is the opposite of `RISC`, and given the massive degree of
        technical superiority RISC designs have shown over their predecessors,
        "CISC" has taken on a pejorative meaning.

        Therefore, the only processors that everyone consistently describes
        as CISC (besides mainframe processors) are the `Intel 8086` and its
        derivatives.
        Other CISC processors include the Motorola 68000, Zilog Z80,
        and the MOS 6502, but aficionados of those processors can be reluctant
        to describe them as CISC because that would lump them together with
        the 8086.

    floating-point unit
    FPU
        The part of the processor that performs calculations with
        floating-point values (as opposed to integers).
        Compared to integer operations, floating-point operations are
        slow and require a lot of circuitry.
        However, they can represent numbers which are far larger and smaller
        than the equivalent amount of bits could as an integer.

    I
        Matthew Frazier. I am currently a student of Computer Science at
        North Carolina State University, and I designed Kelev.
        If you see "I" in the manual, it's referring to me (unless
        labeled otherwise).

    instruction set architecture
        The specification of what instructions a processor accepts,
        and what effect they have. By necessity, it also includes the
        data formats that the processor uses and its `register file`,
        but the ideal is for the ISA to be as independent of the actual
        implementation as possible.

    Intel 8086
        A `CISC` processor that completely took over the world in the 1980's.
        If you're reading this on a desktop or laptop computer, it's probably
        running a processor descended from the 8086.
        It originally became popular through its inclusion in the IBM PC,
        and stayed popular because of the massive amount of software
        written for it.

        However, most computer architects describe the 8086 as one of the
        worst-designed processors ever due to its numerous design quirks,
        complicated machine code, and highly variable performance
        characteristics.
        Intel has largely made its derivatives fast by continuing to throw
        more and more transistors at the problem.

    Kelev
        The Hebrew word for "dog."
        It has nothing to do with the characteristics of the processor,
        I just like dogs.

    MIPS
        A RISC instruction set architecture developed at Stanford.
        It stands for "Microprocessor without Interlocked Pipeline Stages."
        However, the name is also a pun on "Million Instructions per Second,"
        a largely discredited measurement of processor performance.

        The original MIPS is a 32-bit architecture like Kelev,
        and Kelev is heavily based on its design -- especially the
        pipeline.

    pipeline
        A processor feature that allows multiple instructions to be
        executing at once.
        They are still executed in order, but different parts of the
        instructions can overlap. For example, in::

            lw $6, [$8]
            add $8, 40

        Once the ``lw`` instruction is done with the ALU, the ``add``
        instruction can use it, even though ``lw`` isn't done yet -- it
        still needs to access the memory.
        This is great for efficiency, but it can cause weird effects like
        load delays and branch delays that programmers must be aware of.

    register
        A small amount of memory built in to the processor chip.
        It's used to hold data the processor is using right at this moment.

    register file
        In the abstract sense, this refers to the set of `register`\s which
        are available to the programmer on a particular `instruction set
        architecture`.

        In the physical sense, this refers to the hardware on the processor
        that actually holds the registers' values,
        and provides them to the `ALU` and other processor components.

    RISC
        An acronym, standing for "Reduced Instruction Set Computing."
        As an adjective, it describes an `instruction set architecture` --
        not specific processors.

        RISC has been defined in various ways. `Wikipedia's article`_ defines
        RISC as a design strategy "based on the insight that simplified
        (as opposed to complex) instructions can provide higher performance
        if this simplicity enables much faster execution of each instruction."

        Dominic Sweetman, in :title:`See MIPS Run`, is more specific,
        describing RISC as "a class of CPU architectures designed for easy
        pipelining."

        However, after discussing processor architecture with many people,
        I have come to the conclusion that in practical usage, RISC means
        "not like the `Intel 8086`."

.. _Wikipedia's article: https://en.wikipedia.org/w/index.php?title=Reduced_instruction_set_computing&oldid=558650396

