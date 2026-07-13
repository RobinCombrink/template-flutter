# template-flutter

Template for a new Flutter repo: enforced from the first commit. Conventional Commits
linting, full-history secret scanning, semantic releases, Dependabot propagation with
update-type-gated auto-merge, strict analyzer modes, and lefthook hooks pulled from the
central dotfiles repo.

## After creating a repo from this template

1. `flutter create .` (keep this `analysis_options.yaml`), replace this README.
2. Install hooks: `lefthook install`.
3. Apply the merge policy and ruleset:

   ```sh
   gh repo edit <owner>/<repo> --enable-squash-merge=false --enable-merge-commit=false \
     --enable-rebase-merge --enable-auto-merge --delete-branch-on-merge
   gh api repos/<owner>/<repo>/rulesets --method POST --input .github/fleet-ruleset.json
   ```

4. Push a `feat:` commit — the first release (v1.0.0) cuts itself.

For a private repo, disable the SARIF upload in `.github/workflows/gitleaks.yml`
(`with: sarif-upload: false`) — code-scanning upload is paid outside public repos.

## What's inside

- `.github/workflows/` — caller stubs for the `actions-*` fleet (release,
  conventional-commits, gitleaks, automerge), each pinned to an exact commit SHA.
- `.github/dependabot.yml` — daily action-pin updates, 3-day cooldown.
- `.github/fleet-ruleset.json` — ruleset for `main`: linear history, required checks,
  no deletion/force-push; repo admins bypass.
- `analysis_options.yaml` — strict casts/inference/raw-types; `avoid_catching_errors`.
- `lefthook.yml` — commit-msg + Flutter stack jobs from the central dotfiles repo.
- `CLAUDE.md` — imports the shared Flutter stack conventions.
