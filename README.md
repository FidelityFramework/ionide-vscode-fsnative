# Ionide for F# (Native)

**F# Native Language Support for Visual Studio Code**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)

A fork of [Ionide-VSCode](https://github.com/ionide/ionide-vscode-fsharp) enhanced for native F# development with the Fidelity framework.

## Overview

Ionide for F# (Native) provides rich IDE support for native F# compilation, powered by [FsNativeAutoComplete (FSNAC)](https://github.com/FidelityFramework/FsNativeAutoComplete).

While the original Ionide extension assumes .NET projects with `.fsproj` and NuGet packages, Ionide.FsNative understands:

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

Search for "Ionide for F# (Native)" in the VS Code Extensions marketplace.

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
| **Ionide.FsNative-VSCode** | This extension |
| [Ionide.FsNative-Vim](https://github.com/FidelityFramework/Ionide-vim-fsnative) | Vim/Neovim plugin |
| [Alloy](https://github.com/FidelityFramework/Alloy) | Native standard library |

## Coexistence with Ionide

Ionide.FsNative can be installed alongside Ionide:
- Different extension IDs and configuration namespaces
- Ionide.FsNative handles `.fidproj`/`.fsnx`, Ionide doesn't recognize them
- Use Ionide for pure .NET, Ionide.FsNative for native or mixed workspaces

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

## Acknowledgments

This project is a fork of [Ionide-VSCode](https://github.com/ionide/ionide-vscode-fsharp). We're grateful to the Ionide maintainers and the F# community for creating the foundation we build upon.

## License

MIT License - see [LICENSE.md](LICENSE.md)

---

*Native F# development, familiar IDE experience.*
