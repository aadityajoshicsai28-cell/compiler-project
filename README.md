# Compiler Visualizer

An interactive React application for exploring how source code moves through a compiler pipeline. Enter a short expression, run an analysis, and inspect the tokens, syntax tree, semantic information, intermediate representation, optimizations, and generated assembly-style instructions side by side.

**Live demo:** [compiler-project.vercel.app](https://compiler-project.vercel.app/)

## What It Does

The visualizer presents six stages of compilation:

1. **Lexical analysis** - Splits the input into tokens.
2. **Syntax analysis** - Builds a text representation and an interactive AST.
3. **Semantic analysis** - Shows inferred types and a symbol table.
4. **Intermediate code generation** - Produces Three-Address Code (TAC).
5. **Code optimization** - Compares the intermediate code with a reduced form.
6. **Code generation** - Converts the optimized instructions into assembly-style output.

The editor includes example inputs for assignments, arithmetic expressions, conditionals, loops, nested expressions, and function calls. It also validates empty input, unbalanced brackets, unclosed strings, suspicious patterns, and inputs longer than 1,000 characters.

## How Analysis Works

The app supports two analysis modes:

- **Groq mode:** When `VITE_GROQ_API_KEY` is configured, the app sends the input to the Groq Chat Completions API and asks for structured compiler-phase data.
- **Local fallback:** When no key is configured, or when the API request fails, the built-in parser generates tokens, an AST, semantic information, TAC, optimized TAC, and assembly-style output in the browser.

The fallback is intentionally educational rather than a complete compiler for a production programming language. It is best suited to short expressions and examples using identifiers, numeric or character literals, assignments, arithmetic and logical operators, comparisons, ternaries, and function calls.

## Quick Start

### Requirements

- Node.js 18 or newer
- npm

### Install and run

```bash
git clone https://github.com/aadityajoshicsai28-cell/compiler-project.git
cd compiler-project
npm install
npm run dev
```

Open the local URL printed by Vite, usually `http://localhost:5173`.

### Optional Groq configuration

Create a `.env` file in the project root:

```env
VITE_GROQ_API_KEY=your_groq_api_key
```

Restart the development server after changing environment variables. Do not commit `.env` or expose a production secret in client-side code. Without this variable, the application still works using its local fallback parser.

## Available Commands

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server. |
| `npm run build` | Create a production build in `dist/`. |
| `npm run preview` | Serve the production build locally. |
| `npm run lint` | Run ESLint across the project. |

## Project Structure

```text
src/
├── App.jsx                    # Routes and main visualizer screen
├── index.css                  # Global styles and Tailwind entrypoint
├── main.jsx                   # React application entrypoint
├── components/
│   ├── CodeInput.jsx          # Editor, examples, validation, and actions
│   ├── PhaseVisualization.jsx # Six-phase result layout
│   ├── TokenTable.jsx         # Lexical analysis output
│   ├── ASTVisualization.jsx   # Interactive AST view
│   ├── TACDisplay.jsx         # Three-Address Code output
│   ├── CodeOptimizer.jsx      # Optimization comparison
│   ├── AssemblyCode.jsx       # Generated target instructions
│   ├── HowItWorks.jsx         # Compiler phases guide
│   └── Footer.jsx             # Footer content
├── hooks/
│   └── useCompiler.js         # Analysis state and fallback behavior
└── services/
    └── groqService.js         # Groq request and local compiler helpers
```

## Technology

- React 19 and React DOM
- Vite
- Tailwind CSS 4
- React Router
- React Icons
- D3 and React D3 Tree
- Groq API, optionally used for AI-assisted analysis

## Limitations

- The application is a teaching aid, not a full language compiler.
- The local parser uses simplified heuristics and does not implement a complete grammar.
- Semantic types in fallback mode are inferred as `auto` and symbols are shown in global scope.
- Generated assembly is illustrative and is not targeted to a specific real processor.
- Groq mode requires a valid API key and network access.

## Contributing

1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-change`.
3. Install dependencies with `npm install`.
4. Make and test your changes with `npm run lint` and `npm run build`.
5. Commit and push your branch.
6. Open a pull request with a clear description of the change.

Bug reports and feature requests are welcome through the [issue tracker](https://github.com/aadityajoshicsai28-cell/compiler-project/issues).

## License

This project is available under the [MIT License](LICENSE).

## Author

[Aaditya Joshi](https://github.com/aadityajoshicsai28-cell)

## Acknowledgements

- [React D3 Tree](https://github.com/bkrem/react-d3-tree) for AST visualization.
- [Groq](https://groq.com/) for the optional AI analysis service.
