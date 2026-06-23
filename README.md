# Rust curriculum for Distributed Systems Engineers
### 8-Week ·  Self-Contained · 100% Verifiable · Repo-Independent · Moderate Difficulty

**Target:** Open-source developers entering Bitcoin, Lightning, Nostr, and distributed systems ecosystems via Rust.

**Primary Source:** [Building Bitcoin in Rust Book By Lukáš Hozda - braiins](https://braiins.com/books/building-bitcoin-in-rust?lang=en)

**Net Systems Value:** The book includes 2× more distributed systems content. Bitcoin is treated as one instance of P2P design, a conscious choice made because other Bitcoin-focused cohorts already cover Bitcoin-specific topics in depth.

**Pedagogy:**
- **Weeks 1–3:** Pure Rust fundamentals. Bitcoin concepts are **opt-in only** (Stretch/Deep Dive).
- **Weeks 4–8:** Bitcoin and P2P concepts enter as anchors (~10–15%), never overwhelming the systems engineering core.
- **QnA First:** Weekly questions are primarily conceptual QnA. Code questions (especially Q10) present a snippet and ask a conceptual question answered verbally, not by writing code.
- **100% Verifiable:** Every assignment specifies exact expected outputs (stdout, test assertions, or file artifacts) validated via `cargo test` or `cargo run`. No mentor reviews. No subjective grading.
- **Repo-Independent:** Outside repos are tagged as **Hints / References only**. All assignments are self-contained. You never need to clone, build, or read external repos to complete Core or Stretch work.
- **Difficulty Mix:** Core = easy (~60%). Stretch = moderate (~25%). Deep Dive = harder (~15%).
- **AI Policy:** Explicitly encouraged in Week 4 and for all Deep Dive assignments. The goal is learning *how* to read production Rust.

**Load Management:**
- **Core (3):** Expected. ~2–3 hours. Completable without any Bitcoin knowledge.
- **Stretch (2):** Optional. Moderate. ~1–2 hours extra.
- **Deep Dive (1):** Optional. Harder. For advanced learners or those with extra time.

---

## 📑 Quick Navigation

| Week | Theme | Core Focus |
|------|-------|------------|
| [Week 1](#week-1--ownership-memory--state-modeling) | The Machine | Structs, ownership, borrowing, enums |
| [Week 2](#week-2--type-systems-safe-apis--error-handling) | The Contract | `Result`, `Option`, traits, generics |
| [Week 3](#week-3--collections-iterators--data-structures) | The Organization | `HashMap`, `VecDeque`, iterators |
| [Week 4](#week-4--concurrency--system-design-synthesis) | The Bridge | Threads, `Arc`, `Mutex`, channels |
| [Week 5](#week-5--networking--protocol-design) | The Wire | TCP, binary protocols, framing |
| [Week 6](#week-6--async-rust--high-concurrency-services) | The Event Loop | Tokio, `async/await`, backpressure |
| [Week 7](#week-7--advanced-rust-for-infrastructure) | The Forge | Workspaces, trait objects, `thiserror` |
| [Week 8](#week-8--p2p-systems--distributed-algorithms) | The Swarm | Gossip, DHTs, consensus, CAP |

---

## Reading References (Hints Only Not Required for Assignments)

These repos are cited as **inspiration** for the curious. You do not need to clone, build, or read them to complete any assignment.

1. [cashubtc/cdk](https://github.com/cashubtc/cdk) — Clean types, error handling, serde.
2. [bitcoindevkit/bdk](https://github.com/bitcoindevkit/bdk) — Wallet primitives, traits, workspaces.
3. [vincenzopalazzo/lampo.rs](https://github.com/vincenzopalazzo/lampo.rs) — Small Lightning node, networking.
4. [Bitshala-Incubator/silent-pay-wallet](https://github.com/Bitshala-Incubator/silent-pay-wallet) — BDK applied, architecture.
5. [lightningdevkit/rust-lightning](https://github.com/lightningdevkit/rust-lightning) — Production async, P2P, state machines.
6. [fedimint/fedimint](https://github.com/fedimint/fedimint) — Distributed systems, consensus, advanced Rust.

---

## Week 1 — Ownership, Memory & State Modeling
**Theme:** The Machine  
**Central Question:** *How does a system safely manage resources without a garbage collector?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Prelude:** "Who is this book for?", "Requirements", "Goals and Structure" (pp. XII–XVI)
- **Ch. 3 (Setting Up):** "Rust: The first contact", "Hello world" (pp. 67–68)
- **Ch. 4 (Taming Rust):** "Memory model" (p. 93), "Strings in Rust" (p. 101), "Lifetimes of owned vs unowned values" (p. 104), "Pattern matching" (p. 111), "User-defined types (structs and enums)" (p. 116)
- **Ch. 4:** "Global 'variables' in Rust" (p. 112)

**Articles:**
- [Rust Ownership Explained](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html) — The Rust Book, Ch. 4.1
- [Stack vs Heap](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#stack-only-data-copy) — Rust Book

**Reference Repos (Hints Only):**
- `cashubtc/cdk` → `crates/cdk/src/types.rs` — Notice how simple structs and enums model protocol state.
- `bitcoindevkit/bdk` → `bdk/src/wallet/mod.rs` — Look at struct definitions only; ignore the logic.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** Explain the difference between the stack and the heap. Why does Rust force you to think about this explicitly when many languages hide it?
2. **Q:** What is ownership in Rust? Describe the three ownership rules in your own words.
3. **Q:** Why can an `i32` be copied implicitly but a `String` cannot? What trait governs this behavior?
4. **Q:** You have a variable `s1 = String::from("hello")` and you write `let s2 = s1;`. What happens to `s1`? Why does Rust design it this way?
5. **Q:** What is the difference between a *move* and a *borrow*? When would you choose one over the other?
6. **Q:** Explain pattern matching with `match`. Why is it safer than a chain of `if/else` statements for enums?
7. **Q:** What happens when an owned value goes out of scope? How does Rust ensure memory is freed without a garbage collector?
8. **Q:** In the context of distributed systems, why might a node prefer stack-allocated arrays for protocol headers instead of heap-allocated vectors?
9. **Q:** What is a struct? What is an enum? Give a real-world example of when an enum is better than a struct for modeling state.
10. **Code:** Look at the following snippet. Will it compile? If not, what is the exact error message you would expect, and why?
    ```rust
    fn main() {
        let s = String::from("hello");
        let len = calculate_length(s);
        println!("{} is {} chars long", s, len);
    }
    fn calculate_length(s: String) -> usize { s.len() }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Hello, Peer! | Build a `Peer` struct and a `greet()` function. |
| 2 | 🟢 Core | Borrow Checker Fix-It Shop | Fix 3 named borrow-checker bugs. |
| 3 | 🟢 Core | Traffic Light State Machine | Model `Red → Green → Yellow → Red` with an enum. |
| 4 | 🟡 Stretch | The Builder Pattern — Simple Config | Build a `ServerConfig` using a builder pattern. |
| 5 | 🟡 Stretch | Stack vs Heap Audit | Use `size_of_val` to measure stack vs heap allocation. |
| 6 | 🔴 Deep Dive | Ownership Analysis — Provided Snippet | Analyze a provided `Proof` snippet and return `[bool; 5]`. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Hello, Peer! (Your First Struct)

**What you'll build:** A simple `Peer` struct that stores a name and an ID, and a function that greets the peer.

**Step-by-step instructions:**
1. Create a new Cargo project: `cargo new week1_hello_peer`
2. In `src/main.rs`, define a struct `Peer` with two fields:
   - `name: String`
   - `id: u64`
3. Write a function `fn greet(peer: &Peer) -> String` that returns:
   - `"Hello, {name}! Your peer ID is {id}."` (replace `{name}` and `{id}` with the actual values)
4. In `main()`, create a `Peer` with `name = "Alice"` and `id = 42`.
5. Print the result of `greet(&peer)`.

**Why `&Peer`?** Because we only need to *read* the peer's data. We don't want to take ownership of it. This is the most common pattern in Rust — pass by reference when you only need to look.

**Starter code (fill in the blanks):**
```rust
struct Peer {
    // TODO: add name and id fields
}

fn greet(peer: &Peer) -> String {
    // TODO: return the formatted string
}

fn main() {
    // TODO: create a Peer and print the greeting
}
```

**Expected Output:**
```
Hello, Alice! Your peer ID is 42.
```

**Verification:**
- `cargo run` should print exactly the line above.
- `cargo test` checks the exact string for `Peer { name: "Alice", id: 42 }`.

**Hints:**
- Use `format!("Hello, {}! Your peer ID is {}.", peer.name, peer.id)` inside `greet`.
- Remember: `peer.name` auto-dereferences from `&Peer` to `Peer`.

---

#### 🟢 Core 2: Borrow Checker Fix-It Shop (3 Easy Fixes)

**What you'll build:** Nothing new. You'll fix 3 tiny broken programs that fail the borrow checker. Each teaches one common mistake.

**You'll receive 3 files:**

**`broken1.rs` — The "Moved String"**
```rust
fn main() {
    let msg = String::from("hello");
    print_message(msg);
    println!("Original: {}", msg); // ERROR: value moved
}
fn print_message(s: String) {
    println!("{}", s);
}
```
**Fix:** Change the function to borrow instead of own. Add `&` in exactly 2 places.

**`broken2.rs` — The "Double Mutable Borrow"**
```rust
fn main() {
    let mut s = String::from("hello");
    let r1 = &mut s;
    let r2 = &mut s;
    println!("{} {}", r1, r2); // ERROR: cannot borrow `s` as mutable more than once
}
```
**Fix:** Use the first reference before creating the second. Move the `println!` that uses `r1` before `let r2`.

**`broken3.rs` — The "Dangling Reference"**
```rust
fn main() {
    let r = create_string();
    println!("{}", r);
}
fn create_string() -> &String {
    let s = String::from("hello");
    &s // ERROR: `s` does not live long enough
}
```
**Fix:** Return the `String` itself (owned), not a reference to it. Change `&String` to `String` and return `s` directly.

**Expected Output:**
```
hello
hello
hello
```

**Verification:**
- `cargo run` should print `hello` three times (one from each fixed file).
- `cargo test` compiles all three files successfully.

**Hints:**
- For `broken1`: The fix is the same as Question 10 above. Add `&` to the parameter and the argument.
- For `broken2`: You can only have ONE mutable borrow at a time. Use it, then drop it, then make another.
- For `broken3`: You cannot return a reference to something that will be destroyed when the function ends. Return the value itself.

---

#### 🟢 Core 3: Traffic Light State Machine

**What you'll build:** An enum that models a traffic light and a function that transitions between states.

**Step-by-step instructions:**
1. Define an enum `TrafficLight` with three variants: `Red`, `Yellow`, and `Green`.
2. Write a function `fn next_state(light: TrafficLight) -> TrafficLight` that returns the next state:
   - `Red` → `Green`
   - `Green` → `Yellow`
   - `Yellow` → `Red`
3. Write a function `fn describe(light: &TrafficLight) -> &'static str` that returns:
   - `"Stop"` for `Red`
   - `"Caution"` for `Yellow`
   - `"Go"` for `Green`
4. In `main()`, start with `Red`, print its description, transition 3 times, printing each state.

**Expected Output:**
```
Current: Red -> Stop
Next: Green -> Go
Next: Yellow -> Caution
Next: Red -> Stop
```

**Verification:**
- `cargo run` prints exactly the 4 lines above.
- `cargo test` checks `next_state` for all 3 transitions and `describe` for all 3 colors.

**Hints:**
- Use `match` in both functions. It's the most idiomatic way.
- `&'static str` means a string literal that lives forever. `"Stop"` is one.

---

#### 🟡 Stretch 4: The Builder Pattern — Simple Config

**What you'll build:** A `ServerConfig` struct built with a builder pattern.

**Step-by-step instructions:**
1. Define `struct ServerConfig { host: String, port: u16 }`.
2. Define `struct ServerConfigBuilder { host: Option<String>, port: Option<u16> }`.
3. Implement:
   - `fn new() -> Self` — starts with `None` for both
   - `fn host(mut self, h: String) -> Self` — sets host
   - `fn port(mut self, p: u16) -> Self` — sets port
   - `fn build(self) -> Result<ServerConfig, &'static str>` — returns `Ok` if both are `Some`, else `Err("incomplete config")`
4. Build a config with `host("localhost")` and `port(8080)`.

**Expected Output:**
```
ServerConfig { host: "localhost", port: 8080 }
```

**Verification:** `cargo test` checks the built config matches.

**Hints:**
- `Option::ok_or("incomplete config")` is one way to convert `Option` to `Result`.
- `self` in builder methods means the builder owns itself and returns itself.

---

#### 🟡 Stretch 5: Stack vs Heap Audit

**What you'll build:** A program that demonstrates which values live on the stack vs. the heap, verified by output.

**Step-by-step instructions:**
1. Define `struct Packet { id: u64, payload: String }`.
2. In `main()`, create:
   ```rust
   let stack_only = 42i32;
   let heap_string = String::from("hello");
   let packet = Packet { id: 1, payload: String::from("data") };
   ```
3. Print the size of each value using `std::mem::size_of_val`:
   ```rust
   println!("i32 size: {} bytes", std::mem::size_of_val(&stack_only));
   println!("String size: {} bytes", std::mem::size_of_val(&heap_string));
   println!("Packet size: {} bytes", std::mem::size_of_val(&packet));
   ```
4. Print the length of the heap-allocated data:
   ```rust
   println!("String heap len: {}", heap_string.len());
   println!("Packet payload heap len: {}", packet.payload.len());
   ```

**Expected Output:**
```
i32 size: 4 bytes
String size: 24 bytes
Packet size: 32 bytes
String heap len: 5
Packet payload heap len: 4
```

**Verification:** `cargo test` asserts exact sizes (platform-dependent, so use `assert!` with comments explaining why).

**Hints:**
- On 64-bit systems, `String` is 24 bytes (pointer + len + capacity, each 8 bytes).
- `Packet` contains a `u64` (8 bytes) + `String` (24 bytes) = 32 bytes on the stack.
- The actual `"hello"` and `"data"` bytes live on the heap. `size_of_val` only measures the stack part.

---

#### 🔴 Deep Dive 6: Ownership Analysis — Provided Code Snippet

**What you'll build:** Analyze ownership in a provided code snippet and answer via a multiple-choice test.

**Step-by-step instructions:**
1. You are given the following snippet in `src/main.rs` (do NOT modify it):
   ```rust
   struct Proof {
       id: String,
       amount: u64,
       secret: String,
   }

   fn inspect(proof: &Proof) -> String {
       format!("{}: {}", proof.id, proof.amount)
   }

   fn consume(proof: Proof) -> u64 {
       proof.amount
   }

   fn main() {
       let p = Proof {
           id: String::from("abc123"),
           amount: 100,
           secret: String::from("shhh"),
       };
       let summary = inspect(&p);
       let taken = consume(p);
       println!("{} | {}", summary, taken);
   }
   ```
2. Answer the following by writing a function `fn analyze() -> [bool; 5]` that returns:
   - `[0]`: `true` if `inspect` borrows `p`, `false` if it owns it
   - `[1]`: `true` if `consume` takes ownership of `p`
   - `[2]`: `true` if `p.id` is moved during `inspect`
   - `[3]`: `true` if `p` can be used after `inspect` is called
   - `[4]`: `true` if `p` can be used after `consume` is called
3. The function should return `[true, true, false, true, false]`.

**Expected Output:**
```
Analysis: [true, true, false, true, false]
```

**Verification:** `cargo test` asserts `analyze() == [true, true, false, true, false]`.

**Hints:**
- `&Proof` means borrow. `Proof` (without `&`) means move/own.
- `p` can be used after `inspect(&p)` because `inspect` only borrows.
- `p` CANNOT be used after `consume(p)` because `consume` took ownership.
- `format!` uses `Display` which only needs `&String`, so `proof.id` is borrowed, not moved.

</details>

---

## Week 2 — Type Systems, Safe APIs & Error Handling
**Theme:** The Contract  
**Central Question:** *How do we model invalid states out of existence?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 4 (Taming Rust):** "User-defined types (structs and enums)" (p. 116), "Static dispatch" (p. 118), "Generic param bounds" (p. 120), "Dynamic dispatch" (p. 121)
- **Ch. 5 (Implementing a Bitcoin Library):** "Error handling in Rust" (pp. 192–200), "Error handling in btclib" (p. 202)
- **Ch. 4:** "Functional Programming in Rust" — "Immutability" (p. 123), "The type system" (p. 127), "Functions and closures" (p. 142)

**Articles:**
- [The Rust Book: Error Handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html) — Ch. 9
- [Traits in Rust](https://doc.rust-lang.org/book/ch10-02-traits.html) — Rust Book, Ch. 10.2

**Reference Repos (Hints Only):**
- `bitcoindevkit/bdk` → `bdk/src/wallet/error.rs` — Study how errors are categorized.
- `cashubtc/cdk` → `crates/cdk/src/error.rs` — Compare error taxonomy.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is the difference between `Option<T>` and `Result<T, E>`? When would you use one versus the other?
2. **Q:** Explain the phrase "make invalid states unrepresentable." How do Rust's type system (enums, structs, generics) help achieve this?
3. **Q:** What is a trait? How is it similar to and different from an interface in Java or a type class in Haskell?
4. **Q:** What is a generic type parameter? Why is `Vec<T>` preferable to writing separate `VecInt`, `VecString`, etc.?
5. **Q:** Describe the builder pattern. Why is it particularly useful in systems programming when constructing complex protocol messages?
6. **Q:** What is the difference between recoverable and unrecoverable errors? Why does Rust use `Result` for the former and `panic!` for the latter?
7. **Q:** In a distributed system, why is it dangerous to use `unwrap()` on network I/O results? What should you do instead?
8. **Q:** What are trait bounds? Why does a function `fn print<T: Display>(item: T)` require `T` to implement `Display`?
9. **Q:** How does `Result` composability (`map`, `and_then`) help prevent deeply nested error-handling code?
10. **Code:** Look at the following snippet. What will it print, and why?
    ```rust
    fn main() {
        let x = Some(5);
        let y: Option<i32> = None;
        println!("{}", x.unwrap_or(0) + y.unwrap_or(0));
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Safe Division | Write `divide(a, b) -> Result<f64, &'static str>` with NaN and zero checks. |
| 2 | 🟢 Core | Shape Area | Define an `Area` trait and implement it for `Circle` and `Rectangle`. |
| 3 | 🟢 Core | Config Parser | Parse `"key=value"` into `Option<(String, String)>` with trimming. |
| 4 | 🟡 Stretch | Generic Key-Value Store | Define a `Store<K, V>` trait and implement it with `HashMap`. |
| 5 | 🟡 Stretch | Error Translation | Wrap `io::Error` and `ParseError` in a custom enum with `From`. |
| 6 | 🔴 Deep Dive | Error Taxonomy Analysis | Map a provided `WalletError` enum's variants to categories and count them. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Safe Division (Your First Result)

**What you'll build:** A function that divides two numbers and returns a `Result` with specific error messages.

**Step-by-step instructions:**
1. Create a new Cargo project: `cargo new week2_safe_division`
2. Write `fn divide(a: f64, b: f64) -> Result<f64, &'static str>`
3. The function should:
   - Return `Ok(a / b)` if `b` is not zero and neither `a` nor `b` is `NaN`
   - Return `Err("Division by zero")` if `b == 0.0`
   - Return `Err("Invalid operand")` if either `a` or `b` is `NaN` (use `f64::is_nan()`)
4. In `main()`, test with 3 cases and print each result using `match`.

**Expected Output:**
```
divide(10.0, 2.0) = Ok(5.0)
divide(10.0, 0.0) = Err("Division by zero")
divide(f64::NAN, 2.0) = Err("Invalid operand")
```

**Verification:**
- `cargo run` prints exactly the 3 lines above.
- `cargo test` asserts exact `Result` values for 6 test cases (including edge cases like `-0.0` and both NaN).

**Hints:**
- Check for NaN FIRST, before checking for zero. Why? Because `NaN == 0.0` is `false`, but you still want to reject NaN inputs.
- Use `f64::is_nan()` to check for NaN. `==` does not work for NaN.

---

#### 🟢 Core 2: Shape Area (Your First Trait)

**What you'll build:** A trait `Area` and two structs that implement it. This teaches how Rust uses traits for polymorphism.

**Step-by-step instructions:**
1. Define a trait `Area` with one method: `fn area(&self) -> f64`
2. Define two structs:
   - `Circle { radius: f64 }`
   - `Rectangle { width: f64, height: f64 }`
3. Implement `Area` for both:
   - Circle area = π × r² (use `std::f64::consts::PI`)
   - Rectangle area = width × height
4. Write a function `fn print_area<T: Area>(shape: &T)` that prints `"The area is {area}"`
5. In `main()`, create one circle and one rectangle, and print both areas.

**Expected Output:**
```
Circle(3.0) area = 28.274333882308138
Rectangle(4.0, 5.0) area = 20.0
```

**Verification:**
- `cargo run` prints the two lines above.
- `cargo test` asserts area within `0.001` for 4 shapes (Circle 3.0, Circle 0.0, Rectangle 4×5, Rectangle 0×0).

**Hints:**
- `print_area` uses a generic with a trait bound. This is called "static dispatch."
- The compiler creates a separate version of `print_area` for `Circle` and `Rectangle`. This is fast!

---

#### 🟢 Core 3: Config Parser (Your First Option Chain)

**What you'll build:** A function that parses a `"key=value"` string and returns `Option<(String, String)>`.

**Step-by-step instructions:**
1. Write `fn parse_config(input: &str) -> Option<(String, String)>`
2. The function should:
   - Return `None` if `input` is empty
   - Find the first `=` sign
   - Return `None` if there is no `=` sign
   - Split into left and right parts
   - Trim whitespace from both parts
   - Return `Some((left, right))`
3. In `main()`, test with 4 cases and print each.

**Expected Output:**
```
parse_config("host=localhost") = Some(("host", "localhost"))
parse_config("badinput") = None
parse_config("") = None
parse_config("  key  =  value  ") = Some(("key", "value"))
```

**Verification:**
- `cargo run` prints the 4 lines above.
- `cargo test` asserts exact `Option` values for 6 test cases.

**Hints:**
- `input.find('=')` returns `Option<usize>`.
- `input[..idx]` gives the left side, `input[idx+1..]` gives the right side.
- Use `.trim()` on both sides to handle whitespace.
- Try writing this using `?` (the try operator) for extra practice: `let idx = input.find('=')?;`

---

#### 🟡 Stretch 4: Generic Key-Value Store

**What you'll build:** A generic storage trait and an in-memory implementation.

**Step-by-step instructions:**
1. Define `trait Store<K, V>` with:
   - `fn get(&self, key: &K) -> Option<&V>`
   - `fn put(&mut self, key: K, value: V)`
2. Define `struct InMemoryStore<K, V> { data: HashMap<K, V> }`
3. Implement `Store` for `InMemoryStore`
4. Test with `K = String`, `V = u32`

**Expected Output:**
```
put("alice", 100) -> get("alice") = Some(100)
get("bob") = None
```

**Verification:** `cargo test` asserts exact values.

**Hints:**
- `HashMap` already has `get` and `insert`. Your trait just wraps it.
- Remember `K` and `V` need to be generic over the struct AND the trait.

---

#### 🟡 Stretch 5: Error Translation — Mini Network Stack

**What you'll build:** An enum that wraps different error types and automatically converts from them.

**Step-by-step instructions:**
1. Define `enum AppError { Io(std::io::Error), Parse(&'static str) }`
2. Implement `From<std::io::Error>` for `AppError` manually:
   ```rust
   impl From<std::io::Error> for AppError {
       fn from(e: std::io::Error) -> Self { AppError::Io(e) }
   }
   ```
3. Write `fn read_file(path: &str) -> Result<String, AppError>` that:
   - Uses `std::fs::read_to_string(path)?` (the `?` auto-converts `io::Error` to `AppError`)
   - If the file contains `"error"`, return `Err(AppError::Parse("invalid content"))`
   - Otherwise return `Ok(contents)`
4. Test with a valid file, a missing file, and a file containing "error".

**Expected Output:**
```
read_file("hello.txt") = Ok("hello world")
read_file("missing.txt") = Err(Io(...))
read_file("bad.txt") = Err(Parse("invalid content"))
```

**Verification:** `cargo test` with temporary files.

**Hints:**
- The `?` operator is magic. It calls `From::from` automatically.
- `std::fs::read_to_string` returns `io::Error` on failure. The `?` converts it to `AppError::Io(...)`.

---

#### 🔴 Deep Dive 6: Error Taxonomy Analysis — Provided Snippet

**What you'll build:** Analyze a provided error enum and map variants to failure categories.

**Step-by-step instructions:**
1. You are given this enum in `src/lib.rs` (do NOT modify it):
   ```rust
   #[derive(Debug)]
   enum WalletError {
       InsufficientFunds { needed: u64, available: u64 },
       InvalidAddress(String),
       NetworkTimeout,
       DatabaseCorrupted,
       UserCancelled,
   }
   ```
2. Write a function `fn categorize(err: &WalletError) -> &'static str` that returns:
   - `"user"` for `UserCancelled`
   - `"network"` for `NetworkTimeout`
   - `"data"` for `DatabaseCorrupted` and `InvalidAddress`
   - `"funds"` for `InsufficientFunds`
3. Write `fn count_by_category(errors: &[WalletError]) -> HashMap<&'static str, usize>`.

**Expected Output:**
```
categorize(InsufficientFunds) = "funds"
categorize(InvalidAddress) = "data"
count_by_category([...]) = {"funds": 1, "data": 2, "network": 1, "user": 1}
```

**Verification:** `cargo test` asserts exact category strings and exact counts.

**Hints:**
- Use `match` on the enum variants.
- `HashMap::entry(category).and_modify(|c| *c += 1).or_insert(1);` is a clean way to count.
- This pattern is how real libraries like BDK organize dozens of error variants into user-facing categories.

</details>

---

## Week 3 — Collections, Iterators & Data Structures
**Theme:** The Organization  
**Central Question:** *How do nodes organize and query information efficiently?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 4 (Taming Rust):** "The type system" (p. 127), "Functions and closures" (p. 142), "Iterators" (p. 145)
- **Ch. 4:** "Strings in Rust" (p. 101)
- **Ch. 5 (Implementing a Bitcoin Library):** "Data types" (p. 163) — skim to see how the book models collections

**Articles:**
- [Rust Book: Common Collections](https://doc.rust-lang.org/book/ch08-00-common-collections.html) — Ch. 8
- [Rust Book: Iterators](https://doc.rust-lang.org/book/ch13-02-iterators.html) — Ch. 13.2

**Reference Repos (Hints Only):**
- `bitcoindevkit/bdk` → Look for `HashMap` usage in UTXO indexing or transaction history.
- `cashubtc/cdk` → Look for `Vec` and `HashMap` in the mint/token storage logic.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** When is `BTreeMap` preferable to `HashMap`? What does a distributed system gain from sorted keys?
2. **Q:** Explain the difference between `iter()`, `iter_mut()`, and `into_iter()`. Who owns the data after each?
3. **Q:** What is a closure? Explain the three closure traits (`Fn`, `FnMut`, `FnOnce`) and when each is required.
4. **Q:** Why does `HashMap<&str, T>` require lifetime annotations but `HashMap<String, T>` does not?
5. **Q:** What is iterator chaining? Why is `collection.iter().filter(...).map(...).collect()` considered idiomatic Rust?
6. **Q:** In a distributed system, why might a node use a `VecDeque` (double-ended queue) for a network message buffer instead of a `Vec`?
7. **Q:** What is the difference between `String` and `&str`? Why can't you use `&str` as a HashMap key if it comes from a local variable?
8. **Q:** Explain the concept of "data locality." Why is a `Vec` often faster than a linked list for sequential access, even though inserting in the middle is expensive?
9. **Q:** What does `collect()` do? What type does it return, and how does Rust know which collection to build?
10. **Code:** Look at the following snippet. What will it print, and why?
    ```rust
    fn main() {
        let nums = vec![1, 2, 3, 4, 5];
        let result: Vec<i32> = nums.iter().map(|x| x * 2).filter(|x| x > &4).collect();
        println!("{:?}", result);
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Contact Book | Build a contact book with add, get, remove, and sorted list using `HashMap`. |
| 2 | 🟢 Core | Number Filter & Transform | Filter, map, sort, and dedup using ONLY iterator methods. No `for` loops. |
| 3 | 🟢 Core | Priority Task Queue | Implement a queue where urgent tasks skip to the front. |
| 4 | 🟡 Stretch | High-Value Transaction Filter | Filter `Transaction` structs by fee and sort descending. |
| 5 | 🟡 Stretch | Closure Capture Fix | Fix a borrow checker error by restructuring closure lifetimes. |
| 6 | 🔴 Deep Dive | Collection Design — Provided Snippet | Analyze why a provided `Mempool` uses `HashMap` vs `VecDeque`. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Contact Book (Your First HashMap)

**What you'll build:** A simple contact book using `HashMap` that stores names and phone numbers.

**Step-by-step instructions:**
1. Create a new Cargo project: `cargo new week3_contact_book`
2. Define `struct ContactBook { entries: HashMap<String, String> }` (name → phone)
3. Implement methods:
   - `fn new() -> Self` — creates empty book
   - `fn add(&mut self, name: &str, phone: &str) -> Result<(), &'static str>` — returns `Err("already exists")` if name present
   - `fn get(&self, name: &str) -> Option<&String>`
   - `fn remove(&mut self, name: &str) -> Option<String>`
   - `fn list(&self) -> Vec<(&String, &String)>` — returns all entries sorted by name
4. In `main()`, add 3 contacts, try to add a duplicate, get one, remove one, and list all.

**Expected Output:**
```
Added Alice
Added Bob
Err: already exists
Bob's phone: Some("555-0199")
Removed Alice: Some("555-0100")
Remaining contacts: [("Bob", "555-0199"), ("Charlie", "555-0233")]
```

**Verification:**
- `cargo run` prints the lines above.
- `cargo test` asserts exact behavior for all 5 methods.

**Hints:**
- For `list()`, collect into a `Vec` and call `.sort_by_key(|(k, _)| k.as_str())`.
- `HashMap::insert` returns the old value. You can use this to detect duplicates.

---

#### 🟢 Core 2: Number Filter & Transform (Iterator Chain Only)

**What you'll build:** A function that filters and transforms a list of numbers using ONLY iterator methods — no `for` loops allowed.

**Step-by-step instructions:**
1. Write `fn process_numbers(nums: &[i32]) -> Vec<i32>` that:
   - Keeps only numbers > 0
   - Multiplies each by 2
   - Sorts the result in ascending order
   - Removes duplicates
2. Use ONLY `.iter()`, `.filter()`, `.map()`, `.collect()`, `.sort()`, `.dedup()` (or their iterator equivalents).

**Expected Output:**
```
Input: [-3, 1, 4, -1, 5, 1, 2]
Output: [2, 4, 10]
```

**Verification:**
- `cargo run` prints the output above.
- `cargo test` asserts exact output for 4 test cases (including empty input and all negatives).

**Hints:**
- Chain: `.iter().filter(|&&x| x > 0).map(|x| x * 2).collect::<Vec<_>>()`
- Then sort and dedup. Or use `BTreeSet` for automatic sort+dedup.
- The `&&x` in filter is because `filter` gives you `&&i32` (reference to reference). You can also write `|x| *x > 0`.

---

#### 🟢 Core 3: Priority Task Queue (VecDeque)

**What you'll build:** A task queue where urgent tasks skip to the front.

**Step-by-step instructions:**
1. Define `struct TaskQueue { queue: VecDeque<String> }`
2. Implement:
   - `fn new() -> Self`
   - `fn add_normal(&mut self, task: String)` — pushes to back
   - `fn add_urgent(&mut self, task: String)` — pushes to front
   - `fn next(&mut self) -> Option<String>` — pops from front
   - `fn is_empty(&self) -> bool`
   - `fn len(&self) -> usize`
3. In `main()`, add tasks in this order: normal("A"), urgent("B"), normal("C"), urgent("D"), then process all.

**Expected Output:**
```
Adding: A (normal)
Adding: B (urgent)
Adding: C (normal)
Adding: D (urgent)
Processing: D
Processing: B
Processing: A
Processing: C
Queue empty: true
```

**Verification:**
- `cargo run` prints the lines above.
- `cargo test` asserts exact processing order for 3 scenarios.

**Hints:**
- `VecDeque::push_back` and `VecDeque::push_front` are your friends.
- `VecDeque::pop_front` removes from the front.
- Think of it like a line at a hospital: urgent patients skip to the front.

---

#### 🟡 Stretch 4: High-Value Transaction Filter *(Light Bitcoin Context)*

**What you'll build:** Filter a list of transactions by fee and sort them.

**Step-by-step instructions:**
1. Define `struct Transaction { id: u32, amount: u64, fee: u64 }`
2. Write `fn high_value_txs(txs: &[Transaction], min_fee: u64) -> Vec<&Transaction>` that:
   - Keeps only transactions with `fee >= min_fee`
   - Sorts by `fee` descending, then `id` ascending
3. Test with 5 transactions.

**Expected Output:**
```
Input: 5 txs with fees [100, 50, 200, 75, 150]; min_fee = 80
Output IDs: [3, 5, 1]
```

**Verification:** `cargo test` asserts exact ordering.

**Hints:**
- Use `.filter(|t| t.fee >= min_fee).collect::<Vec<_>>()` then sort.
- In the sort comparator, compare fees first (reverse), then IDs.

---

#### 🟡 Stretch 5: Closure Capture Fix

**What you'll build:** Fix a borrow checker error involving closures.

**Step-by-step instructions:**
1. You are given broken code in `src/main.rs`:
   ```rust
   fn main() {
       let mut data = vec![1, 2, 3];
       let first = || println!("first: {}", data[0]);
       let mut second = || data.push(4);
       first();
       second();
   }
   ```
2. This fails because `first` immutably borrows `data` and `second` mutably borrows `data` — they overlap.
3. Fix it by restructuring so that `first()` completes before `second` is created.

**Expected Output:**
```
first: 1
```

**Verification:** `cargo test` passes; original broken code is in comments.

**Hints:**
- If a closure borrows a value, you can't use that value again until the closure is dropped.
- Call `first()` before defining `second`, or use `drop(first)` before creating `second`.

---

#### 🔴 Deep Dive 6: Collection Design — Provided Snippet Analysis

**What you'll build:** Analyze why a provided snippet chose specific collections and answer via tests.

**Step-by-step instructions:**
1. You are given this code in `src/lib.rs` (do NOT modify it):
   ```rust
   use std::collections::{HashMap, VecDeque};

   struct Mempool {
       by_id: HashMap<u64, Transaction>,
       by_fee: VecDeque<u64>,
   }

   struct Transaction {
       id: u64,
       fee: u64,
   }
   ```
2. Write a function `fn analyze_design() -> [String; 3]` that returns:
   - `[0]`: Why `HashMap` was chosen for `by_id` (one sentence)
   - `[1]`: Why `VecDeque` was chosen for `by_fee` (one sentence)
   - `[2]`: What would go wrong if `by_id` were a `Vec<Transaction>` instead (one sentence)
3. Expected return:
   ```rust
   [
       String::from("HashMap provides O(1) lookup by id"),
       String::from("VecDeque allows efficient push/pop from both ends for fee ordering"),
       String::from("Vec would require O(n) scan to find a transaction by id"),
   ]
   ```

**Expected Output:**
```
Analysis: ["HashMap provides O(1) lookup by id", "VecDeque allows efficient push/pop from both ends for fee ordering", "Vec would require O(n) scan to find a transaction by id"]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- `HashMap` is for key-based lookup. `VecDeque` is for queue-like behavior.
- A `Vec` requires scanning every element to find by ID, which is slow for large mempools.
- This design pattern appears in real node implementations (see reference repos for inspiration).

</details>

---

## Week 4 — Concurrency & System Design Synthesis
**Theme:** The Bridge  
**Central Question:** *How do we parallelize work safely, and what do production architectures look like under the hood?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Prelude:** "Requirements" — "Threads" definition (p. XV)
- **Ch. 7 (Creating a CPU Miner):** "Networking" (p. 277)
- **Ch. 8 (Building a Bitcoin Node):** "Organization" (p. 311)

**Articles:**
- [The Rust Book: Concurrency](https://doc.rust-lang.org/book/ch16-00-concurrency.html) — Ch. 16
- [Rust by Example: Threads](https://doc.rust-lang.org/rust-by-example/std/threads.html)

**Reference Repos (Hints Only):**
- `fedimint/fedimint` → Search for `Arc<Mutex<...>>` or `tokio::sync` usage in server modules.
- `bitcoindevkit/bdk` → Look for thread-safety patterns in the wallet sync logic.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is a data race? How does Rust's ownership system prevent data races at compile time?
2. **Q:** Explain `Arc` and `Mutex`. Why do you need both to share mutable state across threads?
3. **Q:** What is the difference between `std::sync::Mutex` and `tokio::sync::Mutex`? When would you use each?
4. **Q:** Describe the producer-consumer pattern. Why is it often safer than shared state for distributed systems?
5. **Q:** What are the `Send` and `Sync` traits? Why might a raw pointer `*const T` not be `Send`?
6. **Q:** In a distributed system, why might a node use a worker pool to validate transactions instead of spawning one thread per transaction?
7. **Q:** What is lock contention? How does it manifest, and how can you reduce it?
8. **Q:** Why is `Mutex` poisoning a thing in Rust? How do you recover from a poisoned mutex?
9. **Q:** Use AI to analyze `fedimint` or `bdk`: What are the top 3 concurrency patterns used? Summarize in your own words.
10. **Code:** Look at the following snippet. Will it compile? If not, what is the exact error and why?
    ```rust
    fn main() {
        let v = vec![1, 2, 3];
        let handle = std::thread::spawn(|| {
            println!("{:?}", v);
        });
        handle.join().unwrap();
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Parallel Sum | Split a `Vec<i32>` in half and sum each half in a separate thread. |
| 2 | 🟢 Core | Thread-Safe Counter | 10 threads increment a shared counter 100 times each. Assert exact count. |
| 3 | 🟢 Core | Channel-Based Worker Pool | 4 workers process 20 jobs via `mpsc` channels. Collect all results. |
| 4 | 🟡 Stretch | Concurrency Pattern Analysis | Compare shared-state vs message-passing snippets and identify tradeoffs. |
| 5 | 🟡 Stretch | Deadlock Simulation & Fix | Intentionally deadlock two mutexes, then fix by ordering locks. |
| 6 | 🔴 Deep Dive | Mutex Choice Analysis | Analyze `std::sync::Mutex` vs `tokio::sync::Mutex` snippets and explain when to use each. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Parallel Sum (Your First Threads)

**What you'll build:** A program that splits a list of numbers and sums them in parallel threads.

**Step-by-step instructions:**
1. Create a new Cargo project: `cargo new week4_parallel_sum`
2. In `main()`, create a `Vec<i32>` with at least 6 numbers.
3. Split the vector into two halves at the midpoint.
4. Spawn two threads. Each thread sums one half.
5. Wait for both threads to finish using `join()`.
6. Add the two partial sums and print the total.

**Expected Output:**
```
Input: [1, 2, 3, 4, 5, 6]
Left half sum: 6
Right half sum: 15
Total: 21
```

**Verification:**
- `cargo run` prints the lines above.
- `cargo test` asserts correct total for 3 vectors of varying lengths (including odd lengths).

**Hints:**
- Use `let mid = nums.len() / 2;` to find the split point.
- `nums[..mid]` and `nums[mid..]` give you the two halves.
- `std::thread::spawn(move || { ... })` — the `move` is important!
- `join()` returns a `Result`. You can `unwrap()` it here since we're just learning.

---

#### 🟢 Core 2: Thread-Safe Counter (Arc + Mutex)

**What you'll build:** A counter that 10 threads increment safely.

**Step-by-step instructions:**
1. Create a shared counter using `Arc<Mutex<u32>>`.
2. Start with `0`.
3. Spawn 10 threads.
4. Each thread locks the mutex, increments the counter by 1, and releases the lock. Do this 100 times per thread.
5. Wait for all threads to finish.
6. Print the final value.

**Expected Output:**
```
Final count: 1000
```

**Verification:**
- `cargo run` prints `Final count: 1000`.
- `cargo test` asserts the count is exactly 1000 (not 999 or 1001, which would indicate a race condition).

**Hints:**
- `Arc::clone(&counter)` inside the loop that spawns threads. Each thread needs its own `Arc` pointer.
- `let mut num = counter.lock().unwrap();` gives you a mutable reference.
- `*num += 1;` dereferences the mutex guard to get to the `u32` inside.
- The guard is automatically released when `num` goes out of scope.

---

#### 🟢 Core 3: Channel-Based Worker Pool (Producer-Consumer)

**What you'll build:** A simple worker pool where a main thread sends jobs and worker threads process them.

**Step-by-step instructions:**
1. Create a channel for sending jobs: `std::sync::mpsc::channel::<u32>()`
2. Create a channel for receiving results: `std::sync::mpsc::channel::<String>()`
3. Spawn 4 worker threads. Each worker:
   - Receives a job ID from the jobs channel
   - "Processes" it (just format a string like `"Worker {id} processed job {job_id}"`)
   - Sends the result string to the results channel
4. The main thread sends 20 job IDs (1 to 20) into the jobs channel.
5. The main thread drops the sender (so workers know no more jobs are coming).
6. The main thread collects all 20 results and prints them.

**Expected Output:**
```
All 20 jobs completed.
Sample results:
Worker 2 processed job 5
Worker 0 processed job 1
Worker 3 processed job 8
...
```

**Verification:**
- `cargo run` prints "All 20 jobs completed." and 20 result lines.
- `cargo test` asserts result count == 20 and all worker IDs are in range 0..4.

**Hints:**
- Clone the job sender for each worker? No! Workers should share ONE receiver. Actually, `mpsc` means multiple producers, single consumer. So workers share the receiver.
- `let rx = Arc::new(Mutex::new(rx));` — workers need to share the receiver.
- Alternatively, use `crossbeam` or just have one worker per thread. For simplicity, give each worker its own receiver by cloning `Arc<Mutex<Receiver>>`.
- Or simpler: just spawn 4 threads that all compete for jobs from the same receiver using `Arc<Mutex<Receiver>>`.

---

#### 🟡 Stretch 4: Concurrency Pattern Analysis — Provided Snippets

**What you'll build:** Compare two provided code snippets and identify the correct concurrency pattern.

**Step-by-step instructions:**
1. You are given two snippets in `src/lib.rs`:

   **Snippet A — Shared State:**
   ```rust
   use std::sync::{Arc, Mutex};
   struct SharedCounter(Arc<Mutex<u32>>);
   impl SharedCounter {
       fn increment(&self) { *self.0.lock().unwrap() += 1; }
   }
   ```

   **Snippet B — Message Passing:**
   ```rust
   use std::sync::mpsc;
   struct JobQueue(mpsc::Sender<u32>, mpsc::Receiver<u32>);
   impl JobQueue {
       fn send_job(&self, id: u32) { self.0.send(id).unwrap(); }
       fn recv_job(&self) -> Option<u32> { self.1.recv().ok() }
   }
   ```

2. Write `fn compare_snippets() -> [String; 4]` returning:
   - `[0]`: Which snippet is better for high-contention scenarios (many threads hitting the same data) and why?
   - `[1]`: Which snippet is better for loose coupling (workers don't need to know about each other) and why?
   - `[2]`: What is the main risk of Snippet A if a thread panics while holding the lock?
   - `[3]`: What is the main risk of Snippet B if the receiver is dropped while senders still exist?

3. Expected answers:
   ```rust
   [
       String::from("B is better for high contention because channels decouple producers and consumers"),
       String::from("B is better for loose coupling because workers only communicate via messages"),
       String::from("A risks mutex poisoning if a thread panics while holding the lock"),
       String::from("B risks sender errors if the receiver is dropped early"),
   ]
   ```

**Expected Output:**
```
Comparison: ["B is better for high contention...", "B is better for loose coupling...", "A risks mutex poisoning...", "B risks sender errors..."]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- Mutex poisoning: if a thread panics while holding a `std::sync::Mutex`, the lock is "poisoned" and future `lock()` calls return an error.
- Channel send errors: if all receivers are dropped, `send()` returns `Err(SendError)`.
- These patterns appear in real crates like BDK (shared state) and Fedimint (message passing).

---

#### 🟡 Stretch 5: Deadlock Simulation & Fix

**What you'll build:** Intentionally create a deadlock, then fix it.

**Step-by-step instructions:**
1. Create two accounts: `AccountA` and `AccountB`, each with a `Mutex<u64>` balance.
2. Write a function `transfer(a: &Mutex<u64>, b: &Mutex<u64>, amount: u64)` that:
   - Locks `a`
   - Locks `b`
   - Transfers amount from `a` to `b`
3. Spawn two threads:
   - Thread 1: `transfer(&account_a, &account_b, 10)`
   - Thread 2: `transfer(&account_b, &account_a, 10)`
4. Run it. It should deadlock (hang forever).
5. Fix it by always locking in the same order (e.g., by account ID).

**Expected Output:**
```
Before fix: test hangs / timeout after 5 seconds
After fix: Completed successfully. Final balances: A=100, B=100
```

**Verification:**
- `cargo test` passes for the fixed version.
- The broken version is commented out with a note: "WARNING: This deadlocks!"

**Hints:**
- The deadlock happens because Thread 1 holds A and waits for B, while Thread 2 holds B and waits for A.
- The fix: compare the memory addresses of the mutexes and always lock the lower address first.
- Or simpler: assign IDs to accounts and always lock the lower ID first.

---

#### 🔴 Deep Dive 6: Mutex Choice Analysis — Provided Snippets

**What you'll build:** Analyze two provided mutex snippets and determine which to use in which context.

**Step-by-step instructions:**
1. You are given two snippets in `src/lib.rs`:

   **Snippet A — std::sync::Mutex:**
   ```rust
   use std::sync::Mutex;
   struct SyncCache { data: Mutex<Vec<u32>> }
   impl SyncCache {
       fn add(&self, v: u32) { self.data.lock().unwrap().push(v); }
   }
   ```

   **Snippet B — tokio::sync::Mutex:**
   ```rust
   use tokio::sync::Mutex;
   struct AsyncCache { data: Mutex<Vec<u32>> }
   impl AsyncCache {
       async fn add(&self, v: u32) { self.data.lock().await.push(v); }
   }
   ```

2. Write `fn mutex_analysis() -> [String; 3]` returning:
   - `[0]`: Which snippet is faster and why?
   - `[1]`: Which snippet can be held across `.await` and why?
   - `[2]`: In a function that calls `self.data.lock().await` and then awaits a network response, why is Snippet B required?

3. Expected answers:
   ```rust
   [
       String::from("A is faster because std::sync::Mutex uses OS primitives directly without async overhead"),
       String::from("B can be held across await because tokio::sync::Mutex is async-aware and yields instead of blocking"),
       String::from("B is required because holding a std::sync::Mutex across await would block the async executor thread"),
   ]
   ```

**Expected Output:**
```
Analysis: ["A is faster...", "B can be held across await...", "B is required because..."]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- `std::sync::Mutex` blocks the OS thread. In an async runtime, this blocks the executor thread that might be running many tasks.
- `tokio::sync::Mutex` yields to the executor instead of blocking the thread, so other tasks can run.
- This tradeoff appears in real codebases (see reference repos for inspiration).

</details>

---

## Week 5 — Networking & Protocol Design
**Theme:** The Wire  
**Central Question:** *How do independent machines communicate safely and efficiently?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 7 (Creating a CPU Miner):** "Networking" (p. 277), "Miner that can talk to a node - Asynchronous Rust" (p. 282)
- **Ch. 8 (Building a Bitcoin Node):** "Node discovery" (p. 313), "Fetching the blockchain from other nodes" (p. 316), "Handling requests" (p. 322)
- **Ch. 5 (Implementing a Bitcoin Library):** "Serialization into and deserialization out of files" (p. 256)

**Articles:**
- [Rust by Example: TCP Server](https://doc.rust-lang.org/rust-by-example/std/net/tcp.html)
- [Serde Guide](https://serde.rs/)

**Reference Repos (Hints Only):**
- `vincenzopalazzo/lampo.rs` → Study the networking layer and how it frames Lightning messages.
- `lightningdevkit/rust-lightning` → Look at `PeerManager` and message handling.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is length-prefix framing? Why is it better than newline delimiters for binary protocols?
2. **Q:** What is serialization? Why do distributed systems need to agree on a serialization format (e.g., JSON, bincode)?
3. **Q:** Explain the difference between a `TcpListener` and a `TcpStream`. Which side of a client-server relationship uses each?
4. **Q:** What is a protocol state machine? Model a simple 3-way handshake for a hypothetical peer connection.
5. **Q:** Why should network I/O errors be `Result<T, NetworkError>` rather than `panic!`?
6. **Q:** In Bitcoin, why does a node need to broadcast transactions to multiple peers instead of just one?
7. **Q:** What is `serde`? How does a derive macro like `#[derive(Serialize)]` work at a high level?
8. **Q:** What is the difference between `read_exact` and `read` on a `TcpStream`? When might you use each?
9. **Q:** How does a protocol evolve over time without breaking existing nodes? What is backward compatibility?
10. **Code:** Look at the following snippet. A junior dev wrote this to read a 4-byte message length from a TCP stream. What is the bug, and what kind of corruption could it cause in a running system?
    ```rust
    let mut buf = [0u8; 4];
    stream.read(&mut buf)?;
    let length = u32::from_be_bytes(buf);
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | TCP Echo Server | Listen on 127.0.0.1:7878 and echo back lines with `ECHO:` prefix. |
| 2 | 🟢 Core | Simple Message Protocol — Binary Tags | Define `Ping`, `Pong`, `Text` enum with manual encode/decode. |
| 3 | 🟢 Core | Graceful Handshake Server | Accept `Version` messages. Respond `VERACK` or `REJECT`. |
| 4 | 🟡 Stretch | Length-Prefixed JSON Framing | Send 4-byte length + JSON payload. Read exactly length bytes back. |
| 5 | 🟡 Stretch | Protocol Version Negotiation | Client and server negotiate `min(client_version, server_version)`. |
| 6 | 🔴 Deep Dive | Protocol Parser Bug Hunt | Fix a buggy `read_message_length` that uses `read` instead of `read_exact`. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: TCP Echo Server

**What you'll build:** A TCP server that listens for connections and echoes back whatever it receives.

**Step-by-step instructions:**
1. Create a new Cargo project: `cargo new week5_echo_server`
2. In `src/main.rs`:
   - Create a `TcpListener` bound to `127.0.0.1:7878`
   - Loop forever, accepting connections
   - For each connection, read a line from the stream
   - Write back `ECHO: {line}`
   - Print the peer's address when they connect and disconnect
3. Test with: `echo "hello" | nc 127.0.0.1 7878`

**Expected Output:**
```
Server: New connection from 127.0.0.1:54321
Client receives: ECHO: hello
Server: Connection closed
```

**Verification:**
- `cargo run` in one terminal, `echo "hello" | nc 127.0.0.1 7878` in another.
- Integration test spawns server, connects via `TcpStream`, sends "hello", asserts response starts with "ECHO: hello".

**Hints:**
- Use `std::io::BufReader` to read lines from a `TcpStream`.
- `stream.write_all(format!("ECHO: {}", line).as_bytes())` to respond.
- The server will block on `accept()`. That's fine for this assignment.

---

#### 🟢 Core 2: Simple Message Protocol (Binary Tags)

**What you'll build:** A tiny binary protocol with tagged messages.

**Step-by-step instructions:**
1. Define an enum:
   ```rust
   enum WireMessage {
       Ping { nonce: u64 },
       Pong { nonce: u64 },
       Text { content: String },
   }
   ```
2. Implement `fn encode(msg: &WireMessage) -> Vec<u8>`:
   - `Ping` → byte `0` followed by 8 bytes of `nonce` (big-endian)
   - `Pong` → byte `1` followed by 8 bytes of `nonce` (big-endian)
   - `Text` → byte `2`, followed by 4-byte length (big-endian), followed by UTF-8 bytes
3. Implement `fn decode(buf: &[u8]) -> Result<WireMessage, &'static str>` that reverses the process.

**Expected Output:**
```
encode(Ping(42)) = [0, 0, 0, 0, 0, 0, 0, 42]
decode([0, 0, 0, 0, 0, 0, 0, 42]) -> Ok(Ping(42))
decode([99]) -> Err("unknown tag")
```

**Verification:**
- `cargo test` round-trips all 3 variants and tests error cases.

**Hints:**
- Use `nonce.to_be_bytes()` to convert `u64` to `[u8; 8]`.
- For `Text`, `content.len() as u32` gives you the length. Convert with `.to_be_bytes()`.
- For decoding, `u64::from_be_bytes(buf[1..9].try_into().unwrap())` extracts the nonce.

---

#### 🟢 Core 3: Graceful Handshake Server

**What you'll build:** A server that rejects unknown clients with a polite error message.

**Step-by-step instructions:**
1. Define a handshake protocol:
   - Client sends: `VERSION { version: u32, services: u64 }` (as JSON or your binary format)
   - Server responds: `VERACK` if version == 1
   - Server responds: `REJECT { reason: "unsupported version" }` if version != 1, then closes
2. Implement the server using `TcpListener`.
3. Read the first message from each client.
4. Check the version field.
5. Send the appropriate response.

**Expected Output:**
```
Client sends Version(1, 0) -> receives "VERACK"
Client sends Version(2, 0) -> receives "REJECT: unsupported version", then connection closes
```

**Verification:**
- Integration test sends both versions and asserts responses.

**Hints:**
- Start with JSON over TCP for simplicity. Binary framing comes in Stretch.
- Use `serde_json` to serialize/deserialize the Version struct.
- The server should close the stream after sending REJECT.

---

#### 🟡 Stretch 4: Length-Prefixed JSON Framing

**What you'll build:** A protocol that sends 4-byte length + JSON payload.

**Step-by-step instructions:**
1. Implement `fn send_framed(stream: &mut TcpStream, msg: &WireMessage)`:
   - Serialize `msg` to JSON bytes using `serde_json::to_vec`
   - Send 4-byte big-endian length prefix
   - Send the JSON bytes
2. Implement `fn recv_framed(stream: &mut TcpStream) -> Result<WireMessage, &'static str>`:
   - Read exactly 4 bytes for length
   - Read exactly `length` bytes for payload
   - Deserialize JSON to `WireMessage`

**Expected Output:**
```
Sent 27 bytes
Received: Ping { nonce: 42 }
```

**Verification:** Round-trip test over a `TcpStream`.

**Hints:**
- `read_exact` is critical here. `read` might return fewer bytes than requested.
- `u32::from_be_bytes` converts the 4-byte prefix to a length.

---

#### 🟡 Stretch 5: Protocol Version Negotiation

**What you'll build:** A client and server that negotiate the highest common version.

**Step-by-step instructions:**
1. Client sends its maximum supported version.
2. Server responds with `min(client_version, server_version)`.
3. If the negotiated version is < 1, the server rejects.
4. Implement both client and server logic.

**Expected Output:**
```
Client(3) + Server(2) -> negotiated version = 2
Client(0) + Server(2) -> Reject
```

**Verification:** `cargo test` with mock streams.

**Hints:**
- This is how real P2P protocols work (Bitcoin's `version`/`verack` handshake).
- The server should store its own version as a constant.

---

#### 🔴 Deep Dive 6: Protocol Parser Bug Hunt — Provided Snippet

**What you'll build:** Find and fix a bug in a provided network parser, verified by tests.

**Step-by-step instructions:**
1. You are given this buggy parser in `src/lib.rs`:
   ```rust
   use std::io::{Read, Result};

   fn read_message_length(stream: &mut dyn Read) -> Result<u32> {
       let mut buf = [0u8; 4];
       stream.read(&mut buf)?;
       Ok(u32::from_be_bytes(buf))
   }
   ```
2. The bug: `read()` may return fewer than 4 bytes. The remaining bytes are uninitialized (still 0), causing the length to be wrong. This leads to reading too few or too many bytes for the payload, corrupting the stream.
3. Write `fn read_message_length_fixed(stream: &mut dyn Read) -> Result<u32>` that uses `read_exact` instead.
4. Write a test that simulates a slow stream (one that returns 1 byte at a time) and proves the original fails while the fixed version succeeds.

**Expected Output:**
```
Original parser with slow stream: returns 0 (wrong!)
Fixed parser with slow stream: returns 42 (correct!)
```

**Verification:** `cargo test` asserts the original returns 0 and the fixed returns 42 for a slow stream.

**Hints:**
- `read_exact` loops until the buffer is full or an error occurs.
- To simulate a slow stream, implement a custom `Read` that returns 1 byte per call.
- This exact bug class appears in real networking code (see reference repos for inspiration).

</details>

---

## Week 6 — Async Rust & High-Concurrency Services
**Theme:** The Event Loop  
**Central Question:** *How do nodes handle thousands of simultaneous events without blocking?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 7 (Creating a CPU Miner):** "Asynchronous Rust" (p. 282), "Futures and promises" (p. 283), "Tokio in miner" (p. 287)
- **Ch. 8 (Building a Bitcoin Node):** "Handling requests" (p. 322)

**Articles:**
- [Tokio Tutorial](https://tokio.rs/tokio/tutorial) — Chapters 1–3
- [Async/Await in Rust](https://rust-lang.github.io/async-book/01_getting_started/01_chapter.html)

**Reference Repos (Hints Only):**
- `lightningdevkit/rust-lightning` → Study the `BackgroundProcessor` and async runtime integration.
- `vincenzopalazzo/lampo.rs` → Look at how async tasks manage peer connections.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is the difference between an OS thread and a Tokio task? When is a task more efficient?
2. **Q:** Explain `await`. What happens to the function's state while it is waiting?
3. **Q:** What is a future? Is it executed immediately when created, or does something else need to happen?
4. **Q:** What is backpressure? How does a bounded `tokio::sync::mpsc::channel(n)` help prevent memory exhaustion?
5. **Q:** What is `tokio::select!`? Give an example of when a Bitcoin node might use it.
6. **Q:** Why is holding a `std::sync::Mutex` across an `.await` point problematic? What is the alternative?
7. **Q:** What is cancellation safety? Why might a partially sent network message be dangerous if a task is cancelled?
8. **Q:** In a distributed system, why is non-blocking I/O essential for handling thousands of peer connections?
9. **Q:** How does `rust-lightning` run background tasks? What role does the `BackgroundProcessor` play?
10. **Code:** Look at the following async function. A junior dev says "this looks fine to me." What is the problem, and what symptom would you see in production?
    ```rust
    async fn load_config(path: &str) -> String {
        std::fs::read_to_string(path).unwrap()
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Async Echo Server (Tokio) | Convert the TCP echo server to Tokio with one task per client. |
| 2 | 🟢 Core | Async Timer Race | Race two `sleep` futures with `tokio::select!`. Assert fast timer always wins. |
| 3 | 🟢 Core | Async Broadcast Router | Use `tokio::sync::broadcast` to send 5 messages to 3 subscribers. |
| 4 | 🟡 Stretch | Connection Manager with Backpressure | Drop messages to slow peers using `try_send()` on bounded channels. |
| 5 | 🟡 Stretch | Timeout & Retry with Exponential Backoff | Retry TCP connection 3 times with `timeout` and increasing delays. |
| 6 | 🔴 Deep Dive | Async Flow Analysis — Provided Snippet | Identify the blocking-syscall bug in a provided async peer handler. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Async Echo Server (Tokio)

**What you'll build:** Convert Week 5's echo server to async using Tokio.

**Step-by-step instructions:**
1. Add `tokio = { version = "1", features = ["full"] }` to `Cargo.toml`.
2. Mark `main` as `#[tokio::main]`.
3. Use `tokio::net::TcpListener` instead of `std::net::TcpListener`.
4. For each incoming connection, spawn a Tokio task to handle it.
5. The task reads a line and writes back `ECHO: {line}`.

**Expected Output:**
```
$ echo "async" | nc 127.0.0.1 7878
ECHO: async
```

**Verification:**
- Integration test spawns 3 concurrent clients, all receive correct echo.
- `cargo test` asserts all 3 clients get their messages back.

**Hints:**
- `tokio::io::AsyncBufReadExt` provides `read_line()`.
- `tokio::io::AsyncWriteExt` provides `write_all()`.
- `tokio::spawn(async move { ... })` creates a new task.

---

#### 🟢 Core 2: Async Timer Race

**What you'll build:** A race between two timers using `tokio::select!`.

**Step-by-step instructions:**
1. Create two `tokio::time::sleep` futures: one for 100ms, one for 200ms.
2. Use `tokio::select!` to race them.
3. Print which timer won.
4. Run the race 5 times in a loop and assert the fast timer always wins.

**Expected Output:**
```
Race 1: Fast timer won!
Race 2: Fast timer won!
...
Race 5: Fast timer won!
```

**Verification:**
- `cargo test` asserts all 5 races print "Fast timer won!" and total elapsed < 150ms per race.

**Hints:**
- `tokio::select!` picks whichever branch completes first.
- The other branch is cancelled.
- This is how nodes handle timeouts: "wait for a message OR wait 30 seconds, whichever comes first."

---

#### 🟢 Core 3: Async Broadcast Router

**What you'll build:** A broadcast channel where one sender reaches multiple receivers.

**Step-by-step instructions:**
1. Create a `tokio::sync::broadcast::channel::<String>(16)`.
2. Spawn 3 subscriber tasks. Each task:
   - Subscribes to the channel
   - Receives 5 messages
   - Prints each message with its subscriber ID
3. The main task sends 5 messages: "msg1", "msg2", ..., "msg5".
4. Wait for all subscribers to finish.

**Expected Output:**
```
Subscriber 0 received: msg1
Subscriber 1 received: msg1
Subscriber 2 received: msg1
...
Subscriber 0 received: msg5
Subscriber 1 received: msg5
Subscriber 2 received: msg5
```

**Verification:**
- `cargo test` asserts each subscriber received exactly 5 messages.
- Total messages received across all subscribers = 15.

**Hints:**
- `let mut rx = tx.subscribe();` creates a new subscriber.
- `rx.recv().await` waits for the next message.
- If a subscriber is slow and the channel fills up, messages are dropped. That's backpressure in action!

---

#### 🟡 Stretch 4: Connection Manager with Backpressure

**What you'll build:** A manager that drops messages to slow peers instead of crashing.

**Step-by-step instructions:**
1. Maintain a `HashMap<u32, tokio::sync::mpsc::Sender<String>>`.
2. Each peer gets a bounded channel of capacity 4.
3. When sending a message, use `try_send()`. If the channel is full, print `backpressure: peer {id}` and drop the message.
4. Simulate one slow peer (a task that sleeps 1 second between receives) and one fast peer.
5. Send 10 messages to each.

**Expected Output:**
```
Peer 1 (fast): received all 10 messages
Peer 2 (slow): received 4 messages, then backpressure dropped 6
```

**Verification:** `cargo test` asserts backpressure was triggered for the slow peer.

**Hints:**
- `try_send()` returns `Err(TrySendError::Full)` if the channel is full.
- This is how real systems prevent memory exhaustion under load.

---

#### 🟡 Stretch 5: Timeout & Retry with Exponential Backoff

**What you'll build:** An async connection function that retries with increasing delays.

**Step-by-step instructions:**
1. Write `async fn connect_with_retry(addr: &str) -> Result<TcpStream, &'static str>`.
2. Try to connect up to 3 times.
3. Wait 100ms after attempt 1, 200ms after attempt 2.
4. Use `tokio::time::timeout(Duration::from_millis(50), TcpStream::connect(addr))` for each attempt.
5. If all attempts fail, return `Err("connection failed after 3 attempts")`.

**Expected Output:**
```
connect_with_retry("127.0.0.1:9999") -> Err("connection failed after 3 attempts")
Total elapsed: ~300ms
```

**Verification:**
- `cargo test` with a closed port asserts error and approximate timing (250–350ms).

**Hints:**
- `tokio::time::sleep(Duration::from_millis(delay)).await;` between attempts.
- `timeout` returns `Result<Result<TcpStream, _>, Elapsed>`. Handle both error cases.

---

#### 🔴 Deep Dive 6: Async Flow Analysis — Provided Snippet

**What you'll build:** Analyze a provided async snippet and identify the executor-blocking bug.

**Step-by-step instructions:**
1. You are given this snippet in `src/lib.rs`:
   ```rust
   use tokio::time::{sleep, Duration};

   async fn handle_peer(stream: tokio::net::TcpStream) {
       let config = std::fs::read_to_string("config.txt").unwrap();
       println!("Config loaded: {}", config.len());
       sleep(Duration::from_millis(100)).await;
   }

   async fn handle_peers(mut incoming: tokio::net::TcpListener) {
       while let Ok((stream, _)) = incoming.accept().await {
           tokio::spawn(handle_peer(stream));
       }
   }
   ```
2. Write `fn identify_bug() -> String` that returns a single sentence identifying the bug.
3. Write `fn explain_symptom() -> String` that returns a single sentence describing the production symptom.
4. Expected answers:
   ```rust
   String::from("std::fs::read_to_string blocks the OS thread, freezing the async executor")
   String::from("Under load, all peer connections would stall because the executor thread is blocked")
   ```

**Expected Output:**
```
Bug: std::fs::read_to_string blocks the OS thread, freezing the async executor
Symptom: Under load, all peer connections would stall because the executor thread is blocked
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- `std::fs::read_to_string` is a blocking syscall. In an async runtime, it blocks the executor thread that might be running hundreds of other tasks.
- The fix is `tokio::fs::read_to_string(path).await`.
- This exact bug class appears in real async codebases (see reference repos for inspiration).

</details>

---

## Week 7 — Advanced Rust for Infrastructure
**Theme:** The Forge  
**Central Question:** *How is production-grade infrastructure software actually architected?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 4 (Taming Rust):** "Lifetimes of owned vs unowned values" (p. 104), "Generic param bounds" (p. 120), "Dynamic dispatch" (p. 121)
- **Ch. 5 (Keeping Rust Cultured):** "Rustfmt" (p. 150), "Clippy" (p. 154)
- **Ch. 5 (Implementing a Bitcoin Library):** "Splitting up the big file" (p. 251), "Utility binaries" (p. 261)

**Articles:**
- [Rust Book: Advanced Traits](https://doc.rust-lang.org/book/ch19-03-advanced-traits.html) — Ch. 19.3
- [Rust Book: Smart Pointers](https://doc.rust-lang.org/book/ch15-00-smart-pointers.html) — Ch. 15

**Reference Repos (Hints Only):**
- `Bitshala-Incubator/silent-pay-wallet` — Examine workspace structure and crate boundaries.
- `fedimint/fedimint` — Study how a large Rust project is organized into crates.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is a trait object (`dyn Trait`)? When is it preferable to generics, and what is the performance tradeoff?
2. **Q:** Explain static dispatch vs. dynamic dispatch. Which produces faster code? Which produces smaller binaries?
3. **Q:** What is interior mutability? How does `RefCell` provide it for single-threaded code, and how does `Mutex` provide it for multi-threaded code?
4. **Q:** What is `Cow<'a, str>`? In what scenario is it useful for a protocol parser that might need to return borrowed or owned data?
5. **Q:** What is a Cargo workspace? Why might a Bitcoin project split into `node-core`, `node-network`, and `node-storage` crates?
6. **Q:** Explain exponential backoff with jitter. Why is jitter critical in distributed systems retry logic?
7. **Q:** What are the `Send` and `Sync` traits? Why is `Rc<T>` not `Send`, and why is `RefCell<T>` not `Sync`?
8. **Q:** What is object safety? Why can't a trait with generic methods be made into a `dyn Trait`?
9. **Q:** How does `thiserror` reduce boilerplate compared to manually implementing `std::fmt::Display` and `std::error::Error`?
10. **Code:** Look at the following snippet. A junior dev wants to store different message handlers in a single `Vec`. What is the simplest way to make this work, and what is the runtime tradeoff compared to the generic version?
    ```rust
    trait Handler { fn handle(&self, msg: &str); }
    struct EchoHandler;
    struct UpperHandler;
    // impl Handler for both...

    fn main() {
        let handlers: Vec<Box<dyn Handler>> = vec![
            Box::new(EchoHandler),
            Box::new(UpperHandler),
        ];
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Workspace Refactor | Split Weeks 1–6 code into a Cargo workspace with `core`, `network`, and `app` crates. |
| 2 | 🟢 Core | Retry with Exponential Backoff + Jitter | A sync retry function with doubling delays and random 0–50ms jitter. |
| 3 | 🟢 Core | Dynamic Message Handler Router | A `HashMap<String, Box<dyn MessageHandler>>` that routes by prefix. |
| 4 | 🟡 Stretch | Smart Pointer Audit | Refactor `ContactBook` to `Arc<Mutex<HashMap>>` and document why. |
| 5 | 🟡 Stretch | Error Refactor with thiserror | Convert manual errors to a `thiserror` enum with `#[from]`. Run clippy. |
| 6 | 🔴 Deep Dive | Workspace Design Analysis — Provided Structure | Analyze a provided workspace layout and justify design decisions. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Workspace Refactor

**What you'll build:** Split your previous weeks' code into a proper Cargo workspace.

**Step-by-step instructions:**
1. Create a new directory `week7_workspace`.
2. Inside it, create `Cargo.toml` with:
   ```toml
   [workspace]
   members = ["core", "network", "app"]
   ```
3. Create three crates:
   - `core/` — Move your structs, enums, and traits from Weeks 1–3 here.
   - `network/` — Move your TCP server, protocol, and async code from Weeks 5–6 here.
   - `app/` — A binary crate that imports from `core` and `network` and has a `main()`.
4. Add dependencies in each crate's `Cargo.toml`.
5. Make sure `cargo build` works from the workspace root.
6. Make sure `cargo test --workspace` runs all tests.

**Expected Output:**
```
$ cargo build
   Compiling core v0.1.0
   Compiling network v0.1.0
   Compiling app v0.1.0
    Finished dev target
$ cargo test --workspace
   Running 25 tests
   test result: ok
```

**Verification:**
- CI runs `cargo build` and `cargo test --workspace` successfully.

**Hints:**
- In `app/Cargo.toml`, add `core = { path = "../core" }` and `network = { path = "../network" }`.
- Use `pub` on everything you want to share between crates.
- Workspaces are how real projects like BDK and LDK organize 10+ crates.

---

#### 🟢 Core 2: Retry with Exponential Backoff + Jitter

**What you'll build:** A retry function that waits longer between each attempt and adds randomness.

**Step-by-step instructions:**
1. Write `fn retry<F, T>(mut f: F, max_attempts: u32) -> Result<T, &'static str>` where `F: FnMut() -> Option<T>`.
2. Attempt 1: if `f()` returns `Some`, return `Ok` immediately.
3. Attempt 2: wait `100ms`, try again.
4. Attempt 3: wait `200ms`, try again.
5. Attempt 4+: wait `400ms`, `800ms`, etc. (double each time).
6. Before each wait, add a random jitter of 0–50ms using `rand::random_range(0..50)`.
7. If all attempts fail, return `Err("max retries exceeded")`.

**Expected Output:**
```
Function fails 2 times, succeeds on 3rd.
Total elapsed: ~300-450ms (base 300ms + jitter)
Result: Ok("success")
```

**Verification:**
- `cargo test` with a mock failing function asserts success and approximate timing (300–500ms).

**Hints:**
- `std::thread::sleep` is fine for this sync version. (The async version was Week 6.)
- Jitter prevents "thundering herd" — when many clients retry at exactly the same time.
- `2_u64.pow(attempt)` gives you the exponential factor.

---

#### 🟢 Core 3: Dynamic Message Handler Router

**What you'll build:** A router that can handle different message types using trait objects.

**Step-by-step instructions:**
1. Define a trait:
   ```rust
   trait MessageHandler: Send + Sync {
       fn handle(&self, msg: &str) -> String;
   }
   ```
2. Create three handlers:
   - `EchoHandler` — returns the message unchanged
   - `UppercaseHandler` — returns the message in ALL CAPS
   - `ReverseHandler` — returns the message reversed
3. Create a router:
   ```rust
   struct Router {
       handlers: HashMap<String, Box<dyn MessageHandler>>
   }
   ```
4. Implement `fn route(&self, msg: &str) -> String`:
   - Split `msg` on `:` to get prefix and content
   - Look up the prefix in `handlers`
   - If found, call `handle(content)`
   - If not found, return `"No handler"`
5. Register all three handlers and test.

**Expected Output:**
```
Route("echo:hello") -> "hello"
Route("upper:hello") -> "HELLO"
Route("rev:hello") -> "olleh"
Route("unknown:hello") -> "No handler"
```

**Verification:**
- `cargo test` with 6 routing cases (including empty messages).

**Hints:**
- `Box<dyn MessageHandler>` is a trait object. It uses dynamic dispatch (vtable lookup at runtime).
- This is slower than generics but allows you to mix different handler types in one collection.
- `Send + Sync` bounds are required because the router might be shared across threads.

---

#### 🟡 Stretch 4: Smart Pointer Audit

**What you'll build:** Choose the right smart pointer for a shared data structure.

**Step-by-step instructions:**
1. Take your Week 3 `ContactBook`.
2. You now need to share it between multiple threads that read and write.
3. Refactor it to use `Arc<Mutex<HashMap<...>>>` instead of `HashMap` directly.
4. Add a comment block explaining:
   - Why `Arc` is needed (shared ownership across threads)
   - Why `Mutex` is needed (mutable access from multiple threads)
   - What would go wrong if you used `Rc` instead of `Arc`
   - What would go wrong if you used `RefCell` instead of `Mutex`

**Expected Output:**
```
// Smart Pointer Choice Explanation:
// - Arc: Allows multiple threads to own the HashMap. Rc is not Send, so it can't cross threads.
// - Mutex: Provides interior mutability. RefCell is not Sync, so it can't be shared across threads.
// - Without Arc: Only one thread could own the data.
// - Without Mutex: We'd have a data race.
```

**Verification:** `cargo test` passes with the refactored code.

**Hints:**
- `Arc::clone(&map)` gives each thread its own pointer to the same data.
- `map.lock().unwrap().insert(...)` locks, modifies, and auto-unlocks.

---

#### 🟡 Stretch 5: Error Refactor with `thiserror`

**What you'll build:** Convert manual error types to a clean `thiserror` enum.

**Step-by-step instructions:**
1. Add `thiserror = "1"` to `Cargo.toml`.
2. Define:
   ```rust
   #[derive(thiserror::Error, Debug)]
   enum AppError {
       #[error("IO error: {0}")]
       Io(#[from] std::io::Error),
       #[error("Parse error: {0}")]
       Parse(#[from] std::num::ParseIntError),
       #[error("Invalid config: {message}")]
       InvalidConfig { message: String },
       #[error("Unknown command: {0}")]
       UnknownCommand(String),
   }
   ```
3. Refactor one of your Week 2–5 functions to return `Result<T, AppError>` instead of `Result<T, &'static str>`.
4. Run `cargo clippy` and ensure zero warnings.

**Expected Output:**
```
$ cargo test
All tests pass with new error types
$ cargo clippy
    Finished dev target (no warnings)
```

**Verification:** `cargo test` passes; `cargo clippy` shows no warnings.

**Hints:**
- `#[from]` auto-generates `From` implementations. The `?` operator now works seamlessly.
- `#[error("...")]` generates the `Display` implementation for you.
- This saves ~20 lines of boilerplate per error variant.

---

#### 🔴 Deep Dive 6: Workspace Design Analysis — Provided Structure

**What you'll build:** Analyze a provided workspace structure and justify design decisions.

**Step-by-step instructions:**
1. You are given this workspace layout in `workspace-analysis.md`:
   ```
   my-node/
   ├── Cargo.toml          (workspace root)
   ├── core/
   │   ├── Cargo.toml
   │   └── src/lib.rs      (types, traits, state machines)
   ├── network/
   │   ├── Cargo.toml
   │   └── src/lib.rs      (TCP, protocol framing, peer management)
   ├── storage/
   │   ├── Cargo.toml
   │   └── src/lib.rs      (disk persistence, caching)
   └── app/
       ├── Cargo.toml
       └── src/main.rs     (binary, ties everything together)
   ```
2. Write `fn analyze_workspace() -> [String; 3]` returning:
   - `[0]`: Why `core` is a separate crate (one sentence)
   - `[1]`: Why `network` depends on `core` but not `storage` (one sentence)
   - `[2]`: What would go wrong if everything were in a single `src/main.rs` (one sentence)
3. Expected answers:
   ```rust
   [
       String::from("core is separate so multiple crates can share types without circular dependencies"),
       String::from("network needs core types but storage is an independent concern that only the app needs"),
       String::from("A single file would create tight coupling, slow compilation, and make testing impossible"),
   ]
   ```

**Expected Output:**
```
Analysis: ["core is separate...", "network needs core types...", "A single file would create tight coupling..."]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- Workspaces enforce module boundaries. You can't accidentally import from `storage` in `network` unless you declare the dependency.
- Separate crates compile in parallel, speeding up builds.
- This is how BDK (library) and Fedimint (application) organize their code (see reference repos for inspiration).

</details>

---

## Week 8 — P2P Systems & Distributed Algorithms
**Theme:** The Swarm  
**Central Question:** *How do thousands of independent nodes become a coherent network?*

### 📚 Reading Materials

**From *Building Bitcoin in Rust* (Primary):**
- **Ch. 8 (Building a Bitcoin Node):** "Node discovery" (p. 313), "Fetching the blockchain from other nodes" (p. 316), "Handling requests" (p. 322), "Wrapping up" (p. 334)
- **Ch. 2 (Analyzing the Whitepaper):** "Network" (p. 31), "Incentive" (p. 33), "Simplified Payment Verification" (p. 35), "Privacy" (p. 37), "Calculations" (p. 37)
- **Ch. 7 (Creating a CPU Miner):** "Networking" (p. 277)

**Articles:**
- [Gossip Protocols](https://en.wikipedia.org/wiki/Gossip_protocol)
- [Kademlia DHT](https://en.wikipedia.org/wiki/Kademlia)
- [CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem)

**Reference Repos (Hints Only):**
- `lightningdevkit/rust-lightning` → Study the gossip module for channel announcements.
- `fedimint/fedimint` → Study consensus and distributed state modules.

### 🎙️ 10 Questions (Primarily QnA)

1. **Q:** What is an epidemic (gossip) protocol? Why is it efficient for broadcasting information in a large network?
2. **Q:** Explain the CAP theorem. Where does Bitcoin sit on the CAP triangle, and why?
3. **Q:** What is consistent hashing? Why do distributed databases like DynamoDB use it for partitioning data?
4. **Q:** In Kademlia, what is a k-bucket? Why is XOR distance used instead of Euclidean distance?
5. **Q:** Compare Raft and Nakamoto consensus. What problem does each solve, and what are their tradeoffs?
6. **Q:** How does a Bitcoin node discover peers without a central server? Describe the bootstrapping process.
7. **Q:** What is a heartbeat protocol? How do you balance detecting dead nodes quickly vs. avoiding false positives?
8. **Q:** What is anti-entropy in gossip protocols? Why is it necessary even with push-based gossip?
9. **Q:** In a distributed system, what is a quorum? Why might a system require a majority quorum for configuration changes?
10. **Code:** Look at the following function that calculates XOR distance between two node IDs. A junior dev asks: "Why XOR? Why not just subtract the numbers?" What is the key mathematical property of XOR that makes it perfect for Kademlia's routing table?
    ```rust
    fn xor_distance(a: &[u8; 20], b: &[u8; 20]) -> [u8; 20] {
        let mut result = [0u8; 20];
        for i in 0..20 { result[i] = a[i] ^ b[i]; }
        result
    }
    ```

### 📝 Assignments

| # | Tier | Title | One-Line Summary |
|---|------|-------|------------------|
| 1 | 🟢 Core | Gossip Simulator | Simulate 10 nodes spreading a message. Count rounds and total messages sent. |
| 2 | 🟢 Core | Consistent Hash Ring | Distribute 100 keys across 3 nodes. Add a 4th node. Assert < 25% keys moved. |
| 3 | 🟢 Core | Kademlia XOR Lookup | Calculate XOR distance. Find 2 closest peers to a target from 5 candidates. |
| 4 | 🟡 Stretch | Failure Detection Service | Heartbeat system marking nodes as Suspect then Dead based on elapsed time. |
| 5 | 🟡 Stretch | Consensus Comparison — Structured Q&A | Answer 5 structured questions about Raft vs. Nakamoto. |
| 6 | 🔴 Deep Dive | Gossip Flow Analysis — Provided Snippet | Analyze a provided `GossipStore` and identify data flow and design tradeoffs. |

<details>
<summary><h3><b>📖 Expand All Assignment Details</b></h3></summary>

---

#### 🟢 Core 1: Gossip Simulator

**What you'll build:** A simulation of how a message spreads through a network of 10 nodes.

**Step-by-step instructions:**
1. Define `struct Node { id: u32, has_message: bool }`.
2. Create a `Vec<Node>` of 10 nodes. Node 0 starts with `has_message = true`.
3. Run rounds until all nodes have the message:
   - In each round, every node that has the message picks 2 random neighbors and "infects" them.
   - Count how many total messages were sent.
4. Print the state after each round.

**Expected Output:**
```
Round 0: 1 nodes have the message
Round 1: 3 nodes have the message
Round 2: 6 nodes have the message
Round 3: 10 nodes have the message
Total messages sent: ~18
```

**Verification:**
- `cargo test` asserts all 10 nodes have the message within 10 rounds.
- Total messages sent is logged and should be < 30.

**Hints:**
- Use `rand::random_range(0..10)` to pick random neighbors.
- A node can "infect" a node that already has the message. That's fine — it's still a message sent.
- This is how Bitcoin transactions spread: each node tells a few peers.

---

#### 🟢 Core 2: Consistent Hash Ring

**What you'll build:** A hash ring that distributes keys across servers and minimizes reshuffling when servers are added.

**Step-by-step instructions:**
1. Define `struct HashRing { nodes: BTreeMap<u64, String> }` (hash → node name).
2. For each physical node, add 3 "virtual nodes" by hashing `format!("{name}#{i}")` for `i` in 0..3.
3. Implement `fn add_node(&mut self, name: &str)`.
4. Implement `fn get_node(&self, key: &str) -> Option<&String>`:
   - Hash the key
   - Find the first virtual node with hash >= key_hash (clockwise)
   - If none, wrap around to the first virtual node
5. Test with 100 keys (`"key0"` to `"key99"`) and 3 nodes ("A", "B", "C").
6. Add node "D" and count how many keys moved.

**Expected Output:**
```
Before: A=34, B=33, C=33
After adding D: A=26, B=25, C=25, D=24
Keys moved: 23/100
```

**Verification:**
- `cargo test` asserts key migration count < 30.
- Without consistent hashing, adding a node would move ~33% of keys. With it, only ~25% move.

**Hints:**
- Use `std::collections::hash_map::DefaultHasher` to hash strings.
- `BTreeMap::range(..=hash).next()` finds the first node >= hash.
- Virtual nodes smooth out the distribution. Without them, one node might get unlucky and own almost all keys.

---

#### 🟢 Core 3: Kademlia XOR Lookup

**What you'll build:** A simplified Kademlia routing table that finds the closest peers.

**Step-by-step instructions:**
1. Implement `fn xor_distance(a: &[u8; 20], b: &[u8; 20]) -> [u8; 20]`:
   - For each byte index `i`, `result[i] = a[i] ^ b[i]`
2. Create 5 peers with IDs:
   - `[0x01; 20]` (all bytes are 0x01)
   - `[0x02; 20]`
   - `[0x04; 20]`
   - `[0x08; 20]`
   - `[0x10; 20]`
3. Given a target `[0x03; 20]`, find the 2 closest peers using XOR distance.
4. Print the closest peers and their distances.

**Expected Output:**
```
Target: 03 03 03 ...
Closest: [0x02; 20] (distance: 01 01 01 ...)
         [0x01; 20] (distance: 02 02 02 ...)
```

**Verification:**
- `cargo test` asserts exact peer IDs returned in correct order.

**Hints:**
- XOR distance has a magical property: `distance(a, b) == distance(b, a)`.
- XOR treats each bit independently. The most significant differing bit determines which is "farther."
- This is why Kademlia uses XOR: it creates a metric space where nodes naturally cluster by similarity.

---

#### 🟡 Stretch 4: Failure Detection Service

**What you'll build:** A heartbeat system that marks slow nodes as suspect, then dead.

**Step-by-step instructions:**
1. Define `enum NodeState { Alive, Suspect, Dead }`.
2. Define `struct FailureDetector { nodes: HashMap<u32, (NodeState, Instant)> }`.
3. Implement:
   - `fn heartbeat(&mut self, id: u32)` — marks node as Alive and records time
   - `fn check(&mut self, id: u32)` — checks time since last heartbeat:
     - If > 300ms and < 500ms: mark Suspect
     - If >= 500ms: mark Dead
     - If < 300ms: mark Alive
4. Simulate: Node 3 stops heartbeating. Check at 0ms, 300ms, 500ms, 600ms.

**Expected Output:**
```
Node 3 at 0ms: Alive
Node 3 at 300ms: Suspect
Node 3 at 500ms: Dead
Node 3 at 600ms: Dead
```

**Verification:** `cargo test` with simulated time asserts correct state transitions.

**Hints:**
- Use `std::time::Instant` and `elapsed()` to measure time.
- In tests, you can mock time by storing a `Duration` instead of `Instant`.
- The "Suspect" state gives nodes a grace period before being declared dead.

---

#### 🟡 Stretch 5: Consensus Comparison — Structured Q&A

**What you'll build:** Answer structured questions about Raft vs. Nakamoto, verified by exact string matching.

**Step-by-step instructions:**
1. Write `fn consensus_qa() -> [String; 5]` that returns:
   - `[0]`: Which consensus is for trusted networks and which is for untrusted networks?
   - `[1]`: Which one is faster for finality (committing a decision)?
   - `[2]`: Which one requires knowing all participants ahead of time?
   - `[3]`: What is the main resource Nakamoto uses to secure the network?
   - `[4]`: What is the main failure mode Raft protects against?
2. Expected answers:
   ```rust
   [
       String::from("Raft is for trusted networks, Nakamoto is for untrusted networks"),
       String::from("Raft is faster for finality because it commits immediately with quorum"),
       String::from("Raft requires known participants, Nakamoto is permissionless"),
       String::from("Nakamoto uses proof-of-work (computational energy) to secure the network"),
       String::from("Raft protects against crash faults (nodes going offline)"),
   ]
   ```

**Expected Output:**
```
Q&A: ["Raft is for trusted networks...", "Raft is faster for finality...", "Raft requires known participants...", "Nakamoto uses proof-of-work...", "Raft protects against crash faults..."]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- Raft = leader-based, fast, needs known nodes, handles crash faults.
- Nakamoto = PoW-based, slow, permissionless, handles Byzantine faults.
- Use AI to research if unsure, but formulate answers in your own words.

---

#### 🔴 Deep Dive 6: Gossip Flow Analysis — Provided Snippet

**What you'll build:** Analyze a provided gossip module and identify the data flow.

**Step-by-step instructions:**
1. You are given this snippet in `src/lib.rs`:
   ```rust
   struct GossipStore {
       channels: HashMap<u64, ChannelInfo>,
       updates: Vec<u64>,
   }

   struct ChannelInfo {
       node_a: String,
       node_b: String,
       capacity: u64,
   }

   impl GossipStore {
       fn add_channel(&mut self, id: u64, info: ChannelInfo) {
           self.channels.insert(id, info);
           self.updates.push(id);
       }

       fn get_recent(&self, n: usize) -> Vec<&ChannelInfo> {
           self.updates.iter().rev().take(n)
               .filter_map(|id| self.channels.get(id))
               .collect()
       }

       fn forward_to_peers(&self, id: u64) {
           // Simulated: would send to all connected peers
           println!("Forwarding channel {} to peers", id);
       }
   }
   ```
2. Write `fn analyze_gossip_flow() -> [String; 4]` returning:
   - `[0]`: What data structure stores the canonical channel info?
   - `[1]`: What data structure tracks the order of updates?
   - `[2]`: Why is `get_recent` useful for a syncing peer?
   - `[3]`: What would happen if `updates` were a `HashSet<u64>` instead of a `Vec<u64>`?
3. Expected answers:
   ```rust
   [
       String::from("channels HashMap stores the canonical ChannelInfo by id"),
       String::from("updates Vec tracks the order of updates for recency queries"),
       String::from("get_recent lets a syncing peer fetch only the latest N channels instead of the full set"),
       String::from("A HashSet would lose ordering, making recency queries impossible without a secondary index"),
   ]
   ```

**Expected Output:**
```
Flow: ["channels HashMap...", "updates Vec...", "get_recent lets a syncing peer...", "A HashSet would lose ordering..."]
```

**Verification:** `cargo test` asserts exact strings.

**Hints:**
- `HashMap` = O(1) lookup by ID. `Vec` = preserves insertion order.
- `get_recent` uses `.rev().take(n)` to get the N most recent updates.
- This design pattern appears in Lightning gossip stores (see reference repos for inspiration).

</details>

---

## 🎓 Post-Cohort Capstone (Optional · 4–6 Weeks)

Choose **ONE** track. This is where Bitcoin depth becomes primary.

1. **Mini Bitcoin Core:** Blockchain, validation, PoW, difficulty (ties to the book's Ch. 5–7).
2. **Mini Lightning Node:** Use `lampo.rs` or `rust-lightning` to build a channel-opening service.
3. **Mini Nostr Relay:** Async event ingestion, filtering, and WebSocket broadcast.
4. **Mini DHT / P2P Discovery:** Implement a Kademlia-style lookup service with real networking.
5. **Mini Distributed Log:** Kafka-style partitioned log with producers/consumers.

---

## 📊 Report Card

### Coverage of *Building Bitcoin in Rust*

| Book Part | Coverage | Notes |
|---|---|---|
| Prelude & Setup | 100% | Toolchain, Cargo, workspaces covered. |
| Ch. 1: Introduction | 80% | Rust/Bitcoin synergy discussed. |
| Ch. 2: Whitepaper | 60% | Conceptual coverage; economics omitted. |
| Ch. 3: Setting Up | 100% | Rustup, Cargo, crates covered. |
| Ch. 4: Taming Rust | 95% | Ownership, traits, generics, closures, iterators. |
| Ch. 5: Keeping Rust Cultured | 100% | `rustfmt`, `clippy`, `thiserror` integrated. |
| Ch. 6: Bitcoin Library | 55% | Types, errors, serialization. Mining omitted. |
| Ch. 7: CPU Miner | 25% | PoW concepts only; implementation deferred. |
| Ch. 8: Bitcoin Node | 120% | Networking & P2P covered deeper than the book. |
| Ch. 9: CLI/TUI Wallet | 30% | Wallet state modeled; UI frameworks omitted. |

**Net Book Value:** ~75–80% of the book's educational value, with the cohort going *deeper* on networking, async, and distributed systems.

### Distributed Systems Coverage

| Concept | Week | Depth |
|---|---|---|
| State Machines | 1 | Deep |
| Type-Safe APIs | 2 | Deep |
| Collections & Indexing | 3 | Deep |
| Parallel Processing | 4 | Deep |
| Protocol Design | 5 | Deep |
| Async I/O & Backpressure | 6 | Deep |
| Retry, Load Balancing | 7 | Medium |
| Gossip, DHTs, CAP | 8 | Deep |
| Consensus | 8 | Conceptual |
