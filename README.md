# rule-builder

A CLI tool that keeps AI agent rule files in sync. It traverses directories, finds `.ai-rules` folders, and generates `AGENTS.md` and `Claude.md` files at each level from the rules contained within.

## Install

Clone the repo and add `rule-builder` to your PATH, or run it directly:

```bash
git clone https://github.com/yourusername/rule-builder.git
cd rule-builder

# Option 1: symlink into your PATH
ln -s "$(pwd)/rule-builder" /usr/local/bin/rule-builder

# Option 2: run directly
./rule-builder
```

## Usage

Run `rule-builder` from any directory. It will recursively find all `.ai-rules/` folders and generate output files.

```bash
cd your-project
rule-builder
```

### How it works

1. Recursively walks subdirectories starting from the current working directory
2. At each directory containing a `.ai-rules/` folder:
   - Reads all `.md` files in `.ai-rules/` (sorted alphabetically for deterministic output)
   - Concatenates their contents with a blank line separator
   - Writes the result to `AGENTS.md` in the same directory
   - Copies `AGENTS.md` to `Claude.md` in the same directory
3. Prints a summary of what was generated

### Example

Given this structure:

```
my-project/
├── .ai-rules/
│   ├── coding-style.md
│   └── testing.md
└── backend/
    └── .ai-rules/
        └── api-guidelines.md
```

Running `rule-builder` produces:

```
my-project/
├── .ai-rules/
│   ├── coding-style.md
│   └── testing.md
├── AGENTS.md          ← generated (coding-style.md + testing.md)
├── Claude.md          ← generated (copy of AGENTS.md)
└── backend/
    └── .ai-rules/
    │   └── api-guidelines.md
    ├── AGENTS.md      ← generated (api-guidelines.md)
    └── Claude.md      ← generated (copy of AGENTS.md)
```

Non-`.md` files in `.ai-rules/` are ignored.

## Tests

```bash
./test-rule-builder
```
