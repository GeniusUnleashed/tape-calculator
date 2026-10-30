# tape-calculator

## About this project

Public download and support page for Tape Calculator, a free macOS app with a
paper tape. The app's source code is kept in a separate private repository and
is not published here; do not add it to this repository. This repository holds
README.md (download and support), PRIVACY.md (the privacy policy) and, on
GitHub Releases, the signed and notarized disk images. There is nothing to
build or test here.

## Identity — do not change

Exactly one identity is permitted in this repository:

| | |
|---|---|
| Author name | `Michael Sullivan` |
| Author email | `17531745+GeniusUnleashed@users.noreply.github.com` |
| GitHub account | `GeniusUnleashed` |
| Remote | `https://github.com/GeniusUnleashed/tape-calculator.git` |
| Public contact | `geniusunleashed@mail.aird2.com` |
| App Store seller | Michael Sullivan, as an individual |

Anything else is wrong. If any other name, account, email, remote, SSH
host alias, or `gh` configuration turns up in this folder — in code,
comments, commit messages, config, or store metadata — do not commit it.
Stop and ask.

One standing exception: commit messages may carry the `Co-Authored-By:
Claude …` and `Claude-Session: …` trailers that mark commits made with
Claude's help. They name the tool, not a person or an account tied to
this repository's author — so keep them, and don't strip them to satisfy
the allowlist.

This is an allowlist on purpose. The rule is "only the table above,"
which needs no list of what it excludes and covers names and accounts
that do not exist yet.

Do not put any email address in public-facing files except those in
the table. The public contact is the address for people to write to.

## Three local guards, none of which survives a clone

**The identity pin.** `user.name` and `user.email` are set repo-locally
in `.git/config`, so a change to the global gitconfig from any other
project on this machine cannot alter what this repo commits as.

**The pre-commit hook.** `.git/hooks/pre-commit` refuses any commit
whose `origin` URL, author, or committer does not match the table above.
Author and committer are read as the commit will actually record them,
so `--author`, `-c user.email=…`, and the `GIT_AUTHOR_*` and
`GIT_COMMITTER_*` environment variables are all caught, not just the
config.

**The pre-push hook.** `.git/hooks/pre-push` refuses a push to any URL
but the remote in the table, whether the push names another remote or a
bare URL. It also refuses a push carrying any commit whose recorded
author or committer does not match the table, which catches commits
that never passed the pre-commit hook: `--no-verify`, a rebase or
cherry-pick, or a commit made in a fresh clone before the hooks were
reinstated.

All three live under `.git/`, which is untracked and does not travel
with the repository; the hooks' sources are tracked in `tools/`. After a
fresh clone, reinstate them:

    git config --local user.name "Michael Sullivan"
    git config --local user.email "17531745+GeniusUnleashed@users.noreply.github.com"
    cp tools/pre-commit .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit
    cp tools/pre-push .git/hooks/pre-push && chmod +x .git/hooks/pre-push

Verify at any time:

    git config user.email     # must match the table
    git remote get-url origin # must match the table
