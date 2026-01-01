# Fidelity Editor Tooling - Rebranding Plan

## Overview

Transform the Ionide forks into distinct "Fidelity" branded tools that can be published independently without conflicting with the original Ionide ecosystem.

## Naming Convention

| Original | Fidelity Fork | Publisher/Org |
|----------|---------------|---------------|
| `ionide-vscode-fsharp` | `fidelity-vscode-fsharp` | `FidelityFramework` |
| `Ionide-vim` | `fidelity-vim-fsharp` | `FidelityFramework` |
| `ionide-analyzers` | `fidelity-native-analyzers` | `FidelityFramework` |
| `FsAutoComplete` | `FsNativeAutoComplete` | `FidelityFramework` |

## VSCode Extension (`fidelity-vscode-fsharp`)

### package.json Changes

```json
{
  "name": "fidelity-fsharp",
  "displayName": "Fidelity for F#",
  "publisher": "FidelityFramework",
  "description": "F# Native Language Support, powered by FsNativeAutoComplete",
  "repository": {
    "type": "git",
    "url": "https://github.com/FidelityFramework/fidelity-vscode-fsharp.git"
  }
}
```

### Activation Events - Add Native Support

```json
"activationEvents": [
  "workspaceContains:**/*.fs",
  "workspaceContains:**/*.fsproj",
  "workspaceContains:**/*.fsx",
  "workspaceContains:**/*.fidproj",  // NEW: Native project files
  "workspaceContains:**/*.fsnx",     // NEW: Native script files
  "workspaceContains:**/*.sln"
]
```

### File Associations - Add Native Types

```json
"languages": [
  {
    "id": "fsharp",
    "extensions": [".fs", ".fsi", ".fsx", ".fsscript", ".fsnx"]
  },
  {
    "id": "toml",
    "extensions": [".fidproj"]
  }
]
```

### Configuration Namespace

Change all configuration keys from `FSharp.*` to `fidelity.*`:
- `fidelity.fsac.path` → Path to FSNAC
- `fidelity.enableNativeSupport` → Enable .fidproj support
- `fidelity.nativeProjectPath` → Custom Alloy path

### Internal Namespaces

- `Ionide.VSCode.FSharp` → `Fidelity.VSCode.FSharp`
- Output channel: "Ionide" → "Fidelity"
- View containers: `ionide.*` → `fidelity.*`

## Vim/Neovim Plugin (`fidelity-vim-fsharp`)

### Plugin Structure

```
fidelity-vim-fsharp/
├── autoload/
│   └── fidelity.vim      # Was: fsharp.vim
├── lua/
│   └── fidelity/         # Was: ionide/
│       └── init.lua
├── plugin/
│   └── fidelity.vim      # Was: ionide.vim
├── ftplugin/
│   └── fsharp.vim        # Keep - it's for filetype, not plugin name
└── ftdetect/
    └── fsharp.vim        # Add .fidproj, .fsnx detection
```

### Configuration Variables

Change all `g:fsharp#*` and `g:ionide_*` to `g:fidelity#*`:
- `g:fidelity#fsac_path` → Path to FSNAC
- `g:fidelity#backend` → LSP backend selection
- `g:fidelity#enable_native` → Enable native project support

### Lua Module

```lua
-- Was: require("ionide")
-- Now: require("fidelity")
local fidelity = require("fidelity")
```

## NuGet/Package Publishing

### VSCode Marketplace

- Publisher: `FidelityFramework`
- Extension ID: `FidelityFramework.fidelity-fsharp`
- Gallery icon and branding

### Vim Plugin Managers

Works with:
- vim-plug: `Plug 'FidelityFramework/fidelity-vim-fsharp'`
- packer.nvim: `use 'FidelityFramework/fidelity-vim-fsharp'`
- lazy.nvim: `{ "FidelityFramework/fidelity-vim-fsharp" }`

## Coexistence Strategy

Both Ionide and Fidelity can be installed side-by-side:
- Different publisher/package names
- Different configuration namespaces
- Different output channels
- Different file associations (Fidelity handles .fidproj/.fsnx, Ionide doesn't)

Users can:
1. Use Ionide for .NET projects
2. Use Fidelity for native projects
3. Use Fidelity for everything (it delegates to FCS for .fsproj)

## Implementation Order

1. **Phase 1: Identity** - Rename packages, namespaces, configuration keys
2. **Phase 2: Native Support** - Add .fidproj/.fsnx recognition
3. **Phase 3: FSNAC Integration** - Point to FSNAC binary, add native config
4. **Phase 4: Testing** - Validate both editors work with Firefly samples
5. **Phase 5: Publishing** - Set up VSCode Marketplace and GitHub releases
