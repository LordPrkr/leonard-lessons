# Code Brain Location

Store artifacts under `~/Documents/Code Brain/<repo>/`.

Resolve `<repo>` by canonical repository name, not worktree directory name:

1. Use the git remote basename: `git remote get-url origin`, stripping `.git`.
   - `https://github.com/org/front-end-web-monorepo.git` → `front-end-web-monorepo`
2. If no remote exists and the path looks like `~/code/<repo>/<worktree>`, use `<repo>`.
3. Otherwise use the git top-level directory basename.

Never use generic worktree folder names like `main`, `develop`, `review`, or `test` when a remote or parent repo name is available.
