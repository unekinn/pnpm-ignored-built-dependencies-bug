## To reproduce the bug

1.  Clone the repo:  
    `git clone git@github.com:unekinn/pnpm-ignored-built-dependencies-bug.git`

2.  Enter the repo:  
    `cd pnpm-ignored-built-dependencies-bug`

3.  Run `pnpm i`

    ```
    Lockfile is up to date, resolution step is skipped
    Packages: +7
    +++++++
    Progress: resolved 7, reused 7, downloaded 0, added 7, done

    devDependencies:
    + @swc/core 1.11.13
    + esbuild 0.25.1
    + just-pnpm 1.0.2

    Done in 275ms using pnpm v10.7.0
    ```

4.  Run `pnpm rebuild`

    ```
    node_modules/.pnpm/just-pnpm@1.0.2/node_modules/just-pnpm: Running preinstall script, done in 131ms
    node_modules/.pnpm/just-pnpm@1.0.2/node_modules/just-pnpm: Running postinstall script, done in 111ms
    ```

5.  Run `pnpm i` again

    ```
    Lockfile is up to date, resolution step is skipped
    Already up to date

    ╭ Warning ───────────────────────────────────────────────────────────────────────────────────╮
    │                                                                                            │
    │   Ignored build scripts: @swc/core, esbuild.                                               │
    │   Run "pnpm approve-builds" to pick which dependencies should be allowed to run scripts.   │
    │                                                                                            │
    ╰────────────────────────────────────────────────────────────────────────────────────────────╯

    Done in 241ms using pnpm v10.7.0
    ```

## How the example was made

1. `pnpm init`
2. `corepack use pnpm@latest`
3. `pnpm add -D just-pnpm esbuild @swc/core`
4. `pnpm approve-builds`
5. Select `just-pnpm` for approval
