# Lattice for F#

**F# Native Language Support for Visual Studio Code**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)

A hard fork of [Ionide-VSCode](https://github.com/ionide/ionide-vscode-fsharp) for polyglot systems programming with F# Native, MLIR, LLVM, F*, Lua, and C.

## Overview

Lattice provides rich IDE support for native F# compilation, powered by [FsNativeAutoComplete (FSNAC)](https://github.com/FidelityFramework/FsNativeAutoComplete).

While the original Ionide extension assumes .NET projects with `.fsproj` and NuGet packages, Lattice understands:

- **`.fidproj`** - Native F# project manifests (TOML format)
- **`.fsnx`** - Native F# script files
- **Native type semantics** - UTF-8 strings, value-type options, platform words

## Requirements

- .NET SDK 9.0+ (for FSNAC with FNCS support)
- VS Code 1.52+

## Installation

### From VSIX (Development)

```bash
# Build the extension
./build.sh

# Install the generated .vsix file
code --install-extension release/ionide-fsnative-*.vsix
```

### From Marketplace (Coming Soon)

Search for "Lattice for F#" in the VS Code Extensions marketplace.

## Features

### Standard F# Development

All features from Ionide work as expected for `.fsproj` projects:
- Syntax highlighting
- Auto completions
- Error highlighting and quick fixes
- Tooltips with type information
- Method parameter hints
- Go to Definition / Peek Definition
- Find all references
- Rename refactoring
- Document symbols
- Code formatting (Fantomas)
- F# Interactive integration
- Solution Explorer
- MSBuild integration

### Native F# Development

Additional features for `.fidproj` projects:
- **Native type display** - See UTF-8 string layout, voption semantics
- **SRTP resolution** - View resolved trait implementations
- **Platform bindings** - Understand which functions map to syscalls
- **FS8xxx diagnostics** - Native-specific error codes

## Project Files

### Standard (.fsproj)

Works exactly like Ionide - MSBuild project files with NuGet dependencies.

### Native (.fidproj)

TOML-based project manifests for native compilation:

```toml
[package]
name = "my_project"

[dependencies]
alloy = { path = "../alloy/src" }

[build]
sources = ["Program.fs"]
output = "my_project"
output_kind = "console"
```

## The Fidelity Ecosystem

| Project | Role |
|---------|------|
| [Firefly](https://github.com/FidelityFramework/Firefly) | AOT compiler |
| [FSNAC](https://github.com/FidelityFramework/FsNativeAutoComplete) | Language server |
| **lattice-vscode** | This extension |
| [lattice-vim](https://github.com/FidelityFramework/lattice-vim) | Vim/Neovim plugin |
| [Alloy](https://github.com/FidelityFramework/Alloy) | Native standard library |

## Coexistence with Ionide

Lattice can be installed alongside Ionide:
- Different extension IDs and configuration namespaces
- Lattice handles `.fidproj`/`.fsnx`, Ionide doesn't recognize them
- Use Ionide for pure .NET, Lattice for native or mixed workspaces

## Building

```bash
# Restore tools
dotnet tool restore

# Build
./build.sh
```

## Contributing

Contributions are welcome! Areas of interest:
- Testing with Fidelity projects
- FSNAC integration improvements
- Documentation and examples

## Heritage

This project is a hard fork of [Ionide-VSCode](https://github.com/ionide/ionide-vscode-fsharp), created by Krzysztof Cieślak and maintained by the Ionide community.

See [IONIDE_HERITAGE.md](IONIDE_HERITAGE.md) for the full story of the ion → lattice progression.

## Acknowledgments

We are deeply grateful to Krzysztof Cieślak and all Ionide contributors for creating the exceptional foundation we build upon. Lattice serves a fundamentally different use case (native/freestanding F# compilation) and does not compete with Ionide.

## License

MIT License - see [LICENSE.md](LICENSE.md)

---

*Native F# development, familiar IDE experience.*
