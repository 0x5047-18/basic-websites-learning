# Dev Log: Animated Portfolio

**Author:** 0x5047-18
**Description:** A collection of technical challenges, edge cases, and learnings encountered during the development of the animated portfolio project.

---

## Version Control & Git

### Edge Case: Resetting the Root Commit

**Context**
When initializing the repository, I needed to modify the very first commit. I attempted to use the standard `git reset HEAD~1` command to undo the commit while retaining the file changes in the staging area.

**The Issue**
Git returned a fatal error: `ambiguous argument 'HEAD~1': unknown revision`.
This occurs because `HEAD~1` attempts to reference the parent of the current commit. In a repository with only one commit (the root commit), there is no parent history to reference.

**The Solution**
To delete the root commit but keep all file changes staged (effectively a "soft reset" for the first commit), use the following low-level plumbing command:

```bash
git update-ref -d HEAD