
﻿# git-oops
=======
# git-oops

[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org/)
[![npm downloads](https://img.shields.io/npm/dt/git-oops.svg)](https://www.npmjs.com/package/git-oops)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Fast, safe, terminal-first Git helper for common workflow fixes.**

Move commits off wrong branch, split changes, yank safely, and more. Optimizes for correctness, safety, and zero surprises.

## ✨ Features

- 🛡️ **Safety-first**: Non-destructive by default with safety tags before risky operations
- ⚡ **Lightning fast**: <200ms for non-LLM operations
- 🎯 **Just works**: Zero configuration, works on macOS, Linux, and Windows
- 🧪 **Battle-tested**: 88% test coverage across real-world scenarios
- 💡 **Smart**: Optional AI assistance for commit messages and conflict resolution

## 🚀 Installation

**Requires Node.js 18+**

```bash
npm install -g git-oops
```

Once installed, use either:

```bash
git-oops <command>    # Direct command
git oops <command>    # Git alias (if supported by your Git version)
```

## Commands

### Quick Fixes

#### `save [message]`

Quickly save all changes with a commit (like `git add . && git commit`)

```bash
git oops save                           # Quick save with default message
git oops save -m "fix: updated styles"  # Save with custom message
git oops save --yes                     # Skip confirmation
```

#### `fixup`

Fix the last commit with current changes

```bash
git oops fixup                    # Add current changes to last commit
git oops fixup -m "better title" # Also update the commit message
git oops fixup --dry-run         # See what would happen
```

#### `undo`

Safely undo recent commits (keeps changes in working directory)

```bash
git oops undo           # Undo last commit
git oops undo -n 3      # Undo last 3 commits
git oops undo --dry-run # Preview what would be undone
```

### Workflow Fixes

#### `wrong-branch [new-branch]`

Move commits from current branch to a new branch and reset current branch to upstream

```bash
git oops wrong-branch              # Auto-generate branch name
git oops wrong-branch feature/fix  # Specify branch name
git oops wrong-branch --dry-run    # See what would happen
```

#### `split`

Split staged changes into separate commits by top-level directory

```bash
git oops split           # Split by directory
git oops split --dry-run # Preview the plan
```

#### `yank`

"Just let me pull" - stash dirty work, pull with rebase, and restore

```bash
git oops yank
```

#### `revert-merge <sha>`

Safely revert a merge commit with proper safety checks

```bash
git oops revert-merge abc1234      # Revert merge commit
git oops revert-merge abc1234 -m 2 # Use parent 2 as mainline
git oops revert-merge abc1234 --dry-run # Preview the revert
```

### State Management

#### `pocket`

Save exact working state to a hidden ref

```bash
git oops pocket              # Save locally
git oops pocket --push       # Save and push to origin
```

## Safety Features

- **Safety tags**: All destructive operations create backup tags automatically
- **Confirmation prompts**: Asks before doing anything destructive (use `--yes` to skip)
- **Dry run mode**: Preview what would happen with `--dry-run`
- **Push detection**: Warns when modifying pushed commits
- **Protected branch detection**: Extra warnings for main/master branches

## Usage

Use either:

- `git-oops <command>`
- `git oops <command>` (Git auto-discovers the binary)

## Examples

**Made a typo in your last commit?**

```bash
# Fix it and update the commit
echo "fixed typo" >> file.txt
git oops fixup
```

**Committed on the wrong branch?**

```bash
git oops wrong-branch feature/actual-fix
```

**Need to quickly save everything?**

```bash
git oops save -m "WIP: working on feature X"
```

**Accidentally committed sensitive data?**

```bash
git oops undo  # Undoes commit but keeps changes
# Remove sensitive data, then recommit
```

**Mixed up different changes in staging?**

```bash
git oops split  # Splits by directory into separate commits
```
## Command Demonstrations

Below are video demonstrations of git-oops commands in action:

<table>
  <tr>
    <td width="50%">
      <h3>Save Command</h3>
      <p>Quickly save all changes with a commit, similar to <code>git add . && git commit</code>.</p>
      <a href="https://github.com/user-attachments/assets/2a267d7b-a271-4e8f-8bf9-799f24686a35">📹 Watch Save Command Demo</a>
    </td>
    <td width="50%">
      <h3>Fixup Command</h3>
      <p>Fix the last commit by adding current changes without creating a new commit.</p>
      <a href="https://github.com/user-attachments/assets/21d78501-12ad-469b-8d8e-3a8863cf0c88">📹 Watch Fixup Command Demo</a>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>Wrong Branch Command</h3>
      <p>Move commits from the current branch to the correct target branch.</p>
      <a href="https://github.com/user-attachments/assets/df15e652-04b9-40c3-b2cc-8dfcac3a825c">📹 Watch Wrong Branch Command Demo</a>
    </td>
    <td width="50%">
      <h3>Undo Command</h3>
      <p>Safely undo the most recent commit while preserving the changes.</p>
      <a href="https://github.com/user-attachments/assets/a1022c8f-f0d4-4eb1-9f3e-61d3e5b72c5f">📹 Watch Undo Command Demo</a>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>Split Command</h3>
      <p>Split a large commit into smaller, focused commits by directory.</p>
      <a href="https://github.com/user-attachments/assets/bbe9f425-f5fd-4ac7-9bf1-d62d9801c3ec">📹 Watch Split Command Demo</a>
    </td>
    <td width="50%">
      <h3>Pocket Command</h3>
      <p>Save your current working state to a hidden reference for later retrieval.</p>
      <a href="https://github.com/user-attachments/assets/d437f322-e17a-4b24-8b3b-81f6e9bb6d46">📹 Watch Pocket Command Demo</a>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>Revert Merge Command</h3>
      <p>Safely revert a merge commit with proper handling of multiple parents.</p>
      <a href="https://github.com/user-attachments/assets/1f6275b5-3b4c-4ba0-8e35-bb78d46c2b37">📹 Watch Revert Merge Command Demo</a>
    </td>
    <td width="50%">
      <h3>Yank Command</h3>
      <p>Extract specific commits from one branch and apply them to another branch.</p>
      <a href="https://github.com/user-attachments/assets/52f4fcd5-79b7-4eae-a92d-bf586ef30441">📹 Watch Yank Command Demo</a>
    </td>
  </tr>
</table>

## License

MIT





