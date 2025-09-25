# Strukt

**Strukt** is a next-generation **Diagrams-as-Code language and engine**.  
Write simple, composable text → get clean, verifiable, scalable diagrams (SVG/PNG/PDF).  
Built with **Rust** (core engine) + **TypeScript** (tooling & integrations).

---

## Why Strukt?

Existing tools (Mermaid, PlantUML, D2) are powerful, but they hit limits:
- **Fragile layouts** → nodes jump around on small edits.
- **Poor scale** → slow or unreadable with thousands of nodes.
- **One-way** → DSL to diagram, no round-trip editing.
- **No verification** → invalid edges/structures silently render.

Strukt aims to be **x100 better** by being:

- ⚡ **Fast & Scalable** – Rust core + incremental WASM layouts; handles 10k nodes.  
- 🛡 **Verifiable** – type system & constraints to catch invalid diagrams.  
- 🔄 **Round-Trippable** – DSL ↔ visual editor sync with stable IDs.  
- 🧩 **Composable** – core IR + modules (flow, sequence, state, ERD, etc.).  
- 🎨 **Themeable** – JSON/CSS tokens for colors, fonts, shapes, dark/print modes.  
- 🌐 **Everywhere** – CLI, MDX/Docusaurus, VSCode, HTTP API, Studio editor.  

---

## Quick Example

```strukt
diagram Checkout direction: TB

group Web {
  UI: "UI"
  GW: "Gateway"
}

SVC: "Payment Service" class: primary
DB: "Ledger DB"

UI -> GW label: click
GW -> SVC label: POST /pay
SVC -> DB label: write
````

Generates →

![Example diagram](docs/assets/checkout-example.svg)

---

## Getting Started

### CLI

```bash
# Install (future)
cargo install strukt-cli

# Render
strukt render flow.strukt -o out.svg
```

### Node / TypeScript

```bash
npm install @strukt/core

import { render } from "@strukt/core";

const svg = await render(`
A: "Login"
B: "MFA"
A -> B label: "OTP"
`);
console.log(svg);
```

### MDX / Docs

Use `@strukt/mdx` to render code fences:

<pre>
```strukt
A -> B
```
</pre>

---

## Roadmap

* [x] Core IR (Rust, serde)
* [x] Parser (pest/chumsky)
* [ ] WASM build (`libstrukt`)
* [ ] CLI (`strukt render ...`)
* [ ] MDX/Docusaurus plugin
* [ ] VSCode extension
* [ ] Strukt Studio (visual editor)
* [ ] Plugin API (shapes, themes, constraints)
* [ ] Cloud service (HTTP render, collab)

See [ROADMAP.md](docs/ROADMAP.md) for details.

---

## Project Structure

```
/strukt
  /core        # Rust lib (AST, IR, layout, render)
  /cli         # Rust CLI
  /bindings    # NPM wrapper (wasm-bindgen)
  /packages
    /mdx       # MDX plugin
    /vscode    # VSCode extension
    /react     # React components
  /docs        # Documentation + examples
```

---

## Philosophy

Strukt isn’t just another DSL.
It’s a **Diagram Operating System**:

* One **language** for all diagram types.
* One **core** for parsing, layout, validation.
* Multiple **frontends**: text, visual, API.
* Extensible through plugins, constraints, themes.

> **Goal:** become the GraphQL of diagrams.
> Write once → render anywhere → verify always.

---

## License

MIT (core + tooling).
Commercial licensing available for enterprise (Strukt Studio, Cloud).

---

## Contributing

Contributions welcome!
Check out [CONTRIBUTING.md](CONTRIBUTING.md) for setup instructions.

---

## Links

* Website: [https://strukt.dev](https://strukt.dev) (coming soon)
* Docs: [https://docs.strukt.dev](https://docs.strukt.dev)
* Playground: [https://play.strukt.dev](https://play.strukt.dev)
