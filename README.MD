# TaskGlitch – Bug Fix Assignment

## 🐞 Bugs Identified & Fixes

### Bug 1: Duplicate Tasks on Load

**Problem:**
Tasks were being fetched twice on initial load due to multiple `useEffect` hooks
triggering API calls. This caused duplicate tasks to appear unpredictably.

**Fix:**
Removed the redundant `useEffect` responsible for the second fetch and ensured
tasks are loaded only once during initial mount.

**Commit:**
`Fix duplicate task fetch by removing redundant useEffect`

---
