# Coding guide: object-oriented (Java)

Load the language section under the [coding standards loading rule](coding-standards.md#apply-these-rules) when implementing, designing, or reviewing non-trivial Java code. Existing project/framework conventions win; this guide refines the [coding conventions](coding-conventions.md#language-defaults) defaults. Do not change working code's paradigm merely to follow it.

## Object-oriented principles

- Give each type one cohesive responsibility and let it own and enforce its invariants; validate at construction so invalid instances cannot exist.
- Encapsulate state: expose behavior and narrow accessors, not mutable internals; return copies or unmodifiable views.
- Prefer composition and delegation to inheritance; inherit only for a true is-a relationship designed for extension, otherwise seal or finalize.
- Add interfaces only at real substitution, integration, or testing boundaries, not one per class.
- Default to immutable value objects; confine mutation to a small, well-scoped owner.
- Tell, don't ask: put behavior with the data it uses instead of querying state and deciding elsewhere. Do not create classes that only hold unrelated utilities.

## Java

### Apply

- Use `record` for immutable data carriers; validate in the compact constructor. Use classes when identity, mutable lifecycle, or inheritance is needed.
- Model closed hierarchies with `sealed` interfaces plus records/enums and exhaustive pattern-matching `switch`; avoid `instanceof` chains and unchecked casts.
- Make fields `private final` and classes `final` by default; open for extension deliberately and document the contract.
- Use constructor injection with required dependencies; avoid field injection, service locators, and mutable static state.
- Use `Optional` only as a return type for "maybe absent"; never as a field, parameter, or collection element, and never `Optional.get()` without a check. Do not return `null` collections.
- Use unchecked exceptions for programming errors and checked ones only for recoverable conditions callers must handle. Never swallow exceptions; preserve the cause when wrapping; manage resources with try-with-resources.
- Override `equals`, `hashCode`, and `toString` together and consistently (or use a record); never base equality on mutable fields used as map keys.
- Use `List.of`/`Set.of`/`Map.of` and `copyOf` for immutable collections; program to interfaces (`List`, `Map`) in signatures. Do not mutate collections you receive.
- Use streams for declarative transformations; use a plain loop when it has side effects, early exit, or is clearer. Avoid long or nested stream pipelines.
- Use `java.util.concurrent` (executors, `CompletableFuture`, concurrent collections, atomics) over raw `Thread`, `wait`/`notify`, or `synchronized` sprawl; share immutable data; use virtual threads for blocking I/O only where the project's JDK supports them.
- Follow the project's package layout, naming, and `@Override`/annotation conventions; keep packages cohesive and avoid cyclic dependencies.
- Run the project's formatter and static analysis (for example Checkstyle, Spotless, Error Prone, SpotBugs) and fix findings rather than suppressing them.

### References

- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html): formatting, naming, and practice defaults when the project has none.
- [JEP 395: Records](https://openjdk.org/jeps/395): semantics and constraints of records.
- [JEP 409: Sealed Classes](https://openjdk.org/jeps/409): sealed hierarchies and their use with pattern matching.
- [SEI CERT Oracle Coding Standard for Java](https://cmu-sei.github.io/secure-coding-standards/sei-cert-oracle-coding-standard-for-java/): secure and reliable coding rules.
- [The Java Language Specification, SE 21](https://docs.oracle.com/javase/specs/jls/se21/html/index.html): authoritative language semantics. Joshua Bloch's Effective Java covers the design idioms above.
