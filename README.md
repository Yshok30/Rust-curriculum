<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rust for Distributed Systems Engineers — 8-Week Cohort</title>
<style>
  :root {
    --core: #22c55e;
    --stretch: #f59e0b;
    --deep: #ef4444;
    --bg: #0f172a;
    --card: #1e293b;
    --text: #e2e8f0;
    --muted: #94a3b8;
    --border: #334155;
    --accent: #38bdf8;
  }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.7;
    max-width: 900px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }
  h1 { color: #f8fafc; border-bottom: 3px solid var(--accent); padding-bottom: 0.5rem; }
  h2 {
    color: var(--accent);
    margin-top: 3rem;
    padding: 1rem;
    background: var(--card);
    border-radius: 12px;
    border-left: 6px solid var(--accent);
  }
  h3 {
    color: #cbd5e1;
    margin-top: 2rem;
    border-bottom: 1px solid var(--border);
    padding-bottom: 0.3rem;
  }
  h4 { color: #e2e8f0; margin-top: 1.5rem; }
  .badge {
    display: inline-block;
    padding: 0.15rem 0.6rem;
    border-radius: 999px;
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-right: 0.5rem;
  }
  .badge-core { background: rgba(34,197,94,0.15); color: var(--core); border: 1px solid var(--core); }
  .badge-stretch { background: rgba(245,158,11,0.15); color: var(--stretch); border: 1px solid var(--stretch); }
  .badge-deep { background: rgba(239,68,68,0.15); color: var(--deep); border: 1px solid var(--deep); }
  .badge-hint { background: rgba(56,189,248,0.15); color: var(--accent); border: 1px solid var(--accent); }
  .week-meta {
    background: var(--card);
    padding: 1rem 1.5rem;
    border-radius: 12px;
    margin: 1rem 0 2rem;
    border: 1px solid var(--border);
  }
  .week-meta strong { color: var(--accent); }
  .question-list {
    background: var(--card);
    padding: 1.5rem;
    border-radius: 12px;
    border: 1px solid var(--border);
    margin-bottom: 1.5rem;
  }
  .question-list ol { padding-left: 1.5rem; }
  .question-list li { margin-bottom: 1rem; }
  .question-list li::marker { color: var(--accent); font-weight: bold; }
  .code-q {
    background: #0b1220;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 1rem;
    margin-top: 0.5rem;
    font-family: "Fira Code", Consolas, Monaco, monospace;
    font-size: 0.9rem;
    color: #a5b4fc;
    overflow-x: auto;
  }
  .assignment-overview {
    background: var(--card);
    padding: 1.5rem;
    border-radius: 12px;
    border: 1px solid var(--border);
    margin-bottom: 1rem;
  }
  .assignment-overview ul { list-style: none; padding-left: 0; }
  .assignment-overview li { padding: 0.4rem 0; border-bottom: 1px solid var(--border); }
  .assignment-overview li:last-child { border-bottom: none; }
  details {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
  }
  summary {
    cursor: pointer;
    padding: 1rem 1.5rem;
    background: linear-gradient(90deg, rgba(56,189,248,0.1), transparent);
    font-weight: 700;
    color: var(--accent);
    font-size: 1.05rem;
    user-select: none;
    list-style: none;
  }
  summary::-webkit-details-marker { display: none; }
  summary::before {
    content: "▶ ";
    display: inline-block;
    transition: transform 0.2s;
  }
  details[open] summary::before { transform: rotate(90deg); }
  details[open] summary { border-bottom: 1px solid var(--border); }
  .details-inner { padding: 1.5rem; }
  .expected {
    background: #0b1220;
    border-left: 4px solid var(--core);
    padding: 1rem;
    border-radius: 0 8px 8px 0;
    margin: 1rem 0;
    font-family: monospace;
  }
  .expected strong { color: var(--core); }
  .hints {
    background: rgba(56,189,248,0.08);
    border-left: 4px solid var(--accent);
    padding: 1rem;
    border-radius: 0 8px 8px 0;
    margin: 1rem 0;
  }
  .hints strong { color: var(--accent); }
  .verify {
    background: rgba(34,197,94,0.08);
    border-left: 4px solid var(--core);
    padding: 1rem;
    border-radius: 0 8px 8px 0;
    margin: 1rem 0;
  }
  .verify strong { color: var(--core); }
  .reading {
    background: rgba(245,158,11,0.08);
    border-left: 4px solid var(--stretch);
    padding: 1rem;
    border-radius: 0 8px 8px 0;
    margin: 1rem 0;
  }
  .reading strong { color: var(--stretch); }
  .repo-hint {
    font-size: 0.85rem;
    color: var(--muted);
    font-style: italic;
    border-top: 1px dashed var(--border);
    margin-top: 1rem;
    padding-top: 1rem;
  }
  .repo-hint a { color: var(--accent); }
  code { background: #0b1220; padding: 0.15rem 0.35rem; border-radius: 4px; font-family: monospace; color: #a5b4fc; }
  pre { background: #0b1220; padding: 1rem; border-radius: 8px; overflow-x: auto; border: 1px solid var(--border); }
  pre code { background: transparent; padding: 0; }
  .toc { background: var(--card); padding: 1.5rem; border-radius: 12px; border: 1px solid var(--border); margin-bottom: 2rem; }
  .toc a { color: var(--accent); text-decoration: none; }
  .toc a:hover { text-decoration: underline; }
  .toc ul { list-style: none; padding-left: 0; }
  .toc li { padding: 0.3rem 0; }
  hr { border: none; border-top: 1px solid var(--border); margin: 2rem 0; }
  .rules-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
    margin: 1.5rem 0;
  }
  .rule-card {
    background: var(--card);
    padding: 1rem;
    border-radius: 10px;
    border: 1px solid var(--border);
  }
  .rule-card strong { color: var(--accent); display: block; margin-bottom: 0.5rem; }
</style>
<base target="_blank">
</head>
<body>

# 🦀 Rust for Distributed Systems Engineers
## 8-Week Cohort Curriculum — Final Edition
### <span style="color: var(--accent)">Self-Contained · 100% Verifiable · Repo-Independent · Moderate Difficulty</span>

<div class="toc">

**📑 Jump to Week:**
- [Week 1 — Ownership & Memory](#week1)
- [Week 2 — Types & Errors](#week2)
- [Week 3 — Collections & Iterators](#week3)
- [Week 4 — Concurrency](#week4)
- [Week 5 — Networking](#week5)
- [Week 6 — Async](#week6)
- [Week 7 — Infrastructure](#week7)
- [Week 8 — P2P & Distributed Algorithms](#week8)
- [Capstone & Report Card](#capstone)

</div>

<div class="rules-grid">
  <div class="rule-card">
    <strong>🎯 Target</strong>
    Open-source developers entering Bitcoin, Lightning, Nostr, and distributed systems via Rust.
  </div>
  <div class="rule-card">
    <strong>📊 Difficulty Mix</strong>
    <span class="badge badge-core">Core 60%</span> Easy<br>
    <span class="badge badge-stretch">Stretch 25%</span> Moderate<br>
    <span class="badge badge-deep">Deep Dive 15%</span> Harder
  </div>
  <div class="rule-card">
    <strong>✅ Verifiable</strong>
    Every assignment has exact expected outputs validated by <code>cargo test</code>. No subjective grading.
  </div>
  <div class="rule-card">
    <strong>🔖 Repos are Hints Only</strong>
    External repos are pure inspiration. You never need to clone or build them.
  </div>
</div>

<hr>

<hr>
<h2 id="week1">Week 1 — Ownership, Memory & State Modeling <span style="font-size:0.6em;color:var(--muted)">(The Machine)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How does a system safely manage resources without a garbage collector?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Prelude:</strong> "Who is this book for?", "Requirements", "Goals and Structure" (pp. XII–XVI)</li>
<li><strong>Ch. 3 (Setting Up):</strong> "Rust: The first contact", "Hello world" (pp. 67–68)</li>
<li><strong>Ch. 4 (Taming Rust):</strong> "Memory model" (p. 93), "Strings in Rust" (p. 101), "Lifetimes of owned vs unowned values" (p. 104), "Pattern matching" (p. 111), "User-defined types" (p. 116)</li>
<li><strong>Ch. 4:</strong> "Global 'variables' in Rust" (p. 112)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html">Rust Ownership Explained</a> — Rust Book, Ch. 4.1</li>
<li><a href="https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html#stack-only-data-copy">Stack vs Heap</a> — Rust Book</li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>cashubtc/cdk</code> → <code>crates/cdk/src/types.rs</code> for struct patterns. <code>bitcoindevkit/bdk</code> → <code>bdk/src/wallet/mod.rs</code> for struct definitions.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> Explain the difference between the stack and the heap. Why does Rust force you to think about this explicitly when many languages hide it?</li>
<li><strong>Q2:</strong> What is ownership in Rust? Describe the three ownership rules in your own words.</li>
<li><strong>Q3:</strong> Why can an <code>i32</code> be copied implicitly but a <code>String</code> cannot? What trait governs this behavior?</li>
<li><strong>Q4:</strong> You have <code>s1 = String::from("hello")</code> and you write <code>let s2 = s1;</code>. What happens to <code>s1</code>? Why does Rust design it this way?</li>
<li><strong>Q5:</strong> What is the difference between a <em>move</em> and a <em>borrow</em>? When would you choose one over the other?</li>
<li><strong>Q6:</strong> Explain pattern matching with <code>match</code>. Why is it safer than a chain of <code>if/else</code> statements for enums?</li>
<li><strong>Q7:</strong> What happens when an owned value goes out of scope? How does Rust ensure memory is freed without a garbage collector?</li>
<li><strong>Q8:</strong> In the context of distributed systems, why might a node prefer stack-allocated arrays for protocol headers instead of heap-allocated vectors?</li>
<li><strong>Q9:</strong> What is a struct? What is an enum? Give a real-world example of when an enum is better than a struct for modeling state.</li>
<li><strong>Q10:</strong> Look at the following snippet. Will it compile? If not, what is the exact error message you would expect, and why? Answer verbally — no need to write the fix.
<div class="code-q"><pre><code>fn main() {
    let s = String::from("hello");
    let len = calculate_length(s);
    println!("{} is {} chars long", s, len);
}
fn calculate_length(s: String) -> usize { s.len() }</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Hello, Peer! — Your First Struct</strong> — Build a <code>Peer</code> struct with <code>name</code> and <code>id</code>, and a <code>greet()</code> function that returns a formatted string.</li>
<li><span class="badge badge-core">core</span> <strong>Borrow Checker Fix-It Shop — 3 Easy Fixes</strong> — Fix three named borrow-checker bugs: Moved String, Double Mutable Borrow, and Dangling Reference.</li>
<li><span class="badge badge-core">core</span> <strong>Traffic Light State Machine</strong> — Model <code>Red → Green → Yellow → Red</code> with an enum and <code>match</code>. No networking concepts.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>The Builder Pattern — Simple Config</strong> — Build a <code>ServerConfig</code> using a builder that enforces required fields via <code>Result</code>.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Stack vs Heap Audit</strong> — Use <code>std::mem::size_of_val</code> to measure stack sizes and prove heap allocation.</li>
<li><span class="badge badge-deep">deep</span> <strong>Ownership Analysis — Provided Snippet</strong> — Analyze a provided <code>Proof</code> snippet and return a <code>[bool; 5]</code> array identifying ownership semantics.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Hello, Peer!</h4>
<p><strong>What you'll build:</strong> A simple <code>Peer</code> struct that stores a name and an ID, and a function that greets the peer.</p>
<p><strong>Step-by-step:</strong></p>
<ol>
<li>Create a new Cargo project: <code>cargo new week1_hello_peer</code></li>
<li>Define <code>struct Peer { name: String, id: u64 }</code></li>
<li>Write <code>fn greet(peer: &Peer) -> String</code> returning <code>"Hello, {name}! Your peer ID is {id}."</code></li>
<li>In <code>main()</code>, create <code>Peer { name: "Alice", id: 42 }</code> and print <code>greet(&peer)</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Hello, Alice! Your peer ID is 42.</div>
<div class="verify"><strong>Verification:</strong> <code>cargo run</code> prints the exact line. <code>cargo test</code> checks the exact string.</div>
<div class="hints"><strong>Hints:</strong> Use <code>format!()</code> inside <code>greet</code>. <code>peer.name</code> auto-dereferences from <code>&Peer</code>.</div>

<h4><span class="badge badge-core">Core 2</span> Borrow Checker Fix-It Shop</h4>
<p><strong>What you'll build:</strong> Fix 3 tiny broken programs that fail the borrow checker.</p>
<p><strong>File 1 — The "Moved String":</strong></p>
<pre><code>fn main() {
    let msg = String::from("hello");
    print_message(msg);
    println!("Original: {}", msg); // ERROR
}
fn print_message(s: String) { println!("{}", s); }</code></pre>
<p><strong>Fix:</strong> Add <code>&</code> in exactly 2 places to borrow instead of own.</p>
<p><strong>File 2 — The "Double Mutable Borrow":</strong></p>
<pre><code>fn main() {
    let mut s = String::from("hello");
    let r1 = &mut s;
    let r2 = &mut s;
    println!("{} {}", r1, r2); // ERROR
}</code></pre>
<p><strong>Fix:</strong> Move the <code>println!</code> using <code>r1</code> before <code>let r2</code>.</p>
<p><strong>File 3 — The "Dangling Reference":</strong></p>
<pre><code>fn create_string() -> &String {
    let s = String::from("hello");
    &s // ERROR
}</code></pre>
<p><strong>Fix:</strong> Return <code>String</code> (owned), not <code>&String</code>.</p>
<div class="expected"><strong>Expected Output:</strong><br>hello<br>hello<br>hello</div>
<div class="verify"><strong>Verification:</strong> <code>cargo run</code> prints hello 3 times. <code>cargo test</code> compiles all three files.</div>

<h4><span class="badge badge-core">Core 3</span> Traffic Light State Machine</h4>
<p><strong>What you'll build:</strong> An enum that models a traffic light and transitions between states.</p>
<ol>
<li>Define <code>enum TrafficLight { Red, Yellow, Green }</code></li>
<li><code>fn next_state(light: TrafficLight) -> TrafficLight</code>: Red→Green, Green→Yellow, Yellow→Red</li>
<li><code>fn describe(light: &TrafficLight) -> &'static str</code>: Red="Stop", Yellow="Caution", Green="Go"</li>
<li>In <code>main()</code>, start at Red, print description, transition 3 times.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Current: Red -> Stop<br>Next: Green -> Go<br>Next: Yellow -> Caution<br>Next: Red -> Stop</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> checks all 3 transitions and descriptions.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> The Builder Pattern — Simple Config</h4>
<p><strong>What you'll build:</strong> A <code>ServerConfig</code> struct built with a builder pattern.</p>
<ol>
<li><code>struct ServerConfig { host: String, port: u16 }</code></li>
<li><code>struct ServerConfigBuilder { host: Option<String>, port: Option<u16> }</code></li>
<li>Implement <code>new()</code>, <code>host()</code>, <code>port()</code>, and <code>build() -> Result&lt;ServerConfig, &'static str&gt;</code></li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>ServerConfig { host: "localhost", port: 8080 }</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> checks the built config.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Stack vs Heap Audit</h4>
<p><strong>What you'll build:</strong> A program that demonstrates stack vs heap allocation via sizes.</p>
<ol>
<li>Define <code>struct Packet { id: u64, payload: String }</code></li>
<li>Print <code>size_of_val</code> for an <code>i32</code>, a <code>String</code>, and a <code>Packet</code></li>
<li>Print heap lengths of the string contents</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>i32 size: 4 bytes<br>String size: 24 bytes<br>Packet size: 32 bytes<br>String heap len: 5<br>Packet payload heap len: 4</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact sizes (platform-dependent, use <code>assert!</code> with comments).</div>
<div class="hints"><strong>Hints:</strong> On 64-bit systems, <code>String</code> is 24 bytes (ptr + len + cap). <code>Packet</code> = 8 + 24 = 32 bytes on the stack. The actual text lives on the heap.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Ownership Analysis — Provided Snippet</h4>
<p><strong>What you'll build:</strong> Analyze ownership in a provided snippet and answer via a testable array.</p>
<p>You are given this in <code>src/main.rs</code> (do NOT modify):</p>
<pre><code>struct Proof { id: String, amount: u64, secret: String; }
fn inspect(proof: &Proof) -> String { format!("{}: {}", proof.id, proof.amount) }
fn consume(proof: Proof) -> u64 { proof.amount }
fn main() {
    let p = Proof { id: String::from("abc123"), amount: 100, secret: String::from("shhh") };
    let summary = inspect(&p);
    let taken = consume(p);
    println!("{} | {}", summary, taken);
}</code></pre>
<p>Write <code>fn analyze() -> [bool; 5]</code> answering:</p>
<ul>
<li>[0]: <code>inspect</code> borrows <code>p</code>?</li>
<li>[1]: <code>consume</code> takes ownership of <code>p</code>?</li>
<li>[2]: <code>p.id</code> is moved during <code>inspect</code>?</li>
<li>[3]: <code>p</code> can be used after <code>inspect</code>?</li>
<li>[4]: <code>p</code> can be used after <code>consume</code>?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Analysis: [true, true, false, true, false]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts <code>analyze() == [true, true, false, true, false]</code>.</div>
<div class="hints"><strong>Hints:</strong> <code>format!</code> only needs <code>&String</code>, so <code>proof.id</code> is borrowed, not moved. <code>consume(p)</code> moves <code>p</code> entirely.</div>

</div>
</details>


<hr>
<h2 id="week2">Week 2 — Type Systems, Safe APIs & Error Handling <span style="font-size:0.6em;color:var(--muted)">(The Contract)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do we model invalid states out of existence?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 4 (Taming Rust):</strong> "User-defined types" (p. 116), "Static dispatch" (p. 118), "Generic param bounds" (p. 120), "Dynamic dispatch" (p. 121)</li>
<li><strong>Ch. 5 (Implementing a Bitcoin Library):</strong> "Error handling in Rust" (pp. 192–200), "Error handling in btclib" (p. 202)</li>
<li><strong>Ch. 4:</strong> "Functional Programming in Rust" — "Immutability" (p. 123), "The type system" (p. 127), "Functions and closures" (p. 142)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/book/ch09-00-error-handling.html">The Rust Book: Error Handling</a> — Ch. 9</li>
<li><a href="https://doc.rust-lang.org/book/ch10-02-traits.html">Traits in Rust</a> — Rust Book, Ch. 10.2</li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>bitcoindevkit/bdk</code> → <code>bdk/src/wallet/error.rs</code> for error categorization. <code>cashubtc/cdk</code> → <code>crates/cdk/src/error.rs</code> for error taxonomy.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is the difference between <code>Option&lt;T&gt;</code> and <code>Result&lt;T, E&gt;</code>? When would you use one versus the other?</li>
<li><strong>Q2:</strong> Explain the phrase <em>make invalid states unrepresentable.</em> How do Rust's type system (enums, structs, generics) help achieve this?</li>
<li><strong>Q3:</strong> What is a trait? How is it similar to and different from an interface in Java or a type class in Haskell?</li>
<li><strong>Q4:</strong> What is a generic type parameter? Why is <code>Vec&lt;T&gt;</code> preferable to writing separate <code>VecInt</code>, <code>VecString</code>, etc.?</li>
<li><strong>Q5:</strong> Describe the builder pattern. Why is it particularly useful in systems programming when constructing complex protocol messages?</li>
<li><strong>Q6:</strong> What is the difference between recoverable and unrecoverable errors? Why does Rust use <code>Result</code> for the former and <code>panic!</code> for the latter?</li>
<li><strong>Q7:</strong> In a distributed system, why is it dangerous to use <code>unwrap()</code> on network I/O results? What should you do instead?</li>
<li><strong>Q8:</strong> What are trait bounds? Why does a function <code>fn print&lt;T: Display&gt;(item: T)</code> require <code>T</code> to implement <code>Display</code>?</li>
<li><strong>Q9:</strong> How does <code>Result</code> composability (<code>map</code>, <code>and_then</code>) help prevent deeply nested error-handling code?</li>
<li><strong>Q10:</strong> Look at the following snippet. What will it print, and why? Answer verbally — no need to write code.
<div class="code-q"><pre><code>fn main() {
    let x = Some(5);
    let y: Option&lt;i32&gt; = None;
    println!("{}", x.unwrap_or(0) + y.unwrap_or(0));
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Safe Division — Your First Result</strong> — Write <code>divide(a, b) -> Result&lt;f64, &'static str&gt;</code> that checks for division by zero and NaN.</li>
<li><span class="badge badge-core">core</span> <strong>Shape Area — Your First Trait</strong> — Define an <code>Area</code> trait and implement it for <code>Circle</code> and <code>Rectangle</code>.</li>
<li><span class="badge badge-core">core</span> <strong>Config Parser — Your First Option Chain</strong> — Parse <code>"key=value"</code> into <code>Option&lt;(String, String)&gt;</code> with trimming.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Generic Key-Value Store</strong> — Define a <code>Store&lt;K, V&gt;</code> trait and implement it with <code>HashMap</code>.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Error Translation — Mini Network Stack</strong> — Wrap <code>io::Error</code> and <code>ParseError</code> in a custom enum with <code>From</code>.</li>
<li><span class="badge badge-deep">deep</span> <strong>Error Taxonomy Analysis — Provided Snippet</strong> — Map a provided <code>WalletError</code> enum's variants to categories and count them.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Safe Division</h4>
<p><strong>What you'll build:</strong> A function that divides two numbers and returns a <code>Result</code>.</p>
<ol>
<li><code>cargo new week2_safe_division</code></li>
<li>Write <code>fn divide(a: f64, b: f64) -> Result&lt;f64, &'static str&gt;</code></li>
<li>Return <code>Ok(a / b)</code> if valid. Return <code>Err("Division by zero")</code> if <code>b == 0.0</code>. Return <code>Err("Invalid operand")</code> if either is NaN (use <code>f64::is_nan()</code>).</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>divide(10.0, 2.0) = Ok(5.0)<br>divide(10.0, 0.0) = Err("Division by zero")<br>divide(f64::NAN, 2.0) = Err("Invalid operand")</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact Results for 6 cases.</div>
<div class="hints"><strong>Hints:</strong> Check NaN FIRST. <code>NaN == 0.0</code> is <code>false</code>, but you still want to reject it.</div>

<h4><span class="badge badge-core">Core 2</span> Shape Area</h4>
<p><strong>What you'll build:</strong> A trait <code>Area</code> and two structs that implement it.</p>
<ol>
<li>Define <code>trait Area { fn area(&self) -> f64; }</code></li>
<li>Define <code>Circle { radius: f64 }</code> and <code>Rectangle { width: f64, height: f64 }</code></li>
<li>Implement <code>Area</code> for both. Circle = π × r². Rectangle = width × height.</li>
<li>Write <code>fn print_area&lt;T: Area&gt;(shape: &T)</code> and test.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Circle(3.0) area = 28.274333882308138<br>Rectangle(4.0, 5.0) area = 20.0</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts area within 0.001 for 4 shapes.</div>
<div class="hints"><strong>Hints:</strong> This is "static dispatch" — the compiler creates a separate version of <code>print_area</code> per type. Fast!</div>

<h4><span class="badge badge-core">Core 3</span> Config Parser</h4>
<p><strong>What you'll build:</strong> Parse <code>"key=value"</code> into <code>Option&lt;(String, String)&gt;</code>.</p>
<ol>
<li>Write <code>fn parse_config(input: &str) -> Option&lt;(String, String)&gt;</code></li>
<li>Return <code>None</code> if empty or no <code>=</code> found. Split, trim, return <code>Some((left, right))</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>parse_config("host=localhost") = Some(("host", "localhost"))<br>parse_config("badinput") = None<br>parse_config("") = None<br>parse_config("  key  =  value  ") = Some(("key", "value"))</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact Options for 6 cases.</div>
<div class="hints"><strong>Hints:</strong> Try using <code>?</code>: <code>let idx = input.find('=')?;</code></div>

<h4><span class="badge badge-stretch">Stretch 4</span> Generic Key-Value Store</h4>
<p><strong>What you'll build:</strong> A generic storage trait and an in-memory implementation.</p>
<ol>
<li>Define <code>trait Store&lt;K, V&gt;</code> with <code>get</code> and <code>put</code>.</li>
<li>Implement for <code>InMemoryStore&lt;K, V&gt;</code> using <code>HashMap</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>put("alice", 100) -> get("alice") = Some(100)<br>get("bob") = None</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact values.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Error Translation</h4>
<p><strong>What you'll build:</strong> An enum that wraps different error types.</p>
<ol>
<li><code>enum AppError { Io(std::io::Error), Parse(&'static str) }</code></li>
<li>Implement <code>From&lt;std::io::Error&gt;</code> for <code>AppError</code> manually.</li>
<li>Write <code>read_file(path) -> Result&lt;String, AppError&gt;</code> using <code>?</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>read_file("hello.txt") = Ok("hello world")<br>read_file("missing.txt") = Err(Io(...))<br>read_file("bad.txt") = Err(Parse("invalid content"))</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with temporary files.</div>
<div class="hints"><strong>Hints:</strong> The <code>?</code> operator calls <code>From::from</code> automatically. Magic!</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Error Taxonomy Analysis</h4>
<p><strong>What you'll build:</strong> Analyze a provided error enum and map variants to categories.</p>
<p>You are given this in <code>src/lib.rs</code>:</p>
<pre><code>#[derive(Debug)]
enum WalletError {
    InsufficientFunds { needed: u64, available: u64 },
    InvalidAddress(String),
    NetworkTimeout,
    DatabaseCorrupted,
    UserCancelled,
}</code></pre>
<p>Write <code>fn categorize(err: &WalletError) -> &'static str</code> returning:</p>
<ul>
<li><code>"user"</code> for <code>UserCancelled</code></li>
<li><code>"network"</code> for <code>NetworkTimeout</code></li>
<li><code>"data"</code> for <code>DatabaseCorrupted</code> and <code>InvalidAddress</code></li>
<li><code>"funds"</code> for <code>InsufficientFunds</code></li>
</ul>
<p>Also write <code>count_by_category(errors: &[WalletError]) -> HashMap&lt;&'static str, usize&gt;</code>.</p>
<div class="expected"><strong>Expected Output:</strong><br>categorize(InsufficientFunds) = "funds"<br>categorize(InvalidAddress) = "data"<br>count_by_category([...]) = {"funds": 1, "data": 2, "network": 1, "user": 1}</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings and counts.</div>
<div class="hints"><strong>Hints:</strong> <code>HashMap::entry(category).and_modify(|c| *c += 1).or_insert(1);</code> is a clean counting pattern.</div>

</div>
</details>


<hr>
<h2 id="week3">Week 3 — Collections, Iterators & Data Structures <span style="font-size:0.6em;color:var(--muted)">(The Organization)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do nodes organize and query information efficiently?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 4 (Taming Rust):</strong> "The type system" (p. 127), "Functions and closures" (p. 142), "Iterators" (p. 145)</li>
<li><strong>Ch. 4:</strong> "Strings in Rust" (p. 101)</li>
<li><strong>Ch. 5 (Implementing a Bitcoin Library):</strong> "Data types" (p. 163) — skim</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/book/ch08-00-common-collections.html">Rust Book: Common Collections</a> — Ch. 8</li>
<li><a href="https://doc.rust-lang.org/book/ch13-02-iterators.html">Rust Book: Iterators</a> — Ch. 13.2</li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>bitcoindevkit/bdk</code> for <code>HashMap</code> usage in UTXO indexing. <code>cashubtc/cdk</code> for <code>Vec</code> and <code>HashMap</code> in mint storage.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> When is <code>BTreeMap</code> preferable to <code>HashMap</code>? What does a distributed system gain from sorted keys?</li>
<li><strong>Q2:</strong> Explain the difference between <code>iter()</code>, <code>iter_mut()</code>, and <code>into_iter()</code>. Who owns the data after each?</li>
<li><strong>Q3:</strong> What is a closure? Explain the three closure traits (<code>Fn</code>, <code>FnMut</code>, <code>FnOnce</code>) and when each is required.</li>
<li><strong>Q4:</strong> Why does <code>HashMap&lt;&str, T&gt;</code> require lifetime annotations but <code>HashMap&lt;String, T&gt;</code> does not?</li>
<li><strong>Q5:</strong> What is iterator chaining? Why is <code>collection.iter().filter(...).map(...).collect()</code> considered idiomatic Rust?</li>
<li><strong>Q6:</strong> In a distributed system, why might a node use a <code>VecDeque</code> for a network message buffer instead of a <code>Vec</code>?</li>
<li><strong>Q7:</strong> What is the difference between <code>String</code> and <code>&str</code>? Why can't you use <code>&str</code> as a HashMap key if it comes from a local variable?</li>
<li><strong>Q8:</strong> Explain the concept of <em>data locality.</em> Why is a <code>Vec</code> often faster than a linked list for sequential access?</li>
<li><strong>Q9:</strong> What does <code>collect()</code> do? What type does it return, and how does Rust know which collection to build?</li>
<li><strong>Q10:</strong> Look at the following snippet. What will it print, and why? Answer verbally.
<div class="code-q"><pre><code>fn main() {
    let nums = vec![1, 2, 3, 4, 5];
    let result: Vec&lt;i32&gt; = nums.iter().map(|x| x * 2).filter(|x| x > &4).collect();
    println!("{:?}", result);
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Contact Book — Your First HashMap</strong> — Build a contact book with add, get, remove, and sorted list using <code>HashMap</code>.</li>
<li><span class="badge badge-core">core</span> <strong>Number Filter & Transform — Iterator Chain Only</strong> — Filter, map, sort, and dedup using ONLY iterator methods. No <code>for</code> loops.</li>
<li><span class="badge badge-core">core</span> <strong>Priority Task Queue — VecDeque</strong> — Implement a queue where urgent tasks skip to the front.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>High-Value Transaction Filter</strong> — Filter <code>Transaction</code> structs by fee and sort descending.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Closure Capture Fix</strong> — Fix a borrow checker error by restructuring closure lifetimes.</li>
<li><span class="badge badge-deep">deep</span> <strong>Collection Design — Provided Snippet Analysis</strong> — Analyze why a provided <code>Mempool</code> uses <code>HashMap</code> vs <code>VecDeque</code>.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Contact Book</h4>
<p><strong>What you'll build:</strong> A simple contact book using <code>HashMap</code>.</p>
<ol>
<li><code>cargo new week3_contact_book</code></li>
<li><code>struct ContactBook { entries: HashMap&lt;String, String&gt; }</code></li>
<li>Methods: <code>new()</code>, <code>add()</code> (Err if duplicate), <code>get()</code>, <code>remove()</code>, <code>list()</code> (sorted)</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Added Alice<br>Added Bob<br>Err: already exists<br>Bob's phone: Some("555-0199")<br>Removed Alice: Some("555-0100")<br>Remaining contacts: [("Bob", "555-0199"), ("Charlie", "555-0233")]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact behavior for all 5 methods.</div>

<h4><span class="badge badge-core">Core 2</span> Number Filter & Transform</h4>
<p><strong>What you'll build:</strong> A function using ONLY iterator methods.</p>
<ol>
<li>Write <code>fn process_numbers(nums: &[i32]) -> Vec&lt;i32&gt;</code></li>
<li>Keep only numbers > 0, multiply by 2, sort ascending, remove duplicates.</li>
<li>No <code>for</code> loops allowed.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Input: [-3, 1, 4, -1, 5, 1, 2]<br>Output: [2, 4, 10]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact output for 4 cases.</div>
<div class="hints"><strong>Hints:</strong> Chain: <code>.iter().filter(|&&x| x > 0).map(|x| x * 2).collect::&lt;Vec&lt;_&gt;&gt;()</code> then sort/dedup.</div>

<h4><span class="badge badge-core">Core 3</span> Priority Task Queue</h4>
<p><strong>What you'll build:</strong> A queue where urgent tasks skip to the front.</p>
<ol>
<li><code>struct TaskQueue { queue: VecDeque&lt;String&gt; }</code></li>
<li><code>add_normal()</code> pushes back. <code>add_urgent()</code> pushes front. <code>next()</code> pops front.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Adding: A (normal)<br>Adding: B (urgent)<br>Adding: C (normal)<br>Adding: D (urgent)<br>Processing: D<br>Processing: B<br>Processing: A<br>Processing: C<br>Queue empty: true</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact processing order.</div>
<div class="hints"><strong>Hints:</strong> Think of a hospital line: urgent patients skip to the front.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> High-Value Transaction Filter</h4>
<p><strong>What you'll build:</strong> Filter transactions by fee.</p>
<ol>
<li><code>struct Transaction { id: u32, amount: u64, fee: u64 }</code></li>
<li><code>fn high_value_txs(txs: &[Transaction], min_fee: u64) -> Vec&lt;&Transaction&gt;</code></li>
<li>Filter by fee, sort by fee descending then id ascending.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Input: 5 txs with fees [100, 50, 200, 75, 150]; min_fee = 80<br>Output IDs: [3, 5, 1]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact ordering.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Closure Capture Fix</h4>
<p><strong>What you'll build:</strong> Fix a borrow checker error involving closures.</p>
<p>Broken code:</p>
<pre><code>fn main() {
    let mut data = vec![1, 2, 3];
    let first = || println!("first: {}", data[0]);
    let mut second = || data.push(4);
    first();
    second();
}</code></pre>
<p>Fix by restructuring so <code>first()</code> completes before <code>second</code> is created.</p>
<div class="expected"><strong>Expected Output:</strong><br>first: 1</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> passes; original broken code is in comments.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Collection Design Analysis</h4>
<p><strong>What you'll build:</strong> Analyze why a provided snippet chose specific collections.</p>
<p>You are given:</p>
<pre><code>struct Mempool {
    by_id: HashMap&lt;u64, Transaction&gt;,
    by_fee: VecDeque&lt;u64&gt;,
}
struct Transaction { id: u64, fee: u64 }</code></pre>
<p>Write <code>fn analyze_design() -> [String; 3]</code>:</p>
<ul>
<li>[0]: Why <code>HashMap</code> for <code>by_id</code>?</li>
<li>[1]: Why <code>VecDeque</code> for <code>by_fee</code>?</li>
<li>[2]: What would go wrong if <code>by_id</code> were a <code>Vec</code>?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Analysis: ["HashMap provides O(1) lookup by id", "VecDeque allows efficient push/pop from both ends for fee ordering", "Vec would require O(n) scan to find a transaction by id"]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>

</div>
</details>


<hr>
<h2 id="week4">Week 4 — Concurrency & System Design Synthesis <span style="font-size:0.6em;color:var(--muted)">(The Bridge)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do we parallelize work safely, and what do production architectures look like under the hood?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Prelude:</strong> "Requirements" — "Threads" definition (p. XV)</li>
<li><strong>Ch. 7 (Creating a CPU Miner):</strong> "Networking" (p. 277)</li>
<li><strong>Ch. 8 (Building a Bitcoin Node):</strong> "Organization" (p. 311)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/book/ch16-00-concurrency.html">The Rust Book: Concurrency</a> — Ch. 16</li>
<li><a href="https://doc.rust-lang.org/rust-by-example/std/threads.html">Rust by Example: Threads</a></li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>fedimint/fedimint</code> for <code>Arc&lt;Mutex&lt;...&gt;&gt;</code> patterns. <code>bitcoindevkit/bdk</code> for thread-safety in wallet sync.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is a data race? How does Rust's ownership system prevent data races at compile time?</li>
<li><strong>Q2:</strong> Explain <code>Arc</code> and <code>Mutex</code>. Why do you need both to share mutable state across threads?</li>
<li><strong>Q3:</strong> What is the difference between <code>std::sync::Mutex</code> and <code>tokio::sync::Mutex</code>? When would you use each?</li>
<li><strong>Q4:</strong> Describe the producer-consumer pattern. Why is it often safer than shared state for distributed systems?</li>
<li><strong>Q5:</strong> What are the <code>Send</code> and <code>Sync</code> traits? Why might a raw pointer <code>*const T</code> not be <code>Send</code>?</li>
<li><strong>Q6:</strong> In a distributed system, why might a node use a worker pool to validate transactions instead of spawning one thread per transaction?</li>
<li><strong>Q7:</strong> What is lock contention? How does it manifest, and how can you reduce it?</li>
<li><strong>Q8:</strong> Why is <code>Mutex</code> poisoning a thing in Rust? How do you recover from a poisoned mutex?</li>
<li><strong>Q9:</strong> Use AI to analyze <code>fedimint</code> or <code>bdk</code>: What are the top 3 concurrency patterns used? Summarize in your own words.</li>
<li><strong>Q10:</strong> Look at the following snippet. Will it compile? If not, what is the exact error and why? Answer verbally.
<div class="code-q"><pre><code>fn main() {
    let v = vec![1, 2, 3];
    let handle = std::thread::spawn(|| {
        println!("{:?}", v);
    });
    handle.join().unwrap();
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Parallel Sum — Your First Threads</strong> — Split a <code>Vec&lt;i32&gt;</code> in half and sum each half in a separate thread.</li>
<li><span class="badge badge-core">core</span> <strong>Thread-Safe Counter — Arc + Mutex</strong> — 10 threads increment a shared counter 100 times each. Assert exact count.</li>
<li><span class="badge badge-core">core</span> <strong>Channel-Based Worker Pool</strong> — 4 workers process 20 jobs via <code>mpsc</code> channels. Collect all results.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Concurrency Pattern Analysis — Provided Snippets</strong> — Compare shared-state vs message-passing snippets and identify tradeoffs.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Deadlock Simulation & Fix</strong> — Intentionally deadlock two mutexes, then fix by ordering locks.</li>
<li><span class="badge badge-deep">deep</span> <strong>Mutex Choice Analysis — Provided Snippets</strong> — Analyze <code>std::sync::Mutex</code> vs <code>tokio::sync::Mutex</code> snippets and explain when to use each.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Parallel Sum</h4>
<p><strong>What you'll build:</strong> Split a list and sum in parallel threads.</p>
<ol>
<li><code>cargo new week4_parallel_sum</code></li>
<li>Create a <code>Vec&lt;i32&gt;</code> with 6+ numbers.</li>
<li>Split at midpoint. Spawn 2 threads. Each sums one half.</li>
<li>Wait with <code>join()</code>, add partial sums.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Input: [1, 2, 3, 4, 5, 6]<br>Left half sum: 6<br>Right half sum: 15<br>Total: 21</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts correct total for 3 vectors.</div>
<div class="hints"><strong>Hints:</strong> <code>std::thread::spawn(move || { ... })</code> — the <code>move</code> is critical!</div>

<h4><span class="badge badge-core">Core 2</span> Thread-Safe Counter</h4>
<p><strong>What you'll build:</strong> A counter that 10 threads increment safely.</p>
<ol>
<li>Create <code>Arc&lt;Mutex&lt;u32&gt;&gt;</code> starting at 0.</li>
<li>Spawn 10 threads. Each locks, increments by 1, 100 times.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Final count: 1000</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts count == 1000 exactly.</div>
<div class="hints"><strong>Hints:</strong> <code>Arc::clone(&counter)</code> for each thread. <code>*num += 1;</code> dereferences the guard.</div>

<h4><span class="badge badge-core">Core 3</span> Channel-Based Worker Pool</h4>
<p><strong>What you'll build:</strong> A producer-consumer pool with 4 workers.</p>
<ol>
<li>Create <code>mpsc</code> channels for jobs (<code>u32</code>) and results (<code>String</code>).</li>
<li>Spawn 4 workers. Each receives a job ID, formats a result string, sends it back.</li>
<li>Main sends 20 job IDs, drops sender, collects 20 results.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>All 20 jobs completed.<br>Worker 2 processed job 5<br>Worker 0 processed job 1<br>...</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts result count == 20 and worker IDs in range 0..4.</div>
<div class="hints"><strong>Hints:</strong> Workers share the receiver via <code>Arc&lt;Mutex&lt;Receiver&gt;&gt;</code>.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> Concurrency Pattern Analysis</h4>
<p><strong>What you'll build:</strong> Compare two provided snippets.</p>
<p><strong>Snippet A — Shared State:</strong></p>
<pre><code>struct SharedCounter(Arc&lt;Mutex&lt;u32&gt;&gt;);
impl SharedCounter { fn increment(&self) { *self.0.lock().unwrap() += 1; } }</code></pre>
<p><strong>Snippet B — Message Passing:</strong></p>
<pre><code>struct JobQueue(mpsc::Sender&lt;u32&gt;, mpsc::Receiver&lt;u32&gt;);
impl JobQueue { fn send_job(&self, id: u32) { self.0.send(id).unwrap(); } }</code></pre>
<p>Write <code>fn compare_snippets() -> [String; 4]</code> answering tradeoffs.</p>
<div class="expected"><strong>Expected Output:</strong><br>Comparison: ["B is better for high contention...", "B is better for loose coupling...", "A risks mutex poisoning...", "B risks sender errors..."]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Deadlock Simulation & Fix</h4>
<p><strong>What you'll build:</strong> Intentionally deadlock, then fix.</p>
<ol>
<li>Create <code>AccountA</code> and <code>AccountB</code> with <code>Mutex&lt;u64&gt;</code>.</li>
<li><code>transfer(a, b, amount)</code> locks <code>a</code> then <code>b</code>.</li>
<li>Thread 1: <code>transfer(A, B, 10)</code>. Thread 2: <code>transfer(B, A, 10)</code>.</li>
<li>Fix by always locking in the same order (by ID).</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Before fix: test hangs / timeout<br>After fix: Completed successfully. Final balances: A=100, B=100</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> passes for fixed version. Broken version is commented out.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Mutex Choice Analysis</h4>
<p><strong>What you'll build:</strong> Analyze two provided mutex snippets.</p>
<p><strong>Snippet A — std::sync::Mutex:</strong></p>
<pre><code>struct SyncCache { data: Mutex&lt;Vec&lt;u32&gt;&gt; }
impl SyncCache { fn add(&self, v: u32) { self.data.lock().unwrap().push(v); } }</code></pre>
<p><strong>Snippet B — tokio::sync::Mutex:</strong></p>
<pre><code>struct AsyncCache { data: Mutex&lt;Vec&lt;u32&gt;&gt; }
impl AsyncCache { async fn add(&self, v: u32) { self.data.lock().await.push(v); } }</code></pre>
<p>Write <code>fn mutex_analysis() -> [String; 3]</code>:</p>
<ul>
<li>[0]: Which is faster and why?</li>
<li>[1]: Which can be held across <code>.await</code>?</li>
<li>[2]: Why is B required when awaiting a network response after locking?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Analysis: ["A is faster because std::sync::Mutex uses OS primitives directly...", "B can be held across await because tokio::sync::Mutex is async-aware...", "B is required because holding a std::sync::Mutex across await would block the async executor thread"]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>

</div>
</details>


<hr>
<h2 id="week5">Week 5 — Networking & Protocol Design <span style="font-size:0.6em;color:var(--muted)">(The Wire)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do independent machines communicate safely and efficiently?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 7 (Creating a CPU Miner):</strong> "Networking" (p. 277), "Asynchronous Rust" (p. 282)</li>
<li><strong>Ch. 8 (Building a Bitcoin Node):</strong> "Node discovery" (p. 313), "Fetching the blockchain" (p. 316), "Handling requests" (p. 322)</li>
<li><strong>Ch. 5 (Implementing a Bitcoin Library):</strong> "Serialization" (p. 256)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/rust-by-example/std/net/tcp.html">Rust by Example: TCP Server</a></li>
<li><a href="https://serde.rs/">Serde Guide</a></li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>vincenzopalazzo/lampo.rs</code> for Lightning networking. <code>lightningdevkit/rust-lightning</code> for <code>PeerManager</code>.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is length-prefix framing? Why is it better than newline delimiters for binary protocols?</li>
<li><strong>Q2:</strong> What is serialization? Why do distributed systems need to agree on a serialization format?</li>
<li><strong>Q3:</strong> Explain the difference between a <code>TcpListener</code> and a <code>TcpStream</code>. Which side uses each?</li>
<li><strong>Q4:</strong> What is a protocol state machine? Model a simple 3-way handshake for a hypothetical peer connection.</li>
<li><strong>Q5:</strong> Why should network I/O errors be <code>Result&lt;T, NetworkError&gt;</code> rather than <code>panic!</code>?</li>
<li><strong>Q6:</strong> In Bitcoin, why does a node need to broadcast transactions to multiple peers instead of just one?</li>
<li><strong>Q7:</strong> What is <code>serde</code>? How does a derive macro like <code>#[derive(Serialize)]</code> work at a high level?</li>
<li><strong>Q8:</strong> What is the difference between <code>read_exact</code> and <code>read</code> on a <code>TcpStream</code>? When might you use each?</li>
<li><strong>Q9:</strong> How does a protocol evolve over time without breaking existing nodes? What is backward compatibility?</li>
<li><strong>Q10:</strong> Look at the following snippet. A junior dev wrote this to read a 4-byte message length. What is the bug, and what corruption could it cause? Answer verbally.
<div class="code-q"><pre><code>let mut buf = [0u8; 4];
stream.read(&mut buf)?;
let length = u32::from_be_bytes(buf);</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>TCP Echo Server</strong> — Listen on 127.0.0.1:7878 and echo back lines with <code>ECHO:</code> prefix.</li>
<li><span class="badge badge-core">core</span> <strong>Simple Message Protocol — Binary Tags</strong> — Define <code>Ping</code>, <code>Pong</code>, <code>Text</code> enum with manual encode/decode.</li>
<li><span class="badge badge-core">core</span> <strong>Graceful Handshake Server</strong> — Accept <code>Version</code> messages. Respond <code>VERACK</code> or <code>REJECT</code>.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Length-Prefixed JSON Framing</strong> — Send 4-byte length + JSON payload. Read exactly length bytes back.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Protocol Version Negotiation</strong> — Client and server negotiate <code>min(client_version, server_version)</code>.</li>
<li><span class="badge badge-deep">deep</span> <strong>Protocol Parser Bug Hunt — Provided Snippet</strong> — Fix a buggy <code>read_message_length</code> that uses <code>read</code> instead of <code>read_exact</code>.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> TCP Echo Server</h4>
<p><strong>What you'll build:</strong> A TCP server that echoes back whatever it receives.</p>
<ol>
<li><code>cargo new week5_echo_server</code></li>
<li>Create <code>TcpListener</code> on <code>127.0.0.1:7878</code>.</li>
<li>Loop: accept connections, read a line, write back <code>ECHO: {line}</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Server: New connection from 127.0.0.1:54321<br>Client receives: ECHO: hello<br>Server: Connection closed</div>
<div class="verify"><strong>Verification:</strong> Integration test spawns server, connects, sends "hello", asserts response starts with "ECHO: hello".</div>
<div class="hints"><strong>Hints:</strong> Use <code>BufReader</code> to read lines from <code>TcpStream</code>.</div>

<h4><span class="badge badge-core">Core 2</span> Simple Message Protocol</h4>
<p><strong>What you'll build:</strong> A tiny binary protocol with tagged messages.</p>
<ol>
<li>Define <code>enum WireMessage { Ping { nonce: u64 }, Pong { nonce: u64 }, Text { content: String } }</code></li>
<li><code>encode(msg) -> Vec&lt;u8&gt;</code>: Ping→byte 0 + 8 bytes nonce. Pong→byte 1 + 8 bytes. Text→byte 2 + 4-byte length + UTF-8.</li>
<li><code>decode(buf) -> Result&lt;WireMessage, &'static str&gt;</code></li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>encode(Ping(42)) = [0, 0, 0, 0, 0, 0, 0, 42]<br>decode([0, ...]) -> Ok(Ping(42))<br>decode([99]) -> Err("unknown tag")</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> round-trips all variants and tests errors.</div>
<div class="hints"><strong>Hints:</strong> Use <code>nonce.to_be_bytes()</code> and <code>u64::from_be_bytes()</code>.</div>

<h4><span class="badge badge-core">Core 3</span> Graceful Handshake Server</h4>
<p><strong>What you'll build:</strong> A server that rejects unknown clients politely.</p>
<ol>
<li>Client sends <code>VERSION { version: u32, services: u64 }</code>.</li>
<li>Server responds <code>VERACK</code> if version == 1, else <code>REJECT</code> and closes.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Client sends Version(1, 0) -> receives "VERACK"<br>Client sends Version(2, 0) -> receives "REJECT: unsupported version", then connection closes</div>
<div class="verify"><strong>Verification:</strong> Integration test sends both versions and asserts responses.</div>
<div class="hints"><strong>Hints:</strong> Start with JSON over TCP. Use <code>serde_json</code>.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> Length-Prefixed JSON Framing</h4>
<p><strong>What you'll build:</strong> A protocol that sends 4-byte length + JSON payload.</p>
<ol>
<li><code>send_framed(stream, msg)</code>: serialize to JSON, send 4-byte big-endian length, send JSON bytes.</li>
<li><code>recv_framed(stream) -> Result&lt;WireMessage, &'static str&gt;</code>: read exactly 4 bytes for length, read exactly length bytes, deserialize.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Sent 27 bytes<br>Received: Ping { nonce: 42 }</div>
<div class="verify"><strong>Verification:</strong> Round-trip test over <code>TcpStream</code>.</div>
<div class="hints"><strong>Hints:</strong> <code>read_exact</code> is critical. <code>read</code> might return fewer bytes.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Protocol Version Negotiation</h4>
<p><strong>What you'll build:</strong> Client and server negotiate highest common version.</p>
<ol>
<li>Client sends max supported version.</li>
<li>Server responds with <code>min(client_version, server_version)</code>.</li>
<li>If negotiated &lt; 1, reject.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Client(3) + Server(2) -> negotiated version = 2<br>Client(0) + Server(2) -> Reject</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with mock streams.</div>
<div class="hints"><strong>Hints:</strong> This is how Bitcoin's <code>version</code>/<code>verack</code> handshake works.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Protocol Parser Bug Hunt</h4>
<p><strong>What you'll build:</strong> Fix a buggy network parser.</p>
<p>Buggy code:</p>
<pre><code>fn read_message_length(stream: &mut dyn Read) -> Result&lt;u32&gt; {
    let mut buf = [0u8; 4];
    stream.read(&mut buf)?;
    Ok(u32::from_be_bytes(buf))
}</code></pre>
<p>Write <code>read_message_length_fixed</code> using <code>read_exact</code>.</p>
<p>Write a test simulating a slow stream (returns 1 byte at a time).</p>
<div class="expected"><strong>Expected Output:</strong><br>Original parser with slow stream: returns 0 (wrong!)<br>Fixed parser with slow stream: returns 42 (correct!)</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts original returns 0 and fixed returns 42.</div>
<div class="hints"><strong>Hints:</strong> Implement a custom <code>Read</code> that returns 1 byte per call to simulate a slow network.</div>

</div>
</details>


<hr>
<h2 id="week6">Week 6 — Async Rust & High-Concurrency Services <span style="font-size:0.6em;color:var(--muted)">(The Event Loop)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do nodes handle thousands of simultaneous events without blocking?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 7 (Creating a CPU Miner):</strong> "Asynchronous Rust" (p. 282), "Futures and promises" (p. 283), "Tokio in miner" (p. 287)</li>
<li><strong>Ch. 8 (Building a Bitcoin Node):</strong> "Handling requests" (p. 322)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://tokio.rs/tokio/tutorial">Tokio Tutorial</a> — Chapters 1–3</li>
<li><a href="https://rust-lang.github.io/async-book/01_getting_started/01_chapter.html">Async/Await in Rust</a></li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>lightningdevkit/rust-lightning</code> for <code>BackgroundProcessor</code>. <code>vincenzopalazzo/lampo.rs</code> for async peer management.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is the difference between an OS thread and a Tokio task? When is a task more efficient?</li>
<li><strong>Q2:</strong> Explain <code>await</code>. What happens to the function's state while it is waiting?</li>
<li><strong>Q3:</strong> What is a future? Is it executed immediately when created, or does something else need to happen?</li>
<li><strong>Q4:</strong> What is backpressure? How does a bounded <code>tokio::sync::mpsc::channel(n)</code> help prevent memory exhaustion?</li>
<li><strong>Q5:</strong> What is <code>tokio::select!</code>? Give an example of when a Bitcoin node might use it.</li>
<li><strong>Q6:</strong> Why is holding a <code>std::sync::Mutex</code> across an <code>.await</code> point problematic? What is the alternative?</li>
<li><strong>Q7:</strong> What is cancellation safety? Why might a partially sent network message be dangerous if a task is cancelled?</li>
<li><strong>Q8:</strong> In a distributed system, why is non-blocking I/O essential for handling thousands of peer connections?</li>
<li><strong>Q9:</strong> How does <code>rust-lightning</code> run background tasks? What role does the <code>BackgroundProcessor</code> play?</li>
<li><strong>Q10:</strong> Look at the following async function. A junior dev says "this looks fine." What is the problem, and what symptom would you see in production? Answer verbally.
<div class="code-q"><pre><code>async fn load_config(path: &str) -> String {
    std::fs::read_to_string(path).unwrap()
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Async Echo Server (Tokio)</strong> — Convert the TCP echo server to Tokio with one task per client.</li>
<li><span class="badge badge-core">core</span> <strong>Async Timer Race</strong> — Race two <code>sleep</code> futures with <code>tokio::select!</code>. Assert fast timer always wins.</li>
<li><span class="badge badge-core">core</span> <strong>Async Broadcast Router</strong> — Use <code>tokio::sync::broadcast</code> to send 5 messages to 3 subscribers.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Connection Manager with Backpressure</strong> — Drop messages to slow peers using <code>try_send()</code> on bounded channels.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Timeout & Retry with Exponential Backoff</strong> — Retry TCP connection 3 times with <code>timeout</code> and increasing delays.</li>
<li><span class="badge badge-deep">deep</span> <strong>Async Flow Analysis — Provided Snippet</strong> — Identify the blocking-syscall bug in a provided async peer handler.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Async Echo Server</h4>
<p><strong>What you'll build:</strong> Convert Week 5's echo server to async using Tokio.</p>
<ol>
<li>Add <code>tokio = { version = "1", features = ["full"] }</code> to <code>Cargo.toml</code>.</li>
<li>Mark <code>main</code> as <code>#[tokio::main]</code>.</li>
<li>Use <code>tokio::net::TcpListener</code>. Spawn a task per connection.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>$ echo "async" | nc 127.0.0.1 7878<br>ECHO: async</div>
<div class="verify"><strong>Verification:</strong> Integration test spawns 3 concurrent clients, all receive correct echo.</div>
<div class="hints"><strong>Hints:</strong> <code>tokio::io::AsyncBufReadExt</code> provides <code>read_line()</code>. <code>tokio::spawn(async move { ... })</code> creates a task.</div>

<h4><span class="badge badge-core">Core 2</span> Async Timer Race</h4>
<p><strong>What you'll build:</strong> Race two timers using <code>tokio::select!</code>.</p>
<ol>
<li>Create two <code>tokio::time::sleep</code> futures: 100ms and 200ms.</li>
<li>Use <code>tokio::select!</code> to race them.</li>
<li>Run 5 times. Assert fast timer always wins.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Race 1: Fast timer won!<br>...<br>Race 5: Fast timer won!</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts all 5 races print "Fast timer won!" and elapsed &lt; 150ms.</div>
<div class="hints"><strong>Hints:</strong> <code>tokio::select!</code> picks whichever completes first. The other is cancelled.</div>

<h4><span class="badge badge-core">Core 3</span> Async Broadcast Router</h4>
<p><strong>What you'll build:</strong> A broadcast channel with one sender and multiple receivers.</p>
<ol>
<li>Create <code>tokio::sync::broadcast::channel::&lt;String&gt;(16)</code>.</li>
<li>Spawn 3 subscriber tasks. Each receives 5 messages.</li>
<li>Main sends 5 messages. Wait for all subscribers.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Subscriber 0 received: msg1<br>Subscriber 1 received: msg1<br>Subscriber 2 received: msg1<br>...<br>Subscriber 0 received: msg5<br>Subscriber 1 received: msg5<br>Subscriber 2 received: msg5</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts each subscriber received exactly 5 messages (total 15).</div>
<div class="hints"><strong>Hints:</strong> <code>let mut rx = tx.subscribe();</code> creates a subscriber. If the channel fills up, messages drop. That's backpressure!</div>

<h4><span class="badge badge-stretch">Stretch 4</span> Connection Manager with Backpressure</h4>
<p><strong>What you'll build:</strong> Drop messages to slow peers instead of crashing.</p>
<ol>
<li>Maintain <code>HashMap&lt;u32, tokio::sync::mpsc::Sender&lt;String&gt;&gt;</code>.</li>
<li>Each peer gets a bounded channel of capacity 4.</li>
<li>Use <code>try_send()</code>. If full, print <code>backpressure: peer {id}</code> and drop.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Peer 1 (fast): received all 10 messages<br>Peer 2 (slow): received 4 messages, then backpressure dropped 6</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts backpressure was triggered for the slow peer.</div>
<div class="hints"><strong>Hints:</strong> <code>try_send()</code> returns <code>Err(TrySendError::Full)</code> if the channel is full.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Timeout & Retry</h4>
<p><strong>What you'll build:</strong> An async connection function that retries with delays.</p>
<ol>
<li>Write <code>async fn connect_with_retry(addr: &str) -> Result&lt;TcpStream, &'static str&gt;</code>.</li>
<li>Try up to 3 times. Wait 100ms, then 200ms.</li>
<li>Use <code>tokio::time::timeout(Duration::from_millis(50), TcpStream::connect(addr))</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>connect_with_retry("127.0.0.1:9999") -> Err("connection failed after 3 attempts")<br>Total elapsed: ~300ms</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with a closed port asserts error and approximate timing (250–350ms).</div>
<div class="hints"><strong>Hints:</strong> <code>timeout</code> returns <code>Result&lt;Result&lt;TcpStream, _&gt;, Elapsed&gt;</code>. Handle both error cases.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Async Flow Analysis</h4>
<p><strong>What you'll build:</strong> Identify the executor-blocking bug in a provided snippet.</p>
<p>You are given:</p>
<pre><code>async fn handle_peer(stream: tokio::net::TcpStream) {
    let config = std::fs::read_to_string("config.txt").unwrap();
    println!("Config loaded: {}", config.len());
    sleep(Duration::from_millis(100)).await;
}
async fn handle_peers(mut incoming: tokio::net::TcpListener) {
    while let Ok((stream, _)) = incoming.accept().await {
        tokio::spawn(handle_peer(stream));
    }
}</code></pre>
<p>Write <code>fn identify_bug() -> String</code> and <code>fn explain_symptom() -> String</code>:</p>
<div class="expected"><strong>Expected Output:</strong><br>Bug: std::fs::read_to_string blocks the OS thread, freezing the async executor<br>Symptom: Under load, all peer connections would stall because the executor thread is blocked</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>
<div class="hints"><strong>Hints:</strong> The fix is <code>tokio::fs::read_to_string(path).await</code>. <code>std::fs::read_to_string</code> blocks the executor thread.</div>

</div>
</details>


<hr>
<h2 id="week7">Week 7 — Advanced Rust for Infrastructure <span style="font-size:0.6em;color:var(--muted)">(The Forge)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How is production-grade infrastructure software actually architected?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 4 (Taming Rust):</strong> "Lifetimes of owned vs unowned values" (p. 104), "Generic param bounds" (p. 120), "Dynamic dispatch" (p. 121)</li>
<li><strong>Ch. 5 (Keeping Rust Cultured):</strong> "Rustfmt" (p. 150), "Clippy" (p. 154)</li>
<li><strong>Ch. 5 (Implementing a Bitcoin Library):</strong> "Splitting up the big file" (p. 251), "Utility binaries" (p. 261)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://doc.rust-lang.org/book/ch19-03-advanced-traits.html">Rust Book: Advanced Traits</a> — Ch. 19.3</li>
<li><a href="https://doc.rust-lang.org/book/ch15-00-smart-pointers.html">Rust Book: Smart Pointers</a> — Ch. 15</li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>Bitshala-Incubator/silent-pay-wallet</code> for workspace structure. <code>fedimint/fedimint</code> for large-project crate organization.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is a trait object (<code>dyn Trait</code>)? When is it preferable to generics, and what is the performance tradeoff?</li>
<li><strong>Q2:</strong> Explain static dispatch vs. dynamic dispatch. Which produces faster code? Which produces smaller binaries?</li>
<li><strong>Q3:</strong> What is interior mutability? How does <code>RefCell</code> provide it for single-threaded code, and how does <code>Mutex</code> provide it for multi-threaded code?</li>
<li><strong>Q4:</strong> What is <code>Cow&lt;'a, str&gt;</code>? In what scenario is it useful for a protocol parser?</li>
<li><strong>Q5:</strong> What is a Cargo workspace? Why might a Bitcoin project split into <code>node-core</code>, <code>node-network</code>, and <code>node-storage</code> crates?</li>
<li><strong>Q6:</strong> Explain exponential backoff with jitter. Why is jitter critical in distributed systems retry logic?</li>
<li><strong>Q7:</strong> What are the <code>Send</code> and <code>Sync</code> traits? Why is <code>Rc&lt;T&gt;</code> not <code>Send</code>, and why is <code>RefCell&lt;T&gt;</code> not <code>Sync</code>?</li>
<li><strong>Q8:</strong> What is object safety? Why can't a trait with generic methods be made into a <code>dyn Trait</code>?</li>
<li><strong>Q9:</strong> How does <code>thiserror</code> reduce boilerplate compared to manually implementing <code>Display</code> and <code>Error</code>?</li>
<li><strong>Q10:</strong> Look at the following snippet. A junior dev wants to store different message handlers in a single <code>Vec</code>. What is the simplest way to make this work, and what is the runtime tradeoff compared to the generic version? Answer verbally.
<div class="code-q"><pre><code>trait Handler { fn handle(&self, msg: &str); }
struct EchoHandler;
struct UpperHandler;
// impl Handler for both...

fn main() {
    let handlers: Vec&lt;Box&lt;dyn Handler&gt;&gt; = vec![
        Box::new(EchoHandler),
        Box::new(UpperHandler),
    ];
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Workspace Refactor</strong> — Split Weeks 1–6 code into a Cargo workspace with <code>core</code>, <code>network</code>, and <code>app</code> crates.</li>
<li><span class="badge badge-core">core</span> <strong>Retry with Exponential Backoff + Jitter</strong> — A sync retry function with doubling delays and random 0–50ms jitter.</li>
<li><span class="badge badge-core">core</span> <strong>Dynamic Message Handler Router</strong> — A <code>HashMap&lt;String, Box&lt;dyn MessageHandler&gt;&gt;</code> that routes by prefix.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Smart Pointer Audit</strong> — Refactor <code>ContactBook</code> to <code>Arc&lt;Mutex&lt;HashMap&gt;&gt;</code> and document why.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Error Refactor with thiserror</strong> — Convert manual errors to a <code>thiserror</code> enum with <code>#[from]</code>. Run clippy.</li>
<li><span class="badge badge-deep">deep</span> <strong>Workspace Design Analysis — Provided Structure</strong> — Analyze a provided workspace layout and justify design decisions.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Workspace Refactor</h4>
<p><strong>What you'll build:</strong> Split your code into a proper Cargo workspace.</p>
<ol>
<li>Create <code>week7_workspace/Cargo.toml</code> with <code>members = ["core", "network", "app"]</code>.</li>
<li><code>core/</code>: structs, enums, traits from Weeks 1–3.</li>
<li><code>network/</code>: TCP server, protocol, async code from Weeks 5–6.</li>
<li><code>app/</code>: binary that imports both.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>$ cargo build<br>   Compiling core v0.1.0<br>   Compiling network v0.1.0<br>   Compiling app v0.1.0<br>    Finished dev target<br>$ cargo test --workspace<br>   Running 25 tests<br>   test result: ok</div>
<div class="verify"><strong>Verification:</strong> CI runs <code>cargo build</code> and <code>cargo test --workspace</code> successfully.</div>
<div class="hints"><strong>Hints:</strong> In <code>app/Cargo.toml</code>, add <code>core = { path = "../core" }</code> and <code>network = { path = "../network" }</code>.</div>

<h4><span class="badge badge-core">Core 2</span> Retry with Exponential Backoff + Jitter</h4>
<p><strong>What you'll build:</strong> A retry function with increasing delays and randomness.</p>
<ol>
<li>Write <code>fn retry&lt;F, T&gt;(mut f: F, max_attempts: u32) -> Result&lt;T, &'static str&gt;</code> where <code>F: FnMut() -> Option&lt;T&gt;</code>.</li>
<li>Wait 100ms, 200ms, 400ms, etc. (double each time).</li>
<li>Add random jitter 0–50ms using <code>rand::random_range(0..50)</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Function fails 2 times, succeeds on 3rd.<br>Total elapsed: ~300-450ms<br>Result: Ok("success")</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with a mock failing function asserts success and approximate timing (300–500ms).</div>
<div class="hints"><strong>Hints:</strong> Jitter prevents "thundering herd" — many clients retrying at the same instant.</div>

<h4><span class="badge badge-core">Core 3</span> Dynamic Message Handler Router</h4>
<p><strong>What you'll build:</strong> A router using trait objects.</p>
<ol>
<li>Define <code>trait MessageHandler: Send + Sync { fn handle(&self, msg: &str) -> String; }</code></li>
<li>Create <code>EchoHandler</code>, <code>UppercaseHandler</code>, <code>ReverseHandler</code>.</li>
<li><code>struct Router { handlers: HashMap&lt;String, Box&lt;dyn MessageHandler&gt;&gt; }</code></li>
<li><code>route(msg)</code> splits on <code>:</code>, looks up prefix, calls <code>handle</code>.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Route("echo:hello") -> "hello"<br>Route("upper:hello") -> "HELLO"<br>Route("rev:hello") -> "olleh"<br>Route("unknown:hello") -> "No handler"</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with 6 routing cases.</div>
<div class="hints"><strong>Hints:</strong> <code>Box&lt;dyn MessageHandler&gt;</code> uses dynamic dispatch (vtable lookup). Slower than generics but allows mixing types.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> Smart Pointer Audit</h4>
<p><strong>What you'll build:</strong> Refactor <code>ContactBook</code> for thread safety.</p>
<ol>
<li>Refactor to <code>Arc&lt;Mutex&lt;HashMap&lt;...&gt;&gt;&gt;</code>.</li>
<li>Add comments explaining: Why <code>Arc</code>? Why <code>Mutex</code>? What breaks with <code>Rc</code> or <code>RefCell</code>?</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>// Smart Pointer Choice Explanation:<br>// - Arc: Allows multiple threads to own the HashMap. Rc is not Send.<br>// - Mutex: Provides interior mutability across threads. RefCell is not Sync.</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> passes with refactored code.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Error Refactor with thiserror</h4>
<p><strong>What you'll build:</strong> Convert manual errors to <code>thiserror</code>.</p>
<ol>
<li>Add <code>thiserror = "1"</code> to <code>Cargo.toml</code>.</li>
<li>Define <code>AppError</code> with <code>#[error("...")]</code> and <code>#[from]</code> for <code>io::Error</code> and <code>ParseIntError</code>.</li>
<li>Refactor a Week 2–5 function to return <code>Result&lt;T, AppError&gt;</code>.</li>
<li>Run <code>cargo clippy</code>. Ensure zero warnings.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>$ cargo test<br>All tests pass<br>$ cargo clippy<br>    Finished dev target (no warnings)</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> passes; <code>cargo clippy</code> shows no warnings.</div>
<div class="hints"><strong>Hints:</strong> <code>#[from]</code> auto-generates <code>From</code> implementations. The <code>?</code> operator works seamlessly.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Workspace Design Analysis</h4>
<p><strong>What you'll build:</strong> Analyze a provided workspace layout.</p>
<p>You are given:</p>
<pre><code>my-node/
├── Cargo.toml          (workspace root)
├── core/
│   └── src/lib.rs      (types, traits, state machines)
├── network/
│   └── src/lib.rs      (TCP, protocol framing, peer management)
├── storage/
│   └── src/lib.rs      (disk persistence, caching)
└── app/
    └── src/main.rs     (binary, ties everything together)</code></pre>
<p>Write <code>fn analyze_workspace() -> [String; 3]</code>:</p>
<ul>
<li>[0]: Why is <code>core</code> a separate crate?</li>
<li>[1]: Why does <code>network</code> depend on <code>core</code> but not <code>storage</code>?</li>
<li>[2]: What would go wrong if everything were in a single <code>src/main.rs</code>?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Analysis: ["core is separate so multiple crates can share types without circular dependencies", "network needs core types but storage is an independent concern that only the app needs", "A single file would create tight coupling, slow compilation, and make testing impossible"]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>
<div class="hints"><strong>Hints:</strong> Workspaces enforce module boundaries. Separate crates compile in parallel.</div>

</div>
</details>


<hr>
<h2 id="week8">Week 8 — P2P Systems & Distributed Algorithms <span style="font-size:0.6em;color:var(--muted)">(The Swarm)</span></h2>

<div class="week-meta">
<strong>🎯 Central Question:</strong> <em>How do thousands of independent nodes become a coherent network?</em><br>
<strong>⏱️ Load:</strong> <span class="badge badge-core">Core ~2-3 hrs</span> <span class="badge badge-stretch">Stretch +1-2 hrs</span> <span class="badge badge-deep">Deep Dive optional</span>
</div>

<h3>📚 Reading Materials</h3>

<div class="reading">
<strong>📖 From <em>Building Bitcoin in Rust</em> (Primary):</strong>
<ul>
<li><strong>Ch. 8 (Building a Bitcoin Node):</strong> "Node discovery" (p. 313), "Fetching the blockchain" (p. 316), "Handling requests" (p. 322), "Wrapping up" (p. 334)</li>
<li><strong>Ch. 2 (Analyzing the Whitepaper):</strong> "Network" (p. 31), "Incentive" (p. 33), "Simplified Payment Verification" (p. 35), "Privacy" (p. 37), "Calculations" (p. 37)</li>
<li><strong>Ch. 7 (Creating a CPU Miner):</strong> "Networking" (p. 277)</li>
</ul>
<strong>🔗 Articles:</strong>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Gossip_protocol">Gossip Protocols</a></li>
<li><a href="https://en.wikipedia.org/wiki/Kademlia">Kademlia DHT</a></li>
<li><a href="https://en.wikipedia.org/wiki/CAP_theorem">CAP Theorem</a></li>
</ul>
</div>
<div class="repo-hint">
💡 <strong>Reference Repos (Hints Only):</strong> <code>lightningdevkit/rust-lightning</code> for gossip module. <code>fedimint/fedimint</code> for consensus and distributed state.
</div>


<h3>🎙️ 10 Questions (Primarily QnA)</h3>
<div class="question-list">
<ol>
<li><strong>Q1:</strong> What is an epidemic (gossip) protocol? Why is it efficient for broadcasting information in a large network?</li>
<li><strong>Q2:</strong> Explain the CAP theorem. Where does Bitcoin sit on the CAP triangle, and why?</li>
<li><strong>Q3:</strong> What is consistent hashing? Why do distributed databases like DynamoDB use it for partitioning data?</li>
<li><strong>Q4:</strong> In Kademlia, what is a k-bucket? Why is XOR distance used instead of Euclidean distance?</li>
<li><strong>Q5:</strong> Compare Raft and Nakamoto consensus. What problem does each solve, and what are their tradeoffs?</li>
<li><strong>Q6:</strong> How does a Bitcoin node discover peers without a central server? Describe the bootstrapping process.</li>
<li><strong>Q7:</strong> What is a heartbeat protocol? How do you balance detecting dead nodes quickly vs. avoiding false positives?</li>
<li><strong>Q8:</strong> What is anti-entropy in gossip protocols? Why is it necessary even with push-based gossip?</li>
<li><strong>Q9:</strong> In a distributed system, what is a quorum? Why might a system require a majority quorum for configuration changes?</li>
<li><strong>Q10:</strong> Look at the following function. A junior dev asks: "Why XOR? Why not just subtract?" What is the key mathematical property of XOR that makes it perfect for Kademlia's routing table? Answer verbally.
<div class="code-q"><pre><code>fn xor_distance(a: &[u8; 20], b: &[u8; 20]) -> [u8; 20] {
    let mut result = [0u8; 20];
    for i in 0..20 { result[i] = a[i] ^ b[i]; }
    result
}</code></pre></div></li>
</ol>
</div>

<h3>📝 Assignments Overview</h3>
<div class="assignment-overview">
<ul>
<li><span class="badge badge-core">core</span> <strong>Gossip Simulator</strong> — Simulate 10 nodes spreading a message. Count rounds and total messages sent.</li>
<li><span class="badge badge-core">core</span> <strong>Consistent Hash Ring</strong> — Distribute 100 keys across 3 nodes. Add a 4th node. Assert &lt; 25% keys moved.</li>
<li><span class="badge badge-core">core</span> <strong>Kademlia XOR Lookup</strong> — Calculate XOR distance. Find 2 closest peers to a target from 5 candidates.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Failure Detection Service</strong> — Heartbeat system marking nodes as Suspect then Dead based on elapsed time.</li>
<li><span class="badge badge-stretch">stretch</span> <strong>Consensus Comparison — Structured Q&A</strong> — Answer 5 structured questions about Raft vs. Nakamoto.</li>
<li><span class="badge badge-deep">deep</span> <strong>Gossip Flow Analysis — Provided Snippet</strong> — Analyze a provided <code>GossipStore</code> and identify data flow and design tradeoffs.</li>
</ul>
</div>

<details>
<summary>📖 <strong>Expand All Assignment Details</strong></summary>
<div class="details-inner">

<h4><span class="badge badge-core">Core 1</span> Gossip Simulator</h4>
<p><strong>What you'll build:</strong> Simulate how a message spreads through 10 nodes.</p>
<ol>
<li><code>struct Node { id: u32, has_message: bool }</code></li>
<li>Node 0 starts with the message.</li>
<li>Each round: every infected node picks 2 random neighbors and infects them.</li>
<li>Count total messages sent.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Round 0: 1 nodes have the message<br>Round 1: 3 nodes have the message<br>Round 2: 6 nodes have the message<br>Round 3: 10 nodes have the message<br>Total messages sent: ~18</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts all 10 nodes infected within 10 rounds. Total messages &lt; 30.</div>
<div class="hints"><strong>Hints:</strong> This is how Bitcoin transactions spread: each node tells a few peers.</div>

<h4><span class="badge badge-core">Core 2</span> Consistent Hash Ring</h4>
<p><strong>What you'll build:</strong> Distribute keys across servers with minimal reshuffling.</p>
<ol>
<li><code>struct HashRing { nodes: BTreeMap&lt;u64, String&gt; }</code></li>
<li>Each physical node gets 3 virtual nodes via hashing <code>format!("{name}#{i}")</code>.</li>
<li><code>get_node(key)</code>: hash key, find first virtual node ≥ hash (clockwise), wrap around.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Before: A=34, B=33, C=33<br>After adding D: A=26, B=25, C=25, D=24<br>Keys moved: 23/100</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts key migration count &lt; 30.</div>
<div class="hints"><strong>Hints:</strong> Use <code>DefaultHasher</code>. <code>BTreeMap::range(..=hash).next()</code> finds the first node ≥ hash.</div>

<h4><span class="badge badge-core">Core 3</span> Kademlia XOR Lookup</h4>
<p><strong>What you'll build:</strong> Find closest peers using XOR distance.</p>
<ol>
<li><code>fn xor_distance(a: &[u8; 20], b: &[u8; 20]) -> [u8; 20]</code>: byte-wise XOR.</li>
<li>5 peers: <code>[0x01; 20]</code>, <code>[0x02; 20]</code>, <code>[0x04; 20]</code>, <code>[0x08; 20]</code>, <code>[0x10; 20]</code>.</li>
<li>Target: <code>[0x03; 20]</code>. Find 2 closest.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Target: 03 03 03 ...<br>Closest: [0x02; 20] (distance: 01 01 01 ...)<br>         [0x01; 20] (distance: 02 02 02 ...)</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact peer IDs in correct order.</div>
<div class="hints"><strong>Hints:</strong> XOR has a magical property: <code>distance(a, b) == distance(b, a)</code>. The most significant differing bit determines distance.</div>

<h4><span class="badge badge-stretch">Stretch 4</span> Failure Detection Service</h4>
<p><strong>What you'll build:</strong> A heartbeat system with Suspect and Dead states.</p>
<ol>
<li><code>enum NodeState { Alive, Suspect, Dead }</code></li>
<li><code>struct FailureDetector { nodes: HashMap&lt;u32, (NodeState, Instant)&gt; }</code></li>
<li><code>heartbeat(id)</code> marks Alive. <code>check(id)</code>: &gt;300ms = Suspect, ≥500ms = Dead.</li>
</ol>
<div class="expected"><strong>Expected Output:</strong><br>Node 3 at 0ms: Alive<br>Node 3 at 300ms: Suspect<br>Node 3 at 500ms: Dead<br>Node 3 at 600ms: Dead</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> with simulated time asserts correct state transitions.</div>
<div class="hints"><strong>Hints:</strong> Use <code>std::time::Instant</code> and <code>elapsed()</code>. Mock time in tests by storing <code>Duration</code>.</div>

<h4><span class="badge badge-stretch">Stretch 5</span> Consensus Comparison — Structured Q&A</h4>
<p><strong>What you'll build:</strong> Answer structured questions about Raft vs. Nakamoto.</p>
<p>Write <code>fn consensus_qa() -> [String; 5]</code>:</p>
<ul>
<li>[0]: Which consensus is for trusted vs. untrusted networks?</li>
<li>[1]: Which is faster for finality?</li>
<li>[2]: Which requires known participants?</li>
<li>[3]: What resource does Nakamoto use to secure the network?</li>
<li>[4]: What failure mode does Raft protect against?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Q&A: ["Raft is for trusted networks, Nakamoto is for untrusted networks", "Raft is faster for finality because it commits immediately with quorum", "Raft requires known participants, Nakamoto is permissionless", "Nakamoto uses proof-of-work (computational energy) to secure the network", "Raft protects against crash faults (nodes going offline)"]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>
<div class="hints"><strong>Hints:</strong> Raft = leader-based, fast, known nodes, crash faults. Nakamoto = PoW, slow, permissionless, Byzantine faults.</div>

<h4><span class="badge badge-deep">Deep Dive 6</span> Gossip Flow Analysis</h4>
<p><strong>What you'll build:</strong> Analyze a provided gossip module.</p>
<p>You are given:</p>
<pre><code>struct GossipStore {
    channels: HashMap&lt;u64, ChannelInfo&gt;,
    updates: Vec&lt;u64&gt;,
}
struct ChannelInfo { node_a: String, node_b: String, capacity: u64 }
impl GossipStore {
    fn add_channel(&mut self, id: u64, info: ChannelInfo) {
        self.channels.insert(id, info);
        self.updates.push(id);
    }
    fn get_recent(&self, n: usize) -> Vec&lt;&ChannelInfo&gt; {
        self.updates.iter().rev().take(n)
            .filter_map(|id| self.channels.get(id))
            .collect()
    }
    fn forward_to_peers(&self, id: u64) {
        println!("Forwarding channel {} to peers", id);
    }
}</code></pre>
<p>Write <code>fn analyze_gossip_flow() -> [String; 4]</code>:</p>
<ul>
<li>[0]: What stores canonical channel info?</li>
<li>[1]: What tracks update order?</li>
<li>[2]: Why is <code>get_recent</code> useful for a syncing peer?</li>
<li>[3]: What would break if <code>updates</code> were a <code>HashSet</code>?</li>
</ul>
<div class="expected"><strong>Expected Output:</strong><br>Flow: ["channels HashMap stores the canonical ChannelInfo by id", "updates Vec tracks the order of updates for recency queries", "get_recent lets a syncing peer fetch only the latest N channels instead of the full set", "A HashSet would lose ordering, making recency queries impossible without a secondary index"]</div>
<div class="verify"><strong>Verification:</strong> <code>cargo test</code> asserts exact strings.</div>
<div class="hints"><strong>Hints:</strong> <code>HashMap</code> = O(1) lookup. <code>Vec</code> = preserves insertion order. <code>.rev().take(n)</code> gets the N most recent.</div>

</div>
</details>

<hr>

<h2 id="capstone">🎓 Post-Cohort Capstone <span class="badge badge-stretch">Optional · 4–6 Weeks</span></h2>

<p>Choose <strong>ONE</strong> track. This is where Bitcoin depth becomes primary.</p>

<ol>
  <li><strong>Mini Bitcoin Core:</strong> Blockchain, validation, PoW, difficulty (ties to the book's Ch. 5–7).</li>
  <li><strong>Mini Lightning Node:</strong> Use <code>lampo.rs</code> or <code>rust-lightning</code> to build a channel-opening service.</li>
  <li><strong>Mini Nostr Relay:</strong> Async event ingestion, filtering, and WebSocket broadcast.</li>
  <li><strong>Mini DHT / P2P Discovery:</strong> Implement a Kademlia-style lookup service with real networking.</li>
  <li><strong>Mini Distributed Log:</strong> Kafka-style partitioned log with producers/consumers.</li>
</ol>

<h2>📊 Report Card</h2>

<h3>Coverage of <em>Building Bitcoin in Rust</em></h3>
<table style="width:100%; border-collapse: collapse; margin: 1rem 0;">
  <thead>
    <tr style="border-bottom: 2px solid var(--border);">
      <th style="text-align:left; padding:0.6rem;">Book Part</th>
      <th style="text-align:left; padding:0.6rem;">Coverage</th>
      <th style="text-align:left; padding:0.6rem;">Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Prelude & Setup</td><td style="padding:0.6rem;">100%</td><td style="padding:0.6rem;">Toolchain, Cargo, workspaces covered.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 1: Introduction</td><td style="padding:0.6rem;">80%</td><td style="padding:0.6rem;">Rust/Bitcoin synergy discussed.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 2: Whitepaper</td><td style="padding:0.6rem;">60%</td><td style="padding:0.6rem;">Conceptual coverage; economics omitted.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 3: Setting Up</td><td style="padding:0.6rem;">100%</td><td style="padding:0.6rem;">Rustup, Cargo, crates covered.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 4: Taming Rust</td><td style="padding:0.6rem;">95%</td><td style="padding:0.6rem;">Ownership, traits, generics, closures, iterators.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 5: Keeping Rust Cultured</td><td style="padding:0.6rem;">100%</td><td style="padding:0.6rem;"><code>rustfmt</code>, <code>clippy</code>, <code>thiserror</code> integrated.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 6: Bitcoin Library</td><td style="padding:0.6rem;">55%</td><td style="padding:0.6rem;">Types, errors, serialization. Mining omitted.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 7: CPU Miner</td><td style="padding:0.6rem;">25%</td><td style="padding:0.6rem;">PoW concepts only; implementation deferred.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 8: Bitcoin Node</td><td style="padding:0.6rem;">120%</td><td style="padding:0.6rem;">Networking & P2P covered deeper than the book.</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Ch. 9: CLI/TUI Wallet</td><td style="padding:0.6rem;">30%</td><td style="padding:0.6rem;">Wallet state modeled; UI frameworks omitted.</td></tr>
  </tbody>
</table>

<p><strong>Net Book Value:</strong> ~75–80% of the book’s educational value, with the cohort going <em>deeper</em> on networking, async, and distributed systems.</p>

<h3>Distributed Systems Coverage</h3>
<table style="width:100%; border-collapse: collapse; margin: 1rem 0;">
  <thead>
    <tr style="border-bottom: 2px solid var(--border);">
      <th style="text-align:left; padding:0.6rem;">Concept</th>
      <th style="text-align:left; padding:0.6rem;">Week</th>
      <th style="text-align:left; padding:0.6rem;">Depth</th>
    </tr>
  </thead>
  <tbody>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">State Machines</td><td style="padding:0.6rem;">1</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Type-Safe APIs</td><td style="padding:0.6rem;">2</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Collections & Indexing</td><td style="padding:0.6rem;">3</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Parallel Processing</td><td style="padding:0.6rem;">4</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Protocol Design</td><td style="padding:0.6rem;">5</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Async I/O & Backpressure</td><td style="padding:0.6rem;">6</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Retry, Load Balancing</td><td style="padding:0.6rem;">7</td><td style="padding:0.6rem;">Medium</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Gossip, DHTs, CAP</td><td style="padding:0.6rem;">8</td><td style="padding:0.6rem;">Deep</td></tr>
    <tr style="border-bottom: 1px solid var(--border);"><td style="padding:0.6rem;">Consensus</td><td style="padding:0.6rem;">8</td><td style="padding:0.6rem;">Conceptual</td></tr>
  </tbody>
</table>

<p><strong>Net Systems Value:</strong> ~300% of the book’s distributed systems content. Bitcoin is treated as <em>one instance</em> of P2P design.</p>

</body>
</html>
