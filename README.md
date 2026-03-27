# PNPM warns about unmet peer dep when aliased

PNPM warns about unmet peer dependency when a dependency is coming from outside the workspace, and it declares a peer dependency using an npm: alias syntax.

The warning only happens only on the first `pnpm` call or if you changed dependencies:

```log
~/s/e/pnpm-aliased-peer/b main *❯ pnpm
Packages: +2
++
Progress: resolved 2, reused 2, downloaded 0, added 2, done
 WARN  Issues with peer dependencies found
.
└─┬ a 1.0.0
  └── ✕ unmet peer tslib-aliased@npm:tslib@^2.8.1: found 2.8.1

dependencies:
+ a 1.0.0
+ tslib-aliased <- tslib 2.8.1

Done in 354ms using pnpm v10.32.1
~/s/e/pnpm-aliased-peer/b main *❯ pnpm
Lockfile is up to date, resolution step is skipped
Already up to date
Done in 229ms using pnpm v10.32.1
```

## Reproduction

1. Clone this repository

   ```sh
   git clone https://github.com/maxpatiiuk/pnpm-aliased-peer-warning
   cd pnpm-aliased-peer-warning
   ```

2. Go into `b/`

   ```
   cd b
   ```

3. Install dependencies

   ```
   pnpm
   ```

   See the warning.

   The warning is not expected - both `tslib` and `tslib-aliased` are declared as dependencies.

Not reproducible if the package in question (`a/`) comes from the current workspace, or uses a relative file path instead of a tarball.

Reproducible even with catalogs.
