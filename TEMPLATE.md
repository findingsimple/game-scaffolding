# Starting a new game from this template

This file is deleted by the rename script — when it's gone, the setup below is done.

## 1. Create the repository

On GitHub: **Use this template → Create a new repository**. Make it **public** if you
want the free GitHub Pages build (private repos skip the deploy step automatically).

```sh
git clone git@github.com:<you>/<your-game>.git
cd <your-game>
make setup
```

## 2. Rename the project

```sh
python3 scripts/new_game.py --name "Your Game" --repo <you>/<your-game> --description "One line."
# --name and --repo are required. Add --dry-run first to preview; --bundle-id com.you.yourgame
# overrides the macOS id; --force runs on a worktree with uncommitted changes.
```

This rewrites the project name (all spellings), the template's repository name and
URLs (README title, badges, the GitHub Pages link), the macOS bundle identifier, resets
`version.txt` / `CHANGELOG.md` to `0.0.0` (your first `feat:` release becomes 0.1.0), and
deletes this file. `LICENSE` and `ASSETS.md`
are left alone on purpose — update the copyright holder and credits by hand. The example game's code
stays — it is your working reference until you replace it.

```sh
make ci                 # must be green
git add -A && git commit -m "chore: rename template to Your Game"
git push
```

## 3. Repository settings (once)

- **Settings → Pages → Source:** *GitHub Actions* (enables the Web deploy).
- **Settings → Actions → General:** tick *Allow GitHub Actions to create and approve
  pull requests* (release-please opens the release PR).
- **Settings → Branches:** protect `main`; require the `CI` checks to pass.
- Optional: **Settings → General → Template repository** if this new repo should itself
  be a template.

## 4. Make it yours

- Write the one-page design doc: copy `docs/gdd-template.md` to `docs/gdd.md` and fill it in.
- Update `LICENSE` (holder/year) and `ASSETS.md` (credits) as you add things.
- Replace `icon.svg`.
- When you no longer need the example, delete `game/` and `tests/` contents and point
  `project.godot` → `run/main_scene` at your own scene. Keep the folder conventions.
- Keep `CLAUDE.md` accurate — it is how Claude learns your project's rules.

## Check it worked

- `make ci` green, `make run` shows your title, `make export-web` builds.
- A push to `main` produces a green *CI*, a *Web* deploy (public repos) and, once you have
  a `feat:` or `fix:` commit, a release PR from release-please.
