# Features

This table gives a summary of the features that HLS supports.
Many of these are standard LSP features, but a lot of special features are provided as [code actions](#code-actions) and [code lenses](#code-lenses).

| Feature                                             | [LSP method](./what-is-hls.md#lsp-terminology)                                                    |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------|
| [Diagnostics](#diagnostics)                         | `textDocument/publishDiagnostics`                                                                 |
| [Hovers](#hovers)                                   | `textDocument/hover`                                                                              |
| [Jump to definition](#jump-to-definition)           | `textDocument/definition`                                                                         |
| [Jump to type definition](#jump-to-type-definition) | `textDocument/typeDefinition`                                                                     |
| [Find references](#find-references)                 | `textDocument/references`                                                                         |
| [Completions](#completions)                         | `textDocument/completion`                                                                         |
| [Formatting](#formatting)                           | `textDocument/formatting`, `textDocument/rangeFormatting`                                         |
| [Document symbols](#document-symbols)               | `textDocument/documentSymbol`                                                                     |
| [Workspace symbols](#workspace-symbols)             | `workspace/symbol`                                                                                |
| [Call hierarchy](#call-hierarchy)                   | `textDocument/prepareCallHierarchy`, `callHierarchy/incomingCalls`, `callHierarchy/outgoingCalls` |
| [Highlight references](#highlight-references)       | `textDocument/documentHighlight`                                                                  |
| [Code actions](#code-actions)                       | `textDocument/codeAction`                                                                         |
| [Code lenses](#code-lenses)                         | `textDocument/codeLens`                                                                           |
| [Selection range](#selection-range)                 | `textDocument/selectionRange` |

The individual sections below also identify which [HLS plugin](./what-is-hls.md#hls-plugins) is responsible for providing the given functionality, which is useful if you want to raise an issue report or contribute!
Additionally, not all plugins are supported on all versions of GHC, see the [GHC version support page](supported-versions.md) for details.

## Diagnostics

### GHC compiler errors and warnings

Provided by: `ghcide`

Provides errors and warnings from GHC as diagnostics.

### Hlint hints

Provided by: `hls-hlint-plugin`

Provides hlint hints as diagnostics.

## Hovers

Provided by: `ghcide`

Type information and documentation on hover, [including from local definitions](./configuration.md#how-to-show-local-documentation-on-hover).

## Jump to definition

Provided by: `ghcide`

Jump to the definition of a name.

Known limitations:

- Only works for [local definitions](https://github.com/haskell/haskell-language-server/issues/708).

## Jump to type definition

Provided by: `ghcide`

Known limitations:

- Only works for [local definitions](https://github.com/haskell/haskell-language-server/issues/708).

## Find references

Provided by: `ghcide`

Find references to a name within the project.

## Completions

### Code completions

Provided by: `ghcide`

- Completion of names from qualified imports.
- Completion of names from non-imported modules.

### Pragma completions

Provided by: `hls-pragmas-plugin`

Completions for language pragmas.

## Formatting

Format your code with various Haskell code formatters.

| Formatter       | Provided by                  |
|-----------------|------------------------------|
| Brittany        | `hls-brittany-plugin`        |
| Floskell        | `hls-floskell-plugin`        |
| Fourmolu        | `hls-fourmolu-plugin`        |
| Ormolu          | `hls-ormolu-plugin`          |
| Stylish Haskell | `hls-stylish-haskell-plugin` |

## Document symbols

Provided by: `ghcide`

Provides listing of the symbols defined in a module, used to power outline displays.

## Workspace symbols

Provided by: `ghcide`

Provides listing of the symbols defined in the project, used to power searches.

## Call hierarchy

Provided by: `hls-call-hierarchy-plugin`

Shows ingoing and outgoing calls for a function.

![Call Hierarchy in VSCode](https://github.com/haskell/haskell-language-server/raw/2857eeece0398e1cd4b2ffb6069b05c4d2308b39/plugins/hls-call-hierarchy-plugin/call-hierarchy-in-vscode.gif)

## Highlight references

Provided by: `ghcide`

Highlights references to a name in a document.

## Code actions

### Insert missing pragmas

Provided by: `hls-pragma-plugin`

Code action kind: `quickfix`

Inserts missing pragmas needed by GHC.

### Apply Hlint fixes

Provided by: `hls-hlint-plugin`

Code action kind: `quickfix`

Applies hints, either individually or for the whole file.
Uses [apply-refact](https://github.com/mpickering/apply-refact).

![Hlint Demo](https://user-images.githubusercontent.com/54035/110860028-8f9fa900-82bc-11eb-9fe5-6483d8bb95e6.gif)

Known limitations:

- May have strange behaviour in files with CPP, since `apply-refact` does not support CPP.

### Make import lists fully explicit

Provided by: `hls-explicit-imports-plugin`

Code action kind: `quickfix.literals.style`

Make import lists fully explicit (same as the code lens).

### Qualify imported names

Provided by: `hls-qualify-imported-names-plugin`

Code action kind: `quickfix`

Rewrites imported names to be qualified.

![Qualify Imported Names Demo](../plugins/hls-qualify-imported-names-plugin/qualify-imported-names-demo.gif)

For usage see the ![readme](../plugins/hls-qualify-imported-names-plugin/README.md).

### Refine import

Provided by: `hls-refine-imports-plugin`

Code action kind: `quickfix.import.refine`

Refines imports to more specific modules when names are re-exported (same as the code lens).

### Add missing class methods

Provided by: `hls-class-plugin`

Code action kind: `quickfix`

Adds placeholders for missing class methods in a class instance definition.

### Unfold definition

Provided by: `hls-retrie-plugin`

Code action kind: `refactor.extract`

Extracts a definition from the code.

### Fold definition

Provided by: `hls-retrie-plugin`

Code action kind: `refactor.inline`

Inlines a definition from the code.

![Retrie Demo](https://i.imgur.com/Ev7B87k.gif)

### Insert contents of Template Haskell splice

Provided by: `hls-splice-plugin`

Code action kind: `refactor.rewrite`

Evaluates a Template Haskell splice and inserts the resulting code in its place.

### Convert numbers to alternative formats

Provided by: `hls-alternate-number-format-plugin`

Code action kind: `quickfix.literals.style`

Converts numeric literals to different formats.

![Alternate Number Format Demo](../plugins/hls-alternate-number-format-plugin/HLSAll.gif)

### Add Haddock comments

Provided by: `hls-haddock-comments-plugin`

Code action kind: `quickfix`

Adds Haddock comments for function arguments.

### Wingman

Status: Not supported on GHC 9.2

Provided by: `hls-tactics-plugin`

Provides a variety of code actions for interactive code development, see <https://haskellwingman.dev/> for more details.

![Wingman Demo](https://user-images.githubusercontent.com/307223/92657198-3d4be400-f2a9-11ea-8ad3-f541c8eea891.gif)

## Code lenses

### Add type signature

Provided by: `ghcide`

Shows the type signature for bindings without type signatures, and adds it with a click.

### Evaluation code snippets in comments

Provided by: `hls-eval-plugin`

Evaluates code blocks in comments with a click. [Tutorial](https://github.com/haskell/haskell-language-server/blob/master/plugins/hls-eval-plugin/README.md).

![Eval Demo](https://raw.githubusercontent.com/haskell/haskell-language-server/master/plugins/hls-eval-plugin/demo.gif)

### Make import lists fully explicit code lens

Provided by: `hls-explicit-imports-plugin`

Shows fully explicit import lists and rewrites them with a click (same as the code action).

![Imports code lens Demo](https://imgur.com/pX9kvY4.gif)

### Refine import code lens

Provided by: `hls-refine-imports-plugin`

Shows refined imports and applies them with a click (same as the code action).

### Fix module names

Provided by: `hls-module-name-plugin`

Shows module name matching file path, and applies it with a click.

![Module Name Demo](https://user-images.githubusercontent.com/54035/110860755-78ad8680-82bd-11eb-9845-9ea4b1cc1f76.gif)

## Selection range

Provided by: `hls-selection-range-plugin`

Provides haskell specific
[shrink/expand selection](https://code.visualstudio.com/docs/editor/codebasics#shrinkexpand-selection)
support.

![Selection range demo](https://user-images.githubusercontent.com/16440269/150301502-4c002605-9f8d-43f5-86d3-28846942c4ff.mov)

## Missing features

The following features are supported by the LSP specification but not implemented in HLS.
Contributions welcome!

| Feature                | Status                                                                                   | [LSP method](./what-is-hls.md#lsp-terminology)      |
|------------------------|------------------------------------------------------------------------------------------|-----------------------------------------------------|
| Signature help         | Unimplemented                                                                            | `textDocument/signatureHelp`                        |
| Jump to declaration    | Unclear if useful                                                                        | `textDocument/declaration`                          |
| Jump to implementation | Unclear if useful                                                                        | `textDocument/implementation`                       |
| Renaming               | [Parital implementation](https://github.com/haskell/haskell-language-server/issues/2193) | `textDocument/rename`, `textDocument/prepareRename` |
| Folding                | Unimplemented                                                                            | `textDocument/foldingRange`                         |
| Semantic tokens        | Unimplemented                                                                            | `textDocument/semanticTokens`                       |
| Linked editing         | Unimplemented                                                                            | `textDocument/linkedEditingRange`                   |
| Document links         | Unimplemented                                                                            | `textDocument/documentLink`                         |
| Document color         | Unclear if useful                                                                        | `textDocument/documentColor`                        |
| Color presentation     | Unclear if useful                                                                        | `textDocument/colorPresentation`                    |
| Monikers               | Unclear if useful                                                                        | `textDocument/moniker`                              |
