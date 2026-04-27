# bundler-ruby-version-constraint

## Feature exercised

Exercises Bundler's `ruby` version constraint directive (`ruby "~> 3.2"`) to verify that Mend SCA treats it as platform metadata only — the constraint must not appear as a dependency in the detected tree, and all three real gem dependencies (`rack`, `json`, `multi_json`) must still be fully resolved and reported.

## Expected dependency tree

Direct dependencies (3), all non-optional, all sourced from `https://rubygems.org/`:

- `rack` 3.2.6 — `~> 3.2` constraint; leaf node, no transitive dependencies
- `json` 2.19.4 — `~> 2.7` constraint; leaf node, no transitive dependencies
- `multi_json` 1.20.1 — `~> 1.15` constraint; leaf node, no transitive dependencies

Transitive dependencies: none.

Key assertions:

- The `ruby "~> 3.2"` directive in the Gemfile does NOT appear as a dependency entry.
- The `RUBY VERSION` section in `Gemfile.lock` (`ruby 3.2.0p0`) is metadata only and does NOT appear in the tree.
- All three gems resolve to concrete versions consistent with the lockfile.
- All `optional: false`.
- No children on any node (all gems are leaf nodes).

## Probe metadata

| Field | Value |
|---|---|
| Pattern | bundler-ruby-version-constraint |
| Target | local |
| Package manager | Bundler / RUBYGEMS |
| Source | rubygems.org |
| Direct deps | 3 |
| Transitive deps | 0 |
| Total deps | 3 |
| Ruby version constraint | ~> 3.2 (Gemfile) / ruby 3.2.0p0 (lockfile) |
| Bundler version | 2.5.3 |
| Generated | 2026-04-27 |
