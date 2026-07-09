# Dendritic Nix

A convention for organizing Nix flakes.

**One rule: every `.nix` file is a [flake-parts][flake-parts] module.** Built on two pieces:

- [flake-parts][flake-parts]: Provides module definition and does so files merge/compose better.
- [import-tree][import-tree]: Recursively imports every `.nix` file under a directory.

[flake-parts]: https://flake.parts
[import-tree]: https://github.com/denful/import-tree

A minimal flake:

```nix
{
  inputs.flake-parts.url = "github:hercules-ci/flake-parts";
  inputs.import-tree.url = "github:vic/import-tree";
  outputs = { flake-parts, import-tree, ... }@inputs:
    flake-parts.lib.mkFlake { inherit inputs; }
    (import-tree ./modules);
}
```

One file expresses one aspect and can contribute to `nixosConfigurations`, `homeManagerModules`,
`packages`, `perSystem`, `terranixModules`, etc. at once. A host is an emergent property of which
aspects apply, not a file that lists imports. Conditionality lives *inside* modules (flags/options),
not in what you choose to import.

## Convert to Dendritic Nix flake

## 1. Select a main subdirectory for dendritic parts

The best name for this subdirectory depends on the project. Here are some examples:

- A workspace project (e.g. Cargo) with no other Nix code can use `nix/`
- A Nix-heavy project can use `lib/`, `modules/` or `flake/` if it doesn't already have a set of
  library functions that aren't flake-parts modules, or it doesn't already make use of the term
  modules for something domain-specific.

## 2. Make a minimal flake.nix

When there is already a flake.nix, convert it to a minimal one: All inputs remain, but all outputs
are moved to files in the main subdirectory for dendritic parts. Please structure the imports in a
syntactically consistent way, e.g.

```nix
devshell.url = "github:numtide/devshell";
devshell.inputs.nixpkgs.follows = "nixpkgs";
```

or:

```nix
devshell = {
  url = "github:numtide/devshell";
  inputs.nixpkgs.follows = "nixpkgs";
};
```

with two `\n` between each input block.

## 3. Flake dependencies

Prefer to fetch nixpkgs from `https://nixos.org/channels/nixpkgs-unstable/nixexprs.tar.xz`

These are optional flake dependencies; add them either because the project is a blank slate (new git
repository, new project, or no prior Nix code in the project), or for reasons particular to the one
dependency. If the project already has Nix code, assume you're fighting with opinions and leave them
out from any flake rewrite.

Optionally, some inputs to the flake that I always add are:

- ```nix
  devshell.url = "github:numtide/devshell";
  devshell.inputs.nixpkgs.follows = "nixpkgs";
  ```

  If there's an existing `pkgs.mkShell`, refactor it to a numtide devshell.

- ```nix
  lefthook-nix.url = "github:sudosubin/lefthook.nix";
  lefthook-nix.inputs.nixpkgs.follows = "nixpkgs";
  ```

## 4. Flake input deduplication

Perform one layer of flake.lock input deduplication (_2, _3, etc.) by adding `.follows` on direct inputs.
