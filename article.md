# Git Fundamentals: What I Actually Learned Building This Lab

If you've never used Git before, here's the short version: Git is a tool that
tracks changes to files over time, so you can always go back, see what
changed, and — critically — so multiple people (or multiple copies of the
same project) can work independently without stepping on each other. I
learned all of this the hard way today, by actually doing it, not by reading
about it.

## The problem Git solves

Before I started this lab, I created a plain text file called `notes.txt` and
started editing it. Without Git, every edit just overwrites the last one —
there's no way to see what the file looked like an hour ago, or to combine
changes made in two different places. Git solves this by keeping a full
history of every change, tied to a specific person and moment in time, so
nothing is ever silently lost.

## The three trees

Git organizes your work into three areas:

1. **Working directory** — the actual files on your disk, the ones you edit.
2. **Staging area** — a holding area where you tell Git "this is what I want
   in my next commit."
3. **Repository** — the permanent, committed history.

When I first created `notes.txt`, `git status` told me it was "untracked" —
Git had never seen the file. After I ran `git add notes.txt`, the wording
changed to "Changes to be committed" — the file moved into the staging area.
Only after `git commit -m "..."` did it actually land in the repository.

I actually tested what happens if you skip staging: I edited `notes.txt`
again and ran `git commit -m "..."` directly. Git refused, and told me there
was nothing staged to commit. That's the whole point of the staging area —
it forces you to deliberately choose what goes into a commit, rather than
committing every change sitting in your working directory whether you meant
to or not. If I'd edited three unrelated things, staging lets me commit them
as three separate, meaningful commits instead of one messy one.

## What a commit actually is

A commit is a saved snapshot: the state of your files at that moment, plus a
message explaining why, plus a link back to the commit before it. Running
`git log --oneline` on my repo showed six commits in a row, each one
building on the last:
