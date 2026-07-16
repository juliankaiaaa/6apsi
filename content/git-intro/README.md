# Intro to Git and GitHub

In this course your work lives in a **GitHub repository**, and you submit by
**pushing** your code. This lesson explains just enough Git to do that
confidently. You do not need to memorize commands; keep this page handy and
follow the cycle in section 4.

---

## 1. What Git and GitHub are

- **Git** is a *version control* tool that runs on your computer. It records
  snapshots of your files over time, so you can see what changed, undo
  mistakes, and never lose work.
- **GitHub** is a website that *hosts* Git repositories online. It is where your
  work is stored, where your instructor sees it, and where the autograder runs.
- A **repository** (or **repo**) is one project folder that Git is tracking,
  together with its full history.

> In this course: each activity is its own repo. **Pushing your repo to GitHub
> is how you submit.** There is nothing else to upload.

---

## 2. One-time setup

1. **Install Git** from [git-scm.com](https://git-scm.com) (macOS often has it
   already; check with `git --version`).
2. **Tell Git who you are** (used to label your commits). Run these once:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

3. **Have a GitHub account** and accept your course org invite.

---

## 3. Getting a copy of your repo

After you create your activity repo from the template (see the activity's
README), bring it down to your computer with **clone**. Copy the repo's URL from
its green **Code** button on GitHub, then:

```bash
git clone https://github.com/HAU-6APSI/m1a1-2240-yourname.git
cd m1a1-2240-yourname
```

`clone` makes a local folder linked to the GitHub copy. You only clone once per
repo.

> Prefer the browser? On any repo page press the **`.`** key to open a web
> editor where you can edit, commit, and push without installing anything.

---

## 4. The everyday cycle: edit, add, commit, push

This is the loop you repeat every work session:

```bash
# 1. See what changed
git status

# 2. Stage the files you want to save
git add index.html
# (or stage everything that changed)
git add -A

# 3. Save a snapshot with a short message describing the change
git commit -m "Add page heading and welcome text"

# 4. Send your commits up to GitHub (this is your submission)
git push
```

What each step means:

| Command | What it does |
| --- | --- |
| `git status` | shows which files changed and what is staged |
| `git add <file>` | **stages** a change (marks it to be included in the next commit) |
| `git commit -m "..."` | records a **snapshot** of the staged changes, with a message |
| `git push` | uploads your commits to GitHub |

Think of it as: **edit** your files → **add** the ones you want → **commit** to
save a checkpoint locally → **push** to publish it.

---

## 5. Confirming your submission

After `git push`:

1. Refresh your repo page on GitHub and confirm your latest commit is there.
2. Open the **Actions** tab. Each push runs the **Autograde** check.
3. Open the latest run and read the summary (for example, "6 / 6 tests
   passed"). A green check means your tests passed; a red ✗ means something
   still needs fixing.

You can push as many times as you like before the deadline. Each push re-runs
the check, so use it as feedback while you work.

---

## 6. Good habits

- **Commit small and often** with clear messages ("Add nav links", "Fix title")
  rather than one giant commit at the end.
- **Pull before you start** if you also edited on GitHub or another computer:
  `git pull` brings down changes you do not have yet.
- **Never commit secrets** (passwords, tokens). The repo's `.gitignore` already
  skips files like `node_modules/` and `.env`.
- If a command confuses you, run `git status` - it almost always tells you what
  to do next.

---

## 7. Quick reference

```bash
git clone <url>        # get a copy of a repo (once)
git status             # what changed?
git add -A             # stage all changes
git commit -m "msg"    # save a snapshot
git push               # submit to GitHub
git pull               # get the latest from GitHub
git log --oneline      # see your commit history
```

That is the whole workflow for this course: **clone once, then edit → add →
commit → push** every time you have something to submit.

---

## Sources and further reading

This lesson summarizes the official documentation. Use these to go deeper:

- **Pro Git** (free official book by Scott Chacon and Ben Straub, Apress) -
  especially ch. 1 "Getting Started" and ch. 2 "Git Basics":
  <https://git-scm.com/book/en/v2>
- **Git reference manual** (per-command docs for `clone`, `add`, `commit`,
  `push`, `status`, `pull`, `log`): <https://git-scm.com/docs>
- **Git downloads and install guide:** <https://git-scm.com/downloads>
- **GitHub Docs - Get started:** <https://docs.github.com/en/get-started>
- **GitHub Docs - About repositories:**
  <https://docs.github.com/en/repositories/creating-and-managing-repositories/about-repositories>
- **GitHub Docs - Pushing commits to a remote:**
  <https://docs.github.com/en/get-started/using-git/pushing-commits-to-a-remote-repository>
- **GitHub Docs - GitHub Actions (the autograder runs here):**
  <https://docs.github.com/en/actions>

Specific facts used above: the edit → stage → commit → push model and the
command behaviors in sections 4 and 7 follow the Git reference manual and Pro
Git ch. 2; the clone and submission steps follow GitHub Docs "Get started."
