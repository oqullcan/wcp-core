# WCP (White Cat Protocol) - Core Protocol Library (wcp-core) 🐾

# 🔴 **6/30/2025**

**Summary**

This document summarizes the development vision, philosophy, and technical goals of the Rust protocol library named `wcp-core`. The project aims to build an infrastructure that fundamentally addresses user autonomy, privacy, and security in digital communication, focusing on modern cryptography, proactive privacy techniques, and preparation for post-quantum cryptography. The development is conducted with great care, inspired by its namesake "**White Cat**."

**Note:** This repository is currently **empty**. The codebase, detailed specifications, and API documentation will be uploaded here once the project reaches a certain maturity level and initial internal reviews are completed. This README documents the project's vision, current progress, and future plans until then. Our goal is to provide a transparent development process even before code release.

---

## 1. Project Philosophy and Technical Motivation

WCP-Core is developed as a response to potential weaknesses in existing communication systems and emerging threats, based on the following core principles:

* 🔒 **Security Foundation:**

  * **Inspired by Proven Models:** Fundamentally utilizing concepts from industry-standard, proven cryptographic models such as the Noise Protocol Framework (targeting handshake flows similar to XX) and the Double Ratchet Algorithm.
  * **Trusted Libraries:** Only audited, community-trusted Rust cryptographic libraries (such as `ring`) and carefully managed FFI bindings for specific algorithms (e.g., `libsodium-sys`, with `unsafe` blocks strictly isolated) are used.
  * **Memory Safety:** Fully leveraging Rust's memory safety guarantees, with `#![forbid(unsafe_code)]` strictly applied to project-written code.
  * **Post-Quantum Preparation:** A cryptographic agility infrastructure is planned at the design level to facilitate integration of Post-Quantum Cryptography (PQC) algorithms, aiming to support future algorithm transitions and potential hybrid (classical + PQC) modes.

* 📊 **Proactive Privacy (Metadata Protection):**

  * Recognizing the sensitivity of metadata (packet size, timing, communication patterns, etc.), active protocol-level mechanisms are targeted to minimize leakage.
  * Initial focus includes **deterministic padding** for outgoing traffic (e.g., rounding packet sizes to predefined discrete values) and configurable **timing obfuscation** techniques (details and trade-offs actively under development).

* 🛡️ **Secure API ("Misuse Resistance"):**

  * A critical goal is designing an API that minimizes the chance of developers inadvertently making security mistakes.
  * Techniques such as leveraging Rust's strong type system, modeling state machines, using builder patterns, and enforcing logical ordering of API calls are planned.

* 🌐 **Network Independence:**

  * The core protocol logic is designed to be independent of underlying network transport layers (TCP, UDP, WebSockets, etc.) and potential anonymity layers (Tor, I2P, etc.).

* 📖 **Openness and Auditability Philosophy:**

  * The ultimate goal is to provide a fully open-source (FOSS - under Apache 2.0 OR MIT license), transparent, and independently auditable codebase. Community review will be encouraged after code release.

---

## 2. Development Progress (Current Estimated Status: \~60-70%)

So far, the following core components and capabilities have been largely completed and locally tested (but not yet published):

* **Core Cryptographic Flow:**

  * Initial implementation of handshake logic based on Noise Protocol Framework concepts (currently using the XX pattern with X25519/Ed25519).
  * Secure session management inspired by Double Ratchet principles (key derivation, state management, message numbering).
  * AEAD encryption for messages (currently ChaCha20-Poly1305).
* **Basic Protocol Structure:**

  * Initial implementation of a state machine modeling the protocol’s main states and transitions, supported by Rust’s type system.
  * Serialization/deserialization for core message types (currently using `serde` + `bincode`).
* **Initial Metadata Protection:**

  * Basic deterministic padding mechanism for outgoing packets.
  * Initial functional skeleton for configurable basic timing obfuscation.
* **API Skeleton:**

  * Fundamental `async/await` based Rust API functions managing protocol lifecycle (initiation, send/receive messages, termination).

---

## 3. Remaining Work and Next Steps (Pre-Release Priorities)

To prepare the project for uploading code and detailed documentation to this repository, the following steps are prioritized:

* **Protocol Specification and Detailing:** Preparing and clarifying an official specification document covering all aspects of the protocol (state machine, message formats, cryptographic operations, error codes, security assumptions, etc.). Defining precise specifications beyond being “Noise/DR inspired.”
* **Comprehensive Test Suites:** Significantly increasing unit and integration tests for existing code. Establishing robust fuzzing (`cargo-fuzz`) and property-based testing (`proptest`) infrastructure covering cryptographic operations, state transitions, concurrency, and edge cases. Developing test vectors against known protocol attack classes.
* **API Maturation and Misuse Resistance:** Stabilizing the current API, improving ergonomics, and enhancing misuse resistance (enforced step sequences, type states, etc.). Improving developer experience.
* **Finalizing Advanced Design Decisions:** Determining final designs for cryptographic agility mechanisms (PQC integration, agreement protocols, potential hybrid modes) and advanced metadata protection techniques (padding strategies, timing obfuscation algorithms, and their performance/privacy trade-offs).
* **Performance Analysis and Optimization:** Initial performance profiling and bottleneck identification. Balancing security/privacy features with practical performance.
* **Core Documentation:** Preparing comprehensive API reference (`rustdoc`) and draft guides explaining the protocol overview and usage.
* **Code Review and Refactoring:** Thorough review, cleanup, and improvement of the existing codebase.
* **Security Audit Planning:** Creating a roadmap for independent security audits after the codebase reaches maturity (initial releases will be unaudited).

---

## 4. ⚠️ Important Warnings (For Current Status) ⚠️

* **Code Not Yet Released:** This repository currently serves as a placeholder documenting the project’s vision and progress. Real code and detailed documentation will be uploaded as the above steps complete.
* **Experimental Work:** Even upon release, the project will be considered **experimental** initially. The main goal is gathering feedback and validating the design.
* **No Security Guarantees:** Until extensive testing and **independent security audits** are performed, **no guarantees of security** can be given regarding the protocol or implementation.
* **Not Suitable for Production:** The project in its current or initial released state is **not to be used in production environments.** It may contain serious security vulnerabilities.

---

## 5. License

The published code will be offered under one or both of the following licenses to provide flexibility to developers:

* Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0))
* MIT License ([LICENSE-MIT](LICENSE-MIT) or [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))

According to your preference.

---

WCP-Core: An ambitiously targeted, carefully conducted, and ongoing development process for secure and private communication. The codebase and detailed documentation will soon occupy this space. Stay tuned for updates!

---

