# lattice-vscode

A hard fork of [ionide-vscode-fsharp](https://github.com/ionide/ionide-vscode-fsharp) at 7.30.0, relabelled.
It is Ionide with a partial label change: the manifest says `lattice-fsharp`, the code registers `fsharp.*`
commands and views under the intermediate name, the build says `ionide`, and the extension bundles upstream
`fsautocomplete` from NuGet. It has no capability beyond Ionide, and the features an earlier README promised
(`.fidproj` projects, native type display, SRTP witnesses, platform bindings, native diagnostic codes) are not
implemented.

**Disposition.** Per the consumer contract (`~/repos/clef/docs/fidelity/phg/Lattice_Consumer_Contract.md`,
§6), this client is reduced to a `LanguageClient` registration over the Lattice server plus the Clef-specific
views the contract names (proof lens and ledger view, reachability dimming, a project explorer over the
`.fidproj` model served by CCS). F# Interactive, MSBuild tasks, the `coreclr` debugger launch, the .NET test
explorer, F1 help and the FSAC settings block are retired: Clef has no REPL, no MSBuild, no .NET runtime, and
the editor decides no diagnostic policy.

Upstream license and attribution: see `LICENSE.md`. Ionide is the work of the Ionide community.
