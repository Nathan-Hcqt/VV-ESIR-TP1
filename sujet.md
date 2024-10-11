# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers

1. USS Yorktown
The USS Yorktown is an American warship that encountered a computer bug in 1997. Its operating system was based on a version of Microsoft Windows NT, which was designed for civilian industry. The error was a division by zero, leading to a program crash. The bug affected the entire ship's system, leaving it disabled for a few hours, thus having a global impact.

The repercussions were diverse. For the IT industry, the incident highlighted the importance of security and robustness, especially in critical contexts like the military. There were also financial repercussions. More rigorous testing could have detected this error before it caused problems at sea. Division by zero tests are quite common in computing and are a well-documented issue. A simple test scenario with invalid or missing data would have revealed this flaw. This indicates that either the test scenario was not properly designed, or the tests did not consider relevant edge cases for such a critical environment.

2. The Bug Collection 701
The bug collection 701 concerns a StackOverflowError. Specifically, the method SetUniqueList.add() can trigger an error when the list tries to add itself as an element, causing an infinite recursion stack, thus crashing the program:


test() {
    SetUniqueList l = new SetUniqueList(new LinkedList<Object>());
    l.add((Object) l);
}
When a list adds itself, it creates an infinite loop because each call to hashCode() tries to evaluate the same object repeatedly.

This problem is global (and critical) at the list structure level because it affects the behavior of SetUniqueList when the list contains a circular reference. The problem was resolved after 22 days in version 4.3. The fix involved adding a check to prevent a list from adding a reference to itself, thereby avoiding infinite recursion.

3. Chaos Engineering
Netflix is not the only company practicing this type of engineering. For example, Amazon and Google use similar techniques. Netflix introduced and popularized chaos engineering, a technique for testing fault tolerance in production systems. These experiments involve simulating failures, such as shutting down a server, to observe how the system reacts and adapts.

4. WebAssembly
WASM (WebAssembly) is a binary language designed to be a safe and portable compilation target for the web and other embedding environments. Its structure is compact and includes value types, instructions, functions, local variables, and modules. Memory access is dynamically checked to prevent overflows. WASM uses structured control constructs (e.g., blocks, loops) to avoid irreducible loops. Its behavior can be considered deterministic.

The advantages of a formal specification are:

Clarity and precision in language behaviors and rules
Facilitation of implementation verification
Compatibility across different implementations on various platforms
Even with a formal specification, testing is critically important to correct implementation, errors, and performance. Tests verify that implementations behave correctly under real-world usage conditions, which is essential for identifying errors that formal specifications might not cover.

5. Key Benefits of the Mechanized Specification

According to the author of the paper "Mechanising and Verifying the WebAssembly Specification," the mechanized specification offers several key benefits:
Precision and Clarity: The mechanized specification provides a precise and unambiguous description of WebAssembly's behavior, which is essential for correctly understanding and implementing the language.
Formal Verification: The mechanized specification enables formal verification of the WebAssembly type system, ensuring its soundness. This means that well-typed programs will not encounter certain types of errors during execution.
Issue Identification: The process of mechanizing the specification revealed several issues and inconsistencies in the original WebAssembly specification. These issues were corrected, resulting in a more robust and reliable specification.
Executable Artifacts: The mechanized specification includes a verified executable interpreter and type checker. These artifacts can be used to validate the specification and ensure that implementations conform to it.
Interaction with Host Environment: The mechanized specification models the interaction between WebAssembly and its host environment, a crucial aspect of the language's behavior.

Enhancement of the Original Formal Specification

Yes, the mechanized specification helped improve the original formal specification of WebAssembly. The author notes that the mechanization process uncovered several deficiencies and unsoundness issues in the original specification. These issues were communicated to the WebAssembly working group and subsequently corrected, leading to a more accurate and reliable specification.

Additional Artifacts Derived from the Mechanized Specification

Several artifacts were derived from the mechanized specification:
Verified Executable Interpreter: An interpreter that executes WebAssembly programs while adhering to the formal specification. This interpreter is proven to be correct with respect to the mechanized specification.
Verified Type Checker: A type checker that ensures WebAssembly programs conform to the type system defined in the mechanized specification. This type checker is also proven to be sound and complete.
Proof of Soundness: A fully mechanized proof of the soundness properties of the WebAssembly type system. This proof ensures that well-typed programs enjoy progress and preservation properties during execution.

Verification of the Specification

The author verified the specification through several means:
Formal Proofs: The author provided formal proofs of the soundness properties of the WebAssembly type system. These proofs were mechanized using Isabelle, ensuring their correctness.
Conformance Tests: The executable interpreter derived from the mechanized specification was validated using the official WebAssembly conformance test suite. This ensures that the interpreter behaves correctly according to the specification.
Fuzzing Experiments: The author conducted fuzzing experiments to further validate the mechanized specification and the executable interpreter. These experiments involved generating random WebAssembly programs and comparing the behavior of the verified interpreter with industry implementations.

Need for Testing

No, the mechanized specification does not eliminate the need for testing. While the mechanized specification provides a formal basis for the language and allows for formal verification, testing remains essential for several reasons:
Validation of Conformity: Tests help validate that implementations conform to the formal specification. They can reveal discrepancies between theory and practice.
Detection of Bugs: Tests can identify bugs and unexpected behaviors that may not be covered by the formal specification or the mechanized proofs.
Performance and Optimization: Tests are necessary to evaluate the performance and optimizations of WebAssembly implementations, which are not covered by the formal specification.
Compatibility: Tests ensure that WebAssembly code runs correctly across different platforms and browsers, even if these platforms have slight differences in their implementations.
In summary, while the mechanized specification provides a strong foundation for the formal analysis and verification of WebAssembly, testing remains a crucial component for ensuring the quality, security, and performance of WebAssembly implementations.
