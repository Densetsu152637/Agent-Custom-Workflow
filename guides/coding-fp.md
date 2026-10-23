# Coding guide: functional (TypeScript, Haskell)

Load the relevant language section under the [coding standards loading rule](coding-standards.md#apply-these-rules) when implementing, designing, or reviewing non-trivial TypeScript or Haskell code. Existing project/framework conventions win; this guide then refines the [coding conventions](coding-conventions.md#language-defaults) defaults. Do not change working code's paradigm merely to follow it.

## Functional principles

- Keep a pure core and push effects (I/O, time, randomness, mutation of shared state) to thin edges that call it.
- Prefer immutable data; allow local, controlled mutation inside a function when it is clearer or faster, never hidden shared mutable state.
- Make illegal states unrepresentable: model alternatives as algebraic data types (tagged unions, sum types) instead of flags plus optional fields.
- Write total functions: handle every input, and return explicit failure values (`undefined`/union, `Maybe`, `Either`) instead of throwing for expected cases.
- Compose small named functions; name intermediate steps rather than chaining opaquely.
- Do not force currying, point-free style, or recursion when plain control flow reads better.

## TypeScript

### Apply

- Enable `strict` (including `noUncheckedIndexedAccess` and `exactOptionalPropertyTypes` where the project allows); never weaken it to silence an error.
- Model variants as discriminated unions with a literal `kind`/`type` tag; switch exhaustively and end with a `never` check so new variants fail compilation.
- Use `readonly`, `ReadonlyArray`, `Readonly<T>`, and `as const` for data that must not change; return new values instead of mutating arguments.
- Do not use `any`. Take `unknown` at boundaries and narrow with type guards; validate untrusted input (network, storage, user, parsed JSON) at runtime with the project's validator before it becomes a typed value.
- Avoid unchecked `as` casts and non-null `!`; prefer narrowing, `satisfies`, and branded types for distinct identifiers.
- Prefer `map`/`filter`/`reduce`, `flatMap`, and small pure helpers over loops that mutate accumulators when that reads clearer; use a plain loop when it is simpler or hot.
- Use classes only for meaningful state or lifecycle; otherwise use modules of functions and plain data types, consistent with the [coding conventions](coding-conventions.md#language-defaults).
- Await or explicitly handle every promise per [errors and asynchronous work](coding-conventions.md#errors-and-asynchronous-work); do not repeat or bypass it.
- Do not add a second `Result`/`Either` framework (for example `neverthrow`, `fp-ts` types) when the project's Promise/error composition suffices; use a discriminated union for locally expected failures.
- Export explicit types for public functions; let inference handle locals and callbacks.
- Run the project's ESLint (with `typescript-eslint` rules such as `no-explicit-any`, `no-floating-promises`, `switch-exhaustiveness-check`) and formatter; do not add new tooling.

### References

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/): official language reference (narrowing, unions, generics).
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html): conventions for types, imports, and language features.
- [typescript-eslint rules](https://typescript-eslint.io/rules/): index of lint rules for type-aware checks.

## Haskell

### Apply

- Write total functions: avoid `head`, `tail`, `fromJust`, `!!`, `read`, and incomplete patterns; use pattern matching, `NonEmpty`, or safe lookups, and enable incomplete-pattern warnings as errors in CI.
- Use `newtype` for distinct domain values and algebraic data types for states; keep constructors hidden behind smart constructors when invariants exist.
- Keep `IO` at the edge; keep business logic pure and pass dependencies as arguments or via the project's effect style (mtl classes, effect library, or `ReaderT` pattern) without mixing styles.
- Represent expected failure with `Maybe`, `Either e`, or `ExceptT`; reserve exceptions for truly exceptional or resource cases, and use `bracket`/`finally` for cleanup.
- Use strict fields (`!`), `foldl'`, bang patterns, or `Data.Map.Strict` for accumulators and long-lived data to avoid space leaks; add laziness deliberately.
- Prefer `Text` (or `ByteString` for bytes) over `String` for non-trivial text; keep `String` for small, local uses.
- Declare explicit export lists and qualified imports for containers and text modules (`import qualified Data.Map.Strict as Map`); avoid wildcard imports.
- Give every top-level definition a type signature; keep `-Wall` clean and enable only language extensions the project already uses or needs.
- Avoid lazy I/O (`getContents`, `readFile` streaming misuse, `interact`) for anything that must close or fail predictably.
- Use `where`/`let` and small named helpers for clarity; prefer readable guards and `case` to dense operator chains.
- Run HLint and the project formatter (ormolu or fourmolu) and follow the project's `.hlint.yaml`/formatter config.

### References

- [HaskellWiki Programming guidelines](https://wiki.haskell.org/Programming_guidelines): shared style and good-practice rules.
- [Kowainik Haskell Style Guide](https://kowainik.github.io/posts/2019-02-06-style-guide): practical style, imports, and naming conventions.
- [HLint](https://github.com/ndmitchell/hlint): linter suggesting simpler, more idiomatic code.
- [GHC User's Guide](https://downloads.haskell.org/ghc/latest/docs/users_guide/): compiler flags, warnings, and language extensions.
