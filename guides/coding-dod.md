# Coding guide: data-oriented (C, C++, Rust)

Load the relevant language section under the [coding standards loading rule](coding-standards.md#apply-these-rules) when implementing, designing or reviewing non-trivial C, C++ or Rust code. Existing project/framework conventions win; this guide then refines the [coding conventions](coding-conventions.md#language-defaults) defaults. Do not change working code's paradigm merely to follow it. "Measure before claiming performance gains" applies: layout changes need profiling evidence.

## Data-oriented principles

- Design around the data and its access patterns, not object taxonomies: ask what is read, written, and how often, then shape types and functions to that.
- Choose struct-of-arrays vs array-of-structs from measured hot paths; default to the simpler layout until profiling shows a cost.
- Prefer contiguous storage and batch processing; avoid pointer chasing and per-element heap allocation in hot loops.
- Separate hot data from cold data so frequently touched fields share cache lines.
- Make ownership and lifetimes explicit: one owner per allocation, borrowers documented or type-enforced.
- Express behavior as transforms over collections (functions taking and returning ranges/slices), not per-object methods dispatching one at a time.
- Use handles or indices instead of long-lived pointers where that simplifies lifetimes, relocation, or serialization.

### References

- [Data-Oriented Design (Richard Fabian)](https://www.dataorienteddesign.com/dodbook/): foundations, structs of arrays, and the measure-analyse-implement-confirm loop.

## C

### Apply

- Give every allocation one owner; release with a single exit point or the `goto cleanup` idiom, in reverse acquisition order.
- Use `size_t` for sizes and indices; check arithmetic for overflow before allocating or indexing.
- Pass pointer plus length together (or a small span struct); bounds-check every buffer access.
- Avoid unchecked string functions (`strcpy`, `sprintf`, `gets`); use length-bounded variants and verify truncation.
- Apply `const` to read-only pointers and parameters; use `restrict` only where aliasing is proven absent.
- Expose opaque types (forward-declared structs) at module boundaries; keep layout private.
- Return status codes, with results through out-parameters; document and check every error path.
- Prefer arrays of plain structs (or parallel arrays) over linked structures for hot data.
- Build with `-Wall -Wextra` and run sanitizers (ASan, UBSan) and static analysis where the project allows.

### References

- [SEI CERT C Coding Standard](https://cmu-sei.github.io/secure-coding-standards/sei-cert-c-coding-standard/): rules and recommendations for secure C.
- [Linux kernel coding style](https://www.kernel.org/doc/html/latest/process/coding-style.html): idioms for error-path cleanup and large C codebases.

## C++

### Apply

- Use RAII for every resource; follow the rule of zero, and the rule of five only when a type owns a resource directly.
- Prefer value semantics and composition over inheritance hierarchies.
- Store contiguous data in `std::vector`, `std::array`, and pass `std::span` (or iterator pairs) for views.
- Use `std::unique_ptr` for ownership; raw pointers and references are non-owning; no naked `new`/`delete`.
- Avoid virtual dispatch in hot loops; partition data by type and process each batch with a direct call or `std::variant` visitation.
- Use standard algorithms and ranges over hand-written loops where they state intent.
- Mark `const`, `constexpr`, `noexcept` and `[[nodiscard]]` where correct.
- Use handles or indices into a container instead of pointers that invalidate on reallocation.
- Follow the project's error model (exceptions or error codes/`std::expected`); do not mix styles within a module.

### References

- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines): resource management, interfaces, and performance rules.
- [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html): conventions for classes, functions, ownership, and headers.

## Rust

### Apply

- Prefer plain ownership and borrowing; reach for `Rc`/`RefCell`/`Arc<Mutex>` only when sharing is required.
- Store data in `Vec<T>` and pass `&[T]`/`&mut [T]`; use struct-of-arrays `Vec`s when a hot loop touches few fields.
- Model states with enums so invalid combinations are unrepresentable; match exhaustively.
- Use iterators and adaptors over indexed loops; collect only when a materialized result is needed.
- For graph-like or long-lived data, use index/arena/slotmap or ECS patterns with typed IDs instead of reference cycles.
- Return `Result` and propagate with `?`, adding context; define typed errors in libraries.
- No `unwrap`/`expect` or unchecked indexing on fallible input in library code; reserve them for proven invariants with a message.
- Minimise `unsafe`; wrap it in a small safe API and document the invariant in a `// SAFETY:` comment on each block.
- Run `cargo clippy` and `cargo fmt` clean; justify any `#[allow]`.

### References

- [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/): checklist for idiomatic, interoperable public APIs.
- [Rust Style Guide](https://doc.rust-lang.org/style-guide/): default formatting implemented by `rustfmt`.
- [Clippy Lints](https://clippy.rust-lang.org/master/index.html): lint catalogue for correctness, performance, and idiom.
- [The Rustonomicon](https://doc.rust-lang.org/nomicon/): rules for writing sound `unsafe` code.
